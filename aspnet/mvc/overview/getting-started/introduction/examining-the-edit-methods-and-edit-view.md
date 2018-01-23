---
uid: mvc/overview/getting-started/introduction/examining-the-edit-methods-and-edit-view
title: "檢查編輯方法與編輯檢視 |Microsoft 文件"
author: Rick-Anderson
description: 
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/22/2015
ms.topic: article
ms.assetid: 52a4d5fe-aa31-4471-b3cb-a064f82cb791
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/getting-started/introduction/examining-the-edit-methods-and-edit-view
msc.type: authoredcontent
ms.openlocfilehash: 84aadccc18e7fa0fb56c7a78e144a1bf1038aac5
ms.sourcegitcommit: d1d8071d4093bf2444b5ae19d6e45c3d187e338b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/19/2017
---
<a name="examining-the-edit-methods-and-edit-view"></a><span data-ttu-id="fad2e-102">檢查編輯方法與編輯檢視</span><span class="sxs-lookup"><span data-stu-id="fad2e-102">Examining the Edit Methods and Edit View</span></span>
====================
<span data-ttu-id="fad2e-103">由[Rick Anderson](https://github.com/Rick-Anderson)</span><span class="sxs-lookup"><span data-stu-id="fad2e-103">by [Rick Anderson](https://github.com/Rick-Anderson)</span></span>

[!INCLUDE[Tutorial Note](sample/code-location.md)]

<span data-ttu-id="fad2e-104">在本節中，您將會檢查所產生`Edit`動作方法和檢視電影控制站。</span><span class="sxs-lookup"><span data-stu-id="fad2e-104">In this section, you'll examine the generated `Edit` action methods and views for the movie controller.</span></span> <span data-ttu-id="fad2e-105">但會先進行看起來更好的發行日期簡短轉接。</span><span class="sxs-lookup"><span data-stu-id="fad2e-105">But first will take a short diversion to make the release date look better.</span></span> <span data-ttu-id="fad2e-106">開啟*Models\Movie.cs*檔案，然後加入反白顯示的行，如下所示：</span><span class="sxs-lookup"><span data-stu-id="fad2e-106">Open the *Models\Movie.cs* file and add the highlighted lines shown below:</span></span>

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample1.cs?highlight=2,12-14)]

<span data-ttu-id="fad2e-107">您也可以將日期文化特性特定像這樣：</span><span class="sxs-lookup"><span data-stu-id="fad2e-107">You can also make the date culture specific like this:</span></span>

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample2.cs?highlight=3)]

<span data-ttu-id="fad2e-108">接下來的教學課程中將涵蓋 [DataAnnotations](https://msdn.microsoft.com/en-us/library/system.componentmodel.dataannotations.aspx)。</span><span class="sxs-lookup"><span data-stu-id="fad2e-108">We'll cover [DataAnnotations](https://msdn.microsoft.com/en-us/library/system.componentmodel.dataannotations.aspx) in the next tutorial.</span></span> <span data-ttu-id="fad2e-109">[Display](https://msdn.microsoft.com/en-us/library/system.componentmodel.dataannotations.displayattribute.aspx) 屬性指定要顯示的欄位名稱 (在本例中為 "Release Date"，而不是 "ReleaseDate")。</span><span class="sxs-lookup"><span data-stu-id="fad2e-109">The [Display](https://msdn.microsoft.com/en-us/library/system.componentmodel.dataannotations.displayattribute.aspx) attribute specifies what to display for the name of a field (in this case "Release Date" instead of "ReleaseDate").</span></span> <span data-ttu-id="fad2e-110">[DataType](https://msdn.microsoft.com/en-us/library/system.componentmodel.dataannotations.datatypeattribute.aspx)屬性指定的資料類型，在此情況下它是日期，因此不會顯示儲存在欄位中的時間資訊。</span><span class="sxs-lookup"><span data-stu-id="fad2e-110">The [DataType](https://msdn.microsoft.com/en-us/library/system.componentmodel.dataannotations.datatypeattribute.aspx) attribute specifies the type of the data, in this case it's a date, so the time information stored in the field is not displayed.</span></span> <span data-ttu-id="fad2e-111">[DisplayFormat](https://msdn.microsoft.com/en-us/library/system.componentmodel.dataannotations.displayformatattribute.aspx)屬性所需的正確轉譯日期格式 Chrome 瀏覽器中的 bug。</span><span class="sxs-lookup"><span data-stu-id="fad2e-111">The [DisplayFormat](https://msdn.microsoft.com/en-us/library/system.componentmodel.dataannotations.displayformatattribute.aspx) attribute is needed for a bug in the Chrome browser that renders date formats incorrectly.</span></span>

<span data-ttu-id="fad2e-112">執行應用程式，並瀏覽至`Movies`控制站。</span><span class="sxs-lookup"><span data-stu-id="fad2e-112">Run the application and browse to the `Movies` controller.</span></span> <span data-ttu-id="fad2e-113">將滑鼠指標**編輯**連結，查看它連結到的 URL。</span><span class="sxs-lookup"><span data-stu-id="fad2e-113">Hold the mouse pointer over an **Edit** link to see the URL that it links to.</span></span>

![EditLink_sm](examining-the-edit-methods-and-edit-view/_static/image1.png)

<span data-ttu-id="fad2e-115">**編輯**連結由產生`Html.ActionLink`方法中的*Views\Movies\Index.cshtml*檢視：</span><span class="sxs-lookup"><span data-stu-id="fad2e-115">The **Edit** link was generated by the `Html.ActionLink` method in the *Views\Movies\Index.cshtml* view:</span></span>

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample3.cshtml)]

