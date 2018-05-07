---
title: ASP.NET Core에서 Web API 빌드
author: scottaddie
description: ASP.NET Core에서 Web API를 빌드하는 데 사용할 수 있는 기능과 각 기능을 사용하기에 적합한 시기에 대해 알아봅니다.
manager: wpickett
ms.author: scaddie
ms.custom: mvc
ms.date: 04/24/2018
ms.prod: aspnet-core
ms.technology: aspnet
ms.topic: article
uid: web-api/index
ms.openlocfilehash: f0368258d078673ab5eab21c5ce07f2437cb8ea4
ms.sourcegitcommit: 5130b3034165f5cf49d829fe7475a84aa33d2693
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="build-web-apis-with-aspnet-core"></a><span data-ttu-id="59a4a-103">ASP.NET Core에서 Web API 빌드</span><span class="sxs-lookup"><span data-stu-id="59a4a-103">Build web APIs with ASP.NET Core</span></span>

<span data-ttu-id="59a4a-104">작성자: [Scott Addie](https://github.com/scottaddie)</span><span class="sxs-lookup"><span data-stu-id="59a4a-104">By [Scott Addie](https://github.com/scottaddie)</span></span>

<span data-ttu-id="59a4a-105">[예제 코드 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/web-api/define-controller/samples)([다운로드 방법](xref:tutorials/index#how-to-download-a-sample))</span><span class="sxs-lookup"><span data-stu-id="59a4a-105">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/web-api/define-controller/samples) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>

<span data-ttu-id="59a4a-106">이 문서에서는 ASP.NET Core에서 Web API를 빌드하는 방법과 각 기능을 사용하기에 가장 적합한 시기에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="59a4a-106">This document explains how to build a web API in ASP.NET Core and when it's most appropriate to use each feature.</span></span>

## <a name="derive-class-from-controllerbase"></a><span data-ttu-id="59a4a-107">ControllerBase에서 클래스 파생</span><span class="sxs-lookup"><span data-stu-id="59a4a-107">Derive class from ControllerBase</span></span>

<span data-ttu-id="59a4a-108">Web API를 제공할 목적으로 컨트롤의 [ControllerBase](/dotnet/api/microsoft.aspnetcore.mvc.controllerbase) 클래스에서 상속합니다.</span><span class="sxs-lookup"><span data-stu-id="59a4a-108">Inherit from the [ControllerBase](/dotnet/api/microsoft.aspnetcore.mvc.controllerbase) class in a controller that's intended to serve as a web API.</span></span> <span data-ttu-id="59a4a-109">예:</span><span class="sxs-lookup"><span data-stu-id="59a4a-109">For example:</span></span>

::: moniker range=">= aspnetcore-2.1"
<span data-ttu-id="59a4a-110">[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api/Controllers/PetsController.cs?name=snippet_PetsController&highlight=3)]</span><span class="sxs-lookup"><span data-stu-id="59a4a-110">[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api/Controllers/PetsController.cs?name=snippet_PetsController&highlight=3)]</span></span>
::: moniker-end
::: moniker range="<= aspnetcore-2.0"
<span data-ttu-id="59a4a-111">[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api.Pre21/Controllers/PetsController.cs?name=snippet_PetsController&highlight=3)]</span><span class="sxs-lookup"><span data-stu-id="59a4a-111">[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api.Pre21/Controllers/PetsController.cs?name=snippet_PetsController&highlight=3)]</span></span>
::: moniker-end

<span data-ttu-id="59a4a-112">`ControllerBase` 클래스는 다양한 속성 및 메서드에 대한 액세스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="59a4a-112">The `ControllerBase` class provides access to numerous properties and methods.</span></span> <span data-ttu-id="59a4a-113">앞의 예제에서는 이러한 메서드에 [BadRequest](/dotnet/api/microsoft.aspnetcore.mvc.controllerbase.badrequest) 및 [CreatedAtAction](/dotnet/api/microsoft.aspnetcore.mvc.controllerbase.createdataction)이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="59a4a-113">In the preceding example, some such methods include [BadRequest](/dotnet/api/microsoft.aspnetcore.mvc.controllerbase.badrequest) and [CreatedAtAction](/dotnet/api/microsoft.aspnetcore.mvc.controllerbase.createdataction).</span></span> <span data-ttu-id="59a4a-114">이러한 메서드는 각각 HTTP 400와 201 상태 코드를 반환하는 작업 메서드 내에서 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="59a4a-114">These methods are invoked within action methods to return HTTP 400 and 201 status codes, respectively.</span></span> <span data-ttu-id="59a4a-115">요청 모델 유효성 검사를 수행하기 위해 `ControllerBase`에 의해서도 제공된 [ModelState](/dotnet/api/microsoft.aspnetcore.mvc.controllerbase.modelstate) 속성에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="59a4a-115">The [ModelState](/dotnet/api/microsoft.aspnetcore.mvc.controllerbase.modelstate) property, also provided by `ControllerBase`, is accessed to perform request model validation.</span></span>

