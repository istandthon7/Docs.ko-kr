---
uid: aspnet/overview/owin-and-katana/owin-middleware-in-the-iis-integrated-pipeline
title: "OWIN 미들웨어입니다. iis에서 통합 파이프라인 | Microsoft Docs"
author: Praburaj
description: "이 문서에서는 IIS 통합된 파이프라인의 OWIN 미들웨어 구성 요소 (OMCs)를 실행 하는 방법을 설명 하 고는 OMC 파이프라인 이벤트를 설정 하는 방법에서 실행 합니다. 다음 작업을 수행 해야합니다."
ms.author: aspnetcontent
manager: wpickett
ms.date: 11/07/2013
ms.topic: article
ms.assetid: d031c021-33c2-45a5-bf9f-98f8fa78c2ab
ms.technology: 
ms.prod: .net-framework
msc.legacyurl: /aspnet/overview/owin-and-katana/owin-middleware-in-the-iis-integrated-pipeline
msc.type: authoredcontent
ms.openlocfilehash: 5f6ed1ae0309e9bdd3ca4ae229195835f20bc729
ms.sourcegitcommit: a510f38930abc84c4b302029d019a34dfe76823b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/30/2018
---
<a name="owin-middleware-in-the-iis-integrated-pipeline"></a>IIS 통합된 파이프라인의 OWIN 미들웨어.
====================
여 [Praburaj Thiagarajan](https://github.com/Praburaj), [Rick Anderson](https://github.com/Rick-Anderson)

> 이 문서에서는 IIS 통합된 파이프라인의 OWIN 미들웨어 구성 요소 (OMCs)를 실행 하는 방법을 설명 하 고는 OMC 파이프라인 이벤트를 설정 하는 방법에서 실행 합니다. 검토 해야 [An 프로젝트 Katana 개요](an-overview-of-project-katana.md) 및 [OWIN 시작 클래스 검색](owin-startup-class-detection.md) 이 자습서를 읽기 전에 합니다. 이 자습서는 Rick Anderson에 의해 작성 되었으므로 ( [ @RickAndMSFT ](https://twitter.com/#!/RickAndMSFT) ), Chris Ross, Praburaj Thiagarajan 및 Howard Dierking ( [ @howard \_dierking](https://twitter.com/howard_dierking) ).


하지만 [OWIN](an-overview-of-project-katana.md) 미들웨어 구성 요소 (OMCs)는 주로 서버를 알 수 없는 파이프라인에서 실행 하도록 설계 되었습니다, 뿐 아니라 IIS 통합된 파이프라인에는 OMC를 실행할 수는 (**클래식 모드는 *하지* 지원**). 패키지 관리자 콘솔 (PMC)에서 다음 패키지를 설치 하 여 IIS 통합된 파이프라인에서 작업 하는 OMC 내릴 수 있습니다.

[!code-console[Main](owin-middleware-in-the-iis-integrated-pipeline/samples/sample1.cmd)]

즉, 아직 수 없는 IIS와 System.Web, 외부에서 실행 하는 모든 응용 프로그램 프레임 워크 기존 OWIN 미들웨어 구성 요소에서 얻을 수 있습니다. 

> [!NOTE]
> 모든는 `Microsoft.Owin.Security.*` Visual Studio 2013의 새 Id 시스템으로 배송 패키지 (예: 쿠키, Microsoft 계정, Google, Facebook, Twitter, [전달자 토큰](http://self-issued.info/docs/draft-ietf-oauth-v2-bearer.html), OAuth, 권한 부여 서버, JWT Azure Active 디렉터리 및 Active directory federation services), OMCs로 작성 되어 및 자체 호스팅 시나리오와 IIS에서 호스트 시나리오 모두에서 사용할 수 있습니다.

## <a name="how-owin-middleware-executes-in-the-iis-integrated-pipeline"></a>OWIN 미들웨어입니다. IIS 통합된 파이프라인에서 실행 하는 방법

OWIN 콘솔 응용 프로그램에 대 한 응용 프로그램 파이프라인 사용 하 여 작성 된 [시작 구성](owin-startup-class-detection.md) 구성 요소를 사용 하 여 추가 되는 순서에 의해 설정 됩니다는 `IAppBuilder.Use` 메서드. 즉, OWIN 파이프라인에는 [Katana](an-overview-of-project-katana.md) 런타임 OMCs를 사용 하 여 등록 된 이러한 순서로 처리 됩니다 `IAppBuilder.Use`합니다. IIS 통합된 파이프라인의 요청 파이프라인의 구성 [HttpModules](https://msdn.microsoft.com/library/ms178468(v=vs.85).aspx) 와 같은 미리 정의 된 집합이 파이프라인 이벤트를 구독할 [BeginRequest](https://msdn.microsoft.com/library/system.web.httpapplication.beginrequest.aspx), [AuthenticateRequest](https://msdn.microsoft.com/library/system.web.httpapplication.authenticaterequest.aspx), [AuthorizeRequest](https://msdn.microsoft.com/library/system.web.httpapplication.authorizerequest.aspx)등입니다.

OMC 비교 하면는 [HttpModule](https://msdn.microsoft.com/library/zec9k340(v=vs.85).aspx) ASP.NET 세계 OMC는 미리 정의 된 올바른 파이프라인 이벤트에 등록 되어야 합니다. 예를 들어 HttpModule `MyModule` 요청 도달할 경우 호출 됩니다는 [AuthenticateRequest](https://msdn.microsoft.com/library/system.web.httpapplication.authenticaterequest.aspx) 파이프라인 단계에서에서:

[!code-csharp[Main](owin-middleware-in-the-iis-integrated-pipeline/samples/sample2.cs?highlight=10)]

이 동일한, 이벤트 기반 실행 순서에 참여 하도록 OMC 되려면에서는 [Katana](an-overview-of-project-katana.md) 런타임 코드를 통해 검색는 [시작 구성](owin-startup-class-detection.md) 구독 각 미들웨어 구성 요소에는 통합된 파이프라인 이벤트입니다. 예를 들어 다음 OMC 및 등록 코드를 사용 하면 기본 이벤트 등록 미들웨어 구성 요소를 볼 수 있습니다. (자세한 OWIN 시작 클래스를 만드는 방법에 대 한 지침은, 참조 [OWIN 시작 클래스 검색](owin-startup-class-detection.md).)

1. 빈 웹 응용 프로그램 프로젝트를 만들고 이름을 **owin2**합니다.
2. 패키지 관리자 콘솔 (PMC)에서 다음 명령을 실행 합니다. 

    [!code-console[Main](owin-middleware-in-the-iis-integrated-pipeline/samples/sample3.cmd)]
3. 추가 `OWIN Startup Class` 하 고 이름을 `Startup`합니다. 생성된 된 코드 (변경 내용을 강조 표시)를 다음과 같이 바꿉니다.  

    [!code-csharp[Main](owin-middleware-in-the-iis-integrated-pipeline/samples/sample4.cs?highlight=5-7,15-36)]
4. F5 키를 눌러 앱을 실행 합니다.

시작 구성 세 미들웨어 구성 요소, 처음 두 개의 진단 정보 및 이벤트에 응답 하는 마지막 트랜잭션이 표시 (및 진단 정보를 표시 하는 또한) 포함 된 파이프라인을 설정 합니다. `PrintCurrentIntegratedPipelineStage` 메서드가이 미들웨어에서 호출 되는 통합된 파이프라인 이벤트 및 메시지를 표시 합니다. 다음 출력 창을 표시 합니다.

[!code-console[Main](owin-middleware-in-the-iis-integrated-pipeline/samples/sample5.cmd)]

Katana 런타임 OWIN 미들웨어 구성 요소와의 각 매핑된 [PreExecuteRequestHandler](https://msdn.microsoft.com/library/system.web.httpapplication.prerequesthandlerexecute.aspx) IIS 파이프라인 이벤트에 해당 하는 기본적으로 [PreRequestHandlerExecute](https://msdn.microsoft.com/library/system.web.httpapplication.prerequesthandlerexecute.aspx)합니다.

## <a name="stage-markers"></a>표식 단계

사용 하 여 파이프라인의 특정 단계에서 실행 하는 OMCs를 표시할 수 있습니다는 `IAppBuilder UseStageMarker()` 확장 메서드. 특정 단계에서 미들웨어 구성 요소 집합을 실행 한 단계 마커 마지막 구성 요소 바로 뒤에 삽입을 등록 하는 동안 집합입니다. 규칙이 파이프라인의 단계에서 미들웨어를 실행할 수 있습니다 및 구성 요소 배열에서 실행 해야 합니다 (규칙은이 자습서의 뒷부분에 나오는 설명 됨). 추가 `UseStageMarker` 메서드는 `Configuration` 아래와 같이 코드:

[!code-csharp[Main](owin-middleware-in-the-iis-integrated-pipeline/samples/sample6.cs?highlight=13,19)]

`app.UseStageMarker(PipelineStage.Authenticate)` 호출 (이 경우 두 개의 진단 구성)의 모든 이전에 등록 된 미들웨어 구성 요소를 파이프라인의 인증 단계에서 실행 되도록 구성 합니다. 마지막 미들웨어 구성 요소 (표시 하는 진단 요청에 응답 하)에서 실행 되는 `ResolveCache` 단계 (의 [ResolveRequestCache](https://msdn.microsoft.com/library/system.web.httpapplication.resolverequestcache.aspx) 이벤트).

F5 키를 눌러 앱을 실행 합니다. 출력 창에 표시

[!code-console[Main](owin-middleware-in-the-iis-integrated-pipeline/samples/sample7.cmd)]

## <a name="stage-marker-rules"></a>표식 규칙 단계

Owin 미들웨어 구성 요소 (OMC) 다음 OWIN 파이프라인 단계 이벤트에서 실행 되도록 구성할 수 있습니다.

[!code-csharp[Main](owin-middleware-in-the-iis-integrated-pipeline/samples/sample8.cs)]

1. 기본적으로 OMCs 마지막 이벤트에서 실행 (`PreHandlerExecute`). 바로 이러한 이유로 첫 번째 예제 코드는 "PreExecuteRequestHandler"를 표시 합니다.
2. 사용할 수는 `app.UseStageMarker` OWIN 파이프라인의 각 단계 이전에 실행 되도록 OMC 등록에 나열 된는 `PipelineStage` 열거형입니다.
3. OWIN 파이프라인으로, IIS 파이프라인 정렬 되는 경우 따라서에 대 한 호출 `app.UseStageMarker` 순서 여야 합니다. 이벤트 처리기에 등록 된 마지막 이벤트 앞에 오는 이벤트를 설정할 수 없습니다 `app.UseStageMarker`합니다. 예를 들어 *후* 호출:

    [!code-console[Main](owin-middleware-in-the-iis-integrated-pipeline/samples/sample9.cmd)]

 에 대 한 호출이 `app.UseStageMarker` 전달 `Authenticate` 또는 `PostAuthenticate` 유효 하며, 수 없으며 예외가 throw 됩니다. 기본적으로 최신 단계에서 실행 OMCs `PreHandlerExecute`합니다. 단계 마커를 먼저 실행 되도록 하는 데 사용 됩니다. 순서가 단계 마커를 지정 하면 이전 표식에 반올림 했습니다. 즉, 한 단계 마커 추가 "단계 X 늦어도 실행" 표시 됩니다. OWIN 파이프라인의 다음에 추가 하는 가장 빠른 단계 마커 OMC의 실행 합니다.
4. 최초의 단계에 대 한 호출 `app.UseStageMarker` wins 합니다. 예를 들어, 순서를 전환 하는 경우 `app.UseStageMarker` 이전 예제에서 호출 합니다.

    [!code-csharp[Main](owin-middleware-in-the-iis-integrated-pipeline/samples/sample10.cs?highlight=13,19)]

 출력 창에 표시 됩니다. 

    [!code-console[Main](owin-middleware-in-the-iis-integrated-pipeline/samples/sample11.cmd)]

 모든 연속된 OMCs는 `AuthenticateRequest` 마지막 OMC로 등록 되었으므로 단계는 `Authenticate` 이벤트, 및 `Authenticate` 이벤트에는 다른 모든 이벤트 앞에 합니다.