![Html.ActionLink](examining-the-edit-methods-and-edit-view/_static/image2.png)

<span data-ttu-id="fad2e-117">`Html`物件是協助程式上使用屬性公開[System.Web.Mvc.WebViewPage](https://msdn.microsoft.com/en-us/library/gg402107(VS.98).aspx)基底類別。</span><span class="sxs-lookup"><span data-stu-id="fad2e-117">The `Html` object is a helper that's exposed using a property on the [System.Web.Mvc.WebViewPage](https://msdn.microsoft.com/en-us/library/gg402107(VS.98).aspx) base class.</span></span> <span data-ttu-id="fad2e-118">`ActionLink`方法的協助程式簡化了動態產生 HTML，超連結，連結至動作方法，控制站上。</span><span class="sxs-lookup"><span data-stu-id="fad2e-118">The `ActionLink` method of the helper makes it easy to dynamically generate HTML hyperlinks that link to action methods on controllers.</span></span> <span data-ttu-id="fad2e-119">第一個引數`ActionLink`方法是要呈現的連結文字 (例如， `<a>Edit Me</a>`)。</span><span class="sxs-lookup"><span data-stu-id="fad2e-119">The first argument to the `ActionLink` method is the link text to render (for example, `<a>Edit Me</a>`).</span></span> <span data-ttu-id="fad2e-120">第二個引數是要叫用的動作方法的名稱 (在此情況下，`Edit`動作)。</span><span class="sxs-lookup"><span data-stu-id="fad2e-120">The second argument is the name of the action method to invoke (In this case, the `Edit` action).</span></span> <span data-ttu-id="fad2e-121">最後一個引數是[匿名物件](https://weblogs.asp.net/scottgu/archive/2007/05/15/new-orcas-language-feature-anonymous-types.aspx)，產生 （在本例中，識別碼，4） 的路由資料。</span><span class="sxs-lookup"><span data-stu-id="fad2e-121">The final argument is an [anonymous object](https://weblogs.asp.net/scottgu/archive/2007/05/15/new-orcas-language-feature-anonymous-types.aspx) that generates the route data (in this case, the ID of 4).</span></span>

<span data-ttu-id="fad2e-122">產生的連結，如上圖所示為`http://localhost:1234/Movies/Edit/4`。</span><span class="sxs-lookup"><span data-stu-id="fad2e-122">The generated link shown in the previous image is `http://localhost:1234/Movies/Edit/4`.</span></span> <span data-ttu-id="fad2e-123">預設路由 (在中建立*應用程式\_Start\RouteConfig.cs*) 採用的 URL 模式`{controller}/{action}/{id}`。</span><span class="sxs-lookup"><span data-stu-id="fad2e-123">The default route (established in *App\_Start\RouteConfig.cs*) takes the URL pattern `{controller}/{action}/{id}`.</span></span> <span data-ttu-id="fad2e-124">因此，ASP.NET 會將轉譯`http://localhost:1234/Movies/Edit/4`的要求到`Edit`動作方法的`Movies`控制器會執行參數`ID`等於 4。</span><span class="sxs-lookup"><span data-stu-id="fad2e-124">Therefore, ASP.NET translates `http://localhost:1234/Movies/Edit/4` into a request to the `Edit` action method of the `Movies` controller with the parameter `ID` equal to 4.</span></span> <span data-ttu-id="fad2e-125">檢查下列程式碼從*應用程式\_Start\RouteConfig.cs*檔案。</span><span class="sxs-lookup"><span data-stu-id="fad2e-125">Examine the following code from the *App\_Start\RouteConfig.cs* file.</span></span> <span data-ttu-id="fad2e-126">[MapRoute](../../older-versions-1/controllers-and-routing/asp-net-mvc-routing-overview-cs.md)方法用來將 HTTP 要求路由至正確的控制器與動作方法並提供選擇性的 ID 參數。</span><span class="sxs-lookup"><span data-stu-id="fad2e-126">The [MapRoute](../../older-versions-1/controllers-and-routing/asp-net-mvc-routing-overview-cs.md) method is used to route HTTP requests to the correct controller and action method and supply the optional ID parameter.</span></span> <span data-ttu-id="fad2e-127">[MapRoute](../../older-versions-1/controllers-and-routing/asp-net-mvc-routing-overview-cs.md)方法也會使用[HtmlHelpers](https://msdn.microsoft.com/en-us/library/system.web.mvc.htmlhelper(v=vs.108).aspx)例如`ActionLink`來產生 Url 指定的控制器、 動作方法和任何路由資料。</span><span class="sxs-lookup"><span data-stu-id="fad2e-127">The [MapRoute](../../older-versions-1/controllers-and-routing/asp-net-mvc-routing-overview-cs.md) method is also used by the [HtmlHelpers](https://msdn.microsoft.com/en-us/library/system.web.mvc.htmlhelper(v=vs.108).aspx) such as `ActionLink` to generate URLs given the controller, action method and any route data.</span></span>

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample4.cs?highlight=7)]