::: moniker range=">= aspnetcore-2.1"
## <a name="annotate-class-with-apicontrollerattribute"></a><span data-ttu-id="59a4a-116">ApiControllerAttribute로 클래스에 주석 달기</span><span class="sxs-lookup"><span data-stu-id="59a4a-116">Annotate class with ApiControllerAttribute</span></span>

<span data-ttu-id="59a4a-117">ASP.NET Core 2.1에서는 Web API 컨트롤러 클래스를 나타내는 `[ApiController]` 특성을 소개합니다.</span><span class="sxs-lookup"><span data-stu-id="59a4a-117">ASP.NET Core 2.1 introduces the `[ApiController]` attribute to denote a web API controller class.</span></span> <span data-ttu-id="59a4a-118">예:</span><span class="sxs-lookup"><span data-stu-id="59a4a-118">For example:</span></span>

<span data-ttu-id="59a4a-119">[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api/Controllers/ProductsController.cs?name=snippet_ControllerSignature&highlight=2)]</span><span class="sxs-lookup"><span data-stu-id="59a4a-119">[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api/Controllers/ProductsController.cs?name=snippet_ControllerSignature&highlight=2)]</span></span>

<span data-ttu-id="59a4a-120">이 특성은 일반적으로 유용한 메서드 및 특성에 대한 액세스 권한을 얻기 위해 `ControllerBase`와 결합됩니다.</span><span class="sxs-lookup"><span data-stu-id="59a4a-120">This attribute is commonly coupled with `ControllerBase` to gain access to useful methods and properties.</span></span> <span data-ttu-id="59a4a-121">`ControllerBase`는 [NotFound](/dotnet/api/microsoft.aspnetcore.mvc.controllerbase.notfound) 및 [File](/dotnet/api/microsoft.aspnetcore.mvc.controllerbase.file)과 같은 메서드에 대한 액세스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="59a4a-121">`ControllerBase` provides access to methods such as [NotFound](/dotnet/api/microsoft.aspnetcore.mvc.controllerbase.notfound) and [File](/dotnet/api/microsoft.aspnetcore.mvc.controllerbase.file).</span></span>

<span data-ttu-id="59a4a-122">다른 방법은 `[ApiController]` 특성으로 주석 지정된 사용자 지정 기본 컨트롤러 클래스를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="59a4a-122">Another approach is to create a custom base controller class annotated with the `[ApiController]` attribute:</span></span>

<span data-ttu-id="59a4a-123">[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api/Controllers/MyBaseController.cs?name=snippet_ControllerSignature)]</span><span class="sxs-lookup"><span data-stu-id="59a4a-123">[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api/Controllers/MyBaseController.cs?name=snippet_ControllerSignature)]</span></span>

<span data-ttu-id="59a4a-124">다음 섹션에서는 특성으로 추가된 편리한 기능을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="59a4a-124">The following sections describe convenience features added by the attribute.</span></span>

### <a name="automatic-http-400-responses"></a><span data-ttu-id="59a4a-125">자동 HTTP 400 응답</span><span class="sxs-lookup"><span data-stu-id="59a4a-125">Automatic HTTP 400 responses</span></span>

<span data-ttu-id="59a4a-126">유효성 검사 오류 시 HTTP 400 응답이 자동으로 트리거됩니다.</span><span class="sxs-lookup"><span data-stu-id="59a4a-126">Validation errors automatically trigger an HTTP 400 response.</span></span> <span data-ttu-id="59a4a-127">다음 코드는 실제 작업 시 불필요하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="59a4a-127">The following code becomes unnecessary in your actions:</span></span>

