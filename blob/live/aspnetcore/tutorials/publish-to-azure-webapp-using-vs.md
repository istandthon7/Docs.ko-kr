---
title: "Visual Studio를 사용하여 Azure에 ASP.NET Core 앱 게시"
author: rick-anderson
description: "Visual Studio를 사용하여 Azure App Service에 ASP.NET Core 앱을 게시하는 방법을 알아봅니다."
ms.author: riande
manager: wpickett
ms.date: 12/16/2017
ms.topic: get-started-article
ms.technology: aspnet
ms.prod: asp.net-core
uid: tutorials/publish-to-azure-webapp-using-vs
ms.openlocfilehash: dd31e3a9583a0c152e97ae7cf6b215389298a20c
ms.sourcegitcommit: 3e303620a125325bb9abd4b2d315c106fb8c47fd
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/19/2018
---
<span data-ttu-id="35f0f-103">/ko-kr</span><span class="sxs-lookup"><span data-stu-id="35f0f-103">/en-us</span></span>

# <a name="publish-an-aspnet-core-web-app-to-azure-app-service-using-visual-studio"></a><span data-ttu-id="35f0f-104">Visual Studio를 사용하여 Azure App Service에 ASP.NET Core 웹앱 게시</span><span class="sxs-lookup"><span data-stu-id="35f0f-104">Publish an ASP.NET Core web app to Azure App Service using Visual Studio</span></span>

