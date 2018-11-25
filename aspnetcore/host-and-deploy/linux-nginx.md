---
title: Nginx를 사용하여 Linux에서 ASP.NET Core 호스트
author: rick-anderson
description: Ubuntu 16.04에서 Nginx를 역방향 프록시로 설정하여 Kestrel에서 실행되는 ASP.NET Core 웹앱에 HTTP 트래픽을 전달하는 방법을 알아봅니다.
ms.author: riande
ms.custom: mvc
ms.date: 10/23/2018
uid: host-and-deploy/linux-nginx
ms.openlocfilehash: d29a9287cbce27a54e779fadfa05e57febec0413
ms.sourcegitcommit: 4a6bbe84db24c2f3dd2de065de418fde952c8d40
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/30/2018
ms.locfileid: "50253119"
---
# <a name="host-aspnet-core-on-linux-with-nginx"></a>Nginx를 사용하여 Linux에서 ASP.NET Core 호스트

작성자: [Sourabh Shirhatti](https://twitter.com/sshirhatti)

이 가이드에서는 Ubuntu 16.04 Server에서 프로덕션 준비 ASP.NET Core 환경을 설정하는 방법을 설명합니다. 이 지침은 최신 버전의 Ubuntu에서 작동할 수 있지만 최신 버전에서 테스트되지는 않았습니다.

ASP.NET Core에서 지원하는 다른 Linux 배포에 대한 자세한 내용은 [Linux에서 .NET Core의 필수 구성 요소](/dotnet/core/linux-prerequisites)를 참조하세요.

> [!NOTE]
> Ubuntu 14.04의 경우 Kestrel 프로세스를 모니터링하기 위한 솔루션으로 *supervisord*를 사용하는 것이 좋습니다. *systemd*는 Ubuntu 14.04에서 사용할 수 없습니다. Ubuntu 14.04 지침의 경우 [이 항목의 이전 버전](https://github.com/aspnet/Docs/blob/e9c1419175c4dd7e152df3746ba1df5935aaafd5/aspnetcore/publishing/linuxproduction.md)을 참조하세요.

이 가이드의 내용:

* 기존 ASP.NET Core 앱을 역방향 프록시 서버 뒤에 배치합니다.
* 역방향 프록시 서버를 설정하여 Kestrel 웹 서버에 요청을 전달합니다.
* 웹앱이 시작 시 데몬으로 실행되는지 확인합니다.
* 웹앱 다시 시작을 지원하도록 프로세스 관리 도구를 구성합니다.

## <a name="prerequisites"></a>전제 조건

1. sudo 권한을 가진 표준 사용자 계정으로 Ubuntu 16.04 Server에 액세스합니다.
1. 서버에서 .NET Core 런타임을 설치합니다.
   1. [.NET Core 모든 다운로드 페이지](https://www.microsoft.com/net/download/all)로 이동합니다.
   1. **런타임** 아래의 목록에서 최신 미리 보기 상태가 아닌 런타임을 선택합니다.
   1. Ubuntu 버전의 서버와 일치하는 Ubuntu에 대한 지침을 선택하고 수행합니다.
1. 기존 ASP.NET Core 앱입니다.

## <a name="publish-and-copy-over-the-app"></a>앱 게시 및 복사

[프레임워크 종속 배포](/dotnet/core/deploying/#framework-dependent-deployments-fdd)인 경우 앱을 구성합니다.

서버에서 실행할 수 있는 디렉터리(예: *bin/Release/&lt;target_framework_moniker&gt;/publish*)로 앱을 패키징하기 위해 개발 환경에서 [dotnet publish](/dotnet/core/tools/dotnet-publish)를 실행합니다.

```console
dotnet publish --configuration Release
```

.NET Core 런타임을 서버에서 유지 관리하지 않으려는 경우 앱은 [자체 포함된 배포](/dotnet/core/deploying/#self-contained-deployments-scd)로 게시될 수도 있습니다.

조직의 워크플로에 통합된 도구(예: SCP, SFTP)를 사용하여 ASP.NET Core 앱을 서버에 복사합니다. *var* 디렉터리(예: *var/www/helloapp*)에서 웹앱을 찾는 것이 일반적입니다.

> [!NOTE]
> 프로덕션 배포 시나리오에서 지속적인 통합 워크플로는 앱을 게시하고 자산을 서버로 복사하는 워크플로를 수행합니다.

앱을 테스트합니다.

1. 명령줄에서 `dotnet <app_assembly>.dll` 앱을 실행하세요.
1. 브라우저에서 `http://<serveraddress>:<port>`로 이동하여 앱이 Linux에서 로컬로 작동하는지 확인합니다.

## <a name="configure-a-reverse-proxy-server"></a>역방향 프록시 서버 구성

역방향 프록시는 동적 웹앱을 지원하기 위한 일반적인 설정입니다. 역방향 프록시는 HTTP 요청을 종료하고 이 요청을 ASP.NET Core 앱에 전달합니다.

### <a name="use-a-reverse-proxy-server"></a>역방향 프록시 서버를 사용합니다.

Kestrel은 ASP.NET Core에서 동적 콘텐츠를 제공하는 데 유용합니다. 그러나 웹 지원 기능은 IIS, Apache 또는 Nginx와 같은 서버만큼 기능이 다양하지 않습니다. 역방향 프록시 서버는 정적 콘텐츠 지원, 요청 캐시, 요청 압축 및 HTTP 서버에서 SSL 종료 같은 작업을 오프로드할 수 있습니다. 역방향 프록시 서버는 전용 컴퓨터에 있거나 HTTP 서버와 함께 배포될 수 있습니다.

이 가이드에서는 Nginx의 단일 인스턴스가 사용됩니다. 이 인스턴스는 HTTP 서버와 함께 동일한 서버에서 실행됩니다. 요구 사항에 따라 다른 설정을 선택할 수 있습니다.

요청이 역방향 프록시를 통해 전달되므로 [Microsoft.AspNetCore.HttpOverrides](https://www.nuget.org/packages/Microsoft.AspNetCore.HttpOverrides/) 패키지의 [전달된 헤더 미들웨어](xref:host-and-deploy/proxy-load-balancer)를 사용합니다. 이 미들웨어는 `X-Forwarded-Proto` 헤더를 사용하여 `Request.Scheme`을 업데이트하므로 리디렉션 URI 및 기타 보안 정책이 제대로 작동합니다.

전달된 헤더 미들웨어를 호출한 후에 인증, 링크 생성, 리디렉션 및 지리적 위치 등 체계에 따라 달라지는 구성 요소를 배치해야 합니다. 일반 규칙으로 전달된 헤더 미들웨어는 진단 및 오류 처리 미들웨어를 제외한 다른 미들웨어 전에 실행해야 합니다. 이 순서를 지정하면 전달된 헤더 정보에 따라 달라지는 미들웨어는 처리하기 위해 헤더 값을 사용할 수 있습니다.

::: moniker range=">= aspnetcore-2.0"

[UseAuthentication](/dotnet/api/microsoft.aspnetcore.builder.authappbuilderextensions.useauthentication) 또는 유사한 인증 체계 미들웨어를 호출하기 전에 `Startup.Configure`에서 [UseForwardedHeaders](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersextensions.useforwardedheaders) 메서드를 호출합니다. `X-Forwarded-For` 및 `X-Forwarded-Proto` 헤더를 전달하도록 미들웨어를 구성합니다.

```csharp
app.UseForwardedHeaders(new ForwardedHeadersOptions
{
    ForwardedHeaders = ForwardedHeaders.XForwardedFor | ForwardedHeaders.XForwardedProto
});

app.UseAuthentication();
```

::: moniker-end

::: moniker range="< aspnetcore-2.0"

[UseIdentity](/dotnet/api/microsoft.aspnetcore.builder.builderextensions.useidentity)와 [UseFacebookAuthentication](/dotnet/api/microsoft.aspnetcore.builder.facebookappbuilderextensions.usefacebookauthentication) 또는 유사한 인증 체계 미들웨어를 호출하기 전에 `Startup.Configure`에서 [UseForwardedHeaders](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersextensions.useforwardedheaders) 메서드를 호출합니다. `X-Forwarded-For` 및 `X-Forwarded-Proto` 헤더를 전달하도록 미들웨어를 구성합니다.

```csharp
app.UseForwardedHeaders(new ForwardedHeadersOptions
{
    ForwardedHeaders = ForwardedHeaders.XForwardedFor | ForwardedHeaders.XForwardedProto
});

app.UseIdentity();
app.UseFacebookAuthentication(new FacebookOptions()
{
    AppId = Configuration["Authentication:Facebook:AppId"],
    AppSecret = Configuration["Authentication:Facebook:AppSecret"]
});
```

::: moniker-end

미들웨어에 [ForwardedHeadersOptions](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersoptions)가 지정되지 않은 경우 전달할 기본 헤더는 `None`입니다.

localhost(127.0.0.1, [::1])에서 실행되는 프록시만 기본적으로 신뢰됩니다. 조직 내의 다른 신뢰할 수 있는 프록시 또는 네트워크가 인터넷과 웹 서버 간의 요청을 처리하는 경우 <xref:Microsoft.AspNetCore.Builder.ForwardedHeadersOptions>를 사용하여 <xref:Microsoft.AspNetCore.Builder.ForwardedHeadersOptions.KnownProxies*> 또는 <xref:Microsoft.AspNetCore.Builder.ForwardedHeadersOptions.KnownNetworks*> 목록에 추가합니다. 다음 예제는 IP 주소 10.0.0.100의 신뢰할 수 있는 프록시 서버를 `Startup.ConfigureServices`의 전달된 헤더 미들웨어 `KnownProxies`에 추가합니다.

```csharp
services.Configure<ForwardedHeadersOptions>(options =>
{
    options.KnownProxies.Add(IPAddress.Parse("10.0.0.100"));
});
```

자세한 내용은 <xref:host-and-deploy/proxy-load-balancer>을 참조하세요.

### <a name="install-nginx"></a>Nginx 설치

`apt-get`을 사용하여 Nginx를 설치합니다. 설치 관리자는 시스템 시작 시 Nginx를 디먼으로 실행하는 *systemd* 시작 스크립트를 만듭니다. [Nginx: 공식 Debian/Ubuntu 패키지](https://www.nginx.com/resources/wiki/start/topics/tutorials/install/#official-debian-ubuntu-packages)에서 Ubuntu에 대한 설치 지침을 따르세요.

> [!NOTE]
> 선택적 Nginx 모듈이 필요한 경우 소스에서 Nginx를 빌드해야 할 수 있습니다.

Nginx가 처음 설치되었으므로 다음을 실행하여 명시적으로 시작합니다.

```bash
sudo service nginx start
```

브라우저에 Nginx에 대한 기본 방문 페이지가 표시되는지 확인합니다. 방문 페이지는 `http://<server_IP_address>/index.nginx-debian.html`에 도달할 수 있습니다.

### <a name="configure-nginx"></a>Nginx 구성

Nginx를 역방향 프록시로 구성하여 요청을 ASP.NET Core 앱에 프로그램에 전달하려면 */etc/nginx/sites-available/default*를 수정합니다. 텍스트 편집기에서 해당 항목을 열고 콘텐츠를 다음으로 바꿉니다.

```nginx
server {
    listen        80;
    server_name   example.com *.example.com;
    location / {
        proxy_pass         http://localhost:5000;
        proxy_http_version 1.1;
        proxy_set_header   Upgrade $http_upgrade;
        proxy_set_header   Connection keep-alive;
        proxy_set_header   Host $host;
        proxy_cache_bypass $http_upgrade;
        proxy_set_header   X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header   X-Forwarded-Proto $scheme;
    }
}
```

`server_name`이 일치하지 않으면 Nginx는 기본 서버를 사용합니다. 기본 서버가 정의되지 않은 경우 구성 파일의 첫 번째 서버는 기본 서버입니다. 구성 파일에 있는 444 상태 코드를 반환하는 특정 기본 서버를 추가하는 것이 좋습니다. 기본 서버 구성 예제는 다음과 같습니다.

```nginx
server {
    listen   80 default_server;
    # listen [::]:80 default_server deferred;
    return   444;
}
```

이전 구성 파일과 기본 서버를 사용하여 Nginx는 포트 80에서 호스트 헤더 `example.com` 또는 `*.example.com`가 포함된 공용 트래픽을 허용합니다. 이러한 호스트와 일치하지 않는 요청은 Kestrel로 전달되지 않습니다. Nginx는 일치하는 요청을 `http://localhost:5000`의 Kestrel에 전달합니다. 자세한 내용은 [How nginx processes a request](https://nginx.org/docs/http/request_processing.html)(nginx가 요청을 처리하는 방법)를 참조하세요. Kestrel의 IP/포트를 변경 하려면 [Kestrel: 엔드포인트 구성](xref:fundamentals/servers/kestrel#endpoint-configuration)을 참조합니다.

> [!WARNING]
> 적절한 [server_name 지시문](https://nginx.org/docs/http/server_names.html)을 지정하지 않으면 앱이 보안 취약성에 노출됩니다. 전체 부모 도메인을 제어하는 경우 하위 도메인 와일드카드 바인딩(예: `*.example.com`)에는 이러한 보안 위험이 발생하지 않습니다(취약한 `*.com`과 반대임). 자세한 내용은 [rfc7230 섹션-5.4](https://tools.ietf.org/html/rfc7230#section-5.4)를 참조하세요.

Nginx 구성이 설정되면 `sudo nginx -t`를 실행하여 구성 파일의 구문을 확인합니다. 구성 파일 테스트에 성공하면 `sudo nginx -s reload`를 실행하여 Nginx가 변경 내용을 선택하도록 합니다.

앱을 서버에서 직접 실행하려면:

1. 앱의 디렉터리로 이동합니다.
1. `dotnet <app_assembly.dll>` 앱을 실행합니다. 여기서 `app_assembly.dll`은 앱의 어셈블리 파일 이름입니다.

앱이 서버에서 실행되지만 인터넷을 통해 응답하지 않는 경우 서버의 방화벽을 확인하고 포트 80이 열려 있는지 확인합니다. Ubuntu Azure VM을 사용하는 경우 인바운드 포트 80 트래픽을 사용하는 NSG(네트워크 보안 그룹) 규칙을 추가합니다. 인바운드 규칙을 사용할 때 아웃바운드 트래픽이 자동으로 부여되므로 아웃바운드 포트 80 규칙을 사용하도록 설정할 필요가 없습니다.

앱 테스트를 완료한 후에 명령 프롬프트에서 `Ctrl+C`를 사용하여 앱을 종료합니다.

## <a name="monitoring-the-app"></a>앱 모니터링

서버는 `http://<serveraddress>:80`에 대해 실행된 요청을 `http://127.0.0.1:5000`의 Kestrel에서 실행되는 ASP.NET Core 앱에 전달하도록 설정됩니다. 그러나 Nginx는 Kestrel 프로세스를 관리하도록 설정되지 않습니다. *systemd*를 사용하여 기본 웹앱을 시작 및 모니터링하기 위한 서비스 파일을 만들 수 있습니다. *systemd*는 프로세스를 시작, 중지 및 관리하기 위한 다양하고 강력한 기능을 제공하는 init 시스템입니다. 

### <a name="create-the-service-file"></a>서비스 파일 만들기

서비스 정의 파일을 만듭니다.

```bash
sudo nano /etc/systemd/system/kestrel-helloapp.service
```

앱에 대한 예제 서비스 파일은 다음과 같습니다.

```ini
[Unit]
Description=Example .NET Web API App running on Ubuntu

[Service]
WorkingDirectory=/var/www/helloapp
ExecStart=/usr/bin/dotnet /var/www/helloapp/helloapp.dll
Restart=always
# Restart service after 10 seconds if the dotnet service crashes:
RestartSec=10
KillSignal=SIGINT
SyslogIdentifier=dotnet-example
User=www-data
Environment=ASPNETCORE_ENVIRONMENT=Production
Environment=DOTNET_PRINT_TELEMETRY_MESSAGE=false

[Install]
WantedBy=multi-user.target
```

사용자 *www-data*가 구성에서 사용되지 않을 경우 여기서 정의된 사용자를 먼저 만들고 파일에 대한 적절한 소유권을 제공해야 합니다.

`TimeoutStopSec`를 사용하여 초기 인터럽트 신호를 받은 후 앱이 종료되기를 기다리는 기간을 구성합니다. 이 기간 내에 앱이 종료되지 않으면 앱을 종료하기 위해 SIGKILL이 실행됩니다. 단위 없는 초로 된 값(예: `150`) 또는 시간 범위 값(예: `2min 30s`)으로 값을 입력하거나, 시간 제한을 사용하지 않으려면 `infinity`를 입력합니다. `TimeoutStopSec`의 기본값은 관리자 구성 파일(*systemd-system.conf*, *system.conf.d*, *systemd-user.conf*, *user.conf.d*)의 `DefaultTimeoutStopSec` 값입니다. 대부분의 배포에서 기본 시간 제한은 90초입니다.

```
# The default value is 90 seconds for most distributions.
TimeoutStopSec=90
```

Linux에는 대/소문자를 구분하는 파일 시스템이 있습니다. ASPNETCORE_ENVIRONMENT를 “프로덕션”으로 설정하면 *appsettings.production.json* 대신 구성 파일 *appsettings.Production.json*을 검색합니다.

일부 값(예: SQL 연결 문자열)은 환경 변수를 읽기 위해 구성 공급자에 대해 이스케이프되어야 합니다. 다음 명령을 사용하여 구성 파일에서 사용할 제대로 이스케이프된 값을 생성합니다.

```console
systemd-escape "<value-to-escape>"
```

파일을 저장하고 서비스를 사용하도록 설정합니다.

```bash
sudo systemctl enable kestrel-helloapp.service
```

서비스를 시작하고 실행 중인지 확인합니다.

```
sudo systemctl start kestrel-helloapp.service
sudo systemctl status kestrel-helloapp.service

● kestrel-helloapp.service - Example .NET Web API App running on Ubuntu
    Loaded: loaded (/etc/systemd/system/kestrel-helloapp.service; enabled)
    Active: active (running) since Thu 2016-10-18 04:09:35 NZDT; 35s ago
Main PID: 9021 (dotnet)
    CGroup: /system.slice/kestrel-helloapp.service
            └─9021 /usr/local/bin/dotnet /var/www/helloapp/helloapp.dll
```

역방향 프록시를 구성하고 systemd를 통해 Kestrel을 관리하면 웹앱이 완전히 구성되고 로컬 컴퓨터(`http://localhost`)의 브라우저에서 웹앱에 액세스할 수 있습니다. 차단 중인 방화벽이 없다면 원격 컴퓨터에서 액세스할 수도 있습니다. 응답 헤더를 검사하는 `Server` 헤더는 Kestrel에서 지원하는 ASP.NET Core 앱을 보여줍니다.

```text
HTTP/1.1 200 OK
Date: Tue, 11 Oct 2016 16:22:23 GMT
Server: Kestrel
Keep-Alive: timeout=5, max=98
Connection: Keep-Alive
Transfer-Encoding: chunked
```

### <a name="viewing-logs"></a>로그 보기

Kestrel을 사용하는 웹앱은 `systemd`를 사용하여 관리되므로 모든 이벤트 및 프로세스가 중앙형 저널에 기록됩니다. 그러나 이 저널에는 `systemd`를 통해 관리하는 모든 서비스 및 프로세스에 대한 모든 항목이 포함됩니다. `kestrel-helloapp.service` 관련 항목을 보려면 다음 명령을 사용합니다.

```bash
sudo journalctl -fu kestrel-helloapp.service
```

추가 필터링을 위해 `--since today`, `--until 1 hour ago` 같은 시간 옵션이나 이러한 옵션의 조합을 사용하여 반환되는 항목 수를 줄일 수 있습니다.

```bash
sudo journalctl -fu kestrel-helloapp.service --since "2016-10-18" --until "2016-10-18 04:00"
```

## <a name="data-protection"></a>데이터 보호

[ASP.NET Core 데이터 보호 스택](xref:security/data-protection/introduction)은 인증 미들웨어(예: 쿠키 미들웨어) 및 CSRF(교차 사이트 요청 위조) 보호를 비롯한 여러 ASP.NET Core [미들웨어](xref:fundamentals/middleware/index)에 사용됩니다. 사용자 코드에서 데이터 보호 API가 호출되지 않더라도 영구적 암호화 [키 저장소](xref:security/data-protection/implementation/key-management)를 만들도록 데이터 보호를 구성해야 합니다. 데이터 보호를 구성하지 않으면 키는 메모리에 보관되고 앱이 다시 시작되면 삭제됩니다.

키 링이 메모리에 저장된 경우 앱을 다시 시작하면 다음과 같이 됩니다.

* 모든 쿠키 기반 인증 토큰이 무효화됩니다.
* 사용자는 다음 요청에서 다시 로그인해야 합니다.
* 키 링으로 보호된 데이터의 암호를 더 이상 해독할 수 없습니다. 여기에는 [CSRF 토큰](xref:security/anti-request-forgery#aspnet-core-antiforgery-configuration) 및 [ASP.NET Core MVC TempData 쿠키](xref:fundamentals/app-state#tempdata)가 포함될 수 있습니다.

키 링을 유지하고 암호화하도록 데이터 보호를 구성하려면 다음을 참조하십시오.

* <xref:security/data-protection/implementation/key-storage-providers>
* <xref:security/data-protection/implementation/key-encryption-at-rest>

## <a name="securing-the-app"></a>앱 보안

### <a name="enable-apparmor"></a>AppArmor 사용

LSM(Linux Security Modules)은 Linux 2.6 이후 Linux 커널에 포함된 프레임워크입니다. LSM은 보안 모듈의 다양한 구현을 지원합니다. [AppArmor](https://wiki.ubuntu.com/AppArmor)는 프로그램을 제한된 리소스 집합으로 한정할 수 있는 필수 Access Control 시스템을 구현하는 LSM입니다. AppArmor가 사용하도록 설정되고 제대로 구성되어 있는지 확인합니다.

### <a name="configuring-the-firewall"></a>방화벽 구성

사용되지 않는 모든 외부 포트를 닫습니다. 복잡하지 않은 방화벽(ufw)은 방화벽을 구성하기 위한 명령줄 인터페이스를 제공하여 `iptables`에 대한 프런트 엔드를 제공합니다.

> [!WARNING]
> 방화벽이 올바르게 구성되지 않으면 전체 시스템에 대한 액세스가 차단됩니다. 올바른 SSH 포트를 지정하지 못하면 SSH를 사용하여 시스템에 연결하는 경우 실직적으로 시스템에 액세스할 수 없게 됩니다. 기본 포트는 22입니다. 자세한 내용은 [ufw 소개](https://help.ubuntu.com/community/UFW) 및 [매뉴얼](http://manpages.ubuntu.com/manpages/bionic/man8/ufw.8.html)을 참조하세요.

`ufw`를 설치하고 필요한 모든 포트에서 트래픽을 허용하도록 구성합니다.

```bash
sudo apt-get install ufw

sudo ufw allow 22/tcp
sudo ufw allow 80/tcp
sudo ufw allow 443/tcp

sudo ufw enable
```

### <a name="securing-nginx"></a>Nginx 보안

#### <a name="change-the-nginx-response-name"></a>Nginx 응답 이름 변경

*src/http/ngx_http_header_filter_module.c*를 편집합니다.

```
static char ngx_http_server_string[] = "Server: Web Server" CRLF;
static char ngx_http_server_full_string[] = "Server: Web Server" CRLF;
```

#### <a name="configure-options"></a>옵션 구성

추가 필수 모듈을 사용하여 서버를 구성합니다. [ModSecurity](https://www.modsecurity.org/)와 같은 웹앱 방화벽을 사용하여 앱을 강화해 보세요.

#### <a name="configure-ssl"></a>SSL 구성

* 신뢰할 수 있는 CA(인증 기관)에서 발급된 유효한 인증서를 지정하여 포트 `443`에서 HTTPS 트래픽을 수신 대기하도록 서버를 구성합니다.

* 다음 */etc/nginx/nginx.conf* 파일에 설명된 일부 사례를 채택하여 보안을 강화합니다. 예를 들어 더 강력한 암호화를 선택하고 HTTP를 사용한 모든 트래픽을 HTTPS로 리디렉션합니다.

* HSTS(`HTTP Strict-Transport-Security`) 헤더를 추가하면 클라이언트에서 만든 모든 후속 요청이 HTTPS를 통해 이루어집니다.

* 나중에 SSL을 사용하지 않도록 설정할 경우 HSTS 헤더를 추가하지 않거나 적절한 `max-age`를 선택합니다.

*/etc/nginx/proxy.conf* 구성 파일을 추가합니다.

[!code-nginx[](linux-nginx/proxy.conf)]

*/etc/nginx/nginx.conf* 구성 파일을 편집합니다. 예제에서는 `http` 및 `server` 섹션이 하나의 구성 파일에 포함됩니다.

[!code-nginx[](linux-nginx/nginx.conf?highlight=2)]

#### <a name="secure-nginx-from-clickjacking"></a>클릭재킹(clickjacking)으로부터 Nginx 보호

또한 ‘UI 교정 공격’이라고도 하는[클릭재킹(Clickjacking)](https://blog.qualys.com/securitylabs/2015/10/20/clickjacking-a-common-implementation-mistake-that-can-put-your-websites-in-danger)은 웹 사이트 방문자를 속여서 현재 방문 중인 것과 다른 페이지에서 링크 또는 단추를 클릭하게 하는 악의적인 공격입니다. `X-FRAME-OPTIONS`를 사용하여 사이트를 보호합니다.

클릭재킹 공격을 완화하려면:

1. *nginx.conf* 파일을 편집합니다.

   ```bash
   sudo nano /etc/nginx/nginx.conf
   ```

   `add_header X-Frame-Options "SAMEORIGIN";` 줄을 추가합니다.
1. 파일을 저장합니다.
1. Nginx를 다시 시작합니다.

#### <a name="mime-type-sniffing"></a>MIME 형식 검색

이 헤더는 응답 콘텐츠 형식을 재정의하지 않도록 브라우저에 지시하므로 대부분의 브라우저에서 선언된 콘텐츠 형식이 아닌 응답에 대한 MIME 검색을 차단합니다. `nosniff` 옵션을 사용하면 서버에 콘텐츠가 “text/html”이라고 표시될 경우 브라우저는 콘텐츠를 “text/html”으로 렌더링합니다.

*nginx.conf* 파일을 편집합니다.

```bash
sudo nano /etc/nginx/nginx.conf
```

줄 `add_header X-Content-Type-Options "nosniff";`를 추가하고 파일을 저장한 다음 Nginx를 다시 시작합니다.

## <a name="additional-resources"></a>추가 자료

* [Linux에서 .NET Core의 필수 구성 요소](/dotnet/core/linux-prerequisites)
* [Nginx: 이진 릴리스: 공식 Debian/Ubuntu 패키지](https://www.nginx.com/resources/wiki/start/topics/tutorials/install/#official-debian-ubuntu-packages)
* [프록시 서버 및 부하 분산 장치를 사용하도록 ASP.NET Core 구성](xref:host-and-deploy/proxy-load-balancer)
* [NGINX: 전달된 헤더 사용](https://www.nginx.com/resources/wiki/start/topics/examples/forwarded/)