<span data-ttu-id="fad2e-128">您也可以傳遞使用的查詢字串的動作方法參數。</span><span class="sxs-lookup"><span data-stu-id="fad2e-128">You can also pass action method parameters using a query string.</span></span> <span data-ttu-id="fad2e-129">例如，URL`http://localhost:1234/Movies/Edit?ID=3`也會傳遞參數`ID`為 3`Edit`動作方法的`Movies`控制站。</span><span class="sxs-lookup"><span data-stu-id="fad2e-129">For example, the URL `http://localhost:1234/Movies/Edit?ID=3` also passes the parameter `ID` of 3 to the `Edit` action method of the `Movies` controller.</span></span>

![EditQueryString](examining-the-edit-methods-and-edit-view/_static/image3.png)

<span data-ttu-id="fad2e-131">開啟`Movies`控制站。</span><span class="sxs-lookup"><span data-stu-id="fad2e-131">Open the `Movies` controller.</span></span> <span data-ttu-id="fad2e-132">這兩個`Edit`動作方法如下所示。</span><span class="sxs-lookup"><span data-stu-id="fad2e-132">The two `Edit` action methods are shown below.</span></span>

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample5.cs?highlight=19-21)]

<span data-ttu-id="fad2e-133">請注意，第二個 `Edit` 動作方法的前面是 `HttpPost` 屬性。</span><span class="sxs-lookup"><span data-stu-id="fad2e-133">Notice the second `Edit` action method is preceded by the `HttpPost` attribute.</span></span> <span data-ttu-id="fad2e-134">這個屬性指定的多載`Edit`只會針對 POST 要求叫用方法。</span><span class="sxs-lookup"><span data-stu-id="fad2e-134">This attribute specifies that the overload of the `Edit` method can be invoked only for POST requests.</span></span> <span data-ttu-id="fad2e-135">您可以套用`HttpGet`第一個屬性編輯方法，但是，因為不需要它是預設值。</span><span class="sxs-lookup"><span data-stu-id="fad2e-135">You could apply the `HttpGet` attribute to the first edit method, but that's not necessary because it's the default.</span></span> <span data-ttu-id="fad2e-136">(我們將參照動作方法會隱含地指派`HttpGet`屬性做為`HttpGet`方法。)[繫結](https://msdn.microsoft.com/en-us/library/system.web.mvc.bindattribute(v=vs.108).aspx)屬性是防止駭客過度張貼您的模型資料的另一個重要的安全性機制。</span><span class="sxs-lookup"><span data-stu-id="fad2e-136">(We'll refer to action methods that are implicitly assigned the `HttpGet` attribute as `HttpGet` methods.) The [Bind](https://msdn.microsoft.com/en-us/library/system.web.mvc.bindattribute(v=vs.108).aspx) attribute is another important security mechanism that keeps hackers from over-posting data to your model.</span></span> <span data-ttu-id="fad2e-137">您應該只包含您想要變更繫結屬性中的屬性。</span><span class="sxs-lookup"><span data-stu-id="fad2e-137">You should only include properties in the bind attribute that you want to change.</span></span> <span data-ttu-id="fad2e-138">您可以閱讀 overposting 和中的繫結屬性我[overposting 安全性注意事項](https://go.microsoft.com/fwlink/?LinkId=317598)。</span><span class="sxs-lookup"><span data-stu-id="fad2e-138">You can read about overposting and the bind attribute in my [overposting security note](https://go.microsoft.com/fwlink/?LinkId=317598).</span></span> <span data-ttu-id="fad2e-139">在此教學課程中使用簡單模型中，我們將繫結模型中的所有資料。</span><span class="sxs-lookup"><span data-stu-id="fad2e-139">In the simple model used in this tutorial, we will be binding all the data in the model.</span></span> <span data-ttu-id="fad2e-140">[ValidateAntiForgeryToken](https://msdn.microsoft.com/en-us/library/system.web.mvc.validateantiforgerytokenattribute(v=vs.108).aspx)屬性用於防範偽造要求，並使用成對向上`@Html.AntiForgeryToken()`在編輯檢視檔案 (*Views\Movies\Edit.cshtml*)，如下所示的一部分：</span><span class="sxs-lookup"><span data-stu-id="fad2e-140">The [ValidateAntiForgeryToken](https://msdn.microsoft.com/en-us/library/system.web.mvc.validateantiforgerytokenattribute(v=vs.108).aspx) attribute is used to prevent forgery of a request and is paired up with `@Html.AntiForgeryToken()` in the edit view file (*Views\Movies\Edit.cshtml*), a portion is shown below:</span></span>

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample6.cshtml?highlight=9)]