<span data-ttu-id="59a4a-128">[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api.Pre21/Controllers/PetsController.cs?range=46-49)]</span><span class="sxs-lookup"><span data-stu-id="59a4a-128">[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api.Pre21/Controllers/PetsController.cs?range=46-49)]</span></span>

<span data-ttu-id="59a4a-129">이 기본 동작은 *Startup.ConfigureServices*에서 다음 코드와 함께 사용하지 않도록 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="59a4a-129">This default behavior is disabled with the following code in *Startup.ConfigureServices*:</span></span>

<span data-ttu-id="59a4a-130">[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api/Startup.cs?name=snippet_ConfigureApiBehaviorOptions&highlight=5)]</span><span class="sxs-lookup"><span data-stu-id="59a4a-130">[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api/Startup.cs?name=snippet_ConfigureApiBehaviorOptions&highlight=5)]</span></span>

### <a name="binding-source-parameter-inference"></a><span data-ttu-id="59a4a-131">바인딩 소스 매개 변수 유추</span><span class="sxs-lookup"><span data-stu-id="59a4a-131">Binding source parameter inference</span></span>

<span data-ttu-id="59a4a-132">바인딩 소스 특성은 작업 매개 변수 값이 발견되는 위치를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="59a4a-132">A binding source attribute defines the location at which an action parameter's value is found.</span></span> <span data-ttu-id="59a4a-133">다음 바인딩 소스 특성이 존재합니다.</span><span class="sxs-lookup"><span data-stu-id="59a4a-133">The following binding source attributes exist:</span></span>

|<span data-ttu-id="59a4a-134">특성</span><span class="sxs-lookup"><span data-stu-id="59a4a-134">Attribute</span></span>|<span data-ttu-id="59a4a-135">바인딩 원본</span><span class="sxs-lookup"><span data-stu-id="59a4a-135">Binding source</span></span> |
|---------|---------|
|<span data-ttu-id="59a4a-136">**[[FromBody]](/dotnet/api/microsoft.aspnetcore.mvc.frombodyattribute)**</span><span class="sxs-lookup"><span data-stu-id="59a4a-136">**[[FromBody]](/dotnet/api/microsoft.aspnetcore.mvc.frombodyattribute)**</span></span>     | <span data-ttu-id="59a4a-137">요청 본문</span><span class="sxs-lookup"><span data-stu-id="59a4a-137">Request body</span></span> |
|<span data-ttu-id="59a4a-138">**[[FromForm]](/dotnet/api/microsoft.aspnetcore.mvc.fromformattribute)**</span><span class="sxs-lookup"><span data-stu-id="59a4a-138">**[[FromForm]](/dotnet/api/microsoft.aspnetcore.mvc.fromformattribute)**</span></span>     | <span data-ttu-id="59a4a-139">요청 본문에서 양식 데이터</span><span class="sxs-lookup"><span data-stu-id="59a4a-139">Form data in the request body</span></span> |
|<span data-ttu-id="59a4a-140">**[[FromHeader]](/dotnet/api/microsoft.aspnetcore.mvc.fromheaderattribute)**</span><span class="sxs-lookup"><span data-stu-id="59a4a-140">**[[FromHeader]](/dotnet/api/microsoft.aspnetcore.mvc.fromheaderattribute)**</span></span> | <span data-ttu-id="59a4a-141">요청 헤더</span><span class="sxs-lookup"><span data-stu-id="59a4a-141">Request header</span></span> |
|<span data-ttu-id="59a4a-142">**[[FromQuery]](/dotnet/api/microsoft.aspnetcore.mvc.fromqueryattribute)**</span><span class="sxs-lookup"><span data-stu-id="59a4a-142">**[[FromQuery]](/dotnet/api/microsoft.aspnetcore.mvc.fromqueryattribute)**</span></span>   | <span data-ttu-id="59a4a-143">요청 쿼리 문자열 매개 변수</span><span class="sxs-lookup"><span data-stu-id="59a4a-143">Request query string parameter</span></span> |
|<span data-ttu-id="59a4a-144">**[[FromRoute]](/dotnet/api/microsoft.aspnetcore.mvc.fromrouteattribute)**</span><span class="sxs-lookup"><span data-stu-id="59a4a-144">**[[FromRoute]](/dotnet/api/microsoft.aspnetcore.mvc.fromrouteattribute)**</span></span>   | <span data-ttu-id="59a4a-145">현재 요청의 경로 데이터</span><span class="sxs-lookup"><span data-stu-id="59a4a-145">Route data from the current request</span></span> |
|<span data-ttu-id="59a4a-146">**[[FromServices]](xref:mvc/controllers/dependency-injection#action-injection-with-fromservices)**</span><span class="sxs-lookup"><span data-stu-id="59a4a-146">**[[FromServices]](xref:mvc/controllers/dependency-injection#action-injection-with-fromservices)**</span></span> | <span data-ttu-id="59a4a-147">작업 매개 변수로 삽입된 요청 서비스</span><span class="sxs-lookup"><span data-stu-id="59a4a-147">The request service injected as an action parameter</span></span> |

> [!NOTE]
> <span data-ttu-id="59a4a-148">`%2f`는 `/`에 대해 이스케이프되지 않으므로 값에 `%2f`(즉, `/`)가 포함될 가능성이 있으면 `[FromRoute]`를 사용하지 **마세요**.</span><span class="sxs-lookup"><span data-stu-id="59a4a-148">Do **not** use `[FromRoute]` when values might contain `%2f` (that is `/`) because `%2f` won't be unescaped to `/`.</span></span> <span data-ttu-id="59a4a-149">값에 `%2f`가 포함될 수 있으면 `[FromQuery]`를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="59a4a-149">Use `[FromQuery]` if the value might contain `%2f`.</span></span>

<span data-ttu-id="59a4a-150">`[ApiController]` 특성 없이, 바인딩 소스 특성이 명시적으로 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="59a4a-150">Without the `[ApiController]` attribute, binding source attributes are explicitly defined.</span></span> <span data-ttu-id="59a4a-151">다음 예제에서 `[FromQuery]` 특성은 `discontinuedOnly` 매개 변수 값이 요청 URL의 쿼리 문자열에 제공됨을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="59a4a-151">In the following example, the `[FromQuery]` attribute indicates that the `discontinuedOnly` parameter value is provided in the request URL's query string:</span></span>

<span data-ttu-id="59a4a-152">[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api/Controllers/ProductsController.cs?name=snippet_BindingSourceAttributes&highlight=2)]</span><span class="sxs-lookup"><span data-stu-id="59a4a-152">[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api/Controllers/ProductsController.cs?name=snippet_BindingSourceAttributes&highlight=2)]</span></span>

