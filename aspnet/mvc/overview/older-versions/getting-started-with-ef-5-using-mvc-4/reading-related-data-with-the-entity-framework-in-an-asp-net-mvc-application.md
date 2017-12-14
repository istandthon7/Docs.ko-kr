---
uid: mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application
title: "(5/10) ASP.NET MVC 응용 프로그램에서 Entity Framework와 관련 된 데이터 읽기 | Microsoft Docs"
author: tdykstra
description: "Contoso 대학 샘플 웹 응용 프로그램에는 Entity Framework 5 Code First 및 Visual Studio를 사용 하 여 ASP.NET MVC 4 응용 프로그램을 만드는 방법을 보여 줍니다 중..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/30/2013
ms.topic: article
ms.assetid: 0d6fb83b-71f7-425d-8dec-981197d7ec42
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: f455c3656c9120f4d7e6fccdba8f705e0a1c7d35
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="reading-related-data-with-the-entity-framework-in-an-aspnet-mvc-application-5-of-10"></a><span data-ttu-id="a123a-103">읽기 (5/10) ASP.NET MVC 응용 프로그램에서 Entity Framework 사용 하 여 데이터 관련</span><span class="sxs-lookup"><span data-stu-id="a123a-103">Reading Related Data with the Entity Framework in an ASP.NET MVC Application (5 of 10)</span></span>
====================
<span data-ttu-id="a123a-104">으로 [Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="a123a-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

[<span data-ttu-id="a123a-105">완료 된 프로젝트를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="a123a-105">Download Completed Project</span></span>](http://code.msdn.microsoft.com/Getting-Started-with-dd0e2ed8)

> <span data-ttu-id="a123a-106">Contoso 대학 샘플 웹 응용 프로그램에는 Entity Framework 5 Code First 및 Visual Studio 2012를 사용 하 여 ASP.NET MVC 4 응용 프로그램을 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a123a-106">The Contoso University sample web application demonstrates how to create ASP.NET MVC 4 applications using the Entity Framework 5 Code First and Visual Studio 2012.</span></span> <span data-ttu-id="a123a-107">자습서 시리즈에 대 한 정보를 참조 하십시오. [시리즈의 첫 번째 자습서](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="a123a-107">For information about the tutorial series, see [the first tutorial in the series](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span></span> <span data-ttu-id="a123a-108">시작 부분에서 자습서 시리즈를 시작할 수 있습니다 또는 [이 장의 대 한 시작 프로젝트 다운로드](building-the-ef5-mvc4-chapter-downloads.md) 여기에서 시작 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a123a-108">You can start the tutorial series from the beginning or [download a starter project for this chapter](building-the-ef5-mvc4-chapter-downloads.md) and start here.</span></span>
> 
> > [!NOTE] 
> > 
> > <span data-ttu-id="a123a-109">해결할 수 없는 문제에 직면 하는 경우 [완료 장 다운로드](building-the-ef5-mvc4-chapter-downloads.md) 문제를 재현 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="a123a-109">If you run into a problem you can't resolve, [download the completed chapter](building-the-ef5-mvc4-chapter-downloads.md) and try to reproduce your problem.</span></span> <span data-ttu-id="a123a-110">일반적으로 코드 완성 된 코드를 비교 하 여 문제에 솔루션을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a123a-110">You can generally find the solution to the problem by comparing your code to the completed code.</span></span> <span data-ttu-id="a123a-111">몇 가지 일반적인 오류 및 해결 하는 방법에 대 한 참조 [오류 및 해결 방법입니다.](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)</span><span class="sxs-lookup"><span data-stu-id="a123a-111">For some common errors and how to solve them, see [Errors and Workarounds.](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)</span></span>


<span data-ttu-id="a123a-112">이전 자습서에서 School 데이터 모델을 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="a123a-112">In the previous tutorial you completed the School data model.</span></span> <span data-ttu-id="a123a-113">이 자습서에서는 읽기 및 관련된 데이터를 표시 합니다-즉, 데이터 탐색 속성에는 Entity Framework를 로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="a123a-113">In this tutorial you'll read and display related data — that is, data that the Entity Framework loads into navigation properties.</span></span>

<span data-ttu-id="a123a-114">다음 그림에서는 보여 페이지와 협력 합니다.</span><span class="sxs-lookup"><span data-stu-id="a123a-114">The following illustrations show the pages that you'll work with.</span></span>

![](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image1.png)

![Instructors_index_page_with_instructor_and_course_selected](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image2.png)

## <a name="lazy-eager-and-explicit-loading-of-related-data"></a><span data-ttu-id="a123a-116">지연, 신속 하 게, 및 명시적 관련된 데이터 로드</span><span class="sxs-lookup"><span data-stu-id="a123a-116">Lazy, Eager, and Explicit Loading of Related Data</span></span>

<span data-ttu-id="a123a-117">여러 가지 방법으로 Entity Framework가 엔터티의 탐색 속성에 관련된 데이터를 로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a123a-117">There are several ways that the Entity Framework can load related data into the navigation properties of an entity:</span></span>

- <span data-ttu-id="a123a-118">*지연 로드*합니다.</span><span class="sxs-lookup"><span data-stu-id="a123a-118">*Lazy loading*.</span></span> <span data-ttu-id="a123a-119">먼저 엔터티를 읽으면 관련된 데이터가 검색 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a123a-119">When the entity is first read, related data isn't retrieved.</span></span> <span data-ttu-id="a123a-120">그러나는 탐색 속성에 액세스 하려고 처음으로 해당 탐색 속성에 필요한 데이터가 자동으로 검색 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a123a-120">However, the first time you attempt to access a navigation property, the data required for that navigation property is automatically retrieved.</span></span> <span data-ttu-id="a123a-121">이 인해 데이터베이스에 전송 하는 여러 개의 쿼리-엔터티 자체에 대 한 개와 때마다 관련 엔터티에 대 한 데이터를 검색 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a123a-121">This results in multiple queries sent to the database — one for the entity itself and one each time that related data for the entity must be retrieved.</span></span> 

    ![Lazy_loading_example](https://asp.net/media/2577850/Windows-Live-Writer_Reading-Re.NET-MVC-Application-5-of-10h1_ADC3_Lazy_loading_example_2c44eabb-5fd3-485a-837d-8e3d053f2c0c.png)
- <span data-ttu-id="a123a-123">*즉시 로드*합니다.</span><span class="sxs-lookup"><span data-stu-id="a123a-123">*Eager loading*.</span></span> <span data-ttu-id="a123a-124">엔터티를 읽을 때 함께 관련된 데이터가 검색 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a123a-124">When the entity is read, related data is retrieved along with it.</span></span> <span data-ttu-id="a123a-125">일반적으로 필요한 데이터를 모두 검색 하는 단일 조인 쿼리에서 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="a123a-125">This typically results in a single join query that retrieves all of the data that's needed.</span></span> <span data-ttu-id="a123a-126">즉시 로드를 사용 하 여 지정 된 `Include` 메서드.</span><span class="sxs-lookup"><span data-stu-id="a123a-126">You specify eager loading by using the `Include` method.</span></span>

    ![Eager_loading_example](https://asp.net/media/2577856/Windows-Live-Writer_Reading-Re.NET-MVC-Application-5-of-10h1_ADC3_Eager_loading_example_33f907ff-f0b0-4057-8e75-05a8cacac807.png)
- <span data-ttu-id="a123a-128">*명시적 로드*합니다.</span><span class="sxs-lookup"><span data-stu-id="a123a-128">*Explicit loading*.</span></span> <span data-ttu-id="a123a-129">이 지연 로드를 제외 하 코드에서 관련된 데이터를 명시적으로 검색 탐색 속성에 액세스할 때 자동으로 발생 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a123a-129">This is similar to lazy loading, except that you explicitly retrieve the related data in code; it doesn't happen automatically when you access a navigation property.</span></span> <span data-ttu-id="a123a-130">엔터티 및 호출에 대 한 개체 상태 관리자 항목을 가져오는 하 여 수동으로 관련된 데이터를 로드 하면는 `Collection.Load` 컬렉션에 대 한 메서드 또는 `Reference.Load` 단일 엔터티를 포함 하는 속성에 대 한 메서드.</span><span class="sxs-lookup"><span data-stu-id="a123a-130">You load related data manually by getting the object state manager entry for an entity and calling the `Collection.Load` method for collections or the `Reference.Load` method for properties that hold a single entity.</span></span> <span data-ttu-id="a123a-131">(다음 예제에서는 관리자 탐색 속성을 로드 하려는 경우 바꿨을 것 `Collection(x => x.Courses)` 와 `Reference(x => x.Administrator)`.)</span><span class="sxs-lookup"><span data-stu-id="a123a-131">(In the following example, if you wanted to load the Administrator navigation property, you'd replace `Collection(x => x.Courses)` with `Reference(x => x.Administrator)`.)</span></span>

    ![Explicit_loading_example](https://asp.net/media/2577862/Windows-Live-Writer_Reading-Re.NET-MVC-Application-5-of-10h1_ADC3_Explicit_loading_example_79d8c368-6d82-426f-be9a-2b443644ab15.png)

<span data-ttu-id="a123a-133">속성 값을 즉시 검색 하지 않으므로 지연 로드 및 명시적 로딩 둘 다 라고도 *지연 된 로드*합니다.</span><span class="sxs-lookup"><span data-stu-id="a123a-133">Because they don't immediately retrieve the property values, lazy loading and explicit loading are also both known as *deferred loading*.</span></span>

<span data-ttu-id="a123a-134">일반적으로 알고 있는 경우 관련 된 데이터에 필요한 모든 엔터티 검색, 신속 하 게 로드 최상의 성능을 제공 데이터베이스에 전송 하는 단일 쿼리를 검색할 각 엔터티에 대 한 별개의 쿼리와 보다 일반적으로 더 효율적 이므로 합니다.</span><span class="sxs-lookup"><span data-stu-id="a123a-134">In general, if you know you need related data for every entity retrieved, eager loading offers the best performance, because a single query sent to the database is typically more efficient than separate queries for each entity retrieved.</span></span> <span data-ttu-id="a123a-135">예를 들어 위의 예제에서 각 부서에는 10 개의 관련된 과정을 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a123a-135">For example, in the above examples, suppose that each department has ten related courses.</span></span> <span data-ttu-id="a123a-136">즉시 로드 예는 데이터베이스에 왕복만 단일 (조인) 쿼리 및 단일으로 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a123a-136">The eager loading example would result in just a single (join) query and a single round trip to the database.</span></span> <span data-ttu-id="a123a-137">지연 로드 하 고 명시적 로딩 예는 모두 유발 11 개의 쿼리 및 11 개의 왕복 데이터베이스에 합니다.</span><span class="sxs-lookup"><span data-stu-id="a123a-137">The lazy loading and explicit loading examples would both result in eleven queries and eleven round trips to the database.</span></span> <span data-ttu-id="a123a-138">데이터베이스에 추가 왕복 성능이 저하 때는 대기 시간이 깁니다.</span><span class="sxs-lookup"><span data-stu-id="a123a-138">The extra round trips to the database are especially detrimental to performance when latency is high.</span></span>

<span data-ttu-id="a123a-139">반면에 일부 시나리오에서는 한 지연 로딩이 더 효율적입니다.</span><span class="sxs-lookup"><span data-stu-id="a123a-139">On the other hand, in some scenarios lazy loading is more efficient.</span></span> <span data-ttu-id="a123a-140">즉시 로드에는 SQL Server 없습니다 효율적으로 처리 하는 생성 될 매우 복잡 한 조인이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a123a-140">Eager loading might cause a very complex join to be generated, which SQL Server can't process efficiently.</span></span> <span data-ttu-id="a123a-141">또는 엔터티 집합의 하위 집합에 대 한 엔터티 탐색 속성에 액세스 해야 하는 경우 처리 하는, 즉시 로드 필요한 것 보다 더 많은 데이터를 검색 하기 때문에 한 지연 로딩이 향상 될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a123a-141">Or if you need to access an entity's navigation properties only for a subset of a set of entities you're processing, lazy loading might perform better because eager loading would retrieve more data than you need.</span></span> <span data-ttu-id="a123a-142">성능이 중요 한 경우에 최상의 선택을 하기 위해 두 가지 방식으로 성능을 테스트 하는 가장 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="a123a-142">If performance is critical, it's best to test performance both ways in order to make the best choice.</span></span>

<span data-ttu-id="a123a-143">일반적으로 지연 오프 로드 설정 하는 경우에 명시적으로 로드를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a123a-143">Typically you'd use explicit loading only when you've turned lazy loading off.</span></span> <span data-ttu-id="a123a-144">직렬화 하는 동안 지연 오프 로딩을 설정 해야 하는 경우 한 가지 시나리오가입니다.</span><span class="sxs-lookup"><span data-stu-id="a123a-144">One scenario when you should turn lazy loading off is during serialization.</span></span> <span data-ttu-id="a123a-145">지연 로드 및 serialization, 섞어 쓰지 마세요 하 고 로드는 활성화 지연 하는 경우 의도 한 것 보다 훨씬 더 많은 데이터를 쿼리 하 게 참고 하십시오.</span><span class="sxs-lookup"><span data-stu-id="a123a-145">Lazy loading and serialization don't mix well, and if you aren't careful you can end up querying significantly more data than you intended when lazy loading is enabled.</span></span> <span data-ttu-id="a123a-146">직렬화는 일반적으로 각 속성에는 형식의 인스턴스로 액세스 하 여 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="a123a-146">Serialization generally works by accessing each property on an instance of a type.</span></span> <span data-ttu-id="a123a-147">속성 액세스 지연 로드를 트리거하며 지연 로드 된 엔터티를 serialize 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a123a-147">Property access triggers lazy loading, and those lazy loaded entities are serialized.</span></span> <span data-ttu-id="a123a-148">Serialization 프로세스의 지연 로드 된 엔터티를 잠재적으로 더 많은 지연 로드 및 직렬화를 일으키는 각 속성을 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="a123a-148">The serialization process then accesses each property of the lazy-loaded entities, potentially causing even more lazy loading and serialization.</span></span> <span data-ttu-id="a123a-149">런어웨이 연쇄 반응을이 방지 하려면 지연 엔터티를 serialize 하기 전에 오프 로딩을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a123a-149">To prevent this run-away chain reaction, turn lazy loading off before you serialize an entity.</span></span>

<span data-ttu-id="a123a-150">데이터베이스 컨텍스트 클래스는 기본적으로 지연 로드를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="a123a-150">The database context class performs lazy loading by default.</span></span> <span data-ttu-id="a123a-151">지연 로드를 사용 하지 않도록 설정 하는 방법은 두 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a123a-151">There are two ways to disable lazy loading:</span></span>

- <span data-ttu-id="a123a-152">특정 탐색 속성에 대 한 생략 된 `virtual` 키워드는 속성을 선언 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="a123a-152">For specific navigation properties, omit the `virtual` keyword when you declare the property.</span></span>
- <span data-ttu-id="a123a-153">모든 탐색 속성에 대 한 설정 `LazyLoadingEnabled` 를 `false`합니다.</span><span class="sxs-lookup"><span data-stu-id="a123a-153">For all navigation properties, set `LazyLoadingEnabled` to `false`.</span></span> <span data-ttu-id="a123a-154">예를 들어 컨텍스트 클래스의 생성자에 다음 코드를 넣을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a123a-154">For example, you can put the following code in the constructor of your context class:</span></span> 

    [!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs)]

<span data-ttu-id="a123a-155">지연 로드로 인해 성능 문제가 발생 하는 코드를 마스킹할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a123a-155">Lazy loading can mask code that causes performance problems.</span></span> <span data-ttu-id="a123a-156">예를 들어 eager 또는 명시적 로드를 지정 하지 않으면 하지만 많은 양의 엔터티를 처리 하 고 각 반복에서 몇 가지 탐색 속성을 사용 하 여 코드를 수 없습니다 효율적이 지 (때문에 데이터베이스에 여러 번 왕복).</span><span class="sxs-lookup"><span data-stu-id="a123a-156">For example, code that doesn't specify eager or explicit loading but processes a high volume of entities and uses several navigation properties in each iteration might be very inefficient (because of many round trips to the database).</span></span> <span data-ttu-id="a123a-157">온-프레미스 SQL server를 사용 하 여 개발을 수행 하는 응용 프로그램에는 대기 시간이 증가 및 지연 로드로 인해 Azure SQL 데이터베이스를 이동할 때 성능 문제가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a123a-157">An application that performs well in development using an on premise SQL server might have performance problems when moved to Azure SQL Database due to the increased latency and lazy loading.</span></span> <span data-ttu-id="a123a-158">데이터베이스 쿼리는 실제 테스트 한 부하를 프로 파일링 한 지연 로딩이 적합 한지 결정 하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a123a-158">Profiling the database queries with a realistic test load will help you determine if lazy loading is appropriate.</span></span> <span data-ttu-id="a123a-159">자세한 내용은 참조 [Entity Framework 전략 제공: 관련 데이터를 로드](https://msdn.microsoft.com/en-us/magazine/hh205756.aspx) 및 [SQL Azure로 네트워크 대기 시간 줄이기를 Entity Framework를 사용 하 여](https://msdn.microsoft.com/en-us/magazine/gg309181.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="a123a-159">For more information see [Demystifying Entity Framework Strategies: Loading Related Data](https://msdn.microsoft.com/en-us/magazine/hh205756.aspx) and [Using the Entity Framework to Reduce Network Latency to SQL Azure](https://msdn.microsoft.com/en-us/magazine/gg309181.aspx).</span></span>

## <a name="create-a-courses-index-page-that-displays-department-name"></a><span data-ttu-id="a123a-160">해당 표시 부서 이름 과정 인덱스 페이지 만들기</span><span class="sxs-lookup"><span data-stu-id="a123a-160">Create a Courses Index Page That Displays Department Name</span></span>

<span data-ttu-id="a123a-161">`Course` 엔터티를 포함 하는 탐색 속성에 포함 되어는 `Department` 엔터티 과정에 할당 된 부서입니다.</span><span class="sxs-lookup"><span data-stu-id="a123a-161">The `Course` entity includes a navigation property that contains the `Department` entity of the department that the course is assigned to.</span></span> <span data-ttu-id="a123a-162">가져오기 과정의 목록에 할당 된 부서 이름을 표시 하려면 해야는 `Name` 속성에서는 `Department` 에 있는 엔터티의 `Course.Department` 탐색 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="a123a-162">To display the name of the assigned department in a list of courses, you need to get the `Name` property from the `Department` entity that is in the `Course.Department` navigation property.</span></span>

<span data-ttu-id="a123a-163">라는 컨트롤러를 만들고 `CourseController` 에 대 한는 `Course` 앞에 했던 것과 동일한 옵션을 사용 하 여 엔터티 형식에는 `Student` 컨트롤러, 다음 그림에 나와 있는 것 처럼 (컨텍스트 클래스는 이미지와 달리 DAL 네임 스페이스에 제외 모델 네임 스페이스가 아니라):</span><span class="sxs-lookup"><span data-stu-id="a123a-163">Create a controller named `CourseController` for the `Course` entity type, using the same options that you did earlier for the `Student` controller, as shown in the following illustration (except unlike the image, your context class is in the DAL namespace, not the Models namespace):</span></span>

![Add_Controller_dialog_box_for_Course_controller](https://asp.net/media/2577868/Windows-Live-Writer_Reading-Re.NET-MVC-Application-5-of-10h1_ADC3_Add_Controller_dialog_box_for_Course_controller_c167c11e-2d3e-4b64-a2b9-a0b368b8041d.png)

<span data-ttu-id="a123a-165">열기 *Controllers\CourseController.cs* 살펴보세요는 `Index` 메서드:</span><span class="sxs-lookup"><span data-stu-id="a123a-165">Open *Controllers\CourseController.cs* and look at the `Index` method:</span></span>

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.cs)]

<span data-ttu-id="a123a-166">자동 스 캐 폴딩이에 대 한 즉시 로드 지정는 `Department` 를 사용 하 여 탐색 속성에서 `Include` 메서드.</span><span class="sxs-lookup"><span data-stu-id="a123a-166">The automatic scaffolding has specified eager loading for the `Department` navigation property by using the `Include` method.</span></span>

<span data-ttu-id="a123a-167">열기 *Views\Course\Index.cshtml* 기존 코드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="a123a-167">Open *Views\Course\Index.cshtml* and replace the existing code with the following code.</span></span> <span data-ttu-id="a123a-168">변경 내용은 강조 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a123a-168">The changes are highlighted:</span></span>

[!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cshtml?highlight=4,15,18,28-30)]

<span data-ttu-id="a123a-169">스 캐 폴드 코드를 다음과 같이 변경을 했습니다.</span><span class="sxs-lookup"><span data-stu-id="a123a-169">You've made the following changes to the scaffolded code:</span></span>

- <span data-ttu-id="a123a-170">제목을 변경 **인덱스** 를 **Courses**합니다.</span><span class="sxs-lookup"><span data-stu-id="a123a-170">Changed the heading from **Index** to **Courses**.</span></span>
- <span data-ttu-id="a123a-171">행 파일에 대 한 링크를 왼쪽으로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="a123a-171">Moved the row links to the left.</span></span>
- <span data-ttu-id="a123a-172">열 머리글 아래에서 추가 **번호** 보여 주는 `CourseID` 속성 값입니다.</span><span class="sxs-lookup"><span data-stu-id="a123a-172">Added a column under the heading **Number** that shows the `CourseID` property value.</span></span> <span data-ttu-id="a123a-173">(기본적으로 기본 키 아닌 스 캐 폴드 된 되므로 일반적으로 최종 사용자에 게 의미가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a123a-173">(By default, primary keys aren't scaffolded because normally they are meaningless to end users.</span></span> <span data-ttu-id="a123a-174">그러나이 경우 기본 키 의미 이며 하려는 표시할지를 기준으로 합니다.)</span><span class="sxs-lookup"><span data-stu-id="a123a-174">However, in this case the primary key is meaningful and you want to show it.)</span></span>
- <span data-ttu-id="a123a-175">마지막 열 머리글을 변경 **DepartmentID** (외래 키의 이름에서 `Department` 엔터티)에 **부서**합니다.</span><span class="sxs-lookup"><span data-stu-id="a123a-175">Changed the last column heading from **DepartmentID** (the name of the foreign key to the `Department` entity) to **Department**.</span></span>

<span data-ttu-id="a123a-176">에 마지막 열에 대 한 스 캐 폴드 코드 표시는 `Name` 의 속성은 `Department` 에 로드 된 엔터티는 `Department` 탐색 속성:</span><span class="sxs-lookup"><span data-stu-id="a123a-176">Notice that for the last column, the scaffolded code displays the `Name` property of the `Department` entity that's loaded into the `Department` navigation property:</span></span>

[!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cshtml)]

<span data-ttu-id="a123a-177">페이지를 실행 (선택 된 **Courses** Contoso 대학 홈 페이지 탭) 부서 이름의 목록을 보려면 합니다.</span><span class="sxs-lookup"><span data-stu-id="a123a-177">Run the page (select the **Courses** tab on the Contoso University home page) to see the list with department names.</span></span>

![Courses_index_page_with_department_names](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image3.png)

## <a name="create-an-instructors-index-page-that-shows-courses-and-enrollments"></a><span data-ttu-id="a123a-179">과정 및 등록을 보여 주는 강사 인덱스 페이지 만들기</span><span class="sxs-lookup"><span data-stu-id="a123a-179">Create an Instructors Index Page That Shows Courses and Enrollments</span></span>

<span data-ttu-id="a123a-180">이 섹션에서는 가상 랩에서 컨트롤러를 만들고에 대 한 보기 된 `Instructor` 강사 인덱스 페이지를 표시 하기 위해 엔터티:</span><span class="sxs-lookup"><span data-stu-id="a123a-180">In this section you'll create a controller and view for the `Instructor` entity in order to display the Instructors Index page:</span></span>

![Instructors_index_page_with_instructor_and_course_selected](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image4.png)

<span data-ttu-id="a123a-182">이 페이지를 읽고 다음과 같이 관련된 데이터를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="a123a-182">This page reads and displays related data in the following ways:</span></span>

- <span data-ttu-id="a123a-183">강사 목록은의 관련된 데이터 표시는 `OfficeAssignment` 엔터티.</span><span class="sxs-lookup"><span data-stu-id="a123a-183">The list of instructors displays related data from the `OfficeAssignment` entity.</span></span> <span data-ttu-id="a123a-184">`Instructor` 및 `OfficeAssignment` 엔터티는 0 또는 1을 한 관계에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a123a-184">The `Instructor` and `OfficeAssignment` entities are in a one-to-zero-or-one relationship.</span></span> <span data-ttu-id="a123a-185">에 대 한 즉시 로드를 사용 하 여는 `OfficeAssignment` 엔터티.</span><span class="sxs-lookup"><span data-stu-id="a123a-185">You'll use eager loading for the `OfficeAssignment` entities.</span></span> <span data-ttu-id="a123a-186">이전에 설명한 대로 기본 테이블의 모든 검색 된 행에 관련된 데이터를 필요로 하는 경우 즉시 로드 일반적으로 더 효율적입니다.</span><span class="sxs-lookup"><span data-stu-id="a123a-186">As explained earlier, eager loading is typically more efficient when you need the related data for all retrieved rows of the primary table.</span></span> <span data-ttu-id="a123a-187">이 경우에 표시 된 모든 강사에 게 사무실 할당을 표시 하려면.</span><span class="sxs-lookup"><span data-stu-id="a123a-187">In this case, you want to display office assignments for all displayed instructors.</span></span>
- <span data-ttu-id="a123a-188">사용자가 관련 강사를 선택할 때 `Course` 엔터티 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a123a-188">When the user selects an instructor, related `Course` entities are displayed.</span></span> <span data-ttu-id="a123a-189">`Instructor` 및 `Course` 엔터티가 서로 다 대 다 관계에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a123a-189">The `Instructor` and `Course` entities are in a many-to-many relationship.</span></span> <span data-ttu-id="a123a-190">에 대 한 즉시 로드를 사용 하 여는 `Course` 엔터티 및 관련 `Department` 엔터티.</span><span class="sxs-lookup"><span data-stu-id="a123a-190">You'll use eager loading for the `Course` entities and their related `Department` entities.</span></span> <span data-ttu-id="a123a-191">이 경우 선택한 강사에 대해서만 courses 필요 하기 때문에 한 지연 로딩이 더 효율적일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a123a-191">In this case, lazy loading might be more efficient because you need courses only for the selected instructor.</span></span> <span data-ttu-id="a123a-192">그러나이 예제에는 자체 탐색 속성에 있는 엔터티 내에서 탐색 속성에 대 한 즉시 로드를 사용 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a123a-192">However, this example shows how to use eager loading for navigation properties within entities that are themselves in navigation properties.</span></span>
- <span data-ttu-id="a123a-193">관련 된 데이터를 사용자가 과정을 선택 하는 경우는 `Enrollments` 엔터티 집합이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a123a-193">When the user selects a course, related data from the `Enrollments` entity set is displayed.</span></span> <span data-ttu-id="a123a-194">`Course` 및 `Enrollment` 엔터티가 서로 일 대 다 관계에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a123a-194">The `Course` and `Enrollment` entities are in a one-to-many relationship.</span></span> <span data-ttu-id="a123a-195">명시적 로드에 대 한 추가 `Enrollment` 엔터티 및 관련 `Student` 엔터티.</span><span class="sxs-lookup"><span data-stu-id="a123a-195">You'll add explicit loading for `Enrollment` entities and their related `Student` entities.</span></span> <span data-ttu-id="a123a-196">(명시적 로딩 필요 하지 않습니다 지연 로드를 사용 하도록 설정 되었지만 명시적 로딩 작업을 수행 하는 방법을 보여 줍니다.)</span><span class="sxs-lookup"><span data-stu-id="a123a-196">(Explicit loading isn't necessary because lazy loading is enabled, but this shows how to do explicit loading.)</span></span>

### <a name="create-a-view-model-for-the-instructor-index-view"></a><span data-ttu-id="a123a-197">강사 인덱스 보기에 대 한 뷰 모델 만들기</span><span class="sxs-lookup"><span data-stu-id="a123a-197">Create a View Model for the Instructor Index View</span></span>

<span data-ttu-id="a123a-198">강사 인덱스 페이지에는 서로 다른 세 테이블 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a123a-198">The Instructor Index page shows three different tables.</span></span> <span data-ttu-id="a123a-199">따라서 각 테이블 중 하나에 대 한 데이터를 보유으로 세 가지 속성을 포함 하는 보기 모델을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a123a-199">Therefore, you'll create a view model that includes three properties, each holding the data for one of the tables.</span></span>

<span data-ttu-id="a123a-200">에 *Viewmodel* 폴더를 만들 *InstructorIndexData.cs* 기존 코드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="a123a-200">In the *ViewModels* folder, create *InstructorIndexData.cs* and replace the existing code with the following code:</span></span>

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cs)]