<span data-ttu-id="fad2e-141">`@Html.AntiForgeryToken()`產生隱藏的表單防偽語彙基元必須完全符合`Edit`方法`Movies`控制站。</span><span class="sxs-lookup"><span data-stu-id="fad2e-141">`@Html.AntiForgeryToken()` generates a hidden form anti-forgery token that must match in the `Edit` method of the `Movies` controller.</span></span> <span data-ttu-id="fad2e-142">閱讀更多關於跨網站要求偽造 （也稱為 XSRF 或 CSRF） 在我的教學課程[MVC 中 XSRF/CSRF 防護](../../security/xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages.md)。</span><span class="sxs-lookup"><span data-stu-id="fad2e-142">You can read more about Cross-site request forgery (also known as XSRF or CSRF) in my tutorial [XSRF/CSRF Prevention in MVC](../../security/xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages.md).</span></span>

<span data-ttu-id="fad2e-143">`HttpGet` `Edit`方法會採用影片 ID 參數在查詢使用 Entity Framework 的電影`Find`方法，並返回編輯檢視中選取的影片。</span><span class="sxs-lookup"><span data-stu-id="fad2e-143">The `HttpGet` `Edit` method takes the movie ID parameter, looks up the movie using the Entity Framework `Find` method, and returns the selected movie to the Edit view.</span></span> <span data-ttu-id="fad2e-144">如果找不到電影， [HttpNotFound](https://msdn.microsoft.com/en-us/library/gg453938(VS.98).aspx)傳回。</span><span class="sxs-lookup"><span data-stu-id="fad2e-144">If a movie cannot be found, [HttpNotFound](https://msdn.microsoft.com/en-us/library/gg453938(VS.98).aspx) is returned.</span></span> <span data-ttu-id="fad2e-145">當 Scaffolding 系統建立 Edit 檢視時，它會檢查 `Movie` 類別，並建立程式碼為類別的每個屬性轉譯 `<label>` 和 `<input>` 元素。</span><span class="sxs-lookup"><span data-stu-id="fad2e-145">When the scaffolding system created the Edit view, it examined the `Movie` class and created code to render `<label>` and `<input>` elements for each property of the class.</span></span> <span data-ttu-id="fad2e-146">下列範例顯示 visual studio scaffolding 系統所產生的編輯檢視：</span><span class="sxs-lookup"><span data-stu-id="fad2e-146">The following example shows the Edit view that was generated by the visual studio scaffolding system:</span></span>

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample7.cshtml)]

<span data-ttu-id="fad2e-147">請注意如何檢視範本都有`@model MvcMovie.Models.Movie`在檔案最上方的陳述式，這會指定檢視預期型別檢視範本模型`Movie`。</span><span class="sxs-lookup"><span data-stu-id="fad2e-147">Notice how the view template has a `@model MvcMovie.Models.Movie` statement at the top of the file — this specifies that the view expects the model for the view template to be of type `Movie`.</span></span>

