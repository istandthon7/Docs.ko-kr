---
uid: web-pages/overview/ui-layouts-and-themes/10-working-with-video
title: "(Razor) 사이트 페이지는 ASP.NET 웹에서 비디오를 표시 | Microsoft Docs"
author: tfitzmac
description: "이 장에서 ASP.NET 웹 페이지에서 Razor 구문 페이지와 비디오를 표시 하는 방법에 설명 합니다."
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/20/2014
ms.topic: article
ms.assetid: 332fb3da-e2a5-460d-bb90-dd911e1e2c95
ms.technology: dotnet-webpages
ms.prod: .net-framework
msc.legacyurl: /web-pages/overview/ui-layouts-and-themes/10-working-with-video
msc.type: authoredcontent
ms.openlocfilehash: 0e1849fb780908b55520d8108e2227d046759987
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="displaying-video-in-an-aspnet-web-pages-razor-site"></a><span data-ttu-id="644cf-103">ASP.NET 웹 페이지 (Razor) 사이트에서 비디오를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="644cf-103">Displaying Video in an ASP.NET Web Pages (Razor) Site</span></span>
====================
<span data-ttu-id="644cf-104">으로 [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="644cf-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="644cf-105">이 문서에서는 사용자가 사이트에 저장 되어 있는 비디오를 볼 수 있도록 ASP.NET 웹 페이지 (Razor) 웹 사이트에서 (미디어) 비디오 플레이어를 사용 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="644cf-105">This article explains how to use a video (media) player in an ASP.NET Web Pages (Razor) website to let users view videos that are stored on the site.</span></span> <span data-ttu-id="644cf-106">Razor 구문이 있는 ASP.NET 웹 페이지를 사용 하면 플래시 재생 (*.swf*), 미디어 플레이어 (*.wmv*), 및 Silverlight (*.xap*) 비디오.</span><span class="sxs-lookup"><span data-stu-id="644cf-106">ASP.NET Web Pages with Razor syntax lets you play Flash (*.swf*), Media Player (*.wmv*), and Silverlight (*.xap*) videos.</span></span>
> 
> <span data-ttu-id="644cf-107">학습 내용:</span><span class="sxs-lookup"><span data-stu-id="644cf-107">What you'll learn:</span></span>
> 
> - <span data-ttu-id="644cf-108">비디오 플레이어를 선택 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="644cf-108">How to choose a video player.</span></span>
> - <span data-ttu-id="644cf-109">웹 페이지에 비디오를 추가 하는 방법.</span><span class="sxs-lookup"><span data-stu-id="644cf-109">How to add video to a web page.</span></span>
> - <span data-ttu-id="644cf-110">비디오 플레이어 특성을 설정 하는 방법.</span><span class="sxs-lookup"><span data-stu-id="644cf-110">How to set video player attributes.</span></span>
> 
> <span data-ttu-id="644cf-111">이 ASP.NET Razor 페이지를 문서에 도입 된 기능:</span><span class="sxs-lookup"><span data-stu-id="644cf-111">These are the ASP.NET Razor pages features introduced in the article:</span></span>
> 
> - <span data-ttu-id="644cf-112">`Video` 도우미입니다.</span><span class="sxs-lookup"><span data-stu-id="644cf-112">The `Video` helper.</span></span>
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="644cf-113">자습서에서 사용 되는 소프트웨어 버전</span><span class="sxs-lookup"><span data-stu-id="644cf-113">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="644cf-114">ASP.NET 웹 페이지 (Razor) 2</span><span class="sxs-lookup"><span data-stu-id="644cf-114">ASP.NET Web Pages (Razor) 2</span></span>
> - <span data-ttu-id="644cf-115">WebMatrix 2</span><span class="sxs-lookup"><span data-stu-id="644cf-115">WebMatrix 2</span></span>
>   
> 
> <span data-ttu-id="644cf-116">이 자습서는 WebMatrix 3 에서도 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="644cf-116">This tutorial also works with WebMatrix 3.</span></span>


## <a name="introduction"></a><span data-ttu-id="644cf-117">소개</span><span class="sxs-lookup"><span data-stu-id="644cf-117">Introduction</span></span>

<span data-ttu-id="644cf-118">사이트에 비디오를 표시 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="644cf-118">You might want to display a video on your site.</span></span> <span data-ttu-id="644cf-119">작업을 수행 하는 한 가지 방법은 같은 YouTube 비디오에 이미 있는 사이트에 연결 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="644cf-119">One way to do that is to link to a site that already has the video, like YouTube.</span></span> <span data-ttu-id="644cf-120">사용자 페이지에 직접 해당이 사이트에서 비디오를 포함 하려는 경우 일반적으로 사이트에서 HTML 태그를 가져올 수 있으며 다음 페이지에 복사.</span><span class="sxs-lookup"><span data-stu-id="644cf-120">If you want to embed a video from these sites directly in your own pages, you can usually get HTML markup from the site and then copy it into your page.</span></span> <span data-ttu-id="644cf-121">예를 들어 다음 예제는 YouTube를 포함 하는 방법을 비디오:</span><span class="sxs-lookup"><span data-stu-id="644cf-121">For example, the following example shows how to embed a YouTube video:</span></span>

[!code-html[Main](10-working-with-video/samples/sample1.html?highlight=10-14)]

<span data-ttu-id="644cf-122">(공용 비디오 공유 사이트)에 없는 자신의 웹 사이트에 있는 비디오를 재생 하려는 경우 다음과 같은 포함 된 태그를 사용 하 여 직접 연결할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="644cf-122">If you want to play a video that's on your own website (not on a public video-sharing site), you can't directly link to it using embedded markup like this.</span></span> <span data-ttu-id="644cf-123">그러나 사용 하 여 사이트에서 비디오를 재생할 수는는 `Video` 미디어 플레이어를 페이지에 직접 렌더링 하는 도우미입니다.</span><span class="sxs-lookup"><span data-stu-id="644cf-123">However, you can play videos from your site by using the `Video` helper, which renders a media player directly in a page.</span></span>

<a id="Choosing_a_Video_Player"></a>
## <a name="choosing-a-video-player"></a><span data-ttu-id="644cf-124">비디오 플레이어를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="644cf-124">Choosing a Video Player</span></span>

<span data-ttu-id="644cf-125">많은 비디오 파일에 대 한 형식 및 각 형식에는 일반적으로 서로 다른 플레이어와 플레이어를 구성 하는 다른 방법이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="644cf-125">There are lots of formats for video files, and each format typically requires a different player and a different way to configure the player.</span></span> <span data-ttu-id="644cf-126">ASP.NET Razor 페이지에 사용 하 여 웹 페이지에 비디오를 재생할 수 있습니다는 `Video` 도우미입니다.</span><span class="sxs-lookup"><span data-stu-id="644cf-126">In ASP.NET Razor pages, you can play a video in a web page using the `Video` helper.</span></span> <span data-ttu-id="644cf-127">`Video` 자동으로 생성 하기 때문에 웹 페이지에 비디오를 포함 하는 과정을 간소화 하는 도우미는 `object` 및 `embed` 비디오 페이지를 추가 하는 일반적으로 사용 되는 HTML 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="644cf-127">The `Video` helper simplifies the process of embedding videos in a web page because it automatically generates the `object` and `embed` HTML elements that are normally used to add video to the page.</span></span>

<span data-ttu-id="644cf-128">`Video` 도우미 다음과 같은 미디어 플레이어를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="644cf-128">The `Video` helper supports the following media players:</span></span>

- <span data-ttu-id="644cf-129">Adobe Flash</span><span class="sxs-lookup"><span data-stu-id="644cf-129">Adobe Flash</span></span>
- <span data-ttu-id="644cf-130">Windows MediaPlayer</span><span class="sxs-lookup"><span data-stu-id="644cf-130">Windows MediaPlayer</span></span>
- <span data-ttu-id="644cf-131">Microsoft Silverlight</span><span class="sxs-lookup"><span data-stu-id="644cf-131">Microsoft Silverlight</span></span>

### <a name="the-flash-player"></a><span data-ttu-id="644cf-132">Flash Player</span><span class="sxs-lookup"><span data-stu-id="644cf-132">The Flash Player</span></span>

<span data-ttu-id="644cf-133">`Flash` 의 플레이어는 `Video` 도우미를 사용 하면 플래시 비디오 재생 (*.swf* 파일) 웹 페이지에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="644cf-133">The `Flash` player of the `Video` helper let you play Flash videos (*.swf* files) in a web page.</span></span> <span data-ttu-id="644cf-134">여기에 최소한 비디오 파일의 경로를 제공 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="644cf-134">At a minimum, you have to provide a path to the video file.</span></span> <span data-ttu-id="644cf-135">경로만 지정 하면 플레이어는 플래시의 현재 버전으로 설정 된 기본값을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="644cf-135">If you specify nothing but the path, the player uses default values that are set by the current version of Flash.</span></span> <span data-ttu-id="644cf-136">일반적인 기본 설정은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="644cf-136">Typical default settings are:</span></span>

- <span data-ttu-id="644cf-137">비디오의 기본 너비 및 높이 사용 하 여 표시 되 없이 배경색입니다.</span><span class="sxs-lookup"><span data-stu-id="644cf-137">The video is displayed using its default width and height and without a background color.</span></span>
- <span data-ttu-id="644cf-138">이 비디오는 페이지가 로드 될 때 자동으로 재생 됩니다.</span><span class="sxs-lookup"><span data-stu-id="644cf-138">The video plays automatically when the page loads.</span></span>
- <span data-ttu-id="644cf-139">비디오에는 명시적으로 중지 될 때까지 계속 반복 합니다.</span><span class="sxs-lookup"><span data-stu-id="644cf-139">The video loops continuously until it's explicitly stopped.</span></span>
- <span data-ttu-id="644cf-140">비디오의 특정 크기에 맞게 비디오를 자르는 것이 아니라 비디오를 모두 표시할 수 있도록 크기가 조정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="644cf-140">The video is scaled to show all of the video, rather than cropping the video to fit a specific size.</span></span>
- <span data-ttu-id="644cf-141">창에서 비디오를 재생합니다.</span><span class="sxs-lookup"><span data-stu-id="644cf-141">The video plays in a window.</span></span>

### <a name="the-mediaplayer-player"></a><span data-ttu-id="644cf-142">MediaPlayer 플레이어</span><span class="sxs-lookup"><span data-stu-id="644cf-142">The MediaPlayer Player</span></span>

<span data-ttu-id="644cf-143">`MediaPlayer` 의 플레이어는 `Video` 도우미를 사용 하면 Windows Media 비디오 재생 (*.wmv* 파일), Windows Media audio (*.wma* 파일), 및 MP3 (*.mp3* 웹 페이지에서 파일).</span><span class="sxs-lookup"><span data-stu-id="644cf-143">The `MediaPlayer` player of the `Video` helper lets you play Windows Media videos (*.wmv* files), Windows Media audio (*.wma* files), and MP3 (*.mp3* files) in a web page.</span></span> <span data-ttu-id="644cf-144">미디어 파일 재생;의 경로가 있어야 합니다. 다른 모든 매개 변수는 선택적입니다.</span><span class="sxs-lookup"><span data-stu-id="644cf-144">You must include path of the media file to play; all other parameters are optional.</span></span> <span data-ttu-id="644cf-145">-경로만 지정 하면 플레이어와 같은 MediaPlayer의 현재 버전에서 설정한 기본 설정을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="644cf-145">If you specify only a path, the player uses default settings set by the current version of MediaPlayer, such as:</span></span>

- <span data-ttu-id="644cf-146">비디오의 기본 너비 및 높이 사용 하 여 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="644cf-146">The video is displayed using its default width and height.</span></span>
- <span data-ttu-id="644cf-147">이 비디오는 페이지가 로드 될 때 자동으로 재생 됩니다.</span><span class="sxs-lookup"><span data-stu-id="644cf-147">The video plays automatically when the page loads.</span></span>
- <span data-ttu-id="644cf-148">한 번 재생 (해당 하지 않는 반복) 합니다.</span><span class="sxs-lookup"><span data-stu-id="644cf-148">The video plays once (it doesn't loop).</span></span>
- <span data-ttu-id="644cf-149">플레이어는 사용자 인터페이스에서 컨트롤의 전체 집합을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="644cf-149">The player displays the full set of controls in the user interface.</span></span>
- <span data-ttu-id="644cf-150">창에서 비디오에서 담당합니다.</span><span class="sxs-lookup"><span data-stu-id="644cf-150">The video plays in in a window.</span></span>

### <a name="the-silverlight-player"></a><span data-ttu-id="644cf-151">Silverlight 플레이어</span><span class="sxs-lookup"><span data-stu-id="644cf-151">The Silverlight Player</span></span>

<span data-ttu-id="644cf-152">`Silverlight` 의 플레이어는 `Video` 도우미를 사용 하면 Windows Media Video 재생 (*.wmv* 파일), Windows Media Audio (*.wma* 파일), 및 MP3 (*.mp3* 파일)입니다.</span><span class="sxs-lookup"><span data-stu-id="644cf-152">The `Silverlight` player of the `Video` helper lets you play Windows Media Video (*.wmv* files), Windows Media Audio (*.wma* files), and MP3 (*.mp3* files).</span></span> <span data-ttu-id="644cf-153">Silverlight 기반 응용 프로그램 패키지를 가리키도록 path 매개 변수를 설정 해야 합니다 (*.xap* 파일).</span><span class="sxs-lookup"><span data-stu-id="644cf-153">You must set the path parameter to point to a Silverlight-based application package (*.xap* file).</span></span> <span data-ttu-id="644cf-154">또한 width 및 height 매개 변수를 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="644cf-154">You also must set the width and height parameters.</span></span> <span data-ttu-id="644cf-155">다른 모든 매개 변수는 선택적 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="644cf-155">All other parameters are optional.</span></span> <span data-ttu-id="644cf-156">를 사용 하면 Silverlight 플레이어 비디오에 대 한 필수 매개 변수를 설정 하는 경우 Silverlight 플레이어 배경색을 사용 하지 않고 비디오를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="644cf-156">When you use the Silverlight player for video, if you set only the required parameters, the Silverlight player displays the video without a background color.</span></span>

> [!NOTE]
> <span data-ttu-id="644cf-157">Silverlight 아직 모르는 경우:는 *.xap* 파일은 압축된 파일의 레이아웃 지침을 포함 하는 *.xaml* 파일, 어셈블리 및 선택적 리소스에서 관리 되는 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="644cf-157">In case you don't already know Silverlight: the *.xap* file is a compressed file that contains layout instructions in a *.xaml* file, managed code in assemblies, and optional resources.</span></span> <span data-ttu-id="644cf-158">만들 수는 *.xap* Silverlight 응용 프로그램 프로젝트와 Visual Studio에서 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="644cf-158">You can create a *.xap* file in Visual Studio as a Silverlight application project.</span></span>


<span data-ttu-id="644cf-159">`Silverlight` 비디오 플레이어 모두 플레이어에 제공 하는 설정 및에서 제공 되는 설정을 사용 하는 *.xap* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="644cf-159">The `Silverlight` video player uses both the settings that you provide for the player and the settings that are provided in the *.xap* file.</span></span>

> [!TIP] 
> 
> <a id="SB_MimeTypes"></a>
> ### <a name="mime-types"></a><span data-ttu-id="644cf-160">MIME 형식</span><span class="sxs-lookup"><span data-stu-id="644cf-160">MIME Types</span></span>
> 
> <span data-ttu-id="644cf-161">브라우저 파일을 다운로드 하는 경우 브라우저는 파일 형식 렌더링 되는 문서에 대해 지정 된 MIME 형식과 일치 하는지 합니다.</span><span class="sxs-lookup"><span data-stu-id="644cf-161">When a browser downloads a file, the browser makes sure that the file type matches the MIME type that's specified for the document that's being rendered.</span></span> <span data-ttu-id="644cf-162">MIME 형식이 파일의 콘텐츠 유형 또는 미디어 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="644cf-162">The MIME type is the content type or media type of a file.</span></span> <span data-ttu-id="644cf-163">`Video` 도우미 다음 MIME 형식을 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="644cf-163">The `Video` helper uses the following MIME types:</span></span>
> 
> - `application/x-shockwave-flash`
> - `application/x-mplayer2`
> - `application/x-silverlight-2`


<a id="Playing_Flash"></a>
## <a name="playing-flash-swf-videos"></a><span data-ttu-id="644cf-164">Flash (.swf) 비디오 재생</span><span class="sxs-lookup"><span data-stu-id="644cf-164">Playing Flash (.swf) Videos</span></span>

<span data-ttu-id="644cf-165">이 절차에서는 명명 된 플래시 비디오를 재생 하는 방법을 보여 줍니다 *sample.swf*합니다.</span><span class="sxs-lookup"><span data-stu-id="644cf-165">This procedure shows you how to play a Flash video named *sample.swf*.</span></span> <span data-ttu-id="644cf-166">절차에서는 인지 라는 폴더가 *미디어* 사이트에는 *.swf* 파일은 해당 폴더에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="644cf-166">The procedure assumes that you've got a folder named *Media* on your site and that the *.swf* file is in that folder.</span></span>

1. <span data-ttu-id="644cf-167">에 설명 된 대로 웹 사이트에 ASP.NET Web Helpers Library를 추가 [ASP.NET 웹 페이지 사이트에서 설치 도우미](https://go.microsoft.com/fwlink/?LinkId=252372)추가 하지 않은 경우.</span><span class="sxs-lookup"><span data-stu-id="644cf-167">Add the ASP.NET Web Helpers Library to your website as described in [Installing Helpers in an ASP.NET Web Pages Site](https://go.microsoft.com/fwlink/?LinkId=252372), if you haven't already added it.</span></span>
2. <span data-ttu-id="644cf-168">웹 사이트에서 페이지를 추가 하 고 이름을 *FlashVideo.cshtml*합니다.</span><span class="sxs-lookup"><span data-stu-id="644cf-168">In the website, add a page and name it *FlashVideo.cshtml*.</span></span>
3. <span data-ttu-id="644cf-169">페이지에 다음 태그를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="644cf-169">Add the following markup to the page:</span></span> 

    [!code-cshtml[Main](10-working-with-video/samples/sample2.cshtml)]
4. <span data-ttu-id="644cf-170">브라우저에서 페이지를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="644cf-170">Run the page in a browser.</span></span> <span data-ttu-id="644cf-171">(있는지 확인 페이지에서 선택한는 **파일** 실행 하기 전에 작업 영역입니다.) 페이지가 표시 되 고 자동으로 재생 합니다.</span><span class="sxs-lookup"><span data-stu-id="644cf-171">(Make sure the page is selected in the **Files** workspace before you run it.) The page is displayed and the video plays automatically.</span></span> 

    <span data-ttu-id="644cf-172">![[image] ] (10-working-with-video/_static/image1.jpg "ch08_video 1.jpg")</span><span class="sxs-lookup"><span data-stu-id="644cf-172">![[image]](10-working-with-video/_static/image1.jpg "ch08_video-1.jpg")</span></span>

<span data-ttu-id="644cf-173">설정할 수 있습니다는 `quality` 는 플래시 비디오에 대 한 매개 변수 `low`, `autolow`, `autohigh`, `medium`, `high`, 및 `best`:</span><span class="sxs-lookup"><span data-stu-id="644cf-173">You can set the `quality` parameter for a Flash video to `low`, `autolow`, `autohigh`, `medium`, `high`, and `best`:</span></span>

[!code-cshtml[Main](10-working-with-video/samples/sample3.cshtml)]

<span data-ttu-id="644cf-174">사용 하 여 특정 크기를 재생할는 플래시 비디오를 변경할 수는 `scale` 매개 변수를 다음으로 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="644cf-174">You can change the Flash video to play at a specific size using the `scale` parameter, which you can set to the following:</span></span>

- <span data-ttu-id="644cf-175">`showall`.</span><span class="sxs-lookup"><span data-stu-id="644cf-175">`showall`.</span></span> <span data-ttu-id="644cf-176">이렇게 하면 원래의 가로 세로 비율을 유지 하는 동안 표시 전체 비디오.</span><span class="sxs-lookup"><span data-stu-id="644cf-176">This makes the entire video visible while maintaining the original aspect ratio.</span></span> <span data-ttu-id="644cf-177">그러나 각 면 테두리가 있는 게 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="644cf-177">However, you might end up with borders on each side.</span></span>
- <span data-ttu-id="644cf-178">`noorder`.</span><span class="sxs-lookup"><span data-stu-id="644cf-178">`noorder`.</span></span> <span data-ttu-id="644cf-179">원래의 가로 세로 비율을 유지 하는 동안 비디오 크기를 조정이 있지만 잘릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="644cf-179">This scales the video while maintaining the original aspect ratio, but it might be cropped.</span></span>
- <span data-ttu-id="644cf-180">`exactfit`.</span><span class="sxs-lookup"><span data-stu-id="644cf-180">`exactfit`.</span></span> <span data-ttu-id="644cf-181">이렇게 하면 전체 비디오가 표시 원래 가로 세로 비율 유지 하지 않고 있지만 왜곡 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="644cf-181">This makes the entire video visible without preserving the original aspect ratio, but distortion may occur.</span></span>

<span data-ttu-id="644cf-182">지정 하지 않으면는 `scale` 매개 변수를 전체 비디오 볼 수 있습니다 및 자르기 없이 원래 가로 세로 비율 유지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="644cf-182">If you don't specify a `scale` parameter, the entire video will be visible and the original aspect ratio will be maintained without any cropping.</span></span> <span data-ttu-id="644cf-183">사용 하는 방법을 보여 주는 다음 예제는 `scale` 매개 변수:</span><span class="sxs-lookup"><span data-stu-id="644cf-183">The following example shows how to use the `scale` parameter:</span></span>

[!code-cshtml[Main](10-working-with-video/samples/sample4.cshtml)]

<span data-ttu-id="644cf-184">Flash player 설정 명명 된 비디오 모드를 지원 `windowMode`합니다.</span><span class="sxs-lookup"><span data-stu-id="644cf-184">The Flash player supports a video mode setting named `windowMode`.</span></span> <span data-ttu-id="644cf-185">이 설정할 수 있습니다 `window`, `opaque`, 및 `transparent`합니다.</span><span class="sxs-lookup"><span data-stu-id="644cf-185">You can set this to `window`, `opaque`, and `transparent`.</span></span> <span data-ttu-id="644cf-186">기본적으로는 `windowMode` 로 설정 된 `window`, 웹 페이지에서 별도 창에서 비디오를 표시 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="644cf-186">By default, the `windowMode` is set to `window`, which displays the video in a separate window on the web page.</span></span> <span data-ttu-id="644cf-187">`opaque` 설정은 웹 페이지에 있는 비디오 뒤에 있는 모든 항목을 숨깁니다.</span><span class="sxs-lookup"><span data-stu-id="644cf-187">The `opaque` setting hides everything behind the video on the web page.</span></span> <span data-ttu-id="644cf-188">`transparent` 설정을 통해 비디오를 통해 표시 하는 웹 페이지의 배경을 투명 비디오의 일부 라고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="644cf-188">The `transparent` setting lets the background of the web page show through the video, assuming any part of the video is transparent.</span></span>

<a id="Playing_MediaPlayer"></a>
## <a name="playing-mediaplayer-wmv-videos"></a><span data-ttu-id="644cf-189">MediaPlayer 재생 (*.wmv*) 비디오</span><span class="sxs-lookup"><span data-stu-id="644cf-189">Playing MediaPlayer (*.wmv*) Videos</span></span>

<span data-ttu-id="644cf-190">다음 절차는 명명 된 창 미디어 비디오를 재생 하는 방법을 보여 줍니다. *sample.wmv* 에 *미디어* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="644cf-190">The following procedure shows you how to play a Window Media video named *sample.wmv* that's in the *Media* folder.</span></span>

1. <span data-ttu-id="644cf-191">에 설명 된 대로 웹 사이트에 ASP.NET Web Helpers Library를 추가 [ASP.NET 웹 페이지 사이트에서 설치 도우미](https://go.microsoft.com/fwlink/?LinkId=252372)아직 없는 경우, 합니다.</span><span class="sxs-lookup"><span data-stu-id="644cf-191">Add the ASP.NET Web Helpers Library to your website as described in [Installing Helpers in an ASP.NET Web Pages Site](https://go.microsoft.com/fwlink/?LinkId=252372), if you haven't already.</span></span>
2. <span data-ttu-id="644cf-192">명명 된 새 페이지를 만들고 *MediaPlayerVideo.cshtml*합니다.</span><span class="sxs-lookup"><span data-stu-id="644cf-192">Create a new page named *MediaPlayerVideo.cshtml*.</span></span>
3. <span data-ttu-id="644cf-193">페이지에 다음 태그를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="644cf-193">Add the following markup to the page:</span></span> 

    [!code-cshtml[Main](10-working-with-video/samples/sample5.cshtml)]
4. <span data-ttu-id="644cf-194">브라우저에서 페이지를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="644cf-194">Run the page in a browser.</span></span> <span data-ttu-id="644cf-195">이 비디오는 로드 하 고 자동으로 재생 합니다.</span><span class="sxs-lookup"><span data-stu-id="644cf-195">The video loads and plays automatically.</span></span> 

    <span data-ttu-id="644cf-196">![[image] ] (10-working-with-video/_static/image2.jpg "ch08_video 2.jpg")</span><span class="sxs-lookup"><span data-stu-id="644cf-196">![[image]](10-working-with-video/_static/image2.jpg "ch08_video-2.jpg")</span></span>

<span data-ttu-id="644cf-197">설정할 수 있습니다 `playCount` 에 비디오를 자동으로 재생 횟수를 나타내는 정수입니다.</span><span class="sxs-lookup"><span data-stu-id="644cf-197">You can set `playCount` to an integer that indicates how many times to play the video automatically:</span></span>

[!code-cshtml[Main](10-working-with-video/samples/sample6.cshtml)]

<span data-ttu-id="644cf-198">`uiMode` 매개 변수는 컨트롤의 사용자 인터페이스에 표시를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="644cf-198">The `uiMode` parameter lets you specify which controls show up in the user interface.</span></span> <span data-ttu-id="644cf-199">설정할 수 있습니다 `uiMode` 를 `invisible`, `none`, `mini`, 또는 `full`합니다.</span><span class="sxs-lookup"><span data-stu-id="644cf-199">You can set `uiMode` to `invisible`, `none`, `mini`, or `full`.</span></span> <span data-ttu-id="644cf-200">지정 하지 않으면는 `uiMode` 매개 변수를 비디오 됩니다 seek를 표시 하 여 상태 창, 가로 막대형, 단추 및 비디오 창 뿐만 아니라 볼륨 컨트롤을 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="644cf-200">If you don't specify a `uiMode` parameter, the video will be displayed with the status window, seek bar, control buttons, and volume controls in addition to the video window.</span></span> <span data-ttu-id="644cf-201">이러한 컨트롤 플레이어를 사용 하 여 오디오 파일을 재생 하는 경우에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="644cf-201">These controls will also be displayed if you use the player to play an audio file.</span></span> <span data-ttu-id="644cf-202">사용 하는 방법의 예로 `uiMode` 매개 변수:</span><span class="sxs-lookup"><span data-stu-id="644cf-202">Here's an example of how to use the `uiMode` parameter:</span></span>

[!code-cshtml[Main](10-working-with-video/samples/sample7.cshtml)]

<span data-ttu-id="644cf-203">기본적으로 오디오 재생 하는 경우에 합니다.</span><span class="sxs-lookup"><span data-stu-id="644cf-203">By default, audio is on when the video plays.</span></span> <span data-ttu-id="644cf-204">설정 하 여 오디오 음소거 할 수 있습니다는 `mute` 매개 변수를 true로:</span><span class="sxs-lookup"><span data-stu-id="644cf-204">You can mute the audio by setting the `mute` parameter to true:</span></span>

[!code-cshtml[Main](10-working-with-video/samples/sample8.cshtml)]

<span data-ttu-id="644cf-205">설정 하 여 오디오 수준의 MediaPlayer 비디오를 제어할 수 있습니다는 `volume` 매개 변수를 0에서 100 사이의 값입니다.</span><span class="sxs-lookup"><span data-stu-id="644cf-205">You can control the audio level of the MediaPlayer video by setting the `volume` parameter to a value between 0 and 100.</span></span> <span data-ttu-id="644cf-206">기본값은 50입니다.</span><span class="sxs-lookup"><span data-stu-id="644cf-206">The default value is 50.</span></span> <span data-ttu-id="644cf-207">예를 들면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="644cf-207">Here's an example:</span></span>

[!code-cshtml[Main](10-working-with-video/samples/sample9.cshtml)]

<a id="Playing_Silverlight"></a>
## <a name="playing-silverlight-videos"></a><span data-ttu-id="644cf-208">Silverlight 비디오 재생</span><span class="sxs-lookup"><span data-stu-id="644cf-208">Playing Silverlight Videos</span></span>

<span data-ttu-id="644cf-209">이 절차는 Silverlight에 포함 된 비디오를 재생 하는 방법을 보여 줍니다. *.xap* 폴더에 명명 된 페이지 *미디어*합니다.</span><span class="sxs-lookup"><span data-stu-id="644cf-209">This procedure shows you how to play video contained in a Silverlight *.xap* page that's in a folder named *Media*.</span></span>

1. <span data-ttu-id="644cf-210">에 설명 된 대로 웹 사이트에 ASP.NET Web Helpers Library를 추가 [ASP.NET 웹 페이지 사이트에서 설치 도우미](https://go.microsoft.com/fwlink/?LinkId=252372)아직 없는 경우, 합니다.</span><span class="sxs-lookup"><span data-stu-id="644cf-210">Add the ASP.NET Web Helpers Library to your website as described in [Installing Helpers in an ASP.NET Web Pages Site](https://go.microsoft.com/fwlink/?LinkId=252372), if you haven't already .</span></span>
2. <span data-ttu-id="644cf-211">명명 된 새 페이지를 만들고 *SilverlightVideo.cshtml*합니다.</span><span class="sxs-lookup"><span data-stu-id="644cf-211">Create a new page named *SilverlightVideo.cshtml*.</span></span>
3. <span data-ttu-id="644cf-212">페이지에 다음 태그를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="644cf-212">Add the following markup to the page:</span></span> 

    [!code-cshtml[Main](10-working-with-video/samples/sample10.cshtml)]
4. <span data-ttu-id="644cf-213">브라우저에서 페이지를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="644cf-213">Run the page in a browser.</span></span> 

    <span data-ttu-id="644cf-214">![[image] ] (10-working-with-video/_static/image3.jpg "ch08_video 3.jpg")</span><span class="sxs-lookup"><span data-stu-id="644cf-214">![[image]](10-working-with-video/_static/image3.jpg "ch08_video-3.jpg")</span></span>

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a><span data-ttu-id="644cf-215">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="644cf-215">Additional Resources</span></span>


<span data-ttu-id="644cf-216">[Silverlight 개요](https://msdn.microsoft.com/en-us/library/bb404700(VS.95).aspx)</span><span class="sxs-lookup"><span data-stu-id="644cf-216">[Silverlight Overview](https://msdn.microsoft.com/en-us/library/bb404700(VS.95).aspx)</span></span>

[<span data-ttu-id="644cf-217">Flash 개체 및 EMBED 태그 특성</span><span class="sxs-lookup"><span data-stu-id="644cf-217">Flash OBJECT and EMBED tag attributes</span></span>](http://kb2.adobe.com/cps/127/tn_12701.html)

<span data-ttu-id="644cf-218">[Windows Media Player 11 SDK PARAM 태그](https://msdn.microsoft.com/en-us/library/aa392321(VS.85).aspx)</span><span class="sxs-lookup"><span data-stu-id="644cf-218">[Windows Media Player 11 SDK PARAM Tags](https://msdn.microsoft.com/en-us/library/aa392321(VS.85).aspx)</span></span>