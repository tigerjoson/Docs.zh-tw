---
uid: web-forms/overview/older-versions-getting-started/deploying-web-site-projects/users-and-roles-on-the-production-website-vb
title: "使用者和角色在生產網站 (VB) |Microsoft 文件"
author: rick-anderson
description: "ASP.NET 網站管理工具 (WSAT) 提供網頁型使用者介面，來設定成員資格和角色設定，以及如何建立、 編輯、..."
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
ms.contentlocale: zh-TW
ms.lasthandoff: 11/10/2017
---
<a name="users-and-roles-on-the-production-website-vb"></a><span data-ttu-id="4f7fe-103">使用者和角色在生產網站 (VB)</span><span class="sxs-lookup"><span data-stu-id="4f7fe-103">Users and Roles On The Production Website (VB)</span></span>
====================
<span data-ttu-id="4f7fe-104">由[Scott Mitchell](https://twitter.com/ScottOnWriting)</span><span class="sxs-lookup"><span data-stu-id="4f7fe-104">by [Scott Mitchell](https://twitter.com/ScottOnWriting)</span></span>

[<span data-ttu-id="4f7fe-105">下載 PDF</span><span class="sxs-lookup"><span data-stu-id="4f7fe-105">Download PDF</span></span>](http://download.microsoft.com/download/5/C/5/5C57DB8C-5DEA-4B3A-92CA-4405544D313B/aspnet_tutorial16_CustomAWAT_vb.pdf)

> <span data-ttu-id="4f7fe-106">ASP.NET 網站管理工具 (WSAT) 提供網頁型使用者介面來設定成員資格和角色設定以及建立、 編輯和刪除使用者和角色。</span><span class="sxs-lookup"><span data-stu-id="4f7fe-106">The ASP.NET Website Administration Tool (WSAT) provides a web-based user interface for configuring Membership and Roles settings and for creating, editing, and deleting users and roles.</span></span> <span data-ttu-id="4f7fe-107">不幸的是，WSAT 只適用於瀏覽從 localhost，這表示您無法透過瀏覽器連線生產網站管理工具。</span><span class="sxs-lookup"><span data-stu-id="4f7fe-107">Unfortunately, the WSAT only works when visited from localhost, meaning that you cannot reach the production website's Administration Tool through your browser.</span></span> <span data-ttu-id="4f7fe-108">好消息是因應措施，可讓您能夠管理使用者和實際執行的角色。</span><span class="sxs-lookup"><span data-stu-id="4f7fe-108">The good news is that there are workarounds that make it possible to manage users and roles on production.</span></span> <span data-ttu-id="4f7fe-109">本教學課程會查看這些因應措施和其他項目。</span><span class="sxs-lookup"><span data-stu-id="4f7fe-109">This tutorial looks at these workarounds and others.</span></span>


## <a name="introduction"></a><span data-ttu-id="4f7fe-110">簡介</span><span class="sxs-lookup"><span data-stu-id="4f7fe-110">Introduction</span></span>

<span data-ttu-id="4f7fe-111">ASP.NET 2.0 導入了一些*應用程式服務*，其為套件，您可以加入您的 web 應用程式的建置組塊服務。</span><span class="sxs-lookup"><span data-stu-id="4f7fe-111">ASP.NET 2.0 introduced a number of *application services*, which are a suite of building block services that you can add to your web application.</span></span> <span data-ttu-id="4f7fe-112">我們加入活頁簿檢閱網站的成員資格和角色服務回[*設定網站，會使用應用程式服務*教學課程](configuring-a-website-that-uses-application-services-vb.md)。</span><span class="sxs-lookup"><span data-stu-id="4f7fe-112">We added the Membership and Roles services to the Book Reviews website back in the [*Configuring a Website That Uses Application Services* tutorial](configuring-a-website-that-uses-application-services-vb.md).</span></span> <span data-ttu-id="4f7fe-113">成員資格服務可協助建立和管理使用者帳戶。角色服務提供應用程式開發介面，使用者分類成群組。</span><span class="sxs-lookup"><span data-stu-id="4f7fe-113">The Membership service facilitates creating and managing user accounts; the Roles service offers an API for categorizing users into groups.</span></span> <span data-ttu-id="4f7fe-114">活頁簿檢閱站台具有三個使用者帳戶-Scott、 Jisun，和 Alice 層及的系統管理員，Scott 與 Jisun 系統管理員角色中的角色。</span><span class="sxs-lookup"><span data-stu-id="4f7fe-114">The Book Reviews site has three user accounts - Scott, Jisun, and Alice - and a single role, Admin, with Scott and Jisun in the Admin role.</span></span>

<span data-ttu-id="4f7fe-115">ASP。網路的應用程式服務並不限於特定的實作。</span><span class="sxs-lookup"><span data-stu-id="4f7fe-115">ASP.NET's application services are not tied to a specific implementation.</span></span> <span data-ttu-id="4f7fe-116">相反地，您可以指示需要使用特定的應用程式服務*提供者*，和該提供者會實作使用特定技術的服務。</span><span class="sxs-lookup"><span data-stu-id="4f7fe-116">Instead, you instruct the application services to use a particular *provider*, and that provider implements the service using a particular technology.</span></span> <span data-ttu-id="4f7fe-117">我們設定活頁簿檢閱 web 應用程式使用`SqlMembershipProvider`和`SqlRoleProvider`成員資格和角色服務提供者。</span><span class="sxs-lookup"><span data-stu-id="4f7fe-117">We configured the Book Reviews web application to use the `SqlMembershipProvider` and `SqlRoleProvider` providers for the Membership and Roles services.</span></span> <span data-ttu-id="4f7fe-118">這些兩個提供者使用者帳戶和角色的資訊儲存在 SQL Server 資料庫和裝載在虛擬主機公司以網際網路為基礎的 web 應用程式最常使用的提供者。</span><span class="sxs-lookup"><span data-stu-id="4f7fe-118">These two providers store user account and role information in a SQL Server database and are the most commonly used providers for Internet-based web applications hosted at a web hosting company.</span></span>

<span data-ttu-id="4f7fe-119">開發人員使用的成員資格和角色服務的常見挑戰管理使用者和角色在實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="4f7fe-119">A common challenge for developers using the Membership and Roles services is managing the users and roles on the production environment.</span></span> <span data-ttu-id="4f7fe-120">您如何從生產網站刪除使用者帳戶、 加入新的角色，或將現有使用者加入至現有的角色？</span><span class="sxs-lookup"><span data-stu-id="4f7fe-120">How do you delete a user account from the production website, add a new role, or add an existing user to an existing role?</span></span> <span data-ttu-id="4f7fe-121">本教學課程中，瀏覽不同技術可管理使用者和生產性網站上的角色。</span><span class="sxs-lookup"><span data-stu-id="4f7fe-121">This tutorial explores different techniques for managing users and roles on the production website.</span></span>

## <a name="using-the-aspnet-web-site-administration-tool"></a><span data-ttu-id="4f7fe-122">使用 ASP.NET 網頁站台系統管理工具</span><span class="sxs-lookup"><span data-stu-id="4f7fe-122">Using the ASP.NET Web Site Administration Tool</span></span>

<span data-ttu-id="4f7fe-123">ASP.NET 包含[網站管理工具](https://msdn.microsoft.com/en-us/library/yy40ytx0.aspx)(WSAT)，能讓您輕鬆建立及管理使用者帳戶和角色，並指定使用者和角色為基礎的授權規則。</span><span class="sxs-lookup"><span data-stu-id="4f7fe-123">ASP.NET includes a [Web Site Administration Tool](https://msdn.microsoft.com/en-us/library/yy40ytx0.aspx) (WSAT) that makes it easy to create and manage user accounts and roles and to specify user- and role-based authorization rules.</span></span> <span data-ttu-id="4f7fe-124">若要使用 WSAT，按一下 [ASP.NET 組態] 圖示，在 [方案總管] 中，或移至 [網站] 或 [專案] 功能表並選擇 [ASP.NET 組態] 選項。</span><span class="sxs-lookup"><span data-stu-id="4f7fe-124">To use the WSAT, click the ASP.NET Configuration icon in the Solution Explorer, or go to the Website or Project menu and choose the ASP.NET Configuration option.</span></span> <span data-ttu-id="4f7fe-125">兩種方法啟動網頁瀏覽器並指向 WSAT 在的地址如下：`http://localhost:portNumber/asp.netwebadminfiles/default.aspx?applicationPhysicalPath=pathToApplication`</span><span class="sxs-lookup"><span data-stu-id="4f7fe-125">Either approach launches a web browser and points it to the WSAT at an address like: `http://localhost:portNumber/asp.netwebadminfiles/default.aspx?applicationPhysicalPath=pathToApplication`</span></span>

<span data-ttu-id="4f7fe-126">WSAT 分成三個區段：</span><span class="sxs-lookup"><span data-stu-id="4f7fe-126">The WSAT is divided into three sections:</span></span>

- <span data-ttu-id="4f7fe-127">**安全性**-管理使用者、 角色和授權規則。</span><span class="sxs-lookup"><span data-stu-id="4f7fe-127">**Security** - manage users, roles, and authorization rules.</span></span>
- <span data-ttu-id="4f7fe-128">**ApplicationConfiguration** -管理&lt;appSettings&gt;和從這裡的 SMTP 設定。</span><span class="sxs-lookup"><span data-stu-id="4f7fe-128">**ApplicationConfiguration** - manage the &lt;appSettings&gt; and SMTP settings from here.</span></span> <span data-ttu-id="4f7fe-129">您可以也離線應用程式和管理偵錯和追蹤從這裡的設定，以及指定預設的自訂錯誤網頁。</span><span class="sxs-lookup"><span data-stu-id="4f7fe-129">You can also take the application offline and manage debugging and tracing settings from here, as well as specify the default custom error page.</span></span>
- <span data-ttu-id="4f7fe-130">**ProviderConfiguration** -設定應用程式服務所使用的提供者。</span><span class="sxs-lookup"><span data-stu-id="4f7fe-130">**ProviderConfiguration** - configure the providers used by the application services.</span></span>

<span data-ttu-id="4f7fe-131">[安全性] 區段 (示**圖 1**) 包含的連結，建立新使用者、 管理使用者、 建立和管理角色，以及建立及管理存取規則。</span><span class="sxs-lookup"><span data-stu-id="4f7fe-131">The Security section (shown in **Figure 1**) includes links for creating new users, managing users, creating and managing roles, and creating and managing access rules.</span></span> <span data-ttu-id="4f7fe-132">從這裡您可以將新角色加入至系統、 刪除現有的使用者，或新增或移除特定使用者帳戶的角色。</span><span class="sxs-lookup"><span data-stu-id="4f7fe-132">From here you can add a new role to the system, delete an existing user, or add or remove roles from a particular user account.</span></span>

[![](users-and-roles-on-the-production-website-vb/_static/image2.png)](users-and-roles-on-the-production-website-vb/_static/image1.png)

<span data-ttu-id="4f7fe-133">**圖 1**: WSAT 安全性 > 一節包含用於管理使用者和角色選項</span><span class="sxs-lookup"><span data-stu-id="4f7fe-133">**Figure 1**: The WSAT Security Section Includes Options for Managing Users and Roles</span></span>  
<span data-ttu-id="4f7fe-134">([按一下以檢視完整大小的影像](users-and-roles-on-the-production-website-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="4f7fe-134">([Click to view full-size image](users-and-roles-on-the-production-website-vb/_static/image3.png))</span></span>

<span data-ttu-id="4f7fe-135">不幸的是，WSAT 才可存取在本機。</span><span class="sxs-lookup"><span data-stu-id="4f7fe-135">Unfortunately, the WSAT is only accessible locally.</span></span> <span data-ttu-id="4f7fe-136">您無法在遠端的生產網站; 瀏覽 WSAT如果您瀏覽`www.yoursite.com/asp.netwebadminfiles/default.aspx`取得 404 找不到回應。</span><span class="sxs-lookup"><span data-stu-id="4f7fe-136">You cannot visit the WSAT on your remote production website; if you visit `www.yoursite.com/asp.netwebadminfiles/default.aspx` you get a 404 Not Found response.</span></span> <span data-ttu-id="4f7fe-137">可提供簡單的 WSAT 用途的程式碼`Membership`和`Roles`類別在.NET Framework 來建立、 編輯和刪除使用者和角色。</span><span class="sxs-lookup"><span data-stu-id="4f7fe-137">The code that powers the WSAT uses the `Membership` and `Roles` classes in the .NET Framework to create, edit, and delete users and roles.</span></span> <span data-ttu-id="4f7fe-138">這些類別，請參閱 web 應用程式的組態資訊來判斷何種提供者使用。回到[*設定網站，會使用應用程式服務*教學課程](configuring-a-website-that-uses-application-services-vb.md)在我們設定的活頁簿檢閱網站使用`SqlMembershipProvider`和`SqlRoleProvider`提供者。</span><span class="sxs-lookup"><span data-stu-id="4f7fe-138">These classes consult the web application's configuration information to determine what provider to use; back in the [*Configuring a Website That Uses Application Services* tutorial](configuring-a-website-that-uses-application-services-vb.md) we setup the Book Reviews website to use the `SqlMembershipProvider` and `SqlRoleProvider` providers.</span></span> <span data-ttu-id="4f7fe-139">這有權從頭加入`<membership>`和`<roleManager>`區段`Web.config`。</span><span class="sxs-lookup"><span data-stu-id="4f7fe-139">This entailed adding `<membership>` and `<roleManager>` sections to `Web.config`.</span></span>

[!code-xml[Main](users-and-roles-on-the-production-website-vb/samples/sample1.xml)]

<span data-ttu-id="4f7fe-140">請注意，`<membership>`和`<roleManager>`區段參考`SqlMembershipProvider`和`SqlRoleProvider`中的提供者及其`type`分別屬性。</span><span class="sxs-lookup"><span data-stu-id="4f7fe-140">Note that the `<membership>` and `<roleManager>` sections reference the `SqlMembershipProvider` and `SqlRoleProvider` providers in their `type` attribute, respectively.</span></span> <span data-ttu-id="4f7fe-141">這些提供者的使用者和角色資訊儲存在指定的 SQL Server 資料庫。</span><span class="sxs-lookup"><span data-stu-id="4f7fe-141">These providers store the user and role information in a specified SQL Server database.</span></span> <span data-ttu-id="4f7fe-142">這些提供者所使用的資料庫由指定`connectionStringName`屬性`ReviewsConnectionString`，定義在`~/ConfigSections/databaseConnectionStrings.config`檔案。</span><span class="sxs-lookup"><span data-stu-id="4f7fe-142">The database used by these providers is specified by the `connectionStringName` attribute, `ReviewsConnectionString`, which is defined in the `~/ConfigSections/databaseConnectionStrings.config` file.</span></span> <span data-ttu-id="4f7fe-143">請記得，`databaseConnectionStrings.config`開發環境中的檔案包含開發資料庫的連接字串，而`databaseConnectionStrings.config`實際執行的檔案包含實際執行資料庫的連接字串。</span><span class="sxs-lookup"><span data-stu-id="4f7fe-143">Recall that the `databaseConnectionStrings.config` file in the development environment contains the connection string to the development database whereas the `databaseConnectionStrings.config` file on production contains the connection string to the production database.</span></span>

<span data-ttu-id="4f7fe-144">簡而言之，WSAT 必須透過在本機開發環境中，及使用者和角色資訊中指定的資料庫中將它用於`databaseConnectionStrings.config`檔案。</span><span class="sxs-lookup"><span data-stu-id="4f7fe-144">In a nutshell, the WSAT must be accessed locally through the development environment, and it works with the user and role information in the database specified in the `databaseConnectionStrings.config` file.</span></span> <span data-ttu-id="4f7fe-145">因此，若我們變更中的連接字串資訊`databaseConnectionStrings.config`檔案在開發環境上我們可以使用 WSAT 本機來管理使用者和實際執行環境中的角色。</span><span class="sxs-lookup"><span data-stu-id="4f7fe-145">Consequently, if we change the connection string information in the `databaseConnectionStrings.config` file on the development environment we can use the WSAT locally to manage users and roles in the production environment.</span></span>

<span data-ttu-id="4f7fe-146">為了說明這項功能，開啟`databaseConnectionStrings.config`檔案在 Visual Studio 開發環境和開發資料庫連接字串取代為實際執行資料庫連接字串。</span><span class="sxs-lookup"><span data-stu-id="4f7fe-146">To illustrate this functionality, open the `databaseConnectionStrings.config` file in Visual Studio on the development environment and replace the development database connection string with the production database connection string.</span></span> <span data-ttu-id="4f7fe-147">然後啟動 WSAT，請 [安全性] 索引標籤中，加入新的使用者名稱和密碼"password"！ Sam</span><span class="sxs-lookup"><span data-stu-id="4f7fe-147">Then launch the WSAT, go the Security tab, and add a new user named Sam with password "password!"</span></span> <span data-ttu-id="4f7fe-148">（小於的引號）。</span><span class="sxs-lookup"><span data-stu-id="4f7fe-148">(less the quotation marks).</span></span> <span data-ttu-id="4f7fe-149">**圖 2**顯示 WSAT 螢幕時建立此帳戶。</span><span class="sxs-lookup"><span data-stu-id="4f7fe-149">**Figure 2** shows the WSAT screen when creating this account.</span></span>

[![](users-and-roles-on-the-production-website-vb/_static/image5.png)](users-and-roles-on-the-production-website-vb/_static/image4.png)

<span data-ttu-id="4f7fe-150">**圖 2**： 建立名為 Sam 實際執行環境中的新使用者</span><span class="sxs-lookup"><span data-stu-id="4f7fe-150">**Figure 2**: Create a New User Named Sam In the Production Environment</span></span>  
<span data-ttu-id="4f7fe-151">([按一下以檢視完整大小的影像](users-and-roles-on-the-production-website-vb/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="4f7fe-151">([Click to view full-size image](users-and-roles-on-the-production-website-vb/_static/image6.png))</span></span>

<span data-ttu-id="4f7fe-152">因為我們變更中的連接字串`databaseConnectionStrings.config`指向實際資料庫伺服器，Sam 將會加入做為實際執行環境中的使用者。</span><span class="sxs-lookup"><span data-stu-id="4f7fe-152">Because we changed the connection string in `databaseConnectionStrings.config` to point to the production database server, Sam was added as a user in the production environment.</span></span> <span data-ttu-id="4f7fe-153">若要確認這種情況，變更連接字串中的`databaseConnectionStrings.config`傳回至開發資料庫檔案，然後瀏覽`Login.aspx`開發環境中的頁面。</span><span class="sxs-lookup"><span data-stu-id="4f7fe-153">To verify this, change the connection string in the `databaseConnectionStrings.config` file back to the development database and then visit the `Login.aspx` page in the development environment.</span></span> <span data-ttu-id="4f7fe-154">嘗試以 Sam 登入 (請參閱**圖 3**)。</span><span class="sxs-lookup"><span data-stu-id="4f7fe-154">Try to sign in as Sam (see **Figure 3**).</span></span>

[![](users-and-roles-on-the-production-website-vb/_static/image8.png)](users-and-roles-on-the-production-website-vb/_static/image7.png)

<span data-ttu-id="4f7fe-155">**圖 3**： 您無法在開發環境中的 Sam 身分登入</span><span class="sxs-lookup"><span data-stu-id="4f7fe-155">**Figure 3**: You Cannot Sign In As Sam in the Development Environment</span></span>  
<span data-ttu-id="4f7fe-156">([按一下以檢視完整大小的影像](users-and-roles-on-the-production-website-vb/_static/image9.png))</span><span class="sxs-lookup"><span data-stu-id="4f7fe-156">([Click to view full-size image](users-and-roles-on-the-production-website-vb/_static/image9.png))</span></span>

<span data-ttu-id="4f7fe-157">您無法登入為 Sam 開發環境中因為本機資料庫中不存在的使用者帳戶資訊。</span><span class="sxs-lookup"><span data-stu-id="4f7fe-157">You cannot sign in as Sam in the development environment because the user account information does not exist in the local database.</span></span> <span data-ttu-id="4f7fe-158">而是會加入至實際執行資料庫。</span><span class="sxs-lookup"><span data-stu-id="4f7fe-158">Rather, is was added to the production database.</span></span> <span data-ttu-id="4f7fe-159">若要確認這種情況，檢視的內容`aspnet_Users`開發和生產資料庫中的資料表。</span><span class="sxs-lookup"><span data-stu-id="4f7fe-159">To verify this, view the contents of the `aspnet_Users` table in both the development and production databases.</span></span> <span data-ttu-id="4f7fe-160">在開發環境中應該只有 3 個記錄 Scott、 Jisun 及 Alice 的使用者。</span><span class="sxs-lookup"><span data-stu-id="4f7fe-160">In the development environment there should be only three records for users Scott, Jisun, and Alice.</span></span> <span data-ttu-id="4f7fe-161">不過，`aspnet_Users`生產資料庫中的資料表有四個記錄： Scott、 Jisun、 Alice 和 Sam。</span><span class="sxs-lookup"><span data-stu-id="4f7fe-161">However, the `aspnet_Users` table in the production database has four records: Scott, Jisun, Alice, and Sam.</span></span> <span data-ttu-id="4f7fe-162">因此，Sam 可以登入，透過網站在生產環境中，但不是能透過開發環境。</span><span class="sxs-lookup"><span data-stu-id="4f7fe-162">Consequently, Sam can sign in through the website in production, but not through the development environment.</span></span>

[![](users-and-roles-on-the-production-website-vb/_static/image11.png)](users-and-roles-on-the-production-website-vb/_static/image10.png)

<span data-ttu-id="4f7fe-163">**圖 4**: Sam 生產網站上，可以登入</span><span class="sxs-lookup"><span data-stu-id="4f7fe-163">**Figure 4**: Sam Can Sign In On the Production Website</span></span>  
<span data-ttu-id="4f7fe-164">([按一下以檢視完整大小的影像](users-and-roles-on-the-production-website-vb/_static/image12.png))</span><span class="sxs-lookup"><span data-stu-id="4f7fe-164">([Click to view full-size image](users-and-roles-on-the-production-website-vb/_static/image12.png))</span></span>

> [!NOTE]
> <span data-ttu-id="4f7fe-165">別忘了變更連接字串中的`databaseConnectionStrings.config`開發資料庫檔案的連接字串，當您完成 wsat 否則您會使用實際執行資料與測試的開發網站時使用環境。</span><span class="sxs-lookup"><span data-stu-id="4f7fe-165">Don't forget to change the connection string in the `databaseConnectionStrings.config` file back to the development database's connect string when you're done working with the WSAT otherwise you will be working with production data when testing the site through the development environment.</span></span> <span data-ttu-id="4f7fe-166">也請注意，我們剛才所討論的技術可讓我們使用 WSAT 遠端管理使用者和角色，任何其他 WSAT 設定選項 （存取規則、 SMTP 設定、 偵錯和追蹤設定，以及等等） 的變更會修改`Web.config`檔案。</span><span class="sxs-lookup"><span data-stu-id="4f7fe-166">Also keep in mind that while the technique we just discussed allows us to use the WSAT to remotely manage users and roles, changes to any of the other WSAT configuration options (access rules, SMTP settings, debugging and tracing settings, and so on) modify the `Web.config` file.</span></span> <span data-ttu-id="4f7fe-167">因此，對設定進行任何變更將套用至開發環境，而不實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="4f7fe-167">Consequently, any changes made to the settings apply to the development environment and not to the production environment.</span></span>


## <a name="creating-custom-user-and-role-management-web-pages"></a><span data-ttu-id="4f7fe-168">建立自訂的使用者和角色管理 Web 網頁</span><span class="sxs-lookup"><span data-stu-id="4f7fe-168">Creating Custom User and Role Management Web Pages</span></span>

<span data-ttu-id="4f7fe-169">WSAT 提供的系統管理使用者和角色，但只能在本機上啟動，而且需要對連接字串資訊中的變更，以便管理使用者和實際執行的角色。</span><span class="sxs-lookup"><span data-stu-id="4f7fe-169">The WSAT provides an out of the box system for managing users and roles, but can only be launched locally and requires making changes to the connection string information in order to manage the users and roles on production.</span></span> <span data-ttu-id="4f7fe-170">大多數的網站，以支援使用者帳戶也會包含使用者和角色管理網頁可讓系統管理員管理使用者和角色，從站台內的頁面數目。</span><span class="sxs-lookup"><span data-stu-id="4f7fe-170">Most websites that support user accounts also include a number of user and role administration web pages that enable administrators to manage users and roles from pages within the site.</span></span> <span data-ttu-id="4f7fe-171">更輕鬆地管理使用者和角色進行這類 web 為基礎的管理頁面，並是不可或缺的站台其中可能有許多系統管理員或不具有存取權或使用 Visual Studio 啟動 WSAT 技術背景的系統管理員。</span><span class="sxs-lookup"><span data-stu-id="4f7fe-171">Such web-based administration pages make it much easier to manage users and roles and are essential for sites where there may be many administrators or administrators that do not have access to or the technical background to use Visual Studio to launch the WSAT.</span></span>

<span data-ttu-id="4f7fe-172">ASP.NET 包含一些內建實作許多這些系統管理網頁簡單，拖曳和卸除的登入相關的 Web 控制項。</span><span class="sxs-lookup"><span data-stu-id="4f7fe-172">ASP.NET includes a number of built-in Login-related Web controls that make implementing many of these administrative web pages as easy as drag and drop.</span></span> <span data-ttu-id="4f7fe-173">例如，您可以建立適用於 CreateUserWizard 控制項拖曳到頁面，並設定一些屬性，以建立新的使用者帳戶的系統管理員的頁面。</span><span class="sxs-lookup"><span data-stu-id="4f7fe-173">For example, you can create a page for administrators to create a new user account by dragging the CreateUserWizard control onto the page and setting a few properties.</span></span> <span data-ttu-id="4f7fe-174">事實上，在所示的 WSAT 中建立使用者頁面**圖 2**使用相同的適用於 CreateUserWizard 控制項，您可以加入至您的頁面。</span><span class="sxs-lookup"><span data-stu-id="4f7fe-174">In fact, the page for creating users in the WSAT shown in **Figure 2** uses the same CreateUserWizard control that you can add to your pages.</span></span> <span data-ttu-id="4f7fe-175">此外，成員資格和角色服務的功能都是以程式設計方式透過`Membership`和`Roles`.NET Framework 中的類別。</span><span class="sxs-lookup"><span data-stu-id="4f7fe-175">Furthermore, the Membership and Roles services' functionalities are available programmatically through the `Membership` and `Roles` classes in the .NET Framework.</span></span> <span data-ttu-id="4f7fe-176">使用這些類別中，您可以撰寫程式碼來建立、 編輯和刪除使用者和角色，以及新增或移除使用者角色，以判斷使用者是在何種角色，以及執行其他使用者和角色相關的工作。</span><span class="sxs-lookup"><span data-stu-id="4f7fe-176">With these classes you can write code to create, edit, and delete users and roles, as well as to add or remove users to roles, to determine what users are in what roles, and to perform other user- and role-related tasks.</span></span>

<span data-ttu-id="4f7fe-177">在[*設定網站，會使用應用程式服務*教學課程](configuring-a-website-that-uses-application-services-vb.md)我加入頁面的`Admin`資料夾名為`CreateAccount.aspx`。</span><span class="sxs-lookup"><span data-stu-id="4f7fe-177">In the [*Configuring a Website That Uses Application Services* tutorial](configuring-a-website-that-uses-application-services-vb.md) I added a page to the `Admin` folder named `CreateAccount.aspx`.</span></span> <span data-ttu-id="4f7fe-178">此頁面可讓系統管理員將新的使用者帳戶新增至站台，以及指定新建立的使用者是否為系統管理員角色中 (請參閱**圖 5**)。</span><span class="sxs-lookup"><span data-stu-id="4f7fe-178">This page allows an administrator to add a new user account to the site and to specify whether or not the newly created user is in the Admin role (see **Figure 5**).</span></span>

[![](users-and-roles-on-the-production-website-vb/_static/image14.png)](users-and-roles-on-the-production-website-vb/_static/image13.png)

<span data-ttu-id="4f7fe-179">**圖 5**： 系統管理員可以建立新的使用者帳戶</span><span class="sxs-lookup"><span data-stu-id="4f7fe-179">**Figure 5**: Administrators Can Create New User Accounts</span></span>  
<span data-ttu-id="4f7fe-180">([按一下以檢視完整大小的影像](users-and-roles-on-the-production-website-vb/_static/image15.png))</span><span class="sxs-lookup"><span data-stu-id="4f7fe-180">([Click to view full-size image](users-and-roles-on-the-production-website-vb/_static/image15.png))</span></span>

<span data-ttu-id="4f7fe-181">建立使用者和角色 頁面，以及使用的逐步指示以詳細查看`Membership`和`Roles`類別和登入相關的 ASP.NET Web 控制項中，務必閱讀我[網站安全性教學課程](../../older-versions-security/introduction/security-basics-and-asp-net-support-cs.md)。</span><span class="sxs-lookup"><span data-stu-id="4f7fe-181">For a more detailed look at building user and role administration pages, along with step-by-step instructions on using the `Membership` and `Roles` classes and the Login-related ASP.NET Web controls, be sure to read my [Website Security Tutorials](../../older-versions-security/introduction/security-basics-and-asp-net-support-cs.md).</span></span> <span data-ttu-id="4f7fe-182">那里您可以找到相關指引如何建置網頁，來建立新的帳戶、 建立及管理角色，將使用者指派給角色，以及其他常見的管理工作。</span><span class="sxs-lookup"><span data-stu-id="4f7fe-182">There you'll find guidance on how to build web pages for creating new accounts, creating and managing roles, assigning users to roles, and other common administrative tasks.</span></span>

<span data-ttu-id="4f7fe-183">在生產網站上實作 WSAT 類似的功能，您可以一律建置自己的實作 WSAT 功能的網頁的序列。</span><span class="sxs-lookup"><span data-stu-id="4f7fe-183">To implement WSAT-like functionality on the production website you can always build your own series of web pages that implement the WSAT's features.</span></span> <span data-ttu-id="4f7fe-184">為了開始使用，請查看位於資料夾 WSAT 原始碼`%WINDIR%\Microsoft.NET\Framework\v2.0.50727\ASP.NETWebAdminFiles`。</span><span class="sxs-lookup"><span data-stu-id="4f7fe-184">To help get started, check out the WSAT source code, which is located in the folder `%WINDIR%\Microsoft.NET\Framework\v2.0.50727\ASP.NETWebAdminFiles`.</span></span> <span data-ttu-id="4f7fe-185">另一個選項是使用 Dan Clem WSAT 代替他共用在他的文章，[輪流您自己的網站管理工具](http://aspnet.4guysfromrolla.com/articles/052307-1.aspx)。</span><span class="sxs-lookup"><span data-stu-id="4f7fe-185">Another option is to use Dan Clem's WSAT alternative, which he shares in his article, [Rolling Your Own Web Site Administration Tool](http://aspnet.4guysfromrolla.com/articles/052307-1.aspx).</span></span> <span data-ttu-id="4f7fe-186">Dan 讀取器，透過建立自訂的 WSAT 類似工具的程序會逐步引導、 包含 （在 C# 中)，下載他的應用程式原始程式碼，並提供他自訂 WSAT 加入託管網站的逐步指示。</span><span class="sxs-lookup"><span data-stu-id="4f7fe-186">Dan walks readers through the process of building a custom WSAT-like tool, includes his application's source code for download (in C#), and gives step-by-step instructions for adding his custom WSAT to a hosted website.</span></span>

## <a name="summary"></a><span data-ttu-id="4f7fe-187">總結</span><span class="sxs-lookup"><span data-stu-id="4f7fe-187">Summary</span></span>

<span data-ttu-id="4f7fe-188">ASP.NET 網站管理工具 (WSAT) 可用的成員資格和角色的應用程式服務結合來管理使用者和角色的資訊，為您的網站。</span><span class="sxs-lookup"><span data-stu-id="4f7fe-188">The ASP.NET Web Site Administration Tool (WSAT) can be used in tandem with the Membership and Roles application services to manage user and role information for your website.</span></span> <span data-ttu-id="4f7fe-189">不幸的是，WSAT 才可存取在本機，而無法從生產網站中瀏覽。</span><span class="sxs-lookup"><span data-stu-id="4f7fe-189">Unfortunately, the WSAT is only accessible locally and cannot be visited from your production website.</span></span> <span data-ttu-id="4f7fe-190">不過，藉由變更連接字串，在開發環境，以點為實際執行資料庫可以使用 WSAT 管理使用者和生產性網站上的角色。</span><span class="sxs-lookup"><span data-stu-id="4f7fe-190">However, by changing the connection string in the development environment to point to the production database you can use the WSAT to manage the users and roles on the production website.</span></span>

<span data-ttu-id="4f7fe-191">雖然的 WSAT 方法提供快速簡便的方式來管理使用者和角色，它必須啟動 WSAT 從 Visual Studio，以及暫時變更連接字串資訊。</span><span class="sxs-lookup"><span data-stu-id="4f7fe-191">While the WSAT approach affords a quick and easy way to manage users and roles, it necessitates launching the WSAT from Visual Studio as well as temporary changes to the connection string information.</span></span> <span data-ttu-id="4f7fe-192">WSAT 提供快速的方式來管理使用者和角色在生產環境中，但是很麻煩，而且不適用於網站使用多個系統管理員或系統管理員不需要或不熟悉 Visual Studio 和 WSAT。</span><span class="sxs-lookup"><span data-stu-id="4f7fe-192">The WSAT offers a quick way to manage users and roles on production, but is cumbersome and does not work well for websites with multiple administrators or with administrators who do not have or are not familiar with Visual Studio and the WSAT.</span></span> <span data-ttu-id="4f7fe-193">基於這些理由，大多數支援使用者帳戶的網站包含一組系統管理的網頁。</span><span class="sxs-lookup"><span data-stu-id="4f7fe-193">For these reasons, most websites that support user accounts include a set of administrative web pages.</span></span> <span data-ttu-id="4f7fe-194">這類組的網頁就不需要 WSAT，並使用不同的系統管理使用者從任何電腦。</span><span class="sxs-lookup"><span data-stu-id="4f7fe-194">Such a set of web pages eliminates the need for the WSAT and used by various administrative users from any computer.</span></span>

<span data-ttu-id="4f7fe-195">祝您程式設計 ！</span><span class="sxs-lookup"><span data-stu-id="4f7fe-195">Happy Programming!</span></span>

### <a name="further-reading"></a><span data-ttu-id="4f7fe-196">進一步閱讀</span><span class="sxs-lookup"><span data-stu-id="4f7fe-196">Further Reading</span></span>

<span data-ttu-id="4f7fe-197">如需有關在本教學課程所討論的主題的詳細資訊，請參閱下列資源：</span><span class="sxs-lookup"><span data-stu-id="4f7fe-197">For more information on the topics discussed in this tutorial, refer to the following resources:</span></span>

- [<span data-ttu-id="4f7fe-198">正在檢查 ASP。網路的成員資格、 角色和設定檔</span><span class="sxs-lookup"><span data-stu-id="4f7fe-198">Examining ASP.NET's Membership, Roles, and Profile</span></span>](http://aspnet.4guysfromrolla.com/articles/120705-1.aspx)
- [<span data-ttu-id="4f7fe-199">復原您的網站管理工具</span><span class="sxs-lookup"><span data-stu-id="4f7fe-199">Rolling Your Own Web Site Administration Tool</span></span>](http://aspnet.4guysfromrolla.com/articles/052307-1.aspx)
- [<span data-ttu-id="4f7fe-200">網站管理工具概觀</span><span class="sxs-lookup"><span data-stu-id="4f7fe-200">Web Site Administration Tool Overview</span></span>](https://msdn.microsoft.com/en-us/library/yy40ytx0.aspx)
- [<span data-ttu-id="4f7fe-201">網站安全性教學課程</span><span class="sxs-lookup"><span data-stu-id="4f7fe-201">Website Security Tutorials</span></span>](../../older-versions-security/introduction/security-basics-and-asp-net-support-cs.md)

>[!div class="step-by-step"]
[<span data-ttu-id="4f7fe-202">上一步</span><span class="sxs-lookup"><span data-stu-id="4f7fe-202">Previous</span></span>](precompiling-your-website-vb.md)