<span data-ttu-id="fad2e-148">Scaffold 的程式碼會使用數個*helper 方法*來簡化的 HTML 標記。</span><span class="sxs-lookup"><span data-stu-id="fad2e-148">The scaffolded code uses several *helper methods* to streamline the HTML markup.</span></span> <span data-ttu-id="fad2e-149">[ `Html.LabelFor` ](https://msdn.microsoft.com/en-us/library/gg401864(VS.98).aspx) Helper 會顯示欄位的名稱 (&quot;標題&quot;， &quot;ReleaseDate&quot;，&quot;類型&quot;，或&quot;價格&quot;).</span><span class="sxs-lookup"><span data-stu-id="fad2e-149">The [`Html.LabelFor`](https://msdn.microsoft.com/en-us/library/gg401864(VS.98).aspx) helper displays the name of the field (&quot;Title&quot;, &quot;ReleaseDate&quot;, &quot;Genre&quot;, or &quot;Price&quot;).</span></span> <span data-ttu-id="fad2e-150">[ `Html.EditorFor` ](https://msdn.microsoft.com/en-us/library/system.web.mvc.html.editorextensions.editorfor(VS.98).aspx) Helper 可呈現 HTML`<input>`項目。</span><span class="sxs-lookup"><span data-stu-id="fad2e-150">The [`Html.EditorFor`](https://msdn.microsoft.com/en-us/library/system.web.mvc.html.editorextensions.editorfor(VS.98).aspx) helper renders an HTML `<input>` element.</span></span> <span data-ttu-id="fad2e-151">[ `Html.ValidationMessageFor` ](https://msdn.microsoft.com/en-us/library/system.web.mvc.html.validationextensions.validationmessagefor(VS.98).aspx) Helper 會顯示所有與該屬性相關聯的驗證訊息。</span><span class="sxs-lookup"><span data-stu-id="fad2e-151">The [`Html.ValidationMessageFor`](https://msdn.microsoft.com/en-us/library/system.web.mvc.html.validationextensions.validationmessagefor(VS.98).aspx) helper displays any validation messages associated with that property.</span></span>

<span data-ttu-id="fad2e-152">執行應用程式，並瀏覽至*/Movies* URL。</span><span class="sxs-lookup"><span data-stu-id="fad2e-152">Run the application and navigate to the */Movies* URL.</span></span> <span data-ttu-id="fad2e-153">按一下 **Edit** 連結。</span><span class="sxs-lookup"><span data-stu-id="fad2e-153">Click an **Edit** link.</span></span> <span data-ttu-id="fad2e-154">在瀏覽器中，檢視頁面的原始檔。</span><span class="sxs-lookup"><span data-stu-id="fad2e-154">In the browser, view the source for the page.</span></span> <span data-ttu-id="fad2e-155">如下所示的 HTML 表單項目。</span><span class="sxs-lookup"><span data-stu-id="fad2e-155">The HTML for the form element is shown below.</span></span>

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample8.cshtml?highlight=1-2)]

<span data-ttu-id="fad2e-156">`<input>`項目會在 HTML`<form>`項目其`action`屬性設定為張貼到*/電影/編輯*URL。</span><span class="sxs-lookup"><span data-stu-id="fad2e-156">The `<input>` elements are in an HTML `<form>` element whose `action` attribute is set to post to the */Movies/Edit* URL.</span></span> <span data-ttu-id="fad2e-157">表單資料都將張貼至伺服器時**儲存**按鈕。</span><span class="sxs-lookup"><span data-stu-id="fad2e-157">The form data will be posted to the server when the **Save** button is clicked.</span></span> <span data-ttu-id="fad2e-158">第二行中顯示的隱藏[XSRF](../../security/xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages.md)所產生的語彙基元`@Html.AntiForgeryToken()`呼叫。</span><span class="sxs-lookup"><span data-stu-id="fad2e-158">The second line shows the hidden [XSRF](../../security/xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages.md) token generated by the `@Html.AntiForgeryToken()` call.</span></span>

## <a name="processing-the-post-request"></a><span data-ttu-id="fad2e-159">處理 POST 要求</span><span class="sxs-lookup"><span data-stu-id="fad2e-159">Processing the POST Request</span></span>

<span data-ttu-id="fad2e-160">下列清單顯示 `HttpPost` 版本的 `Edit` 動作方法。</span><span class="sxs-lookup"><span data-stu-id="fad2e-160">The following listing shows the `HttpPost` version of the `Edit` action method.</span></span>

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample9.cs)]

