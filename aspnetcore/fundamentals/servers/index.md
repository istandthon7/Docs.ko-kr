---
title: ASP.NET Core의 웹 서버 구현
author: guardrex
description: ASP.NET Core의 웹 서버 Kestrel 및 HTTP.sys를 검색합니다. 서버를 선택하는 방법 및 역방향 프록시 서버를 사용하는 시기에 대해 알아봅니다.
ms.author: tdykstra
ms.custom: mvc
ms.date: 09/21/2018
uid: fundamentals/servers/index
ms.openlocfilehash: 06d4bf09b07fc70a10b3e260e78c29fe189486c5
ms.sourcegitcommit: edb9d2d78c9a4d68b397e74ae2aff088b325a143
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/09/2018
ms.locfileid: "51505728"
---
# <a name="web-server-implementations-in-aspnet-core"></a>ASP.NET Core의 웹 서버 구현

작성자: [Tom Dykstra](https://github.com/tdykstra), [Steve Smith](https://ardalis.com/), [Stephen Halter](https://twitter.com/halter73) 및 [Chris Ross](https://github.com/Tratcher)

ASP.NET Core 앱은 In-process HTTP 서버 구현을 사용하여 실행됩니다. 서버 구현은 HTTP 요청을 수신하고 <xref:Microsoft.AspNetCore.Http.HttpContext>에 구성된 [요청 기능](xref:fundamentals/request-features)의 집합으로 앱에 표시합니다.

ASP.NET Core는 다음과 같은 서버 구현과 함께 제공됩니다.

::: moniker range=">= aspnetcore-2.2"

* [Kestrel](xref:fundamentals/servers/kestrel)은 ASP.NET Core용 기본 플랫폼 간 HTTP 서버입니다.
* `IISHttpServer`는 [in-process 호스팅 모델](xref:fundamentals/servers/aspnet-core-module#in-process-hosting-model)과 Windows의 [ASP.NET Core 모듈](xref:fundamentals/servers/aspnet-core-module)에서 사용됩니다.
* [HTTP.sys](xref:fundamentals/servers/httpsys)는 [Http.Sys 커널 드라이버 및 HTTP 서버 API](https://msdn.microsoft.com/library/windows/desktop/aa364510.aspx)를 기반으로 하는 Windows 전용 HTTP 서버입니다. ASP.NET Core 1.x에서는 HTTP.sys를 [WebListener](xref:fundamentals/servers/weblistener)라고 합니다.

::: moniker-end

::: moniker range="< aspnetcore-2.2"

* [Kestrel](xref:fundamentals/servers/kestrel)은 ASP.NET Core용 기본 플랫폼 간 HTTP 서버입니다.
* [HTTP.sys](xref:fundamentals/servers/httpsys)는 [Http.Sys 커널 드라이버 및 HTTP 서버 API](https://msdn.microsoft.com/library/windows/desktop/aa364510.aspx)를 기반으로 하는 Windows 전용 HTTP 서버입니다. ASP.NET Core 1.x에서는 HTTP.sys를 [WebListener](xref:fundamentals/servers/weblistener)라고 합니다.

::: moniker-end

## <a name="kestrel"></a>Kestrel

Kestrel은 ASP.NET Core 프로젝트 템플릿에 포함된 기본 웹 서버입니다.

::: moniker range=">= aspnetcore-2.0"

Kestrel을 단독으로 사용하거나 IIS, Nginx 또는 Apache 같은 *역방향 프록시 서버*와 함께 사용할 수 있습니다. 역방향 프록시 서버는 인터넷에서 HTTP 요청을 수신하고 몇몇 사전 처리 후에 Kestrel에 전달합니다.

![Kestrel은 역방향 프록시 서버 없이 직접 인터넷과 통신합니다.](kestrel/_static/kestrel-to-internet2.png)

![Kestrel은 IIS, Nginx 또는 Apache 같은 역방향 프록시 서버를 통해 간접적으로 인터넷과 통신합니다.](kestrel/_static/kestrel-to-internet.png)

&mdash;역방향 프록시 서버의 유무에 상관없이&mdash; ASP.NET Core 2.0 이상 앱에 대해 지원되는 유효한 호스팅 구성입니다. 자세한 내용은 [Kestrel를 역방향 프록시와 함께 사용할 경우](xref:fundamentals/servers/kestrel#when-to-use-kestrel-with-a-reverse-proxy)를 참조하세요.

::: moniker-end

::: moniker range="< aspnetcore-2.0"

앱이 내부 네트워크의 요청만을 수락하는 경우 Kestrel을 단독으로 사용할 수 있습니다.

![Kestrel은 내부 네트워크와 직접 통신합니다.](kestrel/_static/kestrel-to-internal.png)

앱을 인터넷에 노출할 경우 Kestrel에서는 IIS, Nginx 또는 Apache를 *역방향 프록시 서버*로 사용해야 합니다. 역방향 프록시 서버는 인터넷에서 HTTP 요청을 수신하고, 다음 다이어그램에서 보여준 대로 몇 가지 사전 처리를 수행한 후에 Kestrel에 전달합니다.

![Kestrel은 IIS, Nginx 또는 Apache 같은 역방향 프록시 서버를 통해 간접적으로 인터넷과 통신합니다.](kestrel/_static/kestrel-to-internet.png)

인터넷에 직접 노출되는 공용 에지 서버 배포에 역방향 프록시를 사용하는 가장 중요한 이유는 보안입니다. 1.x 버전의 Kestrel에는 인터넷의 공격으로부터 보호하기 위한 중요한 보안 기능이 없습니다. 여기에는 적절한 시간 제한, 요청 크기 제한, 동시 연결 제한을 비롯한 다양한 기능이 포함됩니다.

자세한 내용은 [Kestrel를 역방향 프록시와 함께 사용할 경우](xref:fundamentals/servers/kestrel#when-to-use-kestrel-with-a-reverse-proxy)를 참조하세요.

::: moniker-end

Kestrel 또는 [사용자 지정 서버 구현](#custom-servers)이 없으면 IIS, Nginx 또는 Apache를 사용할 수 없습니다. ASP.NET Core는 플랫폼 간에 일관되게 동작하도록 자체 프로세스로 실행되도록 고안되었습니다. IIS, Nginx 및 Apache에서는 고유한 시작 프로시저 및 환경을 지정합니다. 직접 이러한 서버 기술을 사용하려면 ASP.NET Core를 각 서버의 요구 사항에 맞게 적용해야 합니다. ASP.NET Core는 Kestrel과 같은 웹 서버 구현을 사용하여 다른 서버 기술에서 호스팅될 경우 시작 프로세스 및 환경을 제어할 수 있습니다.

### <a name="iis-with-kestrel"></a>IIS 및 Kestrel

::: moniker range=">= aspnetcore-2.2"

[IIS](/iis/get-started/introduction-to-iis/introduction-to-iis-architecture) 또는 [IIS Express](/iis/extensions/introduction-to-iis-express/iis-express-overview)를 사용할 때 ASP.NET Core 앱은 IIS 작업자 프로세스(*in-process* 호스팅 모델)와 동일한 프로세스에서 실행되거나 IIS 작업자 프로세스(*out-of-process* 호스팅 모델)와는 별개로 처리됩니다.

[ASP.NET Core 모듈](xref:fundamentals/servers/aspnet-core-module)은 in-process IIS HTTP Server 또는 out-of-process Kestrel 서버 간의 네이티브 IIS 요청을 처리하는 네이티브 IIS 모듈입니다. 자세한 내용은 <xref:fundamentals/servers/aspnet-core-module>을 참조하세요.

::: moniker-end

::: moniker range="< aspnetcore-2.2"

[IIS](/iis/get-started/introduction-to-iis/introduction-to-iis-architecture) 또는 [IIS Express](/iis/extensions/introduction-to-iis-express/iis-express-overview)를 ASP.NET Core에 대한 역방향 프록시로 사용할 경우 ASP.NET Core 앱은 IIS 작업자 프로세스와 분리된 프로세스에서 실행됩니다. IIS 프로세스에서 [ASP.NET Core 모듈](xref:fundamentals/servers/aspnet-core-module)은 역방향 프록시 관계를 조정합니다. ASP.NET Core 모듈의 기본 기능은 ASP.NET Core 앱을 시작하고, 작동 중단 시 앱을 다시 시작하고, 앱에 HTTP 트래픽을 전달하는 것입니다. 자세한 내용은 <xref:fundamentals/servers/aspnet-core-module>을 참조하세요.

::: moniker-end

### <a name="nginx-with-kestrel"></a>Nginx 및 Kestrel

Linux에서 Kestrel에 대한 역방향 프록시 서버로 Nginx를 사용하는 방법에 대한 자세한 내용은 [Nginx를 사용하여 Linux에서 호스트](xref:host-and-deploy/linux-nginx)를 참조하세요.

### <a name="apache-with-kestrel"></a>Apache 및 Kestrel

Linux에서 Apache에 대한 역방향 프록시 서버로 Nginx를 사용하는 방법에 대한 자세한 내용은 [Apache를 사용하여 Linux에서 호스트](xref:host-and-deploy/linux-apache)를 참조하세요.

## <a name="httpsys"></a>HTTP.sys

::: moniker range=">= aspnetcore-2.0"

Windows에서 ASP.NET Core 앱을 실행할 경우 Kestrel 대신 HTTP.sys를 사용할 수 있습니다. 최상의 성능을 위해 일반적으로 Kestrel을 사용하는 것이 좋습니다. 앱이 인터넷에 노출되고 필수 기능이 Kestrel이 아닌 HTTP.sys에서 지원되는 경우 시나리오에서 HTTP.sys를 사용할 수 있습니다. HTTP.sys에 대한 자세한 내용은 [HTTP.sys](xref:fundamentals/servers/httpsys)를 참조하세요.

![HTTP.sys는 인터넷과 직접 통신합니다.](httpsys/_static/httpsys-to-internet.png)

HTTP.sys는 내부 네트워크에만 노출되는 앱에도 사용할 수 있습니다.

![HTTP.sys는 내부 네트워크와 직접 통신합니다.](httpsys/_static/httpsys-to-internal.png)

::: moniker-end

::: moniker range="< aspnetcore-2.0"

ASP.NET Core 1.x에서는 HTTP.sys의 이름이 [WebListener](xref:fundamentals/servers/weblistener)로 지정됩니다. Windows에서 ASP.NET Core 앱을 실행하는 경우 IIS가 앱을 호스팅하는 데 사용할 수 없는 시나리오의 대안으로 WebListener를 사용합니다.

![WebListener는 인터넷과 직접 통신합니다.](weblistener/_static/weblistener-to-internet.png)

필수 기능이 Kestrel이 아닌 WebListener에서 지원하는 경우 내부 네트워크에만 노출되는 앱에 Kestrel 대신 WebListener를 사용할 수 있습니다. WebListener에 대한 자세한 내용은 [WebListener](xref:fundamentals/servers/weblistener)를 참조하세요.

![WebListener는 내부 네트워크와 직접 통신합니다.](weblistener/_static/weblistener-to-internal.png)

::: moniker-end

## <a name="aspnet-core-server-infrastructure"></a>ASP.NET Core 서버 인프라

`Startup.Configure` 메서드에서 사용할 수 있는 [IApplicationBuilder](/dotnet/api/microsoft.aspnetcore.builder.iapplicationbuilder)는 [IFeatureCollection](/dotnet/api/microsoft.aspnetcore.http.features.ifeaturecollection) 형식의 [ServerFeatures](/dotnet/api/microsoft.aspnetcore.builder.iapplicationbuilder.serverfeatures) 속성을 노출합니다. Kestrel 및 HTTP.sys(ASP.NET Core 1.x에서 WebListener)는 각각 단일 기능인 [IServerAddressesFeature](/dotnet/api/microsoft.aspnetcore.hosting.server.features.iserveraddressesfeature)만을 노출하지만 다른 서버 구현은 추가 기능을 노출할 수 있습니다.

`IServerAddressesFeature`를 사용하여 런타임 시 서버 구현이 바인딩된 포트를 확인할 수 있습니다.

## <a name="custom-servers"></a>사용자 지정 서버

기본 제공 서버가 앱의 요구 사항을 충족하지 않으면 사용자 지정 서버 구현을 만들 수 있습니다. [OWIN(Open Web Interface for .NET) 가이드](xref:fundamentals/owin)에서는 [Nowin](https://github.com/Bobris/Nowin) 기반 [IServer](/dotnet/api/microsoft.aspnetcore.hosting.server.iserver) 구현을 작성하는 방법을 보여 줍니다. 앱이 사용하는 기능 인터페이스에는 구현이 필요합니다. 최소한 [IHttpRequestFeature](/dotnet/api/microsoft.aspnetcore.http.features.ihttprequestfeature) 및 [IHttpResponseFeature](/dotnet/api/microsoft.aspnetcore.http.features.ihttpresponsefeature)이 지원되어야 합니다.

## <a name="server-startup"></a>서버 시작

[Visual Studio](https://www.visualstudio.com/vs/), [Mac용 Visual Studio](https://www.visualstudio.com/vs/mac/) 또는 [Visual Studio Code](https://code.visualstudio.com/)를 사용하는 경우 IDE(통합 개발 환경)에서 앱을 시작할 때 서버가 실행됩니다. Windows의 Visual Studio에서 실행 프로필을 사용하여 [IIS Express](/iis/extensions/introduction-to-iis-express/iis-express-overview)/[ASP.NET Core 모듈](xref:fundamentals/servers/aspnet-core-module) 또는 콘솔에서 앱 및 서버를 시작할 수 있습니다. Visual Studio Code에서 [Omnisharp](https://github.com/OmniSharp/omnisharp-vscode)로 앱 및 서버를 시작합니다. 그러면 CoreCLR 디버거를 활성화합니다. Mac용 Visual Studio를 사용하여 [Mono Soft-Mode 디버거](http://www.mono-project.com/docs/advanced/runtime/docs/soft-debugger/)로 앱 및 서버를 시작합니다.

프로젝트의 폴더에 있는 명령 프롬프트에서 앱을 시작할 때 [dotnet run](/dotnet/core/tools/dotnet-run)은 서버 및 앱을 시작합니다(Kestrel 및 HTTP.sys만 해당). `Debug`(기본값) 또는 `Release`로 설정되어 있는 `-c|--configuration` 옵션으로 구성을 지정합니다. 실행 프로필이 *launchSettings.json* 파일에 있는 경우 `--launch-profile <NAME>` 옵션을 사용하여 실행 프로필(예: `Development` 또는 `Production`)을 설정합니다. 자세한 내용은 [dotnet run](/dotnet/core/tools/dotnet-run) 및 [.NET Core 배포 패키징](/dotnet/core/build/distribution-packaging) 항목을 참조하세요.

## <a name="http2-support"></a>HTTP/2 지원

[HTTP/2](https://httpwg.org/specs/rfc7540.html)는 다음과 같은 배포 시나리오에서 ASP.NET Core를 통해 지원됩니다.

::: moniker range=">= aspnetcore-2.2"

* [Kestrel](xref:fundamentals/servers/kestrel#http2-support)
  * 운영 체제
    * Windows Server 2016/Windows 10 이상&dagger;
    * Linux 및 OpenSSL 1.0.2 이상(예: Ubuntu 16.04 이상)
    * 이후 릴리스에서는 macOS에서 HTTP/2가 지원됩니다.
  * 대상 프레임워크: .NET Core 2.2 이상
* [HTTP.sys](xref:fundamentals/servers/httpsys#http2-support)
  * Windows Server 2016/Windows 10 이상
  * 대상 프레임워크: HTTP.sys 배포에는 적용할 수 없습니다.
* [IIS(In-Process)](xref:host-and-deploy/iis/index#http2-support)
  * Windows Server 2016/Windows 10 이상, IIS 10 이상
  * 대상 프레임워크: .NET Core 2.2 이상
* [IIS(Out-of-process)](xref:host-and-deploy/iis/index#http2-support)
  * Windows Server 2016/Windows 10 이상, IIS 10 이상
  * 공용 에지 서버 연결은 HTTP/2를 사용하지만 Kestrel에 대한 역방향 프록시 연결은 HTTP/1.1을 사용합니다.
  * 대상 프레임워크: IIS Out-of-process 배포에는 적용할 수 없습니다.

&dagger;Kestrel은 Windows Server 2012 R2와 Windows 8.1에서의 HTTP/2 지원을 제한했습니다. 이러한 운영 체제에서 사용할 수 있는 지원 가능 TLS 암호 그룹 목록이 제한되므로 지원이 제한됩니다. TLS 연결을 보호하는 데 ECDSA(타원 곡선 디지털 서명 알고리즘)를 사용하여 생성된 인증서가 필요할 수 있습니다.

::: moniker-end

::: moniker range="< aspnetcore-2.2"

* [HTTP.sys](xref:fundamentals/servers/httpsys#http2-support)
  * Windows Server 2016/Windows 10 이상
  * 대상 프레임워크: HTTP.sys 배포에는 적용할 수 없습니다.
* [IIS(Out-of-process)](xref:host-and-deploy/iis/index#http2-support)
  * Windows Server 2016/Windows 10 이상, IIS 10 이상
  * 공용 에지 서버 연결은 HTTP/2를 사용하지만 Kestrel에 대한 역방향 프록시 연결은 HTTP/1.1을 사용합니다.
  * 대상 프레임워크: IIS Out-of-process 배포에는 적용할 수 없습니다.

::: moniker-end

HTTP/2 연결은 [ALPN(Application-Layer Protocol Negotiation)](https://tools.ietf.org/html/rfc7301#section-3) 및 TLS 1.2 이상을 사용해야 합니다. 자세한 정보는 서버 배포 시나리오와 관련된 항목을 참조하세요.

## <a name="additional-resources"></a>추가 자료

* <xref:fundamentals/servers/kestrel>
* <xref:fundamentals/servers/aspnet-core-module>
* <xref:host-and-deploy/iis/index>
* <xref:host-and-deploy/azure-apps/index>
* <xref:host-and-deploy/linux-nginx>
* <xref:host-and-deploy/linux-apache>
* <xref:fundamentals/servers/httpsys>(ASP.NET Core 1.x에 대해서는 <xref:fundamentals/servers/weblistener> 참조)