### <a name="adding-a-style-for-selected-rows"></a><span data-ttu-id="a123a-201">선택한 행에 대 한 스타일을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a123a-201">Adding a Style for Selected Rows</span></span>

<span data-ttu-id="a123a-202">선택 된 행을 표시 하려면 다른 배경색을 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a123a-202">To mark selected rows you need a different background color.</span></span> <span data-ttu-id="a123a-203">스타일이이 UI를 제공 하려면 다음 강조 표시 된 코드 섹션에 추가 `/* info and errors */` 에 *Content\Site.css*다음과 같이 합니다.</span><span class="sxs-lookup"><span data-stu-id="a123a-203">To provide a style for this UI, add the following highlighted code to the section `/* info and errors */` in *Content\Site.css*, as shown below:</span></span>

[!code-css[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.css?highlight=2-5)]

### <a name="creating-the-instructor-controller-and-views"></a><span data-ttu-id="a123a-204">강사 컨트롤러 및 뷰 만들기</span><span class="sxs-lookup"><span data-stu-id="a123a-204">Creating the Instructor Controller and Views</span></span>

<span data-ttu-id="a123a-205">만들기는 `InstructorController` 다음 그림에 나와 있는 것 처럼 컨트롤러:</span><span class="sxs-lookup"><span data-stu-id="a123a-205">Create an `InstructorController` controller as shown in the following illustration:</span></span>