<span data-ttu-id="59a4a-153">유추 규칙이 작업 매개 변수의 기본 데이터 원본에 대해 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="59a4a-153">Inference rules are applied for the default data sources of action parameters.</span></span> <span data-ttu-id="59a4a-154">이러한 규칙은 작업 매개 변수에 달리 수동으로 적용할 가능성이 높은 바인딩 소스를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="59a4a-154">These rules configure the binding sources you're otherwise likely to manually apply to the action parameters.</span></span> <span data-ttu-id="59a4a-155">바인딩 소스 특성은 다음과 같이 동작합니다.</span><span class="sxs-lookup"><span data-stu-id="59a4a-155">The binding source attributes behave as follows:</span></span>

* <span data-ttu-id="59a4a-156">**[FromBody]** 는 복합 형식 매개 변수에 대해 유추됩니다.</span><span class="sxs-lookup"><span data-stu-id="59a4a-156">**[FromBody]** is inferred for complex type parameters.</span></span> <span data-ttu-id="59a4a-157">이 규칙은 [IFormCollection](/dotnet/api/microsoft.aspnetcore.http.iformcollection) 및 [CancellationToken](/dotnet/api/system.threading.cancellationtoken)과 같이 특별한 의미를 지닌 복합 기본 제공 형식에는 적용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="59a4a-157">An exception to this rule is any complex, built-in type with a special meaning, such as [IFormCollection](/dotnet/api/microsoft.aspnetcore.http.iformcollection) and [CancellationToken](/dotnet/api/system.threading.cancellationtoken).</span></span> <span data-ttu-id="59a4a-158">바인딩 소스 유추 코드는 이러한 특별한 형식을 무시합니다.</span><span class="sxs-lookup"><span data-stu-id="59a4a-158">The binding source inference code ignores those special types.</span></span> <span data-ttu-id="59a4a-159">작업에 명시적으로 지정(`[FromBody]`를 통해)되거나 요청 본문의 바인딩으로 유추된 한 개를 초과하는 매개 변수가 있는 경우 예외가 throw됩니다.</span><span class="sxs-lookup"><span data-stu-id="59a4a-159">When an action has more than one parameter explicitly specified (via `[FromBody]`) or inferred as bound from the request body, an exception is thrown.</span></span> <span data-ttu-id="59a4a-160">예를 들어 다음 작업 서명으로 예외가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="59a4a-160">For example, the following action signatures cause an exception:</span></span>

