---
uid: web-forms/overview/ajax-control-toolkit/animation/executing-animations-using-client-side-code-cs
title: "클라이언트 쪽 코드 (C#)를 사용 하 여 애니메이션 실행 | Microsoft Docs"
author: wenz
description: "ASP.NET AJAX 컨트롤 도구 키트에서 애니메이션 컨트롤은 컨트롤 뿐 아니라 애니메이션 컨트롤을 추가 하는 전체 프레임 워크. 애니메이션 실행 중..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: 0270e0df-6fde-4a8f-a2cb-2cacc55143f2
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/executing-animations-using-client-side-code-cs
msc.type: authoredcontent
ms.openlocfilehash: 6b1911686a79aa692ef193430cd0746a2511105a
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="executing-animations-using-client-side-code-c"></a><span data-ttu-id="27df0-104">클라이언트 쪽 코드 (C#)를 사용 하 여 실행 중인 애니메이션</span><span class="sxs-lookup"><span data-stu-id="27df0-104">Executing Animations Using Client-Side Code (C#)</span></span>
====================
<span data-ttu-id="27df0-105">으로 [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="27df0-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="27df0-106">[코드를 다운로드](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation10.cs.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation10CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="27df0-106">[Download Code](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation10.cs.zip) or [Download PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation10CS.pdf)</span></span>

> <span data-ttu-id="27df0-107">ASP.NET AJAX 컨트롤 도구 키트에서 애니메이션 컨트롤은 컨트롤 뿐 아니라 애니메이션 컨트롤을 추가 하는 전체 프레임 워크.</span><span class="sxs-lookup"><span data-stu-id="27df0-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="27df0-108">애니메이션 실행 사용자 지정 클라이언트 쪽 JavaScript 코드를 사용 하 여 트리거될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27df0-108">The animation execution may also be triggered using custom client-side JavaScript code.</span></span>


## <a name="overview"></a><span data-ttu-id="27df0-109">개요</span><span class="sxs-lookup"><span data-stu-id="27df0-109">Overview</span></span>

<span data-ttu-id="27df0-110">ASP.NET AJAX 컨트롤 도구 키트에서 애니메이션 컨트롤은 컨트롤 뿐 아니라 애니메이션 컨트롤을 추가 하는 전체 프레임 워크.</span><span class="sxs-lookup"><span data-stu-id="27df0-110">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="27df0-111">애니메이션 실행 사용자 지정 클라이언트 쪽 JavaScript 코드를 사용 하 여 트리거될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27df0-111">The animation execution may also be triggered using custom client-side JavaScript code.</span></span>

## <a name="steps"></a><span data-ttu-id="27df0-112">단계</span><span class="sxs-lookup"><span data-stu-id="27df0-112">Steps</span></span>

<span data-ttu-id="27df0-113">우선, 포함 된 `ScriptManager` 페이지; 그런 다음 ASP.NET AJAX 라이브러리 로드 되는 제어 도구 키트를 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="27df0-113">First of all, include the `ScriptManager` in the page; then, the ASP.NET AJAX library is loaded, making it possible to use the Control Toolkit:</span></span>

[!code-aspx[Main](executing-animations-using-client-side-code-cs/samples/sample1.aspx)]

<span data-ttu-id="27df0-114">그러면 다음과 같은 텍스트의 패널에 애니메이션 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="27df0-114">The animation will be applied to a panel of text which looks like this:</span></span>

[!code-aspx[Main](executing-animations-using-client-side-code-cs/samples/sample2.aspx)]

<span data-ttu-id="27df0-115">패널에 대 한 연결 된 CSS 클래스 좋은 배경색을 정의 하 고도 패널 고정된 폭을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="27df0-115">In the associated CSS class for the panel, define a nice background color and also set a fixed width for the panel:</span></span>

[!code-css[Main](executing-animations-using-client-side-code-cs/samples/sample3.css)]

<span data-ttu-id="27df0-116">그런 다음 추가 `AnimationExtender` 페이지에 제공 하는 `ID`, `TargetControlID` 특성과 반드시 `runat="server"`:</span><span class="sxs-lookup"><span data-stu-id="27df0-116">Then, add the `AnimationExtender` to the page, providing an `ID`, the `TargetControlID` attribute and the obligatory `runat="server"`:</span></span>

[!code-aspx[Main](executing-animations-using-client-side-code-cs/samples/sample4.aspx)]

<span data-ttu-id="27df0-117">내에서 `<Animations>` 노드를 사용 하 여 `<OnClick>` 패널에 사용자 애니메이션을 한 번 실행 하려면를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="27df0-117">Within the `<Animations>` node, use `<OnClick>` to run the animations once the user clicks on the panel.</span></span> <span data-ttu-id="27df0-118">Parallelly 실행할 두 개의 애니메이션이 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="27df0-118">Add two animations to be executed parallelly:</span></span>

[!code-xml[Main](executing-animations-using-client-side-code-cs/samples/sample5.xml)]

<span data-ttu-id="27df0-119">으로이 애니메이션 (및 제어 도구 키트를 사용 하 여 만든 다른 애니메이션) 실행 되는 페이지 실행 되 면 JavaScript 코드를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="27df0-119">For the sake of demonstration, this animation (and any other animation created using the Control Toolkit) is executed using JavaScript code, once the page runs.</span></span> <span data-ttu-id="27df0-120">모든 것에 대 한 액세스는 `AnimationExtender` 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="27df0-120">First of all we need access to the `AnimationExtender` control.</span></span> <span data-ttu-id="27df0-121">ASP.NET AJAX 라이브러리에서 제공 된 `$find()` 이 작업에 대 한 함수:</span><span class="sxs-lookup"><span data-stu-id="27df0-121">The ASP.NET AJAX library provides the `$find()` function for this task:</span></span>

[!code-csharp[Main](executing-animations-using-client-side-code-cs/samples/sample6.cs)]

<span data-ttu-id="27df0-122">`AnimationExtender` 제어와 이름이 같은 XML 태그에서 사용 하는 이벤트 처리기 메서드를 포함 하 여 다양 한 API를 노출: `OnClick()`, `OnLoad()`등입니다.</span><span class="sxs-lookup"><span data-stu-id="27df0-122">The `AnimationExtender` control exposes a rich API, including methods with names identical to the event handlers used in the XML markup: `OnClick()`, `OnLoad()`, and so on.</span></span> <span data-ttu-id="27df0-123">예를 들어, 호출은 `OnClick()` 메서드가 실행 내에서 애니메이션은 `<OnClick>` 의 요소는 `AnimationExtender` 컨트롤:</span><span class="sxs-lookup"><span data-stu-id="27df0-123">For instance, a call of the `OnClick()` method executes the animation within the `<OnClick>` element of the `AnimationExtender` control:</span></span>

[!code-javascript[Main](executing-animations-using-client-side-code-cs/samples/sample7.js)]

<span data-ttu-id="27df0-124">페이지가 완전히 로드 되 면 패널 클릭을 에뮬레이션 하는 전체 클라이언트 쪽 JavaScript 코드를 확인 하는 다음과 같습니다는 `pageLoad()`에 의해 호출 되는 ASP.NET AJAX 한 번 페이지 함수 이름을 사용 하 고 모든 포함 된 라이브러리는 JavaScript 로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="27df0-124">Here is the complete client-side JavaScript code that emulates the click on the panel once the page has been fully loaded note that the `pageLoad()` function name is used which is called by ASP.NET AJAX once the page and all included JavaScript libraries have been loaded.</span></span>

[!code-html[Main](executing-animations-using-client-side-code-cs/samples/sample8.html)]


<span data-ttu-id="27df0-125">[![애니메이션은 마우스 클릭 하지 않고 즉시 실행](executing-animations-using-client-side-code-cs/_static/image2.png)](executing-animations-using-client-side-code-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="27df0-125">[![The animation runs immediately, without a mouse click](executing-animations-using-client-side-code-cs/_static/image2.png)](executing-animations-using-client-side-code-cs/_static/image1.png)</span></span>

<span data-ttu-id="27df0-126">마우스 클릭 하지 않고 애니메이션 즉시 실행 ([전체 크기 이미지를 보려면 클릭](executing-animations-using-client-side-code-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="27df0-126">The animation runs immediately, without a mouse click ([Click to view full-size image](executing-animations-using-client-side-code-cs/_static/image3.png))</span></span>

>[!div class="step-by-step"]
<span data-ttu-id="27df0-127">[이전](modifying-animations-from-the-server-side-cs.md)
[다음](changing-an-animation-using-client-side-code-cs.md)</span><span class="sxs-lookup"><span data-stu-id="27df0-127">[Previous](modifying-animations-from-the-server-side-cs.md)
[Next](changing-an-animation-using-client-side-code-cs.md)</span></span>