![Add_Controller_dialog_box_for_Instructor_controller](https://asp.net/media/2577909/Windows-Live-Writer_Reading-Re.NET-MVC-Application-5-of-10h1_ADC3_Add_Controller_dialog_box_for_Instructor_controller_f99c10aa-1efd-49d6-af1d-b00461616107.png)

<span data-ttu-id="a123a-207">열기 *Controllers\InstructorController.cs* 추가 `using` 문에 `ViewModels` 네임 스페이스:</span><span class="sxs-lookup"><span data-stu-id="a123a-207">Open *Controllers\InstructorController.cs* and add a `using` statement for the `ViewModels` namespace:</span></span>

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample7.cs)]

<span data-ttu-id="a123a-208">스 캐 폴드 코드에는 `Index` 메서드 지정에 대해서만 즉시 로드는 `OfficeAssignment` 탐색 속성:</span><span class="sxs-lookup"><span data-stu-id="a123a-208">The scaffolded code in the `Index` method specifies eager loading only for the `OfficeAssignment` navigation property:</span></span>

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample8.cs)]

<span data-ttu-id="a123a-209">대체는 `Index` 메서드 추가 로드를 다음 코드로 관련 데이터의 보기 모델에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="a123a-209">Replace the `Index` method with the following code to load additional related data and put it in the view model:</span></span>

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample9.cs)]