<span data-ttu-id="59a4a-161">[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api/Controllers/TestController.cs?name=snippet_ActionsCausingExceptions)]</span><span class="sxs-lookup"><span data-stu-id="59a4a-161">[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api/Controllers/TestController.cs?name=snippet_ActionsCausingExceptions)]</span></span>

* <span data-ttu-id="59a4a-162">**[FromForm]** 은 [IFormFile](/dotnet/api/microsoft.aspnetcore.http.iformfile) 및 [IFormFileCollection](/dotnet/api/microsoft.aspnetcore.http.iformfilecollection) 형식의 작업 매개 변수에 대해 유추됩니다.</span><span class="sxs-lookup"><span data-stu-id="59a4a-162">**[FromForm]** is inferred for action parameters of type [IFormFile](/dotnet/api/microsoft.aspnetcore.http.iformfile) and [IFormFileCollection](/dotnet/api/microsoft.aspnetcore.http.iformfilecollection).</span></span> <span data-ttu-id="59a4a-163">단순 또는 사용자 정의 형식에 대해서는 유추되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="59a4a-163">It's not inferred for any simple or user-defined types.</span></span>
* <span data-ttu-id="59a4a-164">**[FromRoute]** 는 경로 템플릿에서 매개 변수와 일치하는 작업 매개 변수 이름에 대해 유추됩니다.</span><span class="sxs-lookup"><span data-stu-id="59a4a-164">**[FromRoute]** is inferred for any action parameter name matching a parameter in the route template.</span></span> <span data-ttu-id="59a4a-165">여러 경로가 작업 매개 변수와 일치하는 경우 모든 경로 값은 `[FromRoute]`로 간주됩니다.</span><span class="sxs-lookup"><span data-stu-id="59a4a-165">When multiple routes match an action parameter, any route value is considered `[FromRoute]`.</span></span>
* <span data-ttu-id="59a4a-166">**[FromQuery]** 는 다른 작업 매개 변수에 대해 유추됩니다.</span><span class="sxs-lookup"><span data-stu-id="59a4a-166">**[FromQuery]** is inferred for any other action parameters.</span></span>

<span data-ttu-id="59a4a-167">기본 유추 규칙은 *Startup.ConfigureServices*에서 다음 코드와 함께 사용하지 않도록 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="59a4a-167">The default inference rules are disabled with the following code in *Startup.ConfigureServices*:</span></span>

<span data-ttu-id="59a4a-168">[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api/Startup.cs?name=snippet_ConfigureApiBehaviorOptions&highlight=4)]</span><span class="sxs-lookup"><span data-stu-id="59a4a-168">[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api/Startup.cs?name=snippet_ConfigureApiBehaviorOptions&highlight=4)]</span></span>

### <a name="multipartform-data-request-inference"></a><span data-ttu-id="59a4a-169">다중 파트/폼 데이터 요청 유추</span><span class="sxs-lookup"><span data-stu-id="59a4a-169">Multipart/form-data request inference</span></span>

<span data-ttu-id="59a4a-170">작업 매개 변수를 [[FromForm]](/dotnet/api/microsoft.aspnetcore.mvc.fromformattribute) 특성으로 주석 처리하는 경우 `multipart/form-data` 요청 콘텐츠 형식이 유추됩니다.</span><span class="sxs-lookup"><span data-stu-id="59a4a-170">When an action parameter is annotated with the [[FromForm]](/dotnet/api/microsoft.aspnetcore.mvc.fromformattribute) attribute, the `multipart/form-data` request content type is inferred.</span></span>

<span data-ttu-id="59a4a-171">기본 동작은 *Startup.ConfigureServices*에서 다음 코드와 함께 사용하지 않도록 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="59a4a-171">The default behavior is disabled with the following code in *Startup.ConfigureServices*:</span></span>

