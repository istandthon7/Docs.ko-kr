---
uid: web-forms/overview/ajax-control-toolkit/combobox/how-do-i-use-the-combobox-control-vb
title: "ComboBox 컨트롤을 사용 하려면 어떻게 해야 합니까? (VB) | Microsoft Docs"
author: microsoft
description: "콤보 상자에는 사용자가 선택할 수 있는 옵션의 목록을 사용 하 여 입력란의 유연성을 결합 하는 ASP.NET AJAX 컨트롤입니다."
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/12/2009
ms.topic: article
ms.assetid: e887e7b2-a6e7-4a28-a134-ba334494badb
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/combobox/how-do-i-use-the-combobox-control-vb
msc.type: authoredcontent
ms.openlocfilehash: 54e36cf275dcc4b85253dc3b8bb5b0dbb027af77
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="how-do-i-use-the-combobox-control-vb"></a><span data-ttu-id="7b0f9-104">ComboBox 컨트롤을 사용 하려면 어떻게 해야 합니까?</span><span class="sxs-lookup"><span data-stu-id="7b0f9-104">How do I use the ComboBox Control?</span></span> <span data-ttu-id="7b0f9-105">(VB)</span><span class="sxs-lookup"><span data-stu-id="7b0f9-105">(VB)</span></span>
====================
<span data-ttu-id="7b0f9-106">여 [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="7b0f9-106">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="7b0f9-107">콤보 상자에는 사용자가 선택할 수 있는 옵션의 목록을 사용 하 여 입력란의 유연성을 결합 하는 ASP.NET AJAX 컨트롤입니다.</span><span class="sxs-lookup"><span data-stu-id="7b0f9-107">ComboBox is an ASP.NET AJAX control that combines the flexibility of a TextBox with a list of options from which users can choose.</span></span>


<span data-ttu-id="7b0f9-108">이 자습서의 목표 AJAX 컨트롤 Toolkit ComboBox 컨트롤을 설명 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="7b0f9-108">The goal of this tutorial is to explain the AJAX Control Toolkit ComboBox control.</span></span> <span data-ttu-id="7b0f9-109">ComboBox 표준 ASP.NET DropDownList 컨트롤 및 TextBox 컨트롤 간의 조합 처럼 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="7b0f9-109">The ComboBox works like a combination between a standard ASP.NET DropDownList control and a TextBox control.</span></span> <span data-ttu-id="7b0f9-110">항목의 기존 목록에서 선택 하거나 새 항목을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b0f9-110">You can either select from a pre-existing list of items or enter a new item.</span></span>

<span data-ttu-id="7b0f9-111">ComboBox 자동 완성 컨트롤 extender를 유사 하지만 컨트롤은 다양 한 시나리오에서 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b0f9-111">The ComboBox is similar to the AutoComplete control extender, but the controls are used in different scenarios.</span></span> <span data-ttu-id="7b0f9-112">자동 완성 extender 일치 하는 항목을 검색 하는 웹 서비스를 쿼리 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b0f9-112">The AutoComplete extender queries a web service to get matching entries.</span></span> <span data-ttu-id="7b0f9-113">반면, ComboBox 컨트롤 항목의 집합으로 초기화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b0f9-113">The ComboBox control, in contrast, is initialized with a set of items.</span></span> <span data-ttu-id="7b0f9-114">자동 완성 extender는 사용 하 여 의미 ComboBox 컨트롤을 사용 하는 동안 다양 한 데이터 (자동차 부분의 수백만)를 사용 하 여 작업할 때 적합 한 작은 데이터 집합 작업 (자동차 부분의 수십).</span><span class="sxs-lookup"><span data-stu-id="7b0f9-114">Using the AutoComplete extender makes sense when you are working with a large set of data (millions of car parts) while using the ComboBox control makes sense when working with a small set of data (dozens of car parts).</span></span>

## <a name="selecting-from-a-static-list-of-items"></a><span data-ttu-id="7b0f9-115">항목의 정적 목록에서 선택</span><span class="sxs-lookup"><span data-stu-id="7b0f9-115">Selecting from a Static List of Items</span></span>

<span data-ttu-id="7b0f9-116">ComboBox 컨트롤을 사용 하는 간단한 예제로 시작 하는 s를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b0f9-116">Let�s start with a simple sample of using the ComboBox control.</span></span> <span data-ttu-id="7b0f9-117">드롭다운 목록에서 항목의 정적 목록을 표시 하 고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b0f9-117">Imagine that you want to display a static list of items in a dropdown list.</span></span> <span data-ttu-id="7b0f9-118">그러나 목록이 완전 한지 가능성 남겨 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b0f9-118">However, you want to leave open the possibility that the list is not complete.</span></span> <span data-ttu-id="7b0f9-119">사용자가 목록에 사용자 지정 값을 입력 하도록 허용 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b0f9-119">You want to allow a user to enter a custom value into the list.</span></span>

<span data-ttu-id="7b0f9-120">म ll 새 ASP.NET Web Forms 페이지를 만들고 페이지에서 ComboBox 컨트롤을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b0f9-120">We�ll create a new ASP.NET Web Forms page and use the ComboBox control in the page.</span></span> <span data-ttu-id="7b0f9-121">ASP.NET 페이지에 새 프로젝트에 추가 하 고 디자인 뷰로 전환 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b0f9-121">Add the new ASP.NET page to your project and switch to Design view.</span></span>

<span data-ttu-id="7b0f9-122">페이지에서 ComboBox 컨트롤을 사용 하려면 페이지에 ScriptManager 컨트롤을 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b0f9-122">If you want to use the ComboBox control in the page then you must add a ScriptManager control to the page.</span></span> <span data-ttu-id="7b0f9-123">ScriptManager 컨트롤을 AJAX 확장 탭 아래에서 디자이너 화면으로 끕니다.</span><span class="sxs-lookup"><span data-stu-id="7b0f9-123">Drag the ScriptManager control from beneath the AJAX Extensions tab onto the Designer surface.</span></span> <span data-ttu-id="7b0f9-124">페이지 맨 위에 있는 ScriptManager 컨트롤을 추가 해야 여는 서버 쪽 아래 바로 추가할 수 있습니다 &lt;양식&gt; 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="7b0f9-124">You should add the ScriptManager control at the top of the page; you can add it immediately below the opening server-side &lt;form&gt; tag.</span></span>

<span data-ttu-id="7b0f9-125">다음으로 페이지로 ComboBox 컨트롤을 끕니다.</span><span class="sxs-lookup"><span data-stu-id="7b0f9-125">Next, drag the ComboBox control onto the page.</span></span> <span data-ttu-id="7b0f9-126">다른 들어 컨트롤 및 컨트롤 extender (그림 1 참조) 도구 상자에서 ComboBox 컨트롤을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b0f9-126">You can find the ComboBox control in the Toolbox with the other AJAX Control Toolkit controls and control extenders (see figure1).</span></span>


<span data-ttu-id="7b0f9-127">[![명함을 만들기 위한 단순 양식](how-do-i-use-the-combobox-control-vb/_static/image1.jpg)](how-do-i-use-the-combobox-control-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="7b0f9-127">[![Simple form for creating a business card](how-do-i-use-the-combobox-control-vb/_static/image1.jpg)](how-do-i-use-the-combobox-control-vb/_static/image1.png)</span></span>

<span data-ttu-id="7b0f9-128">**그림 01**: 도구 상자에서 ComboBox 컨트롤을 선택 하면 ([전체 크기 이미지를 보려면 클릭](how-do-i-use-the-combobox-control-vb/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="7b0f9-128">**Figure 01**: Selecting the ComboBox control from the toolbox ([Click to view full-size image](how-do-i-use-the-combobox-control-vb/_static/image2.png))</span></span>


<span data-ttu-id="7b0f9-129">म ll ComboBox 컨트롤을 사용 하 여 선택 항목의 정적 목록을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b0f9-129">We�ll use the ComboBox control to display a static list of choices.</span></span> <span data-ttu-id="7b0f9-130">사용자의 세 개의 선택 목록에서 spiciness 자신의 음식에 대 한 특정 수준의 선택할 수: 가벼운 욕설, 보통 및 핫 (그림 2 참조).</span><span class="sxs-lookup"><span data-stu-id="7b0f9-130">The user can select a particular level of spiciness for their food from a list of three choices: Mild, Medium, and Hot (see Figure 2).</span></span>


<span data-ttu-id="7b0f9-131">[![항목의 정적 목록에서 선택](how-do-i-use-the-combobox-control-vb/_static/image2.jpg)](how-do-i-use-the-combobox-control-vb/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="7b0f9-131">[![Selecting from a static list of items](how-do-i-use-the-combobox-control-vb/_static/image2.jpg)](how-do-i-use-the-combobox-control-vb/_static/image3.png)</span></span>

<span data-ttu-id="7b0f9-132">**그림 02**: 항목의 정적 목록에서 선택 ([전체 크기 이미지를 보려면 클릭](how-do-i-use-the-combobox-control-vb/_static/image4.png))</span><span class="sxs-lookup"><span data-stu-id="7b0f9-132">**Figure 02**: Selecting from a static list of items([Click to view full-size image](how-do-i-use-the-combobox-control-vb/_static/image4.png))</span></span>


<span data-ttu-id="7b0f9-133">두 가지 방법으로 이러한 선택을 ComboBox 컨트롤을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b0f9-133">There are two ways that you can add these choices to the ComboBox control.</span></span> <span data-ttu-id="7b0f9-134">디자인 뷰에서 컨트롤을 마우스로 가리키면 때 옵션 편집 작업 옵션을 선택 하 고 항목 편집기를 열려면 먼저 (그림 3 참조).</span><span class="sxs-lookup"><span data-stu-id="7b0f9-134">First, you select the Edit Options task option when hovering your mouse over the control in Design view and open the Item Editor (see Figure 3).</span></span>


<span data-ttu-id="7b0f9-135">[![콤보 상자 항목 편집](how-do-i-use-the-combobox-control-vb/_static/image3.jpg)](how-do-i-use-the-combobox-control-vb/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="7b0f9-135">[![Editing ComboBox items](how-do-i-use-the-combobox-control-vb/_static/image3.jpg)](how-do-i-use-the-combobox-control-vb/_static/image5.png)</span></span>

<span data-ttu-id="7b0f9-136">**그림 03**: 콤보 상자 편집 항목 ([전체 크기 이미지를 보려면 클릭](how-do-i-use-the-combobox-control-vb/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="7b0f9-136">**Figure 03**: Editing ComboBox items([Click to view full-size image](how-do-i-use-the-combobox-control-vb/_static/image6.png))</span></span>


<span data-ttu-id="7b0f9-137">두 번째 옵션은 여는 태그와 닫는 사이에서 항목의 목록을 추가할 &lt;asp: ComboBox&gt; 소스 뷰에서 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="7b0f9-137">The second option is to add the list of items in between the opening and closing &lt;asp:ComboBox&gt; tags in Source view.</span></span> <span data-ttu-id="7b0f9-138">목록 1의 페이지 항목 목록이 있는 업데이트 된 콤보 상자를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b0f9-138">The page in Listing 1 contains the updated ComboBox that has the list of items.</span></span>

<span data-ttu-id="7b0f9-139">**1-Static.aspx 나열**</span><span class="sxs-lookup"><span data-stu-id="7b0f9-139">**Listing 1 - Static.aspx**</span></span>

[!code-aspx[Main](how-do-i-use-the-combobox-control-vb/samples/sample1.aspx)]

<span data-ttu-id="7b0f9-140">목록 1의 페이지를 열 때 콤보 상자에서 기존 옵션 중 하나를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b0f9-140">When you open the page in Listing 1, you can select one of the pre-existing options from the ComboBox.</span></span> <span data-ttu-id="7b0f9-141">즉, ComboBox DropDownList 컨트롤과 마찬가지로 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="7b0f9-141">In other words, the ComboBox works just like a DropDownList control.</span></span>

<span data-ttu-id="7b0f9-142">그러나 새로운 항목 (예를 들어 슈퍼 매운) 기존 목록에 없는 입력 하는 옵션도 제공 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b0f9-142">However, you also have the option of entering a new choice (for example, Super Spicy) that is not in the existing list.</span></span> <span data-ttu-id="7b0f9-143">따라서 콤보 상자는 또한 TextBox 컨트롤 처럼 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="7b0f9-143">So, the ComboBox also works like a TextBox control.</span></span>

<span data-ttu-id="7b0f9-144">기존 선택 여부에 관계 없이 항목 또는 사용자 입력 항목을 사용자 지정 폼을 제출 하면 사용자가 선택한 레이블 컨트롤에 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b0f9-144">Regardless of whether you pick a pre-existing item or you enter a custom item, when you submit the form, your choice appears in the label control.</span></span> <span data-ttu-id="7b0f9-145">btnSubmit 폼을 제출할 때\_클릭 처리기를 실행 하 고 레이블을 업데이트 (그림 4 참조).</span><span class="sxs-lookup"><span data-stu-id="7b0f9-145">When you submit the form, the btnSubmit\_Click handler executes and updates the label (see Figure 4).</span></span>


<span data-ttu-id="7b0f9-146">[![선택한 항목 표시](how-do-i-use-the-combobox-control-vb/_static/image4.jpg)](how-do-i-use-the-combobox-control-vb/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="7b0f9-146">[![Displaying the selected item](how-do-i-use-the-combobox-control-vb/_static/image4.jpg)](how-do-i-use-the-combobox-control-vb/_static/image7.png)</span></span>

<span data-ttu-id="7b0f9-147">**그림 04**: 선택한 항목 표시 ([전체 크기 이미지를 보려면 클릭](how-do-i-use-the-combobox-control-vb/_static/image8.png))</span><span class="sxs-lookup"><span data-stu-id="7b0f9-147">**Figure 04**: Displaying the selected item([Click to view full-size image](how-do-i-use-the-combobox-control-vb/_static/image8.png))</span></span>


<span data-ttu-id="7b0f9-148">콤보 상자 폼을 제출 하는 선택한 항목을 검색 하기 위한 DropDownList 컨트롤과 같은 속성을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b0f9-148">The ComboBox supports the same properties as the DropDownList control for retrieving the selected item after a form is submitted:</span></span>

- <span data-ttu-id="7b0f9-149">SelectedItem.Text-선택한 항목의 Text 속성의 값을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b0f9-149">SelectedItem.Text - Displays the value of the Text property of the selected item.</span></span>
- <span data-ttu-id="7b0f9-150">SelectedItem.Value-선택한 항목의 Value 속성의 값을 표시 하거나 콤보 상자에 입력 된 텍스트를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b0f9-150">SelectedItem.Value - Displays the value of the Value property of the selected item or displays the text typed into the ComboBox.</span></span>
- <span data-ttu-id="7b0f9-151">SelectedValue-동일 하지만 SelectedItem.Value이이 속성을 사용 하면 기본값 (초기) 선택된 항목을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b0f9-151">SelectedValue - Same as SelectedItem.Value except that this property enables you to specify the default (initial) selected item.</span></span>

<span data-ttu-id="7b0f9-152">입력 한 다음 사용자 지정 선택 콤보 상자에 사용자 지정 선택은 SelectedItem.Text와 SelectedItem.Value 속성에 할당 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b0f9-152">If you type a custom choice into the ComboBox then the custom choice is assigned to both the SelectedItem.Text and SelectedItem.Value properties.</span></span>

## <a name="selecting-the-list-of-items-from-the-database"></a><span data-ttu-id="7b0f9-153">데이터베이스에서 항목의 목록을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7b0f9-153">Selecting the List of Items from the Database</span></span>

<span data-ttu-id="7b0f9-154">데이터베이스에서 콤보 상자를 표시 하는 항목 목록을 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b0f9-154">You can retrieve the list of items that the ComboBox displays from a database.</span></span> <span data-ttu-id="7b0f9-155">예를 들어 SqlDataSource 컨트롤, ObjectDataSource 컨트롤는 LinqDataSource 또는 EntityDataSource ComboBox를 바인딩할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b0f9-155">For example, you can bind the ComboBox to a SqlDataSource control, an ObjectDataSource control, a LinqDataSource, or an EntityDataSource.</span></span>

<span data-ttu-id="7b0f9-156">ComboBox에 동영상 목록을 표시 하 고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b0f9-156">Imagine that you want to display a list of movies in a ComboBox.</span></span> <span data-ttu-id="7b0f9-157">영화 데이터베이스 테이블에서 영화 목록을 검색 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b0f9-157">You want to retrieve the list of movies from the Movies database table.</span></span> <span data-ttu-id="7b0f9-158">아래 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="7b0f9-158">Follow these steps:</span></span>

1. <span data-ttu-id="7b0f9-159">Movies.aspx 라는 페이지 만들기</span><span class="sxs-lookup"><span data-stu-id="7b0f9-159">Create a page named Movies.aspx</span></span>
2. <span data-ttu-id="7b0f9-160">AJAX 확장 탭 아래쪽에서 ScriptManager 페이지 도구 상자에서 끌어 페이지에 ScriptManager 컨트롤을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b0f9-160">Add a ScriptManager control to the page by dragging the ScriptManager from under the AJAX Extensions tab in the Toolbox onto the page.</span></span>
3. <span data-ttu-id="7b0f9-161">ComboBox를 페이지로 끌어 페이지로 ComboBox 컨트롤을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b0f9-161">Add a ComboBox control to the page by dragging the ComboBox onto the page.</span></span>
4. <span data-ttu-id="7b0f9-162">디자인 뷰에서 마우스 포인터로 ComboBox 컨트롤을 선택 하 고는 **데이터 소스 선택** 작업 옵션 (그림 5 참조).</span><span class="sxs-lookup"><span data-stu-id="7b0f9-162">In Design view, hover your mouse over the ComboBox control and select the **Choose Data Source** task option (see Figure 5).</span></span> <span data-ttu-id="7b0f9-163">데이터 소스 구성 마법사가 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b0f9-163">The Data Source Configuration Wizard is launched.</span></span>
5. <span data-ttu-id="7b0f9-164">에 **데이터 원본을 선택** 단계에서는 &lt;새 데이터 원본을&gt; 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="7b0f9-164">In the **Choose a Data Source** step, select the &lt;New data source�&gt; option.</span></span>
6. <span data-ttu-id="7b0f9-165">에 **데이터 소스 형식 선택** 단계, 데이터베이스를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b0f9-165">In the **Choose a Data Source Type** step, select Database.</span></span>
7. <span data-ttu-id="7b0f9-166">에 **데이터 연결 선택** 단계, (예를 들어 MoviesDB.mdf) 해당 데이터베이스를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b0f9-166">In the **Choose Your Data Connection** step, select your database (for example, MoviesDB.mdf).</span></span>
8. <span data-ttu-id="7b0f9-167">에 **응용 프로그램 구성 파일에 연결 문자열 저장** 단계, 연결 문자열을 저장 하도록 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b0f9-167">In the **Save the Connection String to the Application Configuration File** step, select the option to save your connection string.</span></span>
9. <span data-ttu-id="7b0f9-168">에 **Select 문 구성** 단계 영화 데이터베이스 테이블을 선택 하 고 모든 열을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b0f9-168">In the **Configure the Select Statement** step, select the Movies database table and select all of the columns.</span></span>
10. <span data-ttu-id="7b0f9-169">에 **쿼리 테스트** 단계, "마침" 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b0f9-169">In the **Test Query** step, click the Finish button.</span></span>
11. <span data-ttu-id="7b0f9-170">에 **데이터 소스 선택** 단계에서 선택 표시 하려면 필드에 대 한 Title 열 및 데이터에 대 한 Id 열 필드 (그림 참조).</span><span class="sxs-lookup"><span data-stu-id="7b0f9-170">Back in the **Choose Data Source** step, select the Title column for the field to display and the Id column for the data field (see Figure).</span></span>
12. <span data-ttu-id="7b0f9-171">마법사를 닫으려면 확인 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b0f9-171">Click the OK button to close the wizard.</span></span>


<span data-ttu-id="7b0f9-172">[![데이터 원본 선택](how-do-i-use-the-combobox-control-vb/_static/image5.jpg)](how-do-i-use-the-combobox-control-vb/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="7b0f9-172">[![Choosing a data source](how-do-i-use-the-combobox-control-vb/_static/image5.jpg)](how-do-i-use-the-combobox-control-vb/_static/image9.png)</span></span>

<span data-ttu-id="7b0f9-173">**그림 05**: 데이터 원본 선택 ([전체 크기 이미지를 보려면 클릭](how-do-i-use-the-combobox-control-vb/_static/image10.png))</span><span class="sxs-lookup"><span data-stu-id="7b0f9-173">**Figure 05**: Choosing a data source([Click to view full-size image](how-do-i-use-the-combobox-control-vb/_static/image10.png))</span></span>


<span data-ttu-id="7b0f9-174">[![데이터 텍스트 및 값 필드를 선택합니다.](how-do-i-use-the-combobox-control-vb/_static/image6.jpg)](how-do-i-use-the-combobox-control-vb/_static/image11.png)</span><span class="sxs-lookup"><span data-stu-id="7b0f9-174">[![Choosing the data text and value fields](how-do-i-use-the-combobox-control-vb/_static/image6.jpg)](how-do-i-use-the-combobox-control-vb/_static/image11.png)</span></span>

<span data-ttu-id="7b0f9-175">**그림 06**: 데이터 텍스트 및 값 필드 선택 ([전체 크기 이미지를 보려면 클릭](how-do-i-use-the-combobox-control-vb/_static/image12.png))</span><span class="sxs-lookup"><span data-stu-id="7b0f9-175">**Figure 06**: Choosing the data text and value fields([Click to view full-size image](how-do-i-use-the-combobox-control-vb/_static/image12.png))</span></span>


<span data-ttu-id="7b0f9-176">위의 단계를 완료 한 후 ComboBox 영화 데이터베이스 테이블에서의 영화를 나타내는 SqlDataSource 컨트롤에 바인딩됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b0f9-176">After you complete the steps above, the ComboBox is bound to a SqlDataSource control that represents the movies from the Movies database table.</span></span> <span data-ttu-id="7b0f9-177">페이지에 대 한 소스 (I 정리 서식을 약간) 목록 2와 유사 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b0f9-177">The source for the page looks like Listing 2 (I cleaned up the formatting a little bit).</span></span>

<span data-ttu-id="7b0f9-178">**2-Movies.aspx 나열**</span><span class="sxs-lookup"><span data-stu-id="7b0f9-178">**Listing 2 - Movies.aspx**</span></span>

[!code-aspx[Main](how-do-i-use-the-combobox-control-vb/samples/sample2.aspx)]

<span data-ttu-id="7b0f9-179">ComboBox 컨트롤 SqlDataSource 컨트롤을 가리키는 DataSourceID 속성을 갖고 있음을 알게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b0f9-179">Notice that the ComboBox control has a DataSourceID property that points to the SqlDataSource control.</span></span> <span data-ttu-id="7b0f9-180">브라우저에서 페이지를 열 때 데이터베이스에서 영화 목록이 표시 됩니다 (그림 7 참조).</span><span class="sxs-lookup"><span data-stu-id="7b0f9-180">When you open the page in a browser, the list of movies from the database is displayed (see Figure 7).</span></span> <span data-ttu-id="7b0f9-181">선택 목록에서 영화 수 또는 동영상 콤보 상자에 입력 하 여 새 동영상을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b0f9-181">You can either a pick a movie from the list or enter a new movie by typing the movie into the ComboBox.</span></span>


<span data-ttu-id="7b0f9-182">[![동영상 목록을 표시합니다.](how-do-i-use-the-combobox-control-vb/_static/image7.jpg)](how-do-i-use-the-combobox-control-vb/_static/image13.png)</span><span class="sxs-lookup"><span data-stu-id="7b0f9-182">[![Displaying a list of movies](how-do-i-use-the-combobox-control-vb/_static/image7.jpg)](how-do-i-use-the-combobox-control-vb/_static/image13.png)</span></span>

<span data-ttu-id="7b0f9-183">**그림 07**: 영화 목록이 표시 ([전체 크기 이미지를 보려면 클릭](how-do-i-use-the-combobox-control-vb/_static/image14.png))</span><span class="sxs-lookup"><span data-stu-id="7b0f9-183">**Figure 07**: Displaying a list of movies([Click to view full-size image](how-do-i-use-the-combobox-control-vb/_static/image14.png))</span></span>


## <a name="setting-the-dropdownstyle"></a><span data-ttu-id="7b0f9-184">DropDownStyle는 설정</span><span class="sxs-lookup"><span data-stu-id="7b0f9-184">Setting the DropDownStyle</span></span>

<span data-ttu-id="7b0f9-185">ComboBox의 동작을 변경 하려면 ComboBox DropDownStyle 속성을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b0f9-185">You can use the ComboBox DropDownStyle property to change the behavior of the ComboBox.</span></span> <span data-ttu-id="7b0f9-186">이 속성은 있는 허용 가능한 값:</span><span class="sxs-lookup"><span data-stu-id="7b0f9-186">This property accepts there possible values:</span></span>

- <span data-ttu-id="7b0f9-187">드롭다운-(기본값)는 ComboBox 드롭다운 목록에서 화살표를 클릭할 때 표시 됩니다는 사용자 지정 값을 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b0f9-187">DropDown - (default value) The ComboBox displays a dropdown list when you click the arrow and you can enter a custom value.</span></span>
- <span data-ttu-id="7b0f9-188">단순-ComboBox 드롭다운 목록을 자동으로 표시 하 고 사용자 지정 값을 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b0f9-188">Simple - The ComboBox displays a dropdown list automatically and you can enter a custom value.</span></span>
- <span data-ttu-id="7b0f9-189">DropDownList-ComboBox DropDownList 컨트롤과 마찬가지로 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="7b0f9-189">DropDownList - The ComboBox works just like a DropDownList control.</span></span>

<span data-ttu-id="7b0f9-190">단순 및 드롭다운 간의 차이 항목 목록이 표시 될 때입니다.</span><span class="sxs-lookup"><span data-stu-id="7b0f9-190">The different between DropDown and Simple is when the list of items is displayed.</span></span> <span data-ttu-id="7b0f9-191">단순의 경우는 콤보 상자에 포커스를 이동 하면 즉시 목록이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b0f9-191">In the case of Simple, the list is displayed immediately when you move focus to the ComboBox.</span></span> <span data-ttu-id="7b0f9-192">드롭다운에서 경우 항목의 목록을 보려면 화살표를 클릭 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b0f9-192">In the case of DropDown, you must click the arrow to see the list of items.</span></span>

<span data-ttu-id="7b0f9-193">DropDownList 값 검사가 ComboBox 컨트롤 표준 DropDownList 컨트롤 처럼 작동 하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b0f9-193">The DropDownList value causes the ComboBox control to work just like a standard DropDownList control.</span></span> <span data-ttu-id="7b0f9-194">그러나 여기에 중요 한 차이점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b0f9-194">However, there is an important difference here.</span></span> <span data-ttu-id="7b0f9-195">이전 버전의 Internet Explorer 컨트롤 앞에 배치 하는 모든 컨트롤 앞에 표시 됩니다 무한 z-인덱스 DropDownList 컨트롤을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b0f9-195">Older versions of Internet Explorer display a DropDownList control with an infinite z-index so the control will appear in front of any control placed in front of it.</span></span> <span data-ttu-id="7b0f9-196">콤보 상자는 HTML을 렌더링 하기 때문에 &lt;div&gt; 태그는 HTML 대신 &lt;선택&gt; 태그, ComboBox 올바르게는 존중 z 순서 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b0f9-196">Because the ComboBox renders an HTML &lt;div&gt; tag instead of an HTML &lt;select&gt; tag, the ComboBox correctly respects z-ordering.</span></span>

## <a name="setting-the-autocompletemode"></a><span data-ttu-id="7b0f9-197">AutoCompleteMode 설정</span><span class="sxs-lookup"><span data-stu-id="7b0f9-197">Setting the AutoCompleteMode</span></span>

<span data-ttu-id="7b0f9-198">ComboBox AutoCompleteMode 속성을 사용 하 여 콤보 상자에 텍스트를 입력할 때 수행 되는 작업을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b0f9-198">You use the ComboBox AutoCompleteMode property to specify what happens when someone types text into the ComboBox.</span></span> <span data-ttu-id="7b0f9-199">이 속성은 다음 값을 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="7b0f9-199">This property accepts the following possible values:</span></span>

- <span data-ttu-id="7b0f9-200">None-(기본값) 콤보 상자는 자동 완성 동작을 제공 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7b0f9-200">None - (default value) The ComboBox does not provide any auto-complete behavior.</span></span>
- <span data-ttu-id="7b0f9-201">제안-ComboBox 목록을 표시 하 고 목록에서 일치 하는 항목 강조 표시 (그림 8 참조).</span><span class="sxs-lookup"><span data-stu-id="7b0f9-201">Suggest - The ComboBox displays the list and it highlights the matching item in the list (see Figure 8).</span></span>
- <span data-ttu-id="7b0f9-202">추가-콤보 상자 목록에 나타나지 않습니다 하 고 목록에서 입력 한 (그림 9 참조)으로 일치 하는 항목을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b0f9-202">Append - The ComboBox does not display the list and it appends the matching item from the list onto what you have typed (see Figure 9).</span></span>
- <span data-ttu-id="7b0f9-203">SuggestAppend-ComboBox 모두 목록을 표시 하 고 목록에서 입력 한 (그림 10 참조)으로 일치 하는 항목을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b0f9-203">SuggestAppend - The ComboBox both displays the list and appends the matching item from the list onto what you have typed (see Figure 10).</span></span>


<span data-ttu-id="7b0f9-204">[![ComboBox 만듭니다 제안을](how-do-i-use-the-combobox-control-vb/_static/image8.jpg)](how-do-i-use-the-combobox-control-vb/_static/image15.png)</span><span class="sxs-lookup"><span data-stu-id="7b0f9-204">[![The ComboBox makes a suggestion](how-do-i-use-the-combobox-control-vb/_static/image8.jpg)](how-do-i-use-the-combobox-control-vb/_static/image15.png)</span></span>

<span data-ttu-id="7b0f9-205">**그림 08**: The ComboBox 만듭니다 제안 ([전체 크기 이미지를 보려면 클릭](how-do-i-use-the-combobox-control-vb/_static/image16.png))</span><span class="sxs-lookup"><span data-stu-id="7b0f9-205">**Figure 08**: The ComboBox makes a suggestion([Click to view full-size image](how-do-i-use-the-combobox-control-vb/_static/image16.png))</span></span>


<span data-ttu-id="7b0f9-206">[![일치 하는 텍스트를 추가 하는 콤보 상자](how-do-i-use-the-combobox-control-vb/_static/image9.jpg)](how-do-i-use-the-combobox-control-vb/_static/image17.png)</span><span class="sxs-lookup"><span data-stu-id="7b0f9-206">[![ComboBox appends matching text](how-do-i-use-the-combobox-control-vb/_static/image9.jpg)](how-do-i-use-the-combobox-control-vb/_static/image17.png)</span></span>

<span data-ttu-id="7b0f9-207">**그림 09**: ComboBox 일치 하는 텍스트를 추가 ([전체 크기 이미지를 보려면 클릭](how-do-i-use-the-combobox-control-vb/_static/image18.png))</span><span class="sxs-lookup"><span data-stu-id="7b0f9-207">**Figure 09**: ComboBox appends matching text([Click to view full-size image](how-do-i-use-the-combobox-control-vb/_static/image18.png))</span></span>


<span data-ttu-id="7b0f9-208">[![ComboBox를 소개 하 고 추가](how-do-i-use-the-combobox-control-vb/_static/image10.jpg)](how-do-i-use-the-combobox-control-vb/_static/image19.png)</span><span class="sxs-lookup"><span data-stu-id="7b0f9-208">[![The ComboBox suggests and appends](how-do-i-use-the-combobox-control-vb/_static/image10.jpg)](how-do-i-use-the-combobox-control-vb/_static/image19.png)</span></span>

<span data-ttu-id="7b0f9-209">**그림 10**: The ComboBox를 소개 하 고 추가 ([전체 크기 이미지를 보려면 클릭](how-do-i-use-the-combobox-control-vb/_static/image20.png))</span><span class="sxs-lookup"><span data-stu-id="7b0f9-209">**Figure 10**: The ComboBox suggests and appends([Click to view full-size image](how-do-i-use-the-combobox-control-vb/_static/image20.png))</span></span>


## <a name="summary"></a><span data-ttu-id="7b0f9-210">요약</span><span class="sxs-lookup"><span data-stu-id="7b0f9-210">Summary</span></span>

<span data-ttu-id="7b0f9-211">이 자습서에서는 항목의 고정된 된 집합을 표시 하려면 ComboBox 컨트롤을 사용 하는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="7b0f9-211">In this tutorial, you learned how to use the ComboBox control to display a fixed set of items.</span></span> <span data-ttu-id="7b0f9-212">에서는 ComboBox 컨트롤을 항목을 설정 하는 정적 하 고 데이터베이스 테이블에 모두 바인딩됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b0f9-212">We bound the ComboBox control both to a static set of items and to a database table.</span></span> <span data-ttu-id="7b0f9-213">마지막으로, 해당 DropDownStyle 고 AutoCompleteMode 속성을 설정 하 여 ComboBox의 동작을 수정 하는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="7b0f9-213">Finally, you learned how to modify the behavior of the ComboBox by setting its DropDownStyle and AutoCompleteMode properties.</span></span>

>[!div class="step-by-step"]
[<span data-ttu-id="7b0f9-214">이전</span><span class="sxs-lookup"><span data-stu-id="7b0f9-214">Previous</span></span>](how-do-i-use-the-combobox-control-cs.md)