<span data-ttu-id="a123a-210">메서드에 선택적 경로 데이터 (`id`) 및 쿼리 문자열 매개 변수 (`courseID`) 선택한 강사 및 선택한 과정의 ID 값을 제공 하 고 필요한 데이터의 모든 보기를 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="a123a-210">The method accepts optional route data (`id`) and a query string parameter (`courseID`) that provide the ID values of the selected instructor and selected course, and passes all of the required data to the view.</span></span> <span data-ttu-id="a123a-211">매개 변수에서 제공 되는 **선택** 페이지의 하이퍼링크입니다.</span><span class="sxs-lookup"><span data-stu-id="a123a-211">The parameters are provided by the **Select** hyperlinks on the page.</span></span>

> [!TIP] 
> 
> <span data-ttu-id="a123a-212">**경로 데이터**</span><span class="sxs-lookup"><span data-stu-id="a123a-212">**Route data**</span></span>
> 
> <span data-ttu-id="a123a-213">경로 데이터는 모델 바인더는 라우팅 테이블에 지정 된 URL 세그먼트에 있는 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="a123a-213">Route data is data that the model binder found in a URL segment specified in the routing table.</span></span> <span data-ttu-id="a123a-214">예를 들어 기본 경로가 지정 `controller`, `action`, 및 `id` 세그먼트:</span><span class="sxs-lookup"><span data-stu-id="a123a-214">For example, the default route specifies `controller`, `action`, and `id` segments:</span></span>
> 
> <span data-ttu-id="a123a-215">경로입니다. MapRoute 드 (</span><span class="sxs-lookup"><span data-stu-id="a123a-215">routes.MapRoute(</span></span>  
>  <span data-ttu-id="a123a-216">이름: "Default",</span><span class="sxs-lookup"><span data-stu-id="a123a-216">name: "Default",</span></span>  
>  <span data-ttu-id="a123a-217">url: "{controller} / {action} / {id}",</span><span class="sxs-lookup"><span data-stu-id="a123a-217">url: "{controller}/{action}/{id}",</span></span>  
>  <span data-ttu-id="a123a-218">기본값: new {컨트롤러 동작 = "Home", "Index" = id UrlParameter.Optional =}</span><span class="sxs-lookup"><span data-stu-id="a123a-218">defaults: new { controller = "Home", action = "Index", id = UrlParameter.Optional }</span></span>  
> <span data-ttu-id="a123a-219">);</span><span class="sxs-lookup"><span data-stu-id="a123a-219">);</span></span>
> 
> <span data-ttu-id="a123a-220">다음 URL에 기본 경로 매핑합니다 `Instructor` 로 `controller`, `Index` 로 `action` 1을 `id`; 이러한 속성은 경로 데이터 값입니다.</span><span class="sxs-lookup"><span data-stu-id="a123a-220">In the following URL, the default route maps `Instructor` as the `controller`, `Index` as the `action` and 1 as the `id`; these are route data values.</span></span>
> 
> `http://localhost:1230/Instructor/Index/1?courseID=2021`
> 
> <span data-ttu-id="a123a-221">"? courseID 2021 =" 쿼리 문자열 값입니다.</span><span class="sxs-lookup"><span data-stu-id="a123a-221">"?courseID=2021" is a query string value.</span></span> <span data-ttu-id="a123a-222">전달 하는 경우에 모델 바인더 작동할지는 `id` 쿼리 문자열 값으로.</span><span class="sxs-lookup"><span data-stu-id="a123a-222">The model binder will also work if you pass the `id` as a query string value:</span></span>
> 
> `http://localhost:1230/Instructor/Index?id=1&CourseID=2021`
> 
> <span data-ttu-id="a123a-223">Url에 의해 만들어집니다 `ActionLink` Razor 보기에는 문입니다.</span><span class="sxs-lookup"><span data-stu-id="a123a-223">The URLs are created by `ActionLink` statements in the Razor view.</span></span> <span data-ttu-id="a123a-224">다음 코드에서는 `id` 매개 변수 이므로 기본 경로 일치 `id` 경로 데이터에 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a123a-224">In the following code, the `id` parameter matches the default route, so `id` is added to the route data.</span></span>
> 
> [!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample10.cshtml)]
> 
> <span data-ttu-id="a123a-225">다음 코드에서 `courseID` 쿼리 문자열로 추가 기본 경로에 매개 변수가 일치 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a123a-225">In the following code, `courseID` doesn't match a parameter in the default route, so it's added as a query string.</span></span>
> 
> [!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample11.cshtml)]


