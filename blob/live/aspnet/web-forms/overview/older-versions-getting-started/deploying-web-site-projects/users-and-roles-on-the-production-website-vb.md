---
uid: web-forms/overview/older-versions-getting-started/deploying-web-site-projects/users-and-roles-on-the-production-website-vb
title: "사용자 및 역할 프로덕션 웹 사이트 (VB)에서 | Microsoft Docs"
author: rick-anderson
description: "멤버 자격 및 역할 설정을 구성 하기 위한 및 만들기, 웹 기반 사용자 인터페이스를 제공 하는 ASP.NET 웹 사이트 관리 도구 (WSAT) 편집는 중..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/09/2009
ms.topic: article
ms.assetid: 491ed5ae-9be1-4191-87be-65e4e1c57690
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deploying-web-site-projects/users-and-roles-on-the-production-website-vb
msc.type: authoredcontent
ms.openlocfilehash: ced68b633eb34d1ea75671ac4ffe7f512e911a0d
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="users-and-roles-on-the-production-website-vb"></a><span data-ttu-id="4674d-103">사용자 및 역할 프로덕션 웹 사이트 (VB)에서</span><span class="sxs-lookup"><span data-stu-id="4674d-103">Users and Roles On The Production Website (VB)</span></span>
====================
<span data-ttu-id="4674d-104">으로 [Scott Mitchell](https://twitter.com/ScottOnWriting)</span><span class="sxs-lookup"><span data-stu-id="4674d-104">by [Scott Mitchell](https://twitter.com/ScottOnWriting)</span></span>

[<span data-ttu-id="4674d-105">PDF 다운로드</span><span class="sxs-lookup"><span data-stu-id="4674d-105">Download PDF</span></span>](http://download.microsoft.com/download/5/C/5/5C57DB8C-5DEA-4B3A-92CA-4405544D313B/aspnet_tutorial16_CustomAWAT_vb.pdf)

> <span data-ttu-id="4674d-106">ASP.NET 웹 사이트 관리 도구 (WSAT) 및 만들기, 편집 및 삭제 사용자 및 역할 멤버 자격 및 역할 설정을 구성 하기 위한 웹 기반 사용자 인터페이스를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="4674d-106">The ASP.NET Website Administration Tool (WSAT) provides a web-based user interface for configuring Membership and Roles settings and for creating, editing, and deleting users and roles.</span></span> <span data-ttu-id="4674d-107">그러나는 WSAT 에서만 작동 localhost에서 열어 볼 때 프로덕션 웹 사이트 관리 도구 브라우저를 통해 도달할 수 있음을 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="4674d-107">Unfortunately, the WSAT only works when visited from localhost, meaning that you cannot reach the production website's Administration Tool through your browser.</span></span> <span data-ttu-id="4674d-108">다행히도 사용자 및 프로덕션에 대 한 역할을 관리할 수 있도록 해결 방법을 않는다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="4674d-108">The good news is that there are workarounds that make it possible to manage users and roles on production.</span></span> <span data-ttu-id="4674d-109">이 자습서에서는 이러한 해결 방법 및 기타 보고서를 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="4674d-109">This tutorial looks at these workarounds and others.</span></span>


## <a name="introduction"></a><span data-ttu-id="4674d-110">소개</span><span class="sxs-lookup"><span data-stu-id="4674d-110">Introduction</span></span>

<span data-ttu-id="4674d-111">ASP.NET 2.0에는 다양 한 도입 *응용 프로그램 서비스*는 웹 응용 프로그램에 추가할 수 있는 구성 요소 서비스의 모음입니다.</span><span class="sxs-lookup"><span data-stu-id="4674d-111">ASP.NET 2.0 introduced a number of *application services*, which are a suite of building block services that you can add to your web application.</span></span> <span data-ttu-id="4674d-112">책 검토 웹 사이트에 멤버 자격 및 역할 서비스를 다시 추가 [ *서비스를 구성 하는 웹 사이트를 사용 하 여 응용 프로그램* 자습서](configuring-a-website-that-uses-application-services-vb.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="4674d-112">We added the Membership and Roles services to the Book Reviews website back in the [*Configuring a Website That Uses Application Services* tutorial](configuring-a-website-that-uses-application-services-vb.md).</span></span> <span data-ttu-id="4674d-113">사용자 계정 만들기 및 관리,을 용이 하 게 멤버 자격 서비스 역할 서비스는 사용자를 그룹으로 분류 하기 위한 API를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="4674d-113">The Membership service facilitates creating and managing user accounts; the Roles service offers an API for categorizing users into groups.</span></span> <span data-ttu-id="4674d-114">책 검토 사이트에 있는 3 개의 사용자 계정을-Scott, Jisun, 및 Alice-및 Scott 및 관리자 역할의 Jisun Admin, 단일 역할을 합니다.</span><span class="sxs-lookup"><span data-stu-id="4674d-114">The Book Reviews site has three user accounts - Scott, Jisun, and Alice - and a single role, Admin, with Scott and Jisun in the Admin role.</span></span>

<span data-ttu-id="4674d-115">ASP입니다. NET의 응용 프로그램 서비스는 특정 구현에 연결 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4674d-115">ASP.NET's application services are not tied to a specific implementation.</span></span> <span data-ttu-id="4674d-116">특정을 사용 하는 응용 프로그램 서비스를 지시 하는 대신, *공급자*, 해당 공급자 특정 기술을 사용 하 여 서비스를 구현 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4674d-116">Instead, you instruct the application services to use a particular *provider*, and that provider implements the service using a particular technology.</span></span> <span data-ttu-id="4674d-117">책 검토 웹 응용 프로그램 사용 하도록 구성한는 `SqlMembershipProvider` 및 `SqlRoleProvider` 멤버 자격 및 역할 서비스에 대 한 공급자입니다.</span><span class="sxs-lookup"><span data-stu-id="4674d-117">We configured the Book Reviews web application to use the `SqlMembershipProvider` and `SqlRoleProvider` providers for the Membership and Roles services.</span></span> <span data-ttu-id="4674d-118">이러한 두 공급자는 SQL Server 데이터베이스의 사용자 계정과 역할 정보를 저장 하 고는 웹 호스팅 회사에 호스팅된 인터넷 기반 웹 응용 프로그램에 대 한 가장 자주 사용 되는 공급자.</span><span class="sxs-lookup"><span data-stu-id="4674d-118">These two providers store user account and role information in a SQL Server database and are the most commonly used providers for Internet-based web applications hosted at a web hosting company.</span></span>

<span data-ttu-id="4674d-119">사용자 및 프로덕션 환경에 대 한 역할 멤버 자격 및 역할 서비스를 사용 하는 개발자를 위한 일반적인 과제는 관리입니다.</span><span class="sxs-lookup"><span data-stu-id="4674d-119">A common challenge for developers using the Membership and Roles services is managing the users and roles on the production environment.</span></span> <span data-ttu-id="4674d-120">어떻게 않는 프로덕션 웹 사이트에서 사용자 계정을 삭제, 새 역할을 추가 하거나 기존 사용자 기존 역할에?</span><span class="sxs-lookup"><span data-stu-id="4674d-120">How do you delete a user account from the production website, add a new role, or add an existing user to an existing role?</span></span> <span data-ttu-id="4674d-121">이 자습서에는 사용자 및 프로덕션 웹 사이트에 대 한 역할을 관리 하기 위한 다양 한 기술을 탐색 합니다.</span><span class="sxs-lookup"><span data-stu-id="4674d-121">This tutorial explores different techniques for managing users and roles on the production website.</span></span>

## <a name="using-the-aspnet-web-site-administration-tool"></a><span data-ttu-id="4674d-122">ASP.NET 웹 사이트 관리 도구를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="4674d-122">Using the ASP.NET Web Site Administration Tool</span></span>

<span data-ttu-id="4674d-123">ASP.NET에 포함 되어는 [웹 사이트 관리 도구](https://msdn.microsoft.com/en-us/library/yy40ytx0.aspx) (WSAT)을 쉽게 만들고 사용자 계정과 역할을 관리 하 고 사용자 및 역할 기반 권한 부여 규칙을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4674d-123">ASP.NET includes a [Web Site Administration Tool](https://msdn.microsoft.com/en-us/library/yy40ytx0.aspx) (WSAT) that makes it easy to create and manage user accounts and roles and to specify user- and role-based authorization rules.</span></span> <span data-ttu-id="4674d-124">WSAT를 사용 하려면 솔루션 탐색기에서 ASP.NET 구성 아이콘을 클릭 하 고 또는 웹 사이트 또는 프로젝트 메뉴에서 ASP.NET 구성 옵션을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="4674d-124">To use the WSAT, click the ASP.NET Configuration icon in the Solution Explorer, or go to the Website or Project menu and choose the ASP.NET Configuration option.</span></span> <span data-ttu-id="4674d-125">어느 방법이 든 웹 브라우저를 시작 하 고 같은 주소에서 WSAT 가리키는:`http://localhost:portNumber/asp.netwebadminfiles/default.aspx?applicationPhysicalPath=pathToApplication`</span><span class="sxs-lookup"><span data-stu-id="4674d-125">Either approach launches a web browser and points it to the WSAT at an address like: `http://localhost:portNumber/asp.netwebadminfiles/default.aspx?applicationPhysicalPath=pathToApplication`</span></span>

<span data-ttu-id="4674d-126">WSAT는 세 개의 섹션으로 구분 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4674d-126">The WSAT is divided into three sections:</span></span>

- <span data-ttu-id="4674d-127">**보안** -사용자, 역할 및 권한 부여 규칙을 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="4674d-127">**Security** - manage users, roles, and authorization rules.</span></span>
- <span data-ttu-id="4674d-128">**ApplicationConfiguration** -관리는 &lt;appSettings&gt; 및 여기에서 SMTP 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="4674d-128">**ApplicationConfiguration** - manage the &lt;appSettings&gt; and SMTP settings from here.</span></span> <span data-ttu-id="4674d-129">있습니다 수 또한 오프 라인 상태로 응용 프로그램 및 디버깅 및 추적 여기에서 설정 관리으로 기본 사용자 지정 오류 페이지를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="4674d-129">You can also take the application offline and manage debugging and tracing settings from here, as well as specify the default custom error page.</span></span>
- <span data-ttu-id="4674d-130">**ProviderConfiguration** -응용 프로그램 서비스에서 사용 하는 공급자를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="4674d-130">**ProviderConfiguration** - configure the providers used by the application services.</span></span>

<span data-ttu-id="4674d-131">보안 섹션 (에서처럼 **그림 1**) 새 사용자 만들기, 사용자 관리, 만들기 및 역할을 관리 하 고 만들기 및 관리에 대 한 액세스 규칙에 대 한 링크도 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="4674d-131">The Security section (shown in **Figure 1**) includes links for creating new users, managing users, creating and managing roles, and creating and managing access rules.</span></span> <span data-ttu-id="4674d-132">여기에서 수 시스템에 새 역할을 추가, 기존 사용자를 삭제 또는 추가 또는 특정 사용자 계정에서 역할을 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="4674d-132">From here you can add a new role to the system, delete an existing user, or add or remove roles from a particular user account.</span></span>

[![](users-and-roles-on-the-production-website-vb/_static/image2.png)](users-and-roles-on-the-production-website-vb/_static/image1.png)

<span data-ttu-id="4674d-133">**그림 1**: WSAT 보안 섹션에는 사용자 및 역할을 관리 하기 위한 옵션을 포함</span><span class="sxs-lookup"><span data-stu-id="4674d-133">**Figure 1**: The WSAT Security Section Includes Options for Managing Users and Roles</span></span>  
<span data-ttu-id="4674d-134">([전체 크기 이미지를 보려면 클릭](users-and-roles-on-the-production-website-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="4674d-134">([Click to view full-size image](users-and-roles-on-the-production-website-vb/_static/image3.png))</span></span>

<span data-ttu-id="4674d-135">그러나이 WSAT는만 액세스할 수 있는 로컬.</span><span class="sxs-lookup"><span data-stu-id="4674d-135">Unfortunately, the WSAT is only accessible locally.</span></span> <span data-ttu-id="4674d-136">원격 프로덕션 웹 사이트;에 WSAT 방문 수 없습니다. 방문 하는 경우 `www.yoursite.com/asp.netwebadminfiles/default.aspx` 404 찾을 수 없음 응답을 받을입니다.</span><span class="sxs-lookup"><span data-stu-id="4674d-136">You cannot visit the WSAT on your remote production website; if you visit `www.yoursite.com/asp.netwebadminfiles/default.aspx` you get a 404 Not Found response.</span></span> <span data-ttu-id="4674d-137">WSAT 사용 하 여를 구동 하는 코드는 `Membership` 및 `Roles` 를 만들려면.NET Framework의 클래스를 편집 하 고 사용자 및 역할을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="4674d-137">The code that powers the WSAT uses the `Membership` and `Roles` classes in the .NET Framework to create, edit, and delete users and roles.</span></span> <span data-ttu-id="4674d-138">이러한 클래스를 지정 해야 합니다. 어떤 공급자를 확인 하려면 웹 응용 프로그램의 구성 정보를 참조 하십시오. 에 [ *서비스를 구성 하는 웹 사이트를 사용 하 여 응용 프로그램* 자습서](configuring-a-website-that-uses-application-services-vb.md) 책 검토 웹 사이트에서 사용 하도록 설정 하는 `SqlMembershipProvider` 및 `SqlRoleProvider` 공급자입니다.</span><span class="sxs-lookup"><span data-stu-id="4674d-138">These classes consult the web application's configuration information to determine what provider to use; back in the [*Configuring a Website That Uses Application Services* tutorial](configuring-a-website-that-uses-application-services-vb.md) we setup the Book Reviews website to use the `SqlMembershipProvider` and `SqlRoleProvider` providers.</span></span> <span data-ttu-id="4674d-139">추가 포함이 `<membership>` 및 `<roleManager>` 를 섹션 `Web.config`합니다.</span><span class="sxs-lookup"><span data-stu-id="4674d-139">This entailed adding `<membership>` and `<roleManager>` sections to `Web.config`.</span></span>

[!code-xml[Main](users-and-roles-on-the-production-website-vb/samples/sample1.xml)]

<span data-ttu-id="4674d-140">`<membership>` 및 `<roleManager>` 참조 섹션는 `SqlMembershipProvider` 및 `SqlRoleProvider` 의 공급자가 `type` 특성도 각각.</span><span class="sxs-lookup"><span data-stu-id="4674d-140">Note that the `<membership>` and `<roleManager>` sections reference the `SqlMembershipProvider` and `SqlRoleProvider` providers in their `type` attribute, respectively.</span></span> <span data-ttu-id="4674d-141">이러한 공급자 지정된 된 SQL Server 데이터베이스의 사용자 및 역할 정보를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="4674d-141">These providers store the user and role information in a specified SQL Server database.</span></span> <span data-ttu-id="4674d-142">이러한 공급자에서 데이터베이스를 사용 하 여 지정 된 `connectionStringName` 특성 `ReviewsConnectionString`에 정의 된는 `~/ConfigSections/databaseConnectionStrings.config` 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="4674d-142">The database used by these providers is specified by the `connectionStringName` attribute, `ReviewsConnectionString`, which is defined in the `~/ConfigSections/databaseConnectionStrings.config` file.</span></span> <span data-ttu-id="4674d-143">이전에 설명한 대로 `databaseConnectionStrings.config` 반면 개발 데이터베이스를 연결 문자열을 포함 하는 개발 환경에서 파일의 `databaseConnectionStrings.config` 파일 프로덕션에서 프로덕션 데이터베이스에 연결 문자열을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="4674d-143">Recall that the `databaseConnectionStrings.config` file in the development environment contains the connection string to the development database whereas the `databaseConnectionStrings.config` file on production contains the connection string to the production database.</span></span>

<span data-ttu-id="4674d-144">간단히 말해서는 WSAT 개발 환경을 통해 로컬로 액세스 해야 하 고에 지정 된 데이터베이스의 사용자 및 역할 정보 사용 방식과 `databaseConnectionStrings.config` 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="4674d-144">In a nutshell, the WSAT must be accessed locally through the development environment, and it works with the user and role information in the database specified in the `databaseConnectionStrings.config` file.</span></span> <span data-ttu-id="4674d-145">따라서 연결 문자열 정보를 변경 하면는 `databaseConnectionStrings.config` 파일 개발 환경에서 사용 하 여는 WSAT 로컬로 프로덕션 환경에서 사용자 및 역할을 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="4674d-145">Consequently, if we change the connection string information in the `databaseConnectionStrings.config` file on the development environment we can use the WSAT locally to manage users and roles in the production environment.</span></span>

<span data-ttu-id="4674d-146">이 기능을 설명 하기 위해 엽니다는 `databaseConnectionStrings.config` 개발 환경에서 Visual Studio에서 파일을 프로덕션 데이터베이스 연결 문자열과 함께 개발 데이터베이스 연결 문자열을 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="4674d-146">To illustrate this functionality, open the `databaseConnectionStrings.config` file in Visual Studio on the development environment and replace the development database connection string with the production database connection string.</span></span> <span data-ttu-id="4674d-147">WSAT 실행 보안 탭으로 이동 하 고 Sam 암호 "password!" 라는 새 사용자 추가</span><span class="sxs-lookup"><span data-stu-id="4674d-147">Then launch the WSAT, go the Security tab, and add a new user named Sam with password "password!"</span></span> <span data-ttu-id="4674d-148">(작은 따옴표가).</span><span class="sxs-lookup"><span data-stu-id="4674d-148">(less the quotation marks).</span></span> <span data-ttu-id="4674d-149">**그림 2** 이 계정을 만들 때 WSAT 화면을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4674d-149">**Figure 2** shows the WSAT screen when creating this account.</span></span>

[![](users-and-roles-on-the-production-website-vb/_static/image5.png)](users-and-roles-on-the-production-website-vb/_static/image4.png)

<span data-ttu-id="4674d-150">**그림 2**: 프로덕션 환경에 Sam 라는 새 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="4674d-150">**Figure 2**: Create a New User Named Sam In the Production Environment</span></span>  
<span data-ttu-id="4674d-151">([전체 크기 이미지를 보려면 클릭](users-and-roles-on-the-production-website-vb/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="4674d-151">([Click to view full-size image](users-and-roles-on-the-production-website-vb/_static/image6.png))</span></span>

<span data-ttu-id="4674d-152">연결 문자열을 변경 했습니다 때문에 `databaseConnectionStrings.config` 프로덕션 데이터베이스 서버를 가리키도록 Sam은 프로덕션 환경에 사용자로 추가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="4674d-152">Because we changed the connection string in `databaseConnectionStrings.config` to point to the production database server, Sam was added as a user in the production environment.</span></span> <span data-ttu-id="4674d-153">이 확인 하려면 변경에서 연결 문자열은 `databaseConnectionStrings.config` 개발 데이터베이스에 다시 파일을 방문는 `Login.aspx` 개발 환경에서 페이지.</span><span class="sxs-lookup"><span data-stu-id="4674d-153">To verify this, change the connection string in the `databaseConnectionStrings.config` file back to the development database and then visit the `Login.aspx` page in the development environment.</span></span> <span data-ttu-id="4674d-154">Sam로에 로그인 하려고 (참조 **그림 3**).</span><span class="sxs-lookup"><span data-stu-id="4674d-154">Try to sign in as Sam (see **Figure 3**).</span></span>

[![](users-and-roles-on-the-production-website-vb/_static/image8.png)](users-and-roles-on-the-production-website-vb/_static/image7.png)

<span data-ttu-id="4674d-155">**그림 3**: 개발 환경에서 Sam으로 로그인 할 수 없습니다</span><span class="sxs-lookup"><span data-stu-id="4674d-155">**Figure 3**: You Cannot Sign In As Sam in the Development Environment</span></span>  
<span data-ttu-id="4674d-156">([전체 크기 이미지를 보려면 클릭](users-and-roles-on-the-production-website-vb/_static/image9.png))</span><span class="sxs-lookup"><span data-stu-id="4674d-156">([Click to view full-size image](users-and-roles-on-the-production-website-vb/_static/image9.png))</span></span>

<span data-ttu-id="4674d-157">로그인 할 수 없습니다 Sam로 개발 환경에서 사용자 계정 정보 로컬 데이터베이스에 존재 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4674d-157">You cannot sign in as Sam in the development environment because the user account information does not exist in the local database.</span></span> <span data-ttu-id="4674d-158">보다는 프로덕션 데이터베이스에 추가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="4674d-158">Rather, is was added to the production database.</span></span> <span data-ttu-id="4674d-159">이 확인 하려면의 내용 보기는 `aspnet_Users` 개발 및 프로덕션 데이터베이스의 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="4674d-159">To verify this, view the contents of the `aspnet_Users` table in both the development and production databases.</span></span> <span data-ttu-id="4674d-160">개발 환경에서 사용자가 Scott, Jisun, Alice에 대 한 레코드를 3 개만 있을 것입니다.</span><span class="sxs-lookup"><span data-stu-id="4674d-160">In the development environment there should be only three records for users Scott, Jisun, and Alice.</span></span> <span data-ttu-id="4674d-161">그러나는 `aspnet_Users` 프로덕션 데이터베이스의 테이블에 4 개의 레코드가: Scott, Jisun, Alice 및 Sam 합니다.</span><span class="sxs-lookup"><span data-stu-id="4674d-161">However, the `aspnet_Users` table in the production database has four records: Scott, Jisun, Alice, and Sam.</span></span> <span data-ttu-id="4674d-162">따라서 프로덕션 환경에서 웹 사이트를 통해 있지만 개발 환경 통해서가 아니라 Sam에 로그인 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4674d-162">Consequently, Sam can sign in through the website in production, but not through the development environment.</span></span>

[![](users-and-roles-on-the-production-website-vb/_static/image11.png)](users-and-roles-on-the-production-website-vb/_static/image10.png)

<span data-ttu-id="4674d-163">**그림 4**: Sam 프로덕션 웹 사이트에 로그인 할 수</span><span class="sxs-lookup"><span data-stu-id="4674d-163">**Figure 4**: Sam Can Sign In On the Production Website</span></span>  
<span data-ttu-id="4674d-164">([전체 크기 이미지를 보려면 클릭](users-and-roles-on-the-production-website-vb/_static/image12.png))</span><span class="sxs-lookup"><span data-stu-id="4674d-164">([Click to view full-size image](users-and-roles-on-the-production-website-vb/_static/image12.png))</span></span>

> [!NOTE]
> <span data-ttu-id="4674d-165">연결 문자열을 변경 하려면 반드시는 `databaseConnectionStrings.config` 완료 되 면 다시 개발 데이터베이스에 파일의 연결 문자열에서 개발 사이트를 테스트할 때 프로덕션 데이터와 함께 작업 합니다 WSAT 그렇지 않으면 작업 환경입니다.</span><span class="sxs-lookup"><span data-stu-id="4674d-165">Don't forget to change the connection string in the `databaseConnectionStrings.config` file back to the development database's connect string when you're done working with the WSAT otherwise you will be working with production data when testing the site through the development environment.</span></span> <span data-ttu-id="4674d-166">또한 유념 지금까지 설명한 기술을 사용자 및 역할을 원격으로 관리 하는 WSAT를 사용할 수 있습니다, 하는 동안 다른 WSAT 구성 옵션 (액세스 규칙, SMTP 설정, 디버깅 및 추적 설정 및 등)에 대 한 변경의 를수정하는`Web.config` 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="4674d-166">Also keep in mind that while the technique we just discussed allows us to use the WSAT to remotely manage users and roles, changes to any of the other WSAT configuration options (access rules, SMTP settings, debugging and tracing settings, and so on) modify the `Web.config` file.</span></span> <span data-ttu-id="4674d-167">따라서 설정에 대 한 변경 내용을 프로덕션 환경이 아닌 개발 환경에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4674d-167">Consequently, any changes made to the settings apply to the development environment and not to the production environment.</span></span>


## <a name="creating-custom-user-and-role-management-web-pages"></a><span data-ttu-id="4674d-168">사용자 지정 사용자 및 역할 관리 웹 페이지 만들기</span><span class="sxs-lookup"><span data-stu-id="4674d-168">Creating Custom User and Role Management Web Pages</span></span>

<span data-ttu-id="4674d-169">WSAT 사용자 및 역할을 관리 하기 위한 상자 시스템의 부족을 제공 하지만 로컬로 실행할 수 있습니다으로 이루어지며 사용자 및 프로덕션에 대 한 역할을 관리 하기 위해 연결 문자열 정보를 변경 하기.</span><span class="sxs-lookup"><span data-stu-id="4674d-169">The WSAT provides an out of the box system for managing users and roles, but can only be launched locally and requires making changes to the connection string information in order to manage the users and roles on production.</span></span> <span data-ttu-id="4674d-170">사용자 계정을 지 원하는 대부분의 웹 사이트에는 다양 한 사용자 및 관리자는 사이트의 페이지에서 사용자 및 역할을 관리할 수 있도록 역할 관리 웹 페이지 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4674d-170">Most websites that support user accounts also include a number of user and role administration web pages that enable administrators to manage users and roles from pages within the site.</span></span> <span data-ttu-id="4674d-171">이러한 웹 기반 관리 페이지 훨씬 쉬워집니다 사용자 및 역할을 관리 하 고 사이트에 필수적인 많은 관리자 또는 관리자가 없는 WSAT를 시작 하기 위해 Visual Studio를 사용 하 여 기술 배경 또는에 액세스할 수 있게 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4674d-171">Such web-based administration pages make it much easier to manage users and roles and are essential for sites where there may be many administrators or administrators that do not have access to or the technical background to use Visual Studio to launch the WSAT.</span></span>

<span data-ttu-id="4674d-172">끌어서 놓기 만큼 쉬운 이렇게 관리 웹 페이지의 많은 구현 하는 기본 웹 로그인 관련 컨트롤의 ASP.NET에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4674d-172">ASP.NET includes a number of built-in Login-related Web controls that make implementing many of these administrative web pages as easy as drag and drop.</span></span> <span data-ttu-id="4674d-173">예를 들어 관리자가 페이지로 CreateUserWizard 컨트롤을 끌어서 일부 속성을 설정 하 여 새 사용자 계정을 만들 수에 대 한 페이지를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4674d-173">For example, you can create a page for administrators to create a new user account by dragging the CreateUserWizard control onto the page and setting a few properties.</span></span> <span data-ttu-id="4674d-174">사실, 페이지에 표시 된 WSAT 사용자가 만들기 위한 **그림 2** 페이지에 추가할 수 있는 동일한 CreateUserWizard 컨트롤을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4674d-174">In fact, the page for creating users in the WSAT shown in **Figure 2** uses the same CreateUserWizard control that you can add to your pages.</span></span> <span data-ttu-id="4674d-175">또한 구성원 자격 및 역할 서비스 기능을 통해 프로그래밍 방식으로 사용할 수는 `Membership` 및 `Roles` .NET Framework의 클래스.</span><span class="sxs-lookup"><span data-stu-id="4674d-175">Furthermore, the Membership and Roles services' functionalities are available programmatically through the `Membership` and `Roles` classes in the .NET Framework.</span></span> <span data-ttu-id="4674d-176">이러한 클래스와 함께 만들기, 편집 및 삭제 사용자 및 역할을도 사용자 역할에 추가 또는 제거에 대 한 어떤 역할에 사용자가을 확인 하 고 다른 사용자 및 역할 관련 작업을 수행 하는 코드를 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4674d-176">With these classes you can write code to create, edit, and delete users and roles, as well as to add or remove users to roles, to determine what users are in what roles, and to perform other user- and role-related tasks.</span></span>

<span data-ttu-id="4674d-177">에 [ *서비스를 구성 하는 웹 사이트를 사용 하 여 응용 프로그램* 자습서](configuring-a-website-that-uses-application-services-vb.md) 페이지를 추가 했지만 `Admin` 라는 폴더 `CreateAccount.aspx`합니다.</span><span class="sxs-lookup"><span data-stu-id="4674d-177">In the [*Configuring a Website That Uses Application Services* tutorial](configuring-a-website-that-uses-application-services-vb.md) I added a page to the `Admin` folder named `CreateAccount.aspx`.</span></span> <span data-ttu-id="4674d-178">이 페이지에서는 관리자가 사이트에 새 사용자 계정을 추가 하 고 새로 만든된 사용자가 관리자 역할에 있는지 여부를 지정할 수 (참조 **그림 5**).</span><span class="sxs-lookup"><span data-stu-id="4674d-178">This page allows an administrator to add a new user account to the site and to specify whether or not the newly created user is in the Admin role (see **Figure 5**).</span></span>

[![](users-and-roles-on-the-production-website-vb/_static/image14.png)](users-and-roles-on-the-production-website-vb/_static/image13.png)

<span data-ttu-id="4674d-179">**그림 5**: 관리자는 새 사용자 계정을 만들 수 있습니다</span><span class="sxs-lookup"><span data-stu-id="4674d-179">**Figure 5**: Administrators Can Create New User Accounts</span></span>  
<span data-ttu-id="4674d-180">([전체 크기 이미지를 보려면 클릭](users-and-roles-on-the-production-website-vb/_static/image15.png))</span><span class="sxs-lookup"><span data-stu-id="4674d-180">([Click to view full-size image](users-and-roles-on-the-production-website-vb/_static/image15.png))</span></span>

<span data-ttu-id="4674d-181">사용자 및 역할 관리 페이지를 사용 하 여 대 한 단계별 지침과 빌드에 대해 보다 자세한에 대 한는 `Membership` 및 `Roles` 클래스와 ASP.NET 웹 로그인 관련 컨트롤 내용을 반드시 내 [웹 사이트 보안 자습서](../../older-versions-security/introduction/security-basics-and-asp-net-support-cs.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="4674d-181">For a more detailed look at building user and role administration pages, along with step-by-step instructions on using the `Membership` and `Roles` classes and the Login-related ASP.NET Web controls, be sure to read my [Website Security Tutorials](../../older-versions-security/introduction/security-basics-and-asp-net-support-cs.md).</span></span> <span data-ttu-id="4674d-182">찾을 수 있습니다 지침 새 계정 만들기, 만들고 역할을 관리 하기 위한 웹 페이지를 작성 하는 방법에 역할 및 기타 일반 관리 작업에 사용자를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="4674d-182">There you'll find guidance on how to build web pages for creating new accounts, creating and managing roles, assigning users to roles, and other common administrative tasks.</span></span>

<span data-ttu-id="4674d-183">프로덕션 웹 사이트에서 WSAT 유사한 기능을 구현 하려면 사용자 고유의 일련 WSAT의 기능을 구현 하는 웹 페이지의 항상 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4674d-183">To implement WSAT-like functionality on the production website you can always build your own series of web pages that implement the WSAT's features.</span></span> <span data-ttu-id="4674d-184">시작 하십시오. % 폴더에 있는 WSAT 소스 코드를 체크 아웃 `%WINDIR%\Microsoft.NET\Framework\v2.0.50727\ASP.NETWebAdminFiles`합니다.</span><span class="sxs-lookup"><span data-stu-id="4674d-184">To help get started, check out the WSAT source code, which is located in the folder `%WINDIR%\Microsoft.NET\Framework\v2.0.50727\ASP.NETWebAdminFiles`.</span></span> <span data-ttu-id="4674d-185">가 작성 한 문서를 공유 그 Dan Clem WSAT 대체를 사용 하 여 또 다른 옵션은 [롤링 Your 직접 웹 사이트 관리 도구](http://aspnet.4guysfromrolla.com/articles/052307-1.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="4674d-185">Another option is to use Dan Clem's WSAT alternative, which he shares in his article, [Rolling Your Own Web Site Administration Tool](http://aspnet.4guysfromrolla.com/articles/052307-1.aspx).</span></span> <span data-ttu-id="4674d-186">Dan은 판독기는 사용자 지정 WSAT와 유사한 도구를 만드는 과정을 단계별로 안내 합니다., (C#에서) 다운로드에 대 한 자신의 응용 프로그램의 소스 코드를 포함 및 그의 사용자 지정 WSAT 호스팅되는 웹 사이트를 추가 하기 위한 단계별 지침을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="4674d-186">Dan walks readers through the process of building a custom WSAT-like tool, includes his application's source code for download (in C#), and gives step-by-step instructions for adding his custom WSAT to a hosted website.</span></span>

## <a name="summary"></a><span data-ttu-id="4674d-187">요약</span><span class="sxs-lookup"><span data-stu-id="4674d-187">Summary</span></span>

<span data-ttu-id="4674d-188">ASP.NET 웹 사이트 관리 도구 (WSAT) 웹 사이트에 대 한 사용자 및 역할 정보를 관리 하는 멤버 자격 및 역할 응용 프로그램 서비스와 함께에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4674d-188">The ASP.NET Web Site Administration Tool (WSAT) can be used in tandem with the Membership and Roles application services to manage user and role information for your website.</span></span> <span data-ttu-id="4674d-189">안타깝게도,는 WSAT만 액세스할 수 있는 로컬 있으며 프로덕션 웹 사이트를 방문할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4674d-189">Unfortunately, the WSAT is only accessible locally and cannot be visited from your production website.</span></span> <span data-ttu-id="4674d-190">그러나 개발에서 연결 문자열을 변경 하 여 프로덕션 데이터베이스를 가리킬 환경을 사용할 수는 WSAT 사용자 및 프로덕션 웹 사이트에 대 한 역할을 관리 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="4674d-190">However, by changing the connection string in the development environment to point to the production database you can use the WSAT to manage the users and roles on the production website.</span></span>

<span data-ttu-id="4674d-191">사용자 및 역할을 관리 하는 빠르고 쉬운 방법을 제공 하는 WSAT 접근을 하는 동안 연결 문자열 정보를 임시 변경을 Visual Studio에서 WSAT 시작 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4674d-191">While the WSAT approach affords a quick and easy way to manage users and roles, it necessitates launching the WSAT from Visual Studio as well as temporary changes to the connection string information.</span></span> <span data-ttu-id="4674d-192">WSAT 사용자 및 프로덕션 환경에 대 한 역할을 관리 하는 빠른 방법을 제공 하지만 것이 복잡 하 고 여러 관리자 또는 관리자에 게 없거나 Visual Studio와는 WSAT 익숙하지 않은 웹 사이트에 대해 제대로 작동 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4674d-192">The WSAT offers a quick way to manage users and roles on production, but is cumbersome and does not work well for websites with multiple administrators or with administrators who do not have or are not familiar with Visual Studio and the WSAT.</span></span> <span data-ttu-id="4674d-193">이러한 이유로, 사용자 계정을 지 원하는 대부분의 웹 사이트 관리 웹 페이지의 집합을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="4674d-193">For these reasons, most websites that support user accounts include a set of administrative web pages.</span></span> <span data-ttu-id="4674d-194">이러한 웹 페이지는 WSAT 하지 않아도 집합과 모든 컴퓨터에서 다양 한 관리 사용자가 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4674d-194">Such a set of web pages eliminates the need for the WSAT and used by various administrative users from any computer.</span></span>

<span data-ttu-id="4674d-195">만족도 매우 프로그래밍!</span><span class="sxs-lookup"><span data-stu-id="4674d-195">Happy Programming!</span></span>

### <a name="further-reading"></a><span data-ttu-id="4674d-196">추가 정보</span><span class="sxs-lookup"><span data-stu-id="4674d-196">Further Reading</span></span>

<span data-ttu-id="4674d-197">이 자습서에 설명 된 항목에 대 한 자세한 내용은 다음 리소스를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="4674d-197">For more information on the topics discussed in this tutorial, refer to the following resources:</span></span>

- [<span data-ttu-id="4674d-198">ASP를 검사 합니다. NET의 멤버 자격, 역할 및 프로필</span><span class="sxs-lookup"><span data-stu-id="4674d-198">Examining ASP.NET's Membership, Roles, and Profile</span></span>](http://aspnet.4guysfromrolla.com/articles/120705-1.aspx)
- [<span data-ttu-id="4674d-199">자신의 웹 사이트 관리 도구를 롤링합니다.</span><span class="sxs-lookup"><span data-stu-id="4674d-199">Rolling Your Own Web Site Administration Tool</span></span>](http://aspnet.4guysfromrolla.com/articles/052307-1.aspx)
- [<span data-ttu-id="4674d-200">웹 사이트 관리 도구 개요</span><span class="sxs-lookup"><span data-stu-id="4674d-200">Web Site Administration Tool Overview</span></span>](https://msdn.microsoft.com/en-us/library/yy40ytx0.aspx)
- [<span data-ttu-id="4674d-201">웹 사이트 보안 자습서</span><span class="sxs-lookup"><span data-stu-id="4674d-201">Website Security Tutorials</span></span>](../../older-versions-security/introduction/security-basics-and-asp-net-support-cs.md)

>[!div class="step-by-step"]
[<span data-ttu-id="4674d-202">이전</span><span class="sxs-lookup"><span data-stu-id="4674d-202">Previous</span></span>](precompiling-your-website-vb.md)