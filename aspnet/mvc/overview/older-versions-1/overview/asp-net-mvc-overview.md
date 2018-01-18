---
uid: mvc/overview/older-versions-1/overview/asp-net-mvc-overview
title: "ASP.NET MVC 개요 | Microsoft Docs"
author: microsoft
description: "ASP.NET MVC 응용 프로그램 및 ASP.NET Web Forms 응용 프로그램 간의 차이점에 알아봅니다. ASP.NET MVC 응용 프로그램을 구축 하는 시기를 결정 하는 방법에 알아봅니다."
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/27/2009
ms.topic: article
ms.assetid: 2dcb44a4-5cbf-4d62-b363-718104082d86
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions-1/overview/asp-net-mvc-overview
msc.type: authoredcontent
ms.openlocfilehash: f44e6fb1e19d3c2384ebaeeca0ddea8239dd5a3c
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="aspnet-mvc-overview"></a>ASP.NET MVC 개요
====================
여 [Microsoft](https://github.com/microsoft)

> ASP.NET MVC 응용 프로그램 및 ASP.NET Web Forms 응용 프로그램 간의 차이점에 알아봅니다. ASP.NET MVC 응용 프로그램을 구축 하는 시기를 결정 하는 방법에 알아봅니다.


모델-뷰-컨트롤러 (MVC) 아키텍처 패턴에서는 응용 프로그램을 세 가지 주요 구성 요소: 모델, 뷰 및 컨트롤러입니다. ASP.NET MVC 프레임 워크는 MVC 기반 웹 응용 프로그램을 만들기 위한 ASP.NET Web Forms 패턴에 대 한 대안을 제공 합니다. ASP.NET MVC 프레임 워크는 간단 하 고 테스트 하기 편리한 프레젠테이션 프레임 워크는 (Web Forms 기반 응용 프로그램에서와 마찬가지로) 마스터 페이지 및 멤버 자격 기반 인증 같은 기존 ASP.NET 기능과 통합 되어 있습니다. MVC 프레임 워크에 정의 된는 **System.Web.Mvc** 네임 스페이스의 기본 기능, 지원 되는 일부는 **System.Web** 네임 스페이스입니다.   
  
MVC는 많은 개발자에 게 익숙한 하는 표준 디자인 패턴입니다. 일부 유형의 웹 응용 프로그램 MVC 프레임 워크에서 유용 합니다. 다른 사용자는 Web Forms 및 포스트백을 기반으로 하는 기존 ASP.NET 응용 프로그램 패턴을 사용 하려면 계속 됩니다. 다른 유형의 웹 응용 프로그램의 두 가지 방법; 결합 합니다. 상호 배타적이 지 않습니다 다른 제외합니다.   
  
MVC 프레임 워크에는 다음 구성 요소가 포함 됩니다.


[![매개 변수 값을 가지는 컨트롤러 동작 호출](asp-net-mvc-overview/_static/image1.jpg)](asp-net-mvc-overview/_static/image1.png)

**그림 01**: 매개 변수 값을 가지는 컨트롤러 동작 호출 ([전체 크기 이미지를 보려면 클릭](asp-net-mvc-overview/_static/image2.png))


- **모델**합니다. 모델 개체는 응용 프로그램의 데이터 도메인에 대 한 논리를 구현 하는 응용 프로그램의 구성 요소입니다. 종종, 모델 개체를 검색 및 모델 상태를 데이터베이스에 저장 합니다. 예를 들어 제품 개체 수 데이터베이스에서 정보를 검색할 운영, 고 SQL Server의 Products 테이블에 업데이트 된 정보를 다시 써야 합니다.

작은 응용 프로그램에서 모델은 실제 아니라 개념적 분리 경우가 많습니다. 예를 들어 뿐이 응용 프로그램에서는 보기에 전송 하 고 데이터 집합을 읽는 응용 프로그램이 없는 경우 실제 모델 계층 및 관련 된 클래스입니다. 이 경우 데이터 집합의 모델 개체의 역할을 수행 합니다.

- **뷰**합니다. 뷰는 응용 프로그램의 사용자 인터페이스 (UI)를 표시 하는 구성 요소입니다. 일반적으로이 UI는 모델 데이터에서 만들어집니다. 텍스트 상자, 드롭 다운 목록 및 확인란 Products 개체의 현재 상태에 따라 표시 하는 제품 테이블의 편집 뷰 예로 들 수 있습니다.

- **컨트롤러**합니다. 컨트롤러는 사용자 상호 작용 처리, 모델로 작업 하 고, 궁극적으로 UI를 표시 하는 렌더링할 뷰를 선택 하는 구성 요소입니다. MVC 응용 프로그램에서 뷰 정보만 표시 됩니다. 컨트롤러 처리 하며 사용자 입력 및 상호 작용에 응답 합니다. 예를 들어 컨트롤러는 쿼리 문자열 값을 처리 하 고를 쿼리하고 데이터베이스 값을 사용 하 여 모델에 이러한 값을 전달 합니다.

MVC 패턴을 사용 하면 이러한 요소 간의 느슨한 결합을 제공 하는 동안 응용 프로그램 (입력된 논리, 비즈니스 논리 및 UI 논리)의 다양 한 측면을 구분 하는 응용 프로그램을 만들 수 있습니다. 패턴 각 종류의 논리가 응용 프로그램에 있는 위치를 지정 합니다. UI 논리는 뷰에 속해 있습니다. 입력 논리는 컨트롤러에 속해 있습니다. 비즈니스 논리는 모델에 속해 있습니다. 이러한 분리 하면 구현 시 한 번에 하나의 측면에 초점을 맞추려면 있기 때문에 응용 프로그램을 빌드할 때 복잡도 관리할 수 있습니다. 예를 들어 비즈니스 논리에 따라 하지 않고 뷰에만 집중할 수 있습니다.   
  
복잡성을 관리 하는 것 외에도 MVC 패턴 쉽게 Web Forms 기반 ASP.NET 웹 응용 프로그램을 테스트 하는 것 보다 응용 프로그램을 테스트할 수 있습니다. 예를 들어 Web Forms 기반 ASP.NET 웹 응용 프로그램에서 출력을 표시 하 고 사용자 입력에 응답 하는 단일 클래스 사용 됩니다. 개별 페이지를 테스트 하려면 페이지 클래스, 모든 해당 자식 컨트롤 및 응용 프로그램의 다른 종속 클래스를 인스턴스화할 해야 하기 때문에 ASP.NET Web Forms 기반 응용 프로그램에 대 한 자동화 된 테스트 작성 복잡할 수 있습니다. 너무 많은 클래스가 인스턴스화되고 페이지를 실행 하기 때문에 응용 프로그램의 개별 부분에만 집중 하는 테스트를 작성 하기 어려울 수 있습니다. 따라서 ASP.NET Web Forms 기반 응용 프로그램에 대 한 테스트는 MVC 응용 프로그램의 테스트 보다 구현 하기가 매우 어려울 수 있습니다. 또한 Web Forms 기반 ASP.NET 응용 프로그램의 테스트는 웹 서버가 필요 합니다. MVC 프레임 워크 구성 요소를 분리 및가 프레임 워크의 나머지 부분과에서 격리 상태에서 개별 구성 요소를 테스트할 수 있는 인터페이스를 많이 사용 합니다.   
  
MVC 응용 프로그램의 세 가지 주요 구성 요소 간의 느슨한 결합은 병렬 개발을 촉진 하기도 합니다. 예를 들어 한 개발자 보기에서 작업할 수 있습니다, 두 번째 개발자는 컨트롤러 논리에서 작업할 수 있습니다 및 세 번째 개발자는 모델의 비즈니스 논리에 집중할 수 있습니다.

## <a name="deciding-when-to-create-an-mvc-application"></a>MVC 응용 프로그램을 만드는 시기 결정

신중 하 게 고려해 야 여부를 ASP.NET MVC 프레임 워크 또는 ASP.NET Web Forms 모델 중 하나를 사용 하 여 웹 응용 프로그램을 구현 합니다. MVC 프레임 워크, Web Forms 모델을 대체 하지 않습니다. 웹 응용 프로그램에 대 한 두 가지 프레임 워크를 사용할 수 있습니다. (있는 경우 기존의 Web Forms 기반 응용 프로그램, 이러한 계속 항상 정확 하 게 작동 합니다.)   
  
특정 웹 사이트에 대 한 MVC 프레임 워크와 Web Forms 모델을 사용 하도록 결정 하기 전에 각 접근법의 장점을 비교 합니다.

### <a name="advantages-of-an-mvc-based-web-application"></a>MVC 기반 웹 응용 프로그램의 이점

ASP.NET MVC 프레임 워크에는 다음과 같은 이점이 있습니다.

- 예제에서는 응용 프로그램 모델, 뷰 및 컨트롤러를 분할 하 여 복잡성을 관리 하기 쉽습니다.
- 뷰 상태 또는 서버 기반 양식을 사용 하지 않습니다. 이렇게 하면 응용 프로그램의 동작에 대 한 모든 권한을 알아보려는 개발자를 위한 이상적인 MVC 프레임 워크.
- 단일 컨트롤러를 통해 웹 응용 프로그램 요청을 처리 하는 프런트 컨트롤러 패턴을 사용 합니다. 따라서 풍부한 라우팅 인프라를 지 원하는 응용 프로그램을 디자인할 수 있습니다. 자세한 내용은 참조 [프런트 컨트롤러](https://go.microsoft.com/fwlink/?LinkId=106357 "프런트 컨트롤러") MSDN 웹 사이트에 있습니다.
- 테스트 기반 개발 (TDD)에 대 한 향상 된 지원을 제공 합니다.
- 대규모 팀의 개발자와 높은 수준의 응용 프로그램 동작을 제어 해야 하는 웹 디자이너에서 지원 되는 웹 응용 프로그램에 대 한 잘 작동 합니다.

### <a name="advantages-of-a-web-forms-based-web-application"></a>Web Forms 기반 웹 응용 프로그램의 이점

Web Forms 기반 프레임 워크에는 다음과 같은 이점이 있습니다.

- 업무의 웹 응용 프로그램 개발에 도움이 HTTP를 통해 상태를 유지 하는 이벤트 모델을 지원 합니다. Web Forms 기반 응용 프로그램은 수십 가지 수백 개의 서버 컨트롤에서에서 지원 되는 이벤트를 제공 합니다.
- 개별 페이지에 기능을 추가 하는 페이지 컨트롤러 패턴을 사용 합니다. 자세한 내용은 참조 [페이지 컨트롤러](https://go.microsoft.com/fwlink/?LinkId=106359 "페이지 컨트롤러") MSDN 웹 사이트에 있습니다.
- 상태 보기 또는 관리 상태 정보를 쉽게 수행할 수 있는 서버 기반 양식을 사용 합니다.
- 웹 개발자와 많은 수의 신속한 응용 프로그램 개발에 사용할 수 있는 구성 요소를 활용 하려는 디자이너의 소규모 팀을 위한 잘 작동 합니다.
- 덜 복잡 한 응용 프로그램 개발에 일반적으로 때문에 구성 요소 (의 **페이지** 클래스, 컨트롤 및 등) 긴밀 하 게 통합 하 고 일반적으로 MVC 모델 보다 적은 코드를 필요 합니다.

## <a name="features-of-the-aspnet-mvc-framework"></a>ASP.NET MVC 프레임 워크의 기능

ASP.NET MVC 프레임 워크에서는 다음과 같은 기능을 제공합니다.

- (입력된 논리, 비즈니스 논리 및 UI 논리) 응용 프로그램 작업, 테스트 용이성 및 테스트 구동 방식 개발 (TDD) 기본적으로 분리 합니다. MVC 프레임 워크의 모든 핵심 계약은 인터페이스에 기반 하며 모의 개체는 응용 프로그램의 실제 개체의 동작을 모방 하는 시뮬레이션된 개체를 사용 하 여 테스트할 수 있습니다. 있습니다 수 단위 테스트 응용 프로그램이 있으므로 단위 테스트 신속 하 고 유연한 ASP.NET 프로세스에서 컨트롤러를 실행 하지 않고도 합니다. .NET Framework와 호환 되는 모든 단위 테스트 프레임 워크를 사용할 수 있습니다.
- 확장 가능한 플러그형 프레임 워크입니다. ASP.NET MVC 프레임 워크의 구성 요소는 쉽게 교체 하 하거나 사용자 지정할 수 있도록 설계 되었습니다. 사용자 고유의 뷰 엔진, URL 라우팅 정책, 작업 메서드 매개 변수 serialization 및 기타 구성 요소에 연결할 수 있습니다. ASP.NET MVC 프레임 워크는 또한 DI (Dependency Injection) 및의 IOC (Inversion Control) 컨테이너 모델의 사용을 지원 합니다. DI를 사용 하면 개체 자체를 만들 클래스에 의존 하지 않고 클래스에 개체를 삽입할 수 있습니다. IOC 하 개체는 다른 개체를 필요한 경우 첫 번째 개체가 두 번째 개체에서에서 가져와야 구성 파일 같은 외부 소스를 지정 합니다. 이렇게 하면 테스트를 보다 쉽게 있습니다.
- 강력한 URL 매핑 구성 요소 알기 쉽고 검색 가능한 Url이 있는 응용 프로그램을 작성할 수 있습니다. Url에 파일 이름 확장명을 포함 하지 않아도 및 검색에 대 한 잘 작동 하는 URL 이름 지정 패턴을 지원 하도록 설계 된 최적화 (SEO) 및 주소 지정 (REST) representational state transfer 엔진입니다.
- 기존의 ASP.NET 페이지 (.aspx 파일), 사용자 정의 컨트롤 (.ascx 파일) 및 마스터 페이지 (.master 파일) 태그 파일의 태그를 뷰 템플릿으로 사용 하 여 지원 합니다. 있습니다 수 기존 ASP.NET 기능을 사용 하 여 ASP.NET MVC 프레임 워크 중첩 된 마스터 페이지, 인라인 식 (&lt;% = %&gt;), 선언적 서버 컨트롤, 템플릿, 데이터 바인딩, 지역화, 및 등입니다.
- 기존 ASP.NET 기능에 대 한 지원입니다. ASP.NET MVC를 사용 하면 폼 인증 및 Windows 인증, URL 권한 부여, 멤버 자격 및 역할, 출력 및 데이터 캐싱, 세션 및 프로 파일 상태 관리, 상태 모니터링, 구성 시스템 및 공급자와 같은 기능을 사용 하 여 아키텍처입니다.