<span data-ttu-id="a123a-226">코드의 보기 모델의 인스턴스를 만들고 강사 목록에 배치 하 여 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="a123a-226">The code begins by creating an instance of the view model and putting in it the list of instructors.</span></span> <span data-ttu-id="a123a-227">에 대 한 즉시 로드를 지정 하는 코드는 `Instructor.OfficeAssignment` 및 `Instructor.Courses` 탐색 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="a123a-227">The code specifies eager loading for the `Instructor.OfficeAssignment` and the `Instructor.Courses` navigation property.</span></span>

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample12.cs?highlight=3-4)]

<span data-ttu-id="a123a-228">두 번째 `Include` 메서드 과정을를 로드 하 고 로드 된 각 과정에 대 한에 적용 되는 즉시 로드는 `Course.Department` 탐색 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="a123a-228">The second `Include` method loads Courses, and for each Course that is loaded it does eager loading for the `Course.Department` navigation property.</span></span>

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample13.cs)]

<span data-ttu-id="a123a-229">앞에서 설명한 대로 즉시 로드는 필요 하지 않지만 성능을 향상 시키기 위해서입니다.</span><span class="sxs-lookup"><span data-stu-id="a123a-229">As mentioned previously, eager loading is not required but is done to improve performance.</span></span> <span data-ttu-id="a123a-230">보기 항상 필요 하므로 `OfficeAssignment` 엔터티에 것이 더 효율적을 같은 쿼리에서 인출 합니다.</span><span class="sxs-lookup"><span data-stu-id="a123a-230">Since the view always requires the `OfficeAssignment` entity, it's more efficient to fetch that in the same query.</span></span> <span data-ttu-id="a123a-231">`Course`엔터티는 즉시 로드 하지 않고 보다 선택 하는 과정에 페이지를 더 자주 표시할 경우에 지연 로드 보다 더 나은 이므로 웹 페이지에서 강사를 선택한 경우에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="a123a-231">`Course` entities are required when an instructor is selected in the web page, so eager loading is better than lazy loading only if the page is displayed more often with a course selected than without.</span></span>