<span data-ttu-id="35f0f-105">작성자: [Rick Anderson](https://twitter.com/RickAndMSFT), [Cesar Blum Silveira](https://github.com/cesarbs) 및 [Rachel Appel](https://twitter.com/rachelappel)</span><span class="sxs-lookup"><span data-stu-id="35f0f-105">By [Rick Anderson](https://twitter.com/RickAndMSFT), [Cesar Blum Silveira](https://github.com/cesarbs), and [Rachel Appel](https://twitter.com/rachelappel)</span></span>

<span data-ttu-id="35f0f-106">Mac에서 작업하고 있는 경우 [Mac용 Visual Studio에서 Azure에 게시](https://blog.xamarin.com/publish-azure-visual-studio-mac/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="35f0f-106">See [Publish to Azure from Visual Studio for Mac](https://blog.xamarin.com/publish-azure-visual-studio-mac/) if you are working on a Mac.</span></span>

## <a name="set-up"></a><span data-ttu-id="35f0f-107">설치</span><span class="sxs-lookup"><span data-stu-id="35f0f-107">Set up</span></span>

* <span data-ttu-id="35f0f-108">계정이 없는 경우 [체험 Azure 계정](https://aka.ms/K5y5yh)을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="35f0f-108">Open a [free Azure account](https://aka.ms/K5y5yh) if you do not have one.</span></span> 

## <a name="create-a-web-app"></a><span data-ttu-id="35f0f-109">웹앱 만들기</span><span class="sxs-lookup"><span data-stu-id="35f0f-109">Create a web app</span></span>

<span data-ttu-id="35f0f-110">Visual Studio 시작 페이지에서 **파일 > 새로 만들기 > 프로젝트...**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="35f0f-110">In the Visual Studio Start Page, select **File > New > Project...**</span></span>

![파일 메뉴](publish-to-azure-webapp-using-vs/_static/file_new_project.png)

<span data-ttu-id="35f0f-112">**새 프로젝트** 대화 상자를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="35f0f-112">Complete the **New Project** dialog:</span></span>

* <span data-ttu-id="35f0f-113">왼쪽 창에서 **.NET Core**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="35f0f-113">In the left pane, select **.NET Core**.</span></span>
* <span data-ttu-id="35f0f-114">가운데 창에서 **ASP.NET Core 웹 응용 프로그램**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="35f0f-114">In the center pane, select **ASP.NET Core Web Application**.</span></span>
* <span data-ttu-id="35f0f-115">**확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="35f0f-115">Select **OK**.</span></span>

![새 프로젝트 대화 상자](publish-to-azure-webapp-using-vs/_static/new_prj.png)

<span data-ttu-id="35f0f-117">**새 ASP.NET Core 웹 응용 프로그램** 대화 상자에서:</span><span class="sxs-lookup"><span data-stu-id="35f0f-117">In the **New ASP.NET Core Web Application** dialog:</span></span>

* <span data-ttu-id="35f0f-118">**웹 응용 프로그램**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="35f0f-118">Select **Web Application**.</span></span>
* <span data-ttu-id="35f0f-119">**인증 변경**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="35f0f-119">Select **Change Authentication**.</span></span>

![새 프로젝트 대화 상자](publish-to-azure-webapp-using-vs/_static/new_prj_2.png)

<span data-ttu-id="35f0f-121">**인증 변경** 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="35f0f-121">The **Change Authentication** dialog appears.</span></span> 

* <span data-ttu-id="35f0f-122">**개별 사용자 계정**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="35f0f-122">Select **Individual User Accounts**.</span></span>
* <span data-ttu-id="35f0f-123">**확인**을 선택하여 **새 ASP.NET Core 웹 응용 프로그램**으로 돌아간 다음 다시 **확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="35f0f-123">Select **OK** to return to the **New ASP.NET Core Web Application**, then select **OK** again.</span></span>

![새 ASP.NET Core 웹 인증 대화 상자](publish-to-azure-webapp-using-vs/_static/new_prj_auth.png) 

<span data-ttu-id="35f0f-125">Visual Studio는 솔루션을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="35f0f-125">Visual Studio creates the solution.</span></span>

## <a name="run-the-app"></a><span data-ttu-id="35f0f-126">앱 실행</span><span class="sxs-lookup"><span data-stu-id="35f0f-126">Run the app</span></span>

* <span data-ttu-id="35f0f-127">Ctrl+F5를 눌러 프로젝트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="35f0f-127">Press CTRL+F5 to run the project.</span></span>
* <span data-ttu-id="35f0f-128">**정보** 및 **연락처** 링크를 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="35f0f-128">Test the **About** and **Contact** links.</span></span>

![localhost의 Microsoft Edge에서 열린 웹 응용 프로그램](publish-to-azure-webapp-using-vs/_static/show.png)

### <a name="register-a-user"></a><span data-ttu-id="35f0f-130">사용자 등록</span><span class="sxs-lookup"><span data-stu-id="35f0f-130">Register a user</span></span>

* <span data-ttu-id="35f0f-131">**등록**을 선택하고 새 사용자를 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="35f0f-131">Select **Register** and register a new user.</span></span> <span data-ttu-id="35f0f-132">가상의 전자 메일 주소를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35f0f-132">You can use a fictitious email address.</span></span> <span data-ttu-id="35f0f-133">제출하면 페이지에 다음과 같은 오류가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="35f0f-133">When you submit, the page displays the following error:</span></span>

    <span data-ttu-id="35f0f-134">*“내부 서버 오류: 요청을 처리하는 동안 데이터베이스 작업이 실패했습니다. SQL 예외: 데이터베이스를 열 수 없습니다. 응용 프로그램 DB 컨텍스트에 대한 기존 마이그레이션 적용으로 이 문제를 해결할 수 있습니다.”*</span><span class="sxs-lookup"><span data-stu-id="35f0f-134">*"Internal Server Error: A database operation failed while processing the request. SQL exception: Cannot open the database. Applying existing migrations for Application DB context may resolve this issue."*</span></span>
* <span data-ttu-id="35f0f-135">**마이그레이션 적용**을 선택한 다음 페이지가 업데이트되면 페이지를 새로 고칩니다.</span><span class="sxs-lookup"><span data-stu-id="35f0f-135">Select **Apply Migrations** and, once the page updates, refresh the page.</span></span>

![내부 서버 오류: 요청을 처리하는 동안 데이터베이스 작업이 실패했습니다.](publish-to-azure-webapp-using-vs/_static/mig.png)

<span data-ttu-id="35f0f-139">앱은 새 사용자를 등록하는 데 사용한 전자 메일 및 **로그아웃** 링크를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="35f0f-139">The app displays the email used to register the new user and a **Log out** link.</span></span>

![Microsoft Edge에서 열린 웹 응용 프로그램.](publish-to-azure-webapp-using-vs/_static/hello.png)

## <a name="deploy-the-app-to-azure"></a><span data-ttu-id="35f0f-142">Azure에 앱 배포</span><span class="sxs-lookup"><span data-stu-id="35f0f-142">Deploy the app to Azure</span></span>

<span data-ttu-id="35f0f-143">솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 **게시...**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="35f0f-143">Right-click on the project in Solution Explorer and select **Publish...**.</span></span>

![강조 표시된 게시 링크로 열린 바로 가기 메뉴](publish-to-azure-webapp-using-vs/_static/pub.png)

<span data-ttu-id="35f0f-145">**게시** 대화 상자에서:</span><span class="sxs-lookup"><span data-stu-id="35f0f-145">In the **Publish** dialog:</span></span>

* <span data-ttu-id="35f0f-146">**Microsoft Azure App Service**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="35f0f-146">Select **Microsoft Azure App Service**.</span></span>
* <span data-ttu-id="35f0f-147">기어 아이콘을 선택한 다음 **프로필 만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="35f0f-147">Select the gear icon and then select **Create Profile**.</span></span>
* <span data-ttu-id="35f0f-148">**프로필 만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="35f0f-148">Select **Create Profile**.</span></span>

![게시 대화 상자](publish-to-azure-webapp-using-vs/_static/maas1.png)

### <a name="create-azure-resources"></a><span data-ttu-id="35f0f-150">Azure 리소스 만들기</span><span class="sxs-lookup"><span data-stu-id="35f0f-150">Create Azure resources</span></span>

<span data-ttu-id="35f0f-151">**App Service 만들기** 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="35f0f-151">The **Create App Service** dialog appears:</span></span>

* <span data-ttu-id="35f0f-152">구독을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="35f0f-152">Enter your subscription.</span></span>
* <span data-ttu-id="35f0f-153">**앱 이름**, **리소스 그룹** 및 **App Service 계획** 항목 필드가 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="35f0f-153">The **App Name**, **Resource Group**, and **App Service Plan** entry fields are populated.</span></span> <span data-ttu-id="35f0f-154">이러한 이름을 유지하거나 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35f0f-154">You can keep these names or change them.</span></span>

![App Service 대화 상자](publish-to-azure-webapp-using-vs/_static/newrg1.png)

* <span data-ttu-id="35f0f-156">**서비스** 탭을 선택하여 새 데이터베이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="35f0f-156">Select the **Services** tab to create a new database.</span></span>

* <span data-ttu-id="35f0f-157">녹색 **+** 아이콘을 선택하여 새 SQL Database를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="35f0f-157">Select the green **+** icon to create a new SQL Database</span></span>

![새 SQL Database](publish-to-azure-webapp-using-vs/_static/sql.png)

* <span data-ttu-id="35f0f-159">**SQL Database 구성** 대화 상자에서 **새로 만들기...**를 선택하여 새 데이터베이스 서버를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="35f0f-159">Select **New...** on the **Configure SQL Database** dialog to create a new database.</span></span>

![새 SQL Database 및 서버](publish-to-azure-webapp-using-vs/_static/conf.png)

<span data-ttu-id="35f0f-161">**SQL Server 구성** 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="35f0f-161">The **Configure SQL Server** dialog appears.</span></span>

* <span data-ttu-id="35f0f-162">관리자 사용자 이름 및 암호를 입력한 다음 **확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="35f0f-162">Enter an administrator user name and password, and then select **OK**.</span></span> <span data-ttu-id="35f0f-163">기본 **서버 이름**을 유지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35f0f-163">You can keep the default **Server Name**.</span></span> 

> [!NOTE]
> <span data-ttu-id="35f0f-164">"관리자"는 관리자 사용자 이름으로 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="35f0f-164">"admin" is not allowed as the administrator user name.</span></span>

![SQL Server 구성 대화 상자](publish-to-azure-webapp-using-vs/_static/conf_servername.png)

* <span data-ttu-id="35f0f-166">**확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="35f0f-166">Select **OK**.</span></span>

<span data-ttu-id="35f0f-167">Visual Studio가 **App Service 만들기** 대화 상자로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="35f0f-167">Visual Studio returns to the **Create App Service** dialog.</span></span>

* <span data-ttu-id="35f0f-168">**App Service 만들기** 대화 상자에서 **만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="35f0f-168">Select **Create** on the **Create App Service** dialog.</span></span>

![SQL Database 구성 대화 상자](publish-to-azure-webapp-using-vs/_static/conf_final.png)

<span data-ttu-id="35f0f-170">Visual Studio는 Azure에서 웹앱 및 SQL Server를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="35f0f-170">Visual Studio creates the Web app and SQL Server on Azure.</span></span> <span data-ttu-id="35f0f-171">이 단계는 몇 분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35f0f-171">This step can take a few minutes.</span></span> <span data-ttu-id="35f0f-172">만든 리소스에 대한 자세한 내용은 [추가 리소스](#additonal-resources)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="35f0f-172">For information on the resources created, see [Additonal resources](#additonal-resources).</span></span>

<span data-ttu-id="35f0f-173">배포가 완료되면 **설정**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="35f0f-173">When deployment completes, select **Settings**:</span></span>

![SQL Server 구성 대화 상자](publish-to-azure-webapp-using-vs/_static/set.png)

<span data-ttu-id="35f0f-175">**게시** 대화 상자의 **설정** 페이지에서:</span><span class="sxs-lookup"><span data-stu-id="35f0f-175">On the **Settings** page of the **Publish** dialog:</span></span>

  * <span data-ttu-id="35f0f-176">**데이터베이스**를 확장하고 **런타임 시 이 연결 문자열 사용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="35f0f-176">Expand **Databases** and check **Use this connection string at runtime**.</span></span>
  * <span data-ttu-id="35f0f-177">**Entity Framework 마이그레이션**을 확장하고 **게시에 이 마이그레이션 적용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="35f0f-177">Expand **Entity Framework Migrations** and check **Apply this migration on publish**.</span></span>

* <span data-ttu-id="35f0f-178">**저장**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="35f0f-178">Select **Save**.</span></span> <span data-ttu-id="35f0f-179">Visual Studio가 **게시** 대화 상자로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="35f0f-179">Visual Studio returns to the **Publish** dialog.</span></span> 

![게시 대화 상자: 설정 패널](publish-to-azure-webapp-using-vs/_static/pubs.png)

<span data-ttu-id="35f0f-181">**게시**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="35f0f-181">Click **Publish**.</span></span> <span data-ttu-id="35f0f-182">Visual Studio는 Azure에 앱을 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="35f0f-182">Visual Studio publishs your app to Azure.</span></span> <span data-ttu-id="35f0f-183">배포가 완료되면 앱이 브라우저에서 열립니다.</span><span class="sxs-lookup"><span data-stu-id="35f0f-183">When the depoyment completes, the app is opened in a browser.</span></span>

### <a name="test-your-app-in-azure"></a><span data-ttu-id="35f0f-184">Azure에서 앱 테스트</span><span class="sxs-lookup"><span data-stu-id="35f0f-184">Test your app in Azure</span></span>

* <span data-ttu-id="35f0f-185">**정보** 및 **연락처** 링크 테스트</span><span class="sxs-lookup"><span data-stu-id="35f0f-185">Test the **About** and **Contact** links</span></span>

* <span data-ttu-id="35f0f-186">새 사용자 등록</span><span class="sxs-lookup"><span data-stu-id="35f0f-186">Register a new user</span></span>

![Azure App Service의 Microsoft Edge에서 열린 웹 응용 프로그램](publish-to-azure-webapp-using-vs/_static/register.png)

### <a name="update-the-app"></a><span data-ttu-id="35f0f-188">앱 업데이트</span><span class="sxs-lookup"><span data-stu-id="35f0f-188">Update the app</span></span>

* <span data-ttu-id="35f0f-189">*Pages/About.cshtml* Razor 페이지를 편집하고 내용을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="35f0f-189">Edit the *Pages/About.cshtml* Razor page and change its contents.</span></span> <span data-ttu-id="35f0f-190">예를 들어 단락을 수정하여 “Hello ASP.NET Core!” 문구를 표시할 수 있습니다. [!code-html[About](publish-to-azure-webapp-using-vs/sample/about.cshtml?highlight=9&range=1-9)]</span><span class="sxs-lookup"><span data-stu-id="35f0f-190">For example, you can modify the paragraph to say "Hello ASP.NET Core!": [!code-html[About](publish-to-azure-webapp-using-vs/sample/about.cshtml?highlight=9&range=1-9)]</span></span>

* <span data-ttu-id="35f0f-191">프로젝트를 마우스 오른쪽 단추로 클릭하고 **게시...**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="35f0f-191">Right-click on the project and select **Publish...** again.</span></span>

![강조 표시된 게시 링크로 열린 바로 가기 메뉴](publish-to-azure-webapp-using-vs/_static/pub.png)

* <span data-ttu-id="35f0f-193">앱이 게시된 후 변경 내용이 Azure에서 제공되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="35f0f-193">After the app is published, verify the changes you made are available on Azure.</span></span>

![작업이 완료되었는지 확인합니다.](publish-to-azure-webapp-using-vs/_static/final.png)

### <a name="clean-up"></a><span data-ttu-id="35f0f-195">정리</span><span class="sxs-lookup"><span data-stu-id="35f0f-195">Clean up</span></span>

<span data-ttu-id="35f0f-196">앱 테스트를 완료하면 [Azure Portal](https://portal.azure.com/)로 이동하고 앱을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="35f0f-196">When you have finished testing the app, go to the [Azure portal](https://portal.azure.com/) and delete the app.</span></span>

* <span data-ttu-id="35f0f-197">**리소스 그룹**을 선택한 다음 만든 리소스 그룹을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="35f0f-197">Select **Resource groups**, then select the resource group you created.</span></span>

![Azure Portal: 사이드바 메뉴에 있는 리소스 그룹](publish-to-azure-webapp-using-vs/_static/portalrg.png)

* <span data-ttu-id="35f0f-199">**리소스 그룹** 페이지에서 **삭제**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="35f0f-199">In the **Resource groups** page, select **Delete**.</span></span>

![Azure Portal: 리소스 그룹 페이지](publish-to-azure-webapp-using-vs/_static/rgd.png)

* <span data-ttu-id="35f0f-201">리소스 그룹의 이름을 입력하고 **삭제**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="35f0f-201">Enter the name of the resource group and select **Delete**.</span></span> <span data-ttu-id="35f0f-202">이 자습서에서 만든 앱과 다른 모든 리소스는 이제 Azure에서 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="35f0f-202">Your app and all other resources created in this tutorial are now deleted from Azure.</span></span>

### <a name="next-steps"></a><span data-ttu-id="35f0f-203">다음 단계</span><span class="sxs-lookup"><span data-stu-id="35f0f-203">Next steps</span></span>

* [<span data-ttu-id="35f0f-204">Visual Studio 및 Git을 사용하여 Azure에 연속 배포</span><span class="sxs-lookup"><span data-stu-id="35f0f-204">Continuous Deployment to Azure with Visual Studio and Git</span></span>](xref:host-and-deploy/azure-apps/azure-continuous-deployment)

## <a name="additonal-resources"></a><span data-ttu-id="35f0f-205">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="35f0f-205">Additonal resources</span></span>

* [<span data-ttu-id="35f0f-206">Azure App Service</span><span class="sxs-lookup"><span data-stu-id="35f0f-206">Azure App Service</span></span>](https://docs.microsoft.com/en-us/azure/app-service/app-service-web-overview)
* [<span data-ttu-id="35f0f-207">Azure 리소스 그룹</span><span class="sxs-lookup"><span data-stu-id="35f0f-207">Azure resource groups</span></span>](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview#resource-groups)
* [<span data-ttu-id="35f0f-208">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="35f0f-208">Azure SQL Database</span></span>](https://docs.microsoft.com/en-us/azure/sql-database/)