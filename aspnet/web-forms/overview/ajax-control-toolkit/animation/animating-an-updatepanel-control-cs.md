---
uid: web-forms/overview/ajax-control-toolkit/animation/animating-an-updatepanel-control-cs
title: "建立動畫 UpdatePanel 控制項 (C#) |Microsoft 文件"
author: wenz
description: "動畫控制項在 ASP.NET AJAX Control Toolkit 不是只控制項，但若要將動畫加入至控制項的整個架構。 內容..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: e57f8c7c-3940-4bc0-9468-3a0ca69158ea
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/animating-an-updatepanel-control-cs
msc.type: authoredcontent
ms.openlocfilehash: 7e6d8954d2ec886994cdd723121e540b471131f6
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/10/2017
---
<a name="animating-an-updatepanel-control-c"></a><span data-ttu-id="f90f2-104">建立動畫 UpdatePanel 控制項 (C#)</span><span class="sxs-lookup"><span data-stu-id="f90f2-104">Animating an UpdatePanel Control (C#)</span></span>
====================
<span data-ttu-id="f90f2-105">由[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="f90f2-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="f90f2-106">[下載程式碼](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/UpdatePanelAnimation1.cs.zip)或[下載 PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/updatepanelanimation1CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="f90f2-106">[Download Code](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/UpdatePanelAnimation1.cs.zip) or [Download PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/updatepanelanimation1CS.pdf)</span></span>

> <span data-ttu-id="f90f2-107">動畫控制項在 ASP.NET AJAX Control Toolkit 不是只控制項，但若要將動畫加入至控制項的整個架構。</span><span class="sxs-lookup"><span data-stu-id="f90f2-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="f90f2-108">UpdatePanel 的內容，特殊的擴充項存在，高度依賴動畫 framework: UpdatePanelAnimation。</span><span class="sxs-lookup"><span data-stu-id="f90f2-108">For the contents of an UpdatePanel, a special extender exists that relies heavily on the animation framework: UpdatePanelAnimation.</span></span> <span data-ttu-id="f90f2-109">本教學課程會示範如何設定這類動畫的 UpdatePanel。</span><span class="sxs-lookup"><span data-stu-id="f90f2-109">This tutorial shows how to set up such an animation for an UpdatePanel.</span></span>


## <a name="overview"></a><span data-ttu-id="f90f2-110">概觀</span><span class="sxs-lookup"><span data-stu-id="f90f2-110">Overview</span></span>

<span data-ttu-id="f90f2-111">動畫控制項在 ASP.NET AJAX Control Toolkit 不是只控制項，但若要將動畫加入至控制項的整個架構。</span><span class="sxs-lookup"><span data-stu-id="f90f2-111">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="f90f2-112">內容的`UpdatePanel`，特殊的擴充項存在，高度依賴動畫 framework: `UpdatePanelAnimation`。</span><span class="sxs-lookup"><span data-stu-id="f90f2-112">For the contents of an `UpdatePanel`, a special extender exists that relies heavily on the animation framework: `UpdatePanelAnimation`.</span></span> <span data-ttu-id="f90f2-113">本教學課程示範如何設定這類的動畫`UpdatePanel`。</span><span class="sxs-lookup"><span data-stu-id="f90f2-113">This tutorial shows how to set up such an animation for an `UpdatePanel`.</span></span>

## <a name="steps"></a><span data-ttu-id="f90f2-114">步驟</span><span class="sxs-lookup"><span data-stu-id="f90f2-114">Steps</span></span>

<span data-ttu-id="f90f2-115">第一個步驟是包含如往常般`ScriptManager`頁面中，而 ASP.NET AJAX library 載入 Control Toolkit 可用：</span><span class="sxs-lookup"><span data-stu-id="f90f2-115">The first step is as usual to include the `ScriptManager` in the page so that the ASP.NET AJAX library is loaded and the Control Toolkit can be used:</span></span>

[!code-aspx[Main](animating-an-updatepanel-control-cs/samples/sample1.aspx)]

<span data-ttu-id="f90f2-116">在此案例中動畫會套用到 ASP.NET `Wizard` web 控制項位於`UpdatePanel`。</span><span class="sxs-lookup"><span data-stu-id="f90f2-116">The animation in this scenario will be applied to an ASP.NET `Wizard` web control residing in an `UpdatePanel`.</span></span> <span data-ttu-id="f90f2-117">（任意） 的三個步驟會提供觸發回傳足夠選項：</span><span class="sxs-lookup"><span data-stu-id="f90f2-117">Three (arbitrary) steps provide enough options to trigger postbacks:</span></span>

[!code-aspx[Main](animating-an-updatepanel-control-cs/samples/sample2.aspx)]

<span data-ttu-id="f90f2-118">所需的標記`UpdatePanelAnimationExtender`控制項是相當類似於使用的標記`AnimationExtender`。</span><span class="sxs-lookup"><span data-stu-id="f90f2-118">The markup necessary for the `UpdatePanelAnimationExtender` control is quite similar to the markup used for the `AnimationExtender`.</span></span> <span data-ttu-id="f90f2-119">在`TargetControlID`屬性我們提供`ID`的`UpdatePanel`以動畫方式顯示; 內`UpdatePanelAnimationExtender`控制項，`<Animations>`項目會保存 XML 標記的動畫。</span><span class="sxs-lookup"><span data-stu-id="f90f2-119">In the `TargetControlID` attribute we provide the `ID` of the `UpdatePanel` to animate; within the `UpdatePanelAnimationExtender` control, the `<Animations>` element holds XML markup for the animation(s).</span></span> <span data-ttu-id="f90f2-120">但是沒有一項差異： 事件和事件處理常式的數量會限制於`AnimationExtender`。</span><span class="sxs-lookup"><span data-stu-id="f90f2-120">However there is one difference: The amount of events and event handlers is limited in comparison to `AnimationExtender`.</span></span> <span data-ttu-id="f90f2-121">如`UpdatePanels`，只有兩個其中存在：</span><span class="sxs-lookup"><span data-stu-id="f90f2-121">For `UpdatePanels`, only two of them exist:</span></span>

- <span data-ttu-id="f90f2-122">`<OnUpdated>`UpdatePanel 更新時</span><span class="sxs-lookup"><span data-stu-id="f90f2-122">`<OnUpdated>` when the UpdatePanel has been updated</span></span>
- <span data-ttu-id="f90f2-123">`<OnUpdating>`UpdatePanel 開始更新</span><span class="sxs-lookup"><span data-stu-id="f90f2-123">`<OnUpdating>` when the UpdatePanel starts updating</span></span>

<span data-ttu-id="f90f2-124">在此案例中，新的內容`UpdatePanel`（之後回傳） 應該會淡入。</span><span class="sxs-lookup"><span data-stu-id="f90f2-124">In this scenario, the new content of the `UpdatePanel` (after the postback) shall fade in.</span></span> <span data-ttu-id="f90f2-125">這是必要的標記：</span><span class="sxs-lookup"><span data-stu-id="f90f2-125">This is the necessary markup for that:</span></span>

[!code-aspx[Main](animating-an-updatepanel-control-cs/samples/sample3.aspx)]

<span data-ttu-id="f90f2-126">現在每次回傳發生 UpdatePanel 內時，新面板的內容會淡入順暢。</span><span class="sxs-lookup"><span data-stu-id="f90f2-126">Now whenever a postback occurs within the UpdatePanel, the new contents of the panel fade in smoothly.</span></span>


<span data-ttu-id="f90f2-127">[![下一個精靈步驟淡入](animating-an-updatepanel-control-cs/_static/image2.png)](animating-an-updatepanel-control-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="f90f2-127">[![The next wizard step is fading in](animating-an-updatepanel-control-cs/_static/image2.png)](animating-an-updatepanel-control-cs/_static/image1.png)</span></span>

<span data-ttu-id="f90f2-128">下一個精靈步驟淡入 ([按一下以檢視完整大小的影像](animating-an-updatepanel-control-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="f90f2-128">The next wizard step is fading in ([Click to view full-size image](animating-an-updatepanel-control-cs/_static/image3.png))</span></span>

>[!div class="step-by-step"]
<span data-ttu-id="f90f2-129">[上一頁](changing-an-animation-using-client-side-code-cs.md)
[下一頁](dynamically-controlling-updatepanel-animations-cs.md)</span><span class="sxs-lookup"><span data-stu-id="f90f2-129">[Previous](changing-an-animation-using-client-side-code-cs.md)
[Next](dynamically-controlling-updatepanel-animations-cs.md)</span></span>