<span data-ttu-id="a123a-232">강사 ID를 선택한 경우 선택한 강사 강사 보기 모델에 있는 목록에서 검색 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a123a-232">If an instructor ID was selected, the selected instructor is retrieved from the list of instructors in the view model.</span></span> <span data-ttu-id="a123a-233">뷰 모델 `Courses` 속성으로 로드는 `Course` 해당 강사에서 엔터티에 `Courses` 탐색 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="a123a-233">The view model's `Courses` property is then loaded with the `Course` entities from that instructor's `Courses` navigation property.</span></span>

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample14.cs)]

<span data-ttu-id="a123a-234">`Where` 메서드 컬렉션을 반환 하지만 조건 하나만에서 해당 메서드 결과에 전달 되는 경우 `Instructor` 엔터티를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="a123a-234">The `Where` method returns a collection, but in this case the criteria passed to that method result in only a single `Instructor` entity being returned.</span></span> <span data-ttu-id="a123a-235">`Single` 메서드 컬렉션을 단일 `Instructor` 해당 엔터티에 액세스할 수 있는 엔터티 `Courses` 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="a123a-235">The `Single` method converts the collection into a single `Instructor` entity, which gives you access to that entity's `Courses` property.</span></span>

<span data-ttu-id="a123a-236">사용 된 [단일](https://msdn.microsoft.com/en-us/library/system.linq.enumerable.single.aspx) 메서드 컬렉션을 알고 있는 경우 컬렉션에 항목을 하나만 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="a123a-236">You use the [Single](https://msdn.microsoft.com/en-us/library/system.linq.enumerable.single.aspx) method on a collection when you know the collection will have only one item.</span></span> <span data-ttu-id="a123a-237">`Single` 메서드는 전달 된 컬렉션은 비어 있거나 둘 이상의 항목이 없는 경우 예외를 throw 합니다.</span><span class="sxs-lookup"><span data-stu-id="a123a-237">The `Single` method throws an exception if the collection passed to it is empty or if there's more than one item.</span></span> <span data-ttu-id="a123a-238">대신 [SingleOrDefault](https://msdn.microsoft.com/en-us/library/bb342451.aspx), 기본 값을 반환 하 (`null` 이 예제의) 컬렉션이 비어 있는 경우.</span><span class="sxs-lookup"><span data-stu-id="a123a-238">An alternative is [SingleOrDefault](https://msdn.microsoft.com/en-us/library/bb342451.aspx), which returns a default value (`null` in this case) if the collection is empty.</span></span> <span data-ttu-id="a123a-239">그러나이 경우에 여전히 초래 예외 (찾으려고 시도에서 `Courses` 속성에는 `null` 참조), 예외 메시지는 문제의 원인을 477860 덜 명확 하 게 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a123a-239">However, in this case that would still result in an exception (from trying to find a `Courses` property on a `null` reference), and the exception message would less clearly indicate the cause of the problem.</span></span> <span data-ttu-id="a123a-240">호출 하는 경우는 `Single` 메서드를 전달할 수도 있습니다에 `Where` 조건을 호출 하는 대신는 `Where` 메서드 별도로:</span><span class="sxs-lookup"><span data-stu-id="a123a-240">When you call the `Single` method, you can also pass in the `Where` condition instead of calling the `Where` method separately:</span></span>

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample15.cs)]

<span data-ttu-id="a123a-241">위 코드를 아래 코드 대신 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a123a-241">Instead of:</span></span>

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample16.cs)]