<span data-ttu-id="59a4a-172">[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api/Startup.cs?name=snippet_ConfigureApiBehaviorOptions&highlight=3)]</span><span class="sxs-lookup"><span data-stu-id="59a4a-172">[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api/Startup.cs?name=snippet_ConfigureApiBehaviorOptions&highlight=3)]</span></span>

### <a name="attribute-routing-requirement"></a><span data-ttu-id="59a4a-173">특성 라우팅 요구 사항</span><span class="sxs-lookup"><span data-stu-id="59a4a-173">Attribute routing requirement</span></span>

<span data-ttu-id="59a4a-174">특성 라우팅은 요구 사항이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="59a4a-174">Attribute routing becomes a requirement.</span></span> <span data-ttu-id="59a4a-175">예:</span><span class="sxs-lookup"><span data-stu-id="59a4a-175">For example:</span></span>

<span data-ttu-id="59a4a-176">[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api/Controllers/ProductsController.cs?name=snippet_ControllerSignature&highlight=1)]</span><span class="sxs-lookup"><span data-stu-id="59a4a-176">[!code-csharp[](../web-api/define-controller/samples/WebApiSample.Api/Controllers/ProductsController.cs?name=snippet_ControllerSignature&highlight=1)]</span></span>

<span data-ttu-id="59a4a-177">작업은 [UseMvc](/dotnet/api/microsoft.aspnetcore.builder.mvcapplicationbuilderextensions.usemvc#Microsoft_AspNetCore_Builder_MvcApplicationBuilderExtensions_UseMvc_Microsoft_AspNetCore_Builder_IApplicationBuilder_System_Action_Microsoft_AspNetCore_Routing_IRouteBuilder__)에 정의된 [규칙 기반 경로](xref:mvc/controllers/routing#conventional-routing)를 통해 또는 *Startup.Configure*의 [UseMvcWithDefaultRoute](/dotnet/api/microsoft.aspnetcore.builder.mvcapplicationbuilderextensions.usemvcwithdefaultroute#Microsoft_AspNetCore_Builder_MvcApplicationBuilderExtensions_UseMvcWithDefaultRoute_Microsoft_AspNetCore_Builder_IApplicationBuilder_)에 의해 액세스할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="59a4a-177">Actions are inaccessible via [conventional routes](xref:mvc/controllers/routing#conventional-routing) defined in [UseMvc](/dotnet/api/microsoft.aspnetcore.builder.mvcapplicationbuilderextensions.usemvc#Microsoft_AspNetCore_Builder_MvcApplicationBuilderExtensions_UseMvc_Microsoft_AspNetCore_Builder_IApplicationBuilder_System_Action_Microsoft_AspNetCore_Routing_IRouteBuilder__) or by [UseMvcWithDefaultRoute](/dotnet/api/microsoft.aspnetcore.builder.mvcapplicationbuilderextensions.usemvcwithdefaultroute#Microsoft_AspNetCore_Builder_MvcApplicationBuilderExtensions_UseMvcWithDefaultRoute_Microsoft_AspNetCore_Builder_IApplicationBuilder_) in *Startup.Configure*.</span></span>
::: moniker-end

## <a name="additional-resources"></a><span data-ttu-id="59a4a-178">추가 자료</span><span class="sxs-lookup"><span data-stu-id="59a4a-178">Additional resources</span></span>

* [<span data-ttu-id="59a4a-179">컨트롤러 작업 반환 형식</span><span class="sxs-lookup"><span data-stu-id="59a4a-179">Controller action return types</span></span>](xref:web-api/action-return-types)
* [<span data-ttu-id="59a4a-180">사용자 지정 서식 지정기</span><span class="sxs-lookup"><span data-stu-id="59a4a-180">Custom formatters</span></span>](xref:web-api/advanced/custom-formatters)
* [<span data-ttu-id="59a4a-181">응답 데이터 서식 지정</span><span class="sxs-lookup"><span data-stu-id="59a4a-181">Format response data</span></span>](xref:web-api/advanced/formatting)
* [<span data-ttu-id="59a4a-182">Swagger를 사용한 도움말 페이지</span><span class="sxs-lookup"><span data-stu-id="59a4a-182">Help pages using Swagger</span></span>](xref:tutorials/web-api-help-pages-using-swagger)
* [<span data-ttu-id="59a4a-183">컨트롤러 작업에 라우팅</span><span class="sxs-lookup"><span data-stu-id="59a4a-183">Routing to controller actions</span></span>](xref:mvc/controllers/routing)