<span data-ttu-id="fad2e-161">[ValidateAntiForgeryToken](https://msdn.microsoft.com/en-us/library/system.web.mvc.validateantiforgerytokenattribute(v=vs.108).aspx)屬性驗證[XSRF](../../security/xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages.md)所產生的語彙基元`@Html.AntiForgeryToken()`檢視中呼叫。</span><span class="sxs-lookup"><span data-stu-id="fad2e-161">The [ValidateAntiForgeryToken](https://msdn.microsoft.com/en-us/library/system.web.mvc.validateantiforgerytokenattribute(v=vs.108).aspx) attribute validates the [XSRF](../../security/xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages.md) token generated by the `@Html.AntiForgeryToken()` call in the view.</span></span>

<span data-ttu-id="fad2e-162">[ASP.NET MVC 模型繫結器](https://msdn.microsoft.com/en-us/library/dd410405.aspx)採用的已張貼的表單值，並建立`Movie`物件傳遞為`movie`參數。</span><span class="sxs-lookup"><span data-stu-id="fad2e-162">The [ASP.NET MVC model binder](https://msdn.microsoft.com/en-us/library/dd410405.aspx) takes the posted form values and creates a `Movie` object that's passed as the `movie` parameter.</span></span> <span data-ttu-id="fad2e-163">`ModelState.IsValid` 方法會驗證表單中提交的資料可用於修改 (編輯或更新) `Movie` 物件。</span><span class="sxs-lookup"><span data-stu-id="fad2e-163">The `ModelState.IsValid` method verifies that the data submitted in the form can be used to modify (edit or update) a `Movie` object.</span></span> <span data-ttu-id="fad2e-164">如果是有效的資料，將電影資料會儲存至`Movies`集合`db(MovieDBContext`執行個體)。</span><span class="sxs-lookup"><span data-stu-id="fad2e-164">If the data is valid, the movie data is saved to the `Movies` collection of the `db(MovieDBContext` instance).</span></span> <span data-ttu-id="fad2e-165">將新的電影資料會儲存到資料庫，藉由呼叫`SaveChanges`方法`MovieDBContext`。</span><span class="sxs-lookup"><span data-stu-id="fad2e-165">The new movie data is saved to the database by calling the `SaveChanges` method of `MovieDBContext`.</span></span> <span data-ttu-id="fad2e-166">儲存資料之後，程式碼將使用者重新導向至 `MoviesController` 類別的 `Index` 動作方法，此方法會顯示電影集合，包括剛剛所進行的變更。</span><span class="sxs-lookup"><span data-stu-id="fad2e-166">After saving the data, the code redirects the user to the `Index` action method of the `MoviesController` class, which displays the movie collection, including the changes just made.</span></span>

<span data-ttu-id="fad2e-167">只要用戶端驗證決定欄位的值不是有效的則會顯示錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="fad2e-167">As soon as the client side validation determines the values of a field are not valid, an error message is displayed.</span></span> <span data-ttu-id="fad2e-168">如果您停用 JavaScript，就不需要用戶端驗證，但是伺服器會偵測已張貼的值不是有效的並會重新顯示表單值，並顯示錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="fad2e-168">If you disable JavaScript, you won't have client side validation but the server will detect the posted values are not valid, and the form values will be redisplayed with error messages.</span></span> <span data-ttu-id="fad2e-169">稍後在本教學課程中，我們會檢查驗證中更多詳細資料。</span><span class="sxs-lookup"><span data-stu-id="fad2e-169">Later in the tutorial we examine validation in more detail.</span></span>

<span data-ttu-id="fad2e-170">`Html.ValidationMessageFor`中的協助程式*Edit.cshtml*檢視範本負責顯示適當的錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="fad2e-170">The `Html.ValidationMessageFor` helpers in the *Edit.cshtml* view template take care of displaying appropriate error messages.</span></span>

![abcNotValid](examining-the-edit-methods-and-edit-view/_static/image4.png)

<span data-ttu-id="fad2e-172">所有`HttpGet`方法遵循類似的模式。</span><span class="sxs-lookup"><span data-stu-id="fad2e-172">All the `HttpGet` methods follow a similar pattern.</span></span> <span data-ttu-id="fad2e-173">他們取得影片物件 (或清單中的物件，大小寫的`Index`)，並將模型傳遞至檢視。</span><span class="sxs-lookup"><span data-stu-id="fad2e-173">They get a movie object (or list of objects, in the case of `Index`), and pass the model to the view.</span></span> <span data-ttu-id="fad2e-174">`Create`方法傳遞空影片物件建立檢視。</span><span class="sxs-lookup"><span data-stu-id="fad2e-174">The `Create` method passes an empty movie object to the Create view.</span></span> <span data-ttu-id="fad2e-175">建立、編輯、刪除或以其他方式修改資料的所有方法都會在方法的 `HttpPost` 多載中執行這個動作。</span><span class="sxs-lookup"><span data-stu-id="fad2e-175">All the methods that create, edit, delete, or otherwise modify data do so in the `HttpPost` overload of the method.</span></span> <span data-ttu-id="fad2e-176">修改資料中的 HTTP GET 的方法會造成安全性風險，部落格文章項目中所述[ASP.NET MVC 秘訣 #46 – 請勿使用刪除連結，因為它們會產生安全性漏洞](http://stephenwalther.com/blog/archive/2009/01/21/asp.net-mvc-tip-46-ndash-donrsquot-use-delete-links-because.aspx)。</span><span class="sxs-lookup"><span data-stu-id="fad2e-176">Modifying data in an HTTP GET method is a security risk, as described in the blog post entry [ASP.NET MVC Tip #46 – Don't use Delete Links because they create Security Holes](http://stephenwalther.com/blog/archive/2009/01/21/asp.net-mvc-tip-46-ndash-donrsquot-use-delete-links-because.aspx).</span></span> <span data-ttu-id="fad2e-177">修改 GET 方法中的資料也違反 HTTP 最佳作法和架構[REST](http://en.wikipedia.org/wiki/Representational_State_Transfer)模式，以指定 GET 要求，不應該變更應用程式的狀態。</span><span class="sxs-lookup"><span data-stu-id="fad2e-177">Modifying data in a GET method also violates HTTP best practices and the architectural [REST](http://en.wikipedia.org/wiki/Representational_State_Transfer) pattern, which specifies that GET requests should not change the state of your application.</span></span> <span data-ttu-id="fad2e-178">也就是說，執行 GET 作業應該是安全的作業，沒有任何副作用，而且不會修改您的保存資料。</span><span class="sxs-lookup"><span data-stu-id="fad2e-178">In other words, performing a GET operation should be a safe operation that has no side effects and doesn't modify your persisted data.</span></span>

<span data-ttu-id="fad2e-179">如果您使用英文 （美國） 的電腦，您可以略過本節並移至下一個教學課程。</span><span class="sxs-lookup"><span data-stu-id="fad2e-179">If you are using a US-English computer, you can skip this section and go to the next tutorial.</span></span> <span data-ttu-id="fad2e-180">您可以下載此教學課程的 Globalize 新版[這裡](https://archive.msdn.microsoft.com/Project/Download/FileDownload.aspx?ProjectName=aspnetmvcsamples&amp;DownloadId=16475)。</span><span class="sxs-lookup"><span data-stu-id="fad2e-180">You can download the Globalize version of this tutorial [here](https://archive.msdn.microsoft.com/Project/Download/FileDownload.aspx?ProjectName=aspnetmvcsamples&amp;DownloadId=16475).</span></span> <span data-ttu-id="fad2e-181">如需國際化絕佳兩部分教學課程，請參閱[Nadeem 的 ASP.NET MVC 5 國際化](http://afana.me/post/aspnet-mvc-internationalization.aspx)。</span><span class="sxs-lookup"><span data-stu-id="fad2e-181">For an excellent two part tutorial on Internationalization, see [Nadeem's ASP.NET MVC 5 Internationalization](http://afana.me/post/aspnet-mvc-internationalization.aspx).</span></span>


> [!NOTE]
> <span data-ttu-id="fad2e-182">若要支援 jQuery 驗證非英文的地區設定，請使用逗號 (&quot;，&quot;) 的小數點和非英文 （美國） 的日期格式，您必須加入*globalize.js*和您的特定*cultures/globalize.cultures.js*檔案 (從[https://github.com/jquery/globalize](https://github.com/jquery/globalize) ) 和使用 JavaScript `Globalize.parseFloat`。</span><span class="sxs-lookup"><span data-stu-id="fad2e-182">to support jQuery validation for non-English locales that use a comma (&quot;,&quot;) for a decimal point, and non US-English date formats, you must include *globalize.js* and your specific *cultures/globalize.cultures.js* file(from [https://github.com/jquery/globalize](https://github.com/jquery/globalize) ) and JavaScript to use `Globalize.parseFloat`.</span></span> <span data-ttu-id="fad2e-183">您可以從 NuGet 來取得 jQuery 非英文驗證。</span><span class="sxs-lookup"><span data-stu-id="fad2e-183">You can get the jQuery non-English validation from NuGet.</span></span> <span data-ttu-id="fad2e-184">（請勿安裝 Globalize 如果您使用英文地區設定。）</span><span class="sxs-lookup"><span data-stu-id="fad2e-184">(Don't install Globalize if you are using a English locale.)</span></span>


1. <span data-ttu-id="fad2e-185">從**工具**功能表上，按一下**NuGetLibrary 封裝管理員**，然後按一下 **管理方案的 NuGet 套件**。</span><span class="sxs-lookup"><span data-stu-id="fad2e-185">From the **Tools** menu click **NuGetLibrary Package Manager**, and then click **Manage NuGet Packages for Solution**.</span></span>  
  
    ![](examining-the-edit-methods-and-edit-view/_static/image5.png)
2. <span data-ttu-id="fad2e-186">在左窗格中，選取**瀏覽*。** * （請參閱下面的影像）。</span><span class="sxs-lookup"><span data-stu-id="fad2e-186">On the left pane, select **Browse*.***(See the image below.)</span></span>
3. <span data-ttu-id="fad2e-187">在輸入方塊中，輸入*Globalize**。</span><span class="sxs-lookup"><span data-stu-id="fad2e-187">In the input box, enter *Globalize**.</span></span>  
  
    <span data-ttu-id="fad2e-188">![](examining-the-edit-methods-and-edit-view/_static/image6.png)選擇`jQuery.Validation.Globalize`，選擇`MvcMovie`按一下**安裝**。</span><span class="sxs-lookup"><span data-stu-id="fad2e-188">![](examining-the-edit-methods-and-edit-view/_static/image6.png) Choose `jQuery.Validation.Globalize`, choose `MvcMovie` and click **Install**.</span></span> <span data-ttu-id="fad2e-189">*Scripts\jquery.globalize\globalize.js*檔案會加入至您的專案。</span><span class="sxs-lookup"><span data-stu-id="fad2e-189">The *Scripts\jquery.globalize\globalize.js* file will be added to your project.</span></span> <span data-ttu-id="fad2e-190">*Scripts\jquery.globalize\cultures\*資料夾將包含多個文化特性的 JavaScript 檔案。</span><span class="sxs-lookup"><span data-stu-id="fad2e-190">The *Scripts\jquery.globalize\cultures\* folder will contain many culture JavaScript files.</span></span> <span data-ttu-id="fad2e-191">請注意，可能需要五分鐘才能安裝此套件。</span><span class="sxs-lookup"><span data-stu-id="fad2e-191">Note, it may take five minutes to install this package.</span></span>

 <span data-ttu-id="fad2e-192">下列程式碼顯示 Views\Movies\Edit.cshtml 檔案的修改：</span><span class="sxs-lookup"><span data-stu-id="fad2e-192">The following code shows the modifications to the Views\Movies\Edit.cshtml file:</span></span> 

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample10.cshtml)]

<span data-ttu-id="fad2e-193">若要避免重複此程式碼中的每個編輯檢視，您可以將其移動至版面配置檔案。</span><span class="sxs-lookup"><span data-stu-id="fad2e-193">To avoid repeating this code in every Edit view, you can move it to the layout file.</span></span> <span data-ttu-id="fad2e-194">若要最佳化的指令碼下載，請參閱我教學課程[組合和縮製](../../performance/bundling-and-minification.md)。</span><span class="sxs-lookup"><span data-stu-id="fad2e-194">To optimize the script download, see my tutorial [Bundling and Minification](../../performance/bundling-and-minification.md).</span></span>

<span data-ttu-id="fad2e-195">如需詳細資訊，請參閱[ASP.NET MVC 3 國際化](http://afana.me/post/aspnet-mvc-internationalization.aspx)和[ASP.NET MVC 3 國際化-第 2 部分 (NerdDinner)](http://afana.me/post/aspnet-mvc-internationalization-part-2.aspx)。</span><span class="sxs-lookup"><span data-stu-id="fad2e-195">For more information see [ASP.NET MVC 3 Internationalization](http://afana.me/post/aspnet-mvc-internationalization.aspx) and [ASP.NET MVC 3 Internationalization - Part 2 (NerdDinner)](http://afana.me/post/aspnet-mvc-internationalization-part-2.aspx).</span></span>

<span data-ttu-id="fad2e-196">為暫時修正，如果您無法取得您的地區設定中使用的驗證，您可以強制電腦使用英文 （美國），或您可以使用停用 JavaScript 瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="fad2e-196">As a temporary fix, if you can't get validation working in your locale, you can force your computer to use US English or you can disable JavaScript in your browser.</span></span> <span data-ttu-id="fad2e-197">若要強制電腦使用英文 （美國），您可以將全球化項目加入專案根*web.config*檔案。</span><span class="sxs-lookup"><span data-stu-id="fad2e-197">To force your computer to use US English, you can add the globalization element to the projects root *web.config* file.</span></span> <span data-ttu-id="fad2e-198">下列程式碼會顯示與設定為 英文 （美國） 文化特性的全球化項目。</span><span class="sxs-lookup"><span data-stu-id="fad2e-198">The following code shows the globalization element with the culture set to United States English.</span></span>

[!code-xml[Main](examining-the-edit-methods-and-edit-view/samples/sample11.xml)]

<a id="gettingstarted"></a><span data-ttu-id="fad2e-199"><a id="jQueryAjaxJSON"></a>在下一個教學課程中，我們將實作搜尋功能。</span><span class="sxs-lookup"><span data-stu-id="fad2e-199"><a id="jQueryAjaxJSON"></a> In the next tutorial, we'll implement search functionality.</span></span>

>[!div class="step-by-step"]
<span data-ttu-id="fad2e-200">[上一頁](accessing-your-models-data-from-a-controller.md)
[下一頁](adding-search.md)</span><span class="sxs-lookup"><span data-stu-id="fad2e-200">[Previous](accessing-your-models-data-from-a-controller.md)
[Next](adding-search.md)</span></span>