<span data-ttu-id="a123a-242">다음으로 과정을 선택한 경우 선택한 과정의 보기 모델에는 과정의 목록에서 검색 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a123a-242">Next, if a course was selected, the selected course is retrieved from the list of courses in the view model.</span></span> <span data-ttu-id="a123a-243">다음 뷰 모델의 `Enrollments` 속성으로 로드 되는 `Enrollment` 해당 과정에서 엔터티 `Enrollments` 탐색 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="a123a-243">Then the view model's `Enrollments` property is loaded with the `Enrollment` entities from that course's `Enrollments` navigation property.</span></span>

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample17.cs)]

### <a name="modifying-the-instructor-index-view"></a><span data-ttu-id="a123a-244">강사 인덱스 뷰를 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="a123a-244">Modifying the Instructor Index View</span></span>

<span data-ttu-id="a123a-245">*Views\Instructor\Index.cshtml*, 기존 코드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="a123a-245">In *Views\Instructor\Index.cshtml*, replace the existing code with the following code.</span></span> <span data-ttu-id="a123a-246">변경 내용은 강조 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a123a-246">The changes are highlighted:</span></span>

[!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample18.cshtml?highlight=1,4,18,22-27,29,43-48)]

<span data-ttu-id="a123a-247">기존 코드를 다음과 같이 변경을 했습니다.</span><span class="sxs-lookup"><span data-stu-id="a123a-247">You've made the following changes to the existing code:</span></span>

- <span data-ttu-id="a123a-248">모델 클래스를 변경 `InstructorIndexData`합니다.</span><span class="sxs-lookup"><span data-stu-id="a123a-248">Changed the model class to `InstructorIndexData`.</span></span>
- <span data-ttu-id="a123a-249">페이지 제목을 변경 **인덱스** 를 **강사**합니다.</span><span class="sxs-lookup"><span data-stu-id="a123a-249">Changed the page title from **Index** to **Instructors**.</span></span>
- <span data-ttu-id="a123a-250">행 링크 열 왼쪽으로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="a123a-250">Moved the row link columns to the left.</span></span>
- <span data-ttu-id="a123a-251">제거는 **FullName** 열입니다.</span><span class="sxs-lookup"><span data-stu-id="a123a-251">Removed the **FullName** column.</span></span>
- <span data-ttu-id="a123a-252">추가 **Office** 표시 하는 열 `item.OfficeAssignment.Location` 경우에만 `item.OfficeAssignment` null입니다.</span><span class="sxs-lookup"><span data-stu-id="a123a-252">Added an **Office** column that displays `item.OfficeAssignment.Location` only if `item.OfficeAssignment` is not null.</span></span> <span data-ttu-id="a123a-253">(0 또는 1을 한 관계 이므로 수 없는 경우 관련 `OfficeAssignment` 엔터티.)</span><span class="sxs-lookup"><span data-stu-id="a123a-253">(Because this is a one-to-zero-or-one relationship, there might not be a related `OfficeAssignment` entity.)</span></span> 

    [!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample19.cshtml)]
- <span data-ttu-id="a123a-254">추가 된 코드를 동적으로 추가 됩니다 `class="selectedrow"` 에 `tr` 선택한 강사의 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="a123a-254">Added code that will dynamically add `class="selectedrow"` to the `tr` element of the selected instructor.</span></span> <span data-ttu-id="a123a-255">앞에서 만든는 CSS 클래스를 사용 하 여 선택된 된 행에 대 한 배경색을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a123a-255">This sets a background color for the selected row using the CSS class that you created earlier.</span></span> <span data-ttu-id="a123a-256">(의 `valign` 다중 행 열 테이블을 추가할 때 특성 다음 자습서에 도움이 됩니다.)</span><span class="sxs-lookup"><span data-stu-id="a123a-256">(The `valign` attribute will be useful in the following tutorial when you add a multi-row column to the table.)</span></span> 

    [!code-html[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample20.html)]
- <span data-ttu-id="a123a-257">새 추가 `ActionLink` 레이블이 **선택** 를 보내도록 선택한 강사 ID 때문에 있는 다른 각 행에 링크 바로 앞의 `Index` 메서드.</span><span class="sxs-lookup"><span data-stu-id="a123a-257">Added a new `ActionLink` labeled **Select** immediately before the other links in each row, which causes the selected instructor ID to be sent to the `Index` method.</span></span>

<span data-ttu-id="a123a-258">응용 프로그램을 실행 하 고 선택 된 **강사** 탭 합니다. 페이지에 표시 됩니다는 `Location` 속성 관련된 `OfficeAssignment` 엔터티 및 빈 테이블 셀이 있으면 관련 no `OfficeAssignment` 엔터티.</span><span class="sxs-lookup"><span data-stu-id="a123a-258">Run the application and select the **Instructors** tab. The page displays the `Location` property of related `OfficeAssignment` entities and an empty table cell when there's no related `OfficeAssignment` entity.</span></span>

![Instructors_index_page_with_nothing_selected](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image5.png)

<span data-ttu-id="a123a-260">에 *Views\Instructor\Index.cshtml* 파일을 닫은 후 `table` (끝에 요소 파일의), 다음 강조 표시 된 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="a123a-260">In the *Views\Instructor\Index.cshtml* file, after the closing `table` element (at the end of the file), add the following highlighted code.</span></span> <span data-ttu-id="a123a-261">그러면 courses 강사 강사 선택 된 경우와 관련 된 목록이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a123a-261">This displays a list of courses related to an instructor when an instructor is selected.</span></span>

[!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample21.cshtml?highlight=11-46)]

<span data-ttu-id="a123a-262">이 코드를 읽고는 `Courses` 과정의 목록을 표시 하려면 보기 모델의 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="a123a-262">This code reads the `Courses` property of the view model to display a list of courses.</span></span> <span data-ttu-id="a123a-263">또한 제공는 `Select` 하이퍼링크에 선택한 과정의 ID를 전송 하는 `Index` 동작 메서드.</span><span class="sxs-lookup"><span data-stu-id="a123a-263">It also provides a `Select` hyperlink that sends the ID of the selected course to the `Index` action method.</span></span>

> [!NOTE]
> <span data-ttu-id="a123a-264">*.css* 파일은 브라우저에서 캐시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a123a-264">The *.css* file is cached by browsers.</span></span> <span data-ttu-id="a123a-265">응용 프로그램을 실행 하는 경우 변경 내용이 표시 되지 않으면, 하드 새로 고침을 수행 (CTRL 키를 누른 채 클릭 하 고 **새로 고침** CTRL + f 5를 누르거나 단추).</span><span class="sxs-lookup"><span data-stu-id="a123a-265">If you don't see the changes when you run the application, do a hard refresh (hold down the CTRL key while clicking the **Refresh** button, or press CTRL+F5).</span></span>


<span data-ttu-id="a123a-266">페이지를 실행 하 고 강사를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="a123a-266">Run the page and select an instructor.</span></span> <span data-ttu-id="a123a-267">이제 선택한 강사에 할당 하는 과정을 표시 하는 표를 표시 및 각 과정에 대 한 할당 된 부서 이름을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="a123a-267">Now you see a grid that displays courses assigned to the selected instructor, and for each course you see the name of the assigned department.</span></span>

![Instructors_index_page_with_instructor_selected](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image6.png)

<span data-ttu-id="a123a-269">방금 추가한 코드 블록을 한 후 다음 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="a123a-269">After the code block you just added, add the following code.</span></span> <span data-ttu-id="a123a-270">해당 과정을 선택한 경우에 과정에서 등록 된 학생의 목록을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="a123a-270">This displays a list of the students who are enrolled in a course when that course is selected.</span></span>

[!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample22.cshtml)]

<span data-ttu-id="a123a-271">이 코드를 읽고는 `Enrollments` 과정에 학생의 목록을 표시 하려면 보기 모델의 속성 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="a123a-271">This code reads the `Enrollments` property of the view model in order to display a list of students enrolled in the course.</span></span>

<span data-ttu-id="a123a-272">페이지를 실행 하 고 강사를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="a123a-272">Run the page and select an instructor.</span></span> <span data-ttu-id="a123a-273">그런 다음 등록 된 학생 자신의 등급의 목록을 보려면 과정을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="a123a-273">Then select a course to see the list of enrolled students and their grades.</span></span>

![Instructors_index_page_with_instructor_and_course_selected](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image7.png)

### <a name="adding-explicit-loading"></a><span data-ttu-id="a123a-275">명시적 로드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a123a-275">Adding Explicit Loading</span></span>

<span data-ttu-id="a123a-276">열기 *InstructorController.cs* 방법을 확인 하 고 `Index` 메서드 선택한 과정에 대 한 등록의 목록을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="a123a-276">Open *InstructorController.cs* and look at how the `Index` method gets the list of enrollments for a selected course:</span></span>

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample23.cs)]

<span data-ttu-id="a123a-277">즉시 로드에 대 한 지정한 강사 목록을 검색 하는 경우는 `Courses` 탐색 속성 및에 대 한는 `Department` 각 과정의 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="a123a-277">When you retrieved the list of instructors, you specified eager loading for the `Courses` navigation property and for the `Department` property of each course.</span></span> <span data-ttu-id="a123a-278">배치 하는 다음의 `Courses` 고 컬렉션의 보기 모델에 액세스 하는 이제는 `Enrollments` 해당 컬렉션의 엔터티 간에 탐색 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="a123a-278">Then you put the `Courses` collection in the view model, and now you're accessing the `Enrollments` navigation property from one entity in that collection.</span></span> <span data-ttu-id="a123a-279">에 대 한 즉시 로드를 지정 하지 않은 때문에 `Course.Enrollments` 지연 로드의 결과로 페이지에서 해당 속성의 데이터가 나타나는지 탐색 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="a123a-279">Because you didn't specify eager loading for the `Course.Enrollments` navigation property, the data from that property is appearing in the page as a result of lazy loading.</span></span>

<span data-ttu-id="a123a-280">다른 방법으로 코드를 변경 하지 않고 지연 로드를 사용 하지 않도록 설정한 경우는 `Enrollments` 속성 개수 등록 과정 되었습니다에 관계 없이 null이 될 것입니다.</span><span class="sxs-lookup"><span data-stu-id="a123a-280">If you disabled lazy loading without changing the code in any other way, the `Enrollments` property would be null regardless of how many enrollments the course actually had.</span></span> <span data-ttu-id="a123a-281">로드할 경우에서는 `Enrollments` 속성을 즉시 로드 또는 명시적 로드 중 하나를 지정 해야 할 것 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a123a-281">In that case, to load the `Enrollments` property, you'd have to specify either eager loading or explicit loading.</span></span> <span data-ttu-id="a123a-282">즉시 로드를 수행 하는 방법을 이미 살펴보았습니다.</span><span class="sxs-lookup"><span data-stu-id="a123a-282">You've already seen how to do eager loading.</span></span> <span data-ttu-id="a123a-283">명시적 로드의 예를 보려면 대체는 `Index` 메서드를 명시적으로 로드 하는 다음 코드는 `Enrollments` 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="a123a-283">In order to see an example of explicit loading, replace the `Index` method with the following code, which explicitly loads the `Enrollments` property.</span></span> <span data-ttu-id="a123a-284">변경 된 코드를 강조 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a123a-284">The code changed are highlighted.</span></span>

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample24.cs?highlight=20-27)]

<span data-ttu-id="a123a-285">선택한 받은 후 `Course` 엔터티를 새 코드는 해당 과정을 명시적으로 로드 `Enrollments` 탐색 속성:</span><span class="sxs-lookup"><span data-stu-id="a123a-285">After getting the selected `Course` entity, the new code explicitly loads that course's `Enrollments` navigation property:</span></span>

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample25.cs)]

<span data-ttu-id="a123a-286">명시적으로 각 로드 후 `Enrollment` 엔터티의 관련 `Student` 엔터티:</span><span class="sxs-lookup"><span data-stu-id="a123a-286">Then it explicitly loads each `Enrollment` entity's related `Student` entity:</span></span>

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample26.cs)]

<span data-ttu-id="a123a-287">공지를 사용 하는 `Collection` 개체 컬렉션 속성에 대 한 하나의 엔터티를 포함 하는 속성을 사용 하 여 있습니다 하지만 `Reference` 메서드.</span><span class="sxs-lookup"><span data-stu-id="a123a-287">Notice that you use the `Collection` method to load a collection property, but for a property that holds just one entity, you use the `Reference` method.</span></span> <span data-ttu-id="a123a-288">이제 강사 인덱스 페이지를 실행할 수 있습니다를 한 데이터를 검색 하는 방법을 변경 하지만 페이지에 표시 되는 내용에 차이가 없어야을 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="a123a-288">You can run the Instructor Index page now and you'll see no difference in what's displayed on the page, although you've changed how the data is retrieved.</span></span>

## <a name="summary"></a><span data-ttu-id="a123a-289">요약</span><span class="sxs-lookup"><span data-stu-id="a123a-289">Summary</span></span>

<span data-ttu-id="a123a-290">이제 모든 세 가지 방법으로 (지연, 신속 하 게, 및 명시적) 탐색 속성에 관련된 데이터를 로드를 사용 했습니다.</span><span class="sxs-lookup"><span data-stu-id="a123a-290">You've now used all three ways (lazy, eager, and explicit) to load related data into navigation properties.</span></span> <span data-ttu-id="a123a-291">다음 자습서에서 관련된 데이터를 업데이트 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="a123a-291">In the next tutorial you'll learn how to update related data.</span></span>

<span data-ttu-id="a123a-292">다른 Entity Framework 리소스에 대 한 링크에서 확인할 수 있습니다는 [ASP.NET 데이터 액세스 콘텐츠 맵](../../../../whitepapers/aspnet-data-access-content-map.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="a123a-292">Links to other Entity Framework resources can be found in the [ASP.NET Data Access Content Map](../../../../whitepapers/aspnet-data-access-content-map.md).</span></span>

>[!div class="step-by-step"]
<span data-ttu-id="a123a-293">[이전](creating-a-more-complex-data-model-for-an-asp-net-mvc-application.md)
[다음](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md)</span><span class="sxs-lookup"><span data-stu-id="a123a-293">[Previous](creating-a-more-complex-data-model-for-an-asp-net-mvc-application.md)
[Next](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md)</span></span>