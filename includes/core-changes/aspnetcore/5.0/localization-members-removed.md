---
ms.openlocfilehash: 6deeb7debce9b731f3871b7de0ad8df8a8cdafea
ms.sourcegitcommit: 7370aa8203b6036cea1520021b5511d0fd994574
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/02/2020
ms.locfileid: "82728307"
---
### <a name="localization-resourcemanagerwithculturestringlocalizer-class-and-withculture-interface-member-removed"></a><span data-ttu-id="c2b56-101">本地化：ResourceManagerWithCultureStringLocalizer 类和 WithCulture 接口成员已删除</span><span class="sxs-lookup"><span data-stu-id="c2b56-101">Localization: ResourceManagerWithCultureStringLocalizer class and WithCulture interface member removed</span></span>

<span data-ttu-id="c2b56-102">.NET 5.0 预览版 1 删除了 [ResourceManagerWithCultureStringLocalizer](/dotnet/api/microsoft.extensions.localization.resourcemanagerwithculturestringlocalizer?view=dotnet-plat-ext-3.1) 类和 [WithCulture](/dotnet/api/microsoft.extensions.localization.resourcemanagerstringlocalizer.withculture?view=dotnet-plat-ext-3.1) 方法。</span><span class="sxs-lookup"><span data-stu-id="c2b56-102">The [ResourceManagerWithCultureStringLocalizer](/dotnet/api/microsoft.extensions.localization.resourcemanagerwithculturestringlocalizer?view=dotnet-plat-ext-3.1) class and [WithCulture](/dotnet/api/microsoft.extensions.localization.resourcemanagerstringlocalizer.withculture?view=dotnet-plat-ext-3.1) method were removed in .NET 5.0 Preview 1.</span></span>

<span data-ttu-id="c2b56-103">有关上下文，请参阅 [aspnet/Announcements#346](https://github.com/aspnet/Announcements/issues/346) 和 [dotnet/aspnetcore#3324](https://github.com/dotnet/aspnetcore/issues/3324)。</span><span class="sxs-lookup"><span data-stu-id="c2b56-103">For context, see [aspnet/Announcements#346](https://github.com/aspnet/Announcements/issues/346) and [dotnet/aspnetcore#3324](https://github.com/dotnet/aspnetcore/issues/3324).</span></span> <span data-ttu-id="c2b56-104">有关此更改的讨论，请参阅 [dotnet/aspnetcore#7756](https://github.com/dotnet/aspnetcore/issues/7756)。</span><span class="sxs-lookup"><span data-stu-id="c2b56-104">For discussion on this change, see [dotnet/aspnetcore#7756](https://github.com/dotnet/aspnetcore/issues/7756).</span></span>

#### <a name="version-introduced"></a><span data-ttu-id="c2b56-105">引入的版本</span><span class="sxs-lookup"><span data-stu-id="c2b56-105">Version introduced</span></span>

<span data-ttu-id="c2b56-106">5.0 预览版 1</span><span class="sxs-lookup"><span data-stu-id="c2b56-106">5.0 Preview 1</span></span>

#### <a name="old-behavior"></a><span data-ttu-id="c2b56-107">旧行为</span><span class="sxs-lookup"><span data-stu-id="c2b56-107">Old behavior</span></span>

<span data-ttu-id="c2b56-108">`ResourceManagerWithCultureStringLocalizer` 类和 `ResourceManagerStringLocalizer.WithCulture` 方法[在 .NET Core 3.0 预览版 3 及更高版本中已过时](/dotnet/core/compatibility/2.2-3.0#localization-resourcemanagerwithculturestringlocalizer-and-withculture-marked-obsolete)。</span><span class="sxs-lookup"><span data-stu-id="c2b56-108">The `ResourceManagerWithCultureStringLocalizer` class and the `ResourceManagerStringLocalizer.WithCulture` method are [obsolete in .NET Core 3.0 Preview 3 and later](/dotnet/core/compatibility/2.2-3.0#localization-resourcemanagerwithculturestringlocalizer-and-withculture-marked-obsolete).</span></span>

#### <a name="new-behavior"></a><span data-ttu-id="c2b56-109">新行为</span><span class="sxs-lookup"><span data-stu-id="c2b56-109">New behavior</span></span>

<span data-ttu-id="c2b56-110">.NET 5.0 预览版 1 中删除了 `ResourceManagerWithCultureStringLocalizer` 类和 `ResourceManagerStringLocalizer.WithCulture` 方法。</span><span class="sxs-lookup"><span data-stu-id="c2b56-110">The `ResourceManagerWithCultureStringLocalizer` class and the `ResourceManagerStringLocalizer.WithCulture` method have been removed in .NET 5.0 Preview 1.</span></span> <span data-ttu-id="c2b56-111">有关所做更改的清单，请参阅 [dotnet/extensions#2562](https://github.com/dotnet/extensions/pull/2562/files) 上的拉取请求。</span><span class="sxs-lookup"><span data-stu-id="c2b56-111">For an inventory of the changes made, see the pull request at [dotnet/extensions#2562](https://github.com/dotnet/extensions/pull/2562/files).</span></span>

#### <a name="reason-for-change"></a><span data-ttu-id="c2b56-112">更改原因</span><span class="sxs-lookup"><span data-stu-id="c2b56-112">Reason for change</span></span>

<span data-ttu-id="c2b56-113">[ResourceManagerWithCultureStringLocalizer](/dotnet/api/microsoft.extensions.localization.resourcemanagerwithculturestringlocalizer?view=dotnet-plat-ext-3.1) 类和 [ResourceManagerStringLocalizer.WithCulture](/dotnet/api/microsoft.extensions.localization.resourcemanagerstringlocalizer.withculture?view=dotnet-plat-ext-3.1) 方法通常会让本地化用户混淆。</span><span class="sxs-lookup"><span data-stu-id="c2b56-113">The [ResourceManagerWithCultureStringLocalizer](/dotnet/api/microsoft.extensions.localization.resourcemanagerwithculturestringlocalizer?view=dotnet-plat-ext-3.1) class and [ResourceManagerStringLocalizer.WithCulture](/dotnet/api/microsoft.extensions.localization.resourcemanagerstringlocalizer.withculture?view=dotnet-plat-ext-3.1) method were often sources of confusion for users of localization.</span></span> <span data-ttu-id="c2b56-114">创建自定义 <xref:Microsoft.Extensions.Localization.IStringLocalizer> 实现时，混淆尤其严重。</span><span class="sxs-lookup"><span data-stu-id="c2b56-114">The confusion was especially high when creating a custom <xref:Microsoft.Extensions.Localization.IStringLocalizer> implementation.</span></span> <span data-ttu-id="c2b56-115">这个类和方法给使用者的印象是 `IStringLocalizer` 实例应“按语言、按资源”。</span><span class="sxs-lookup"><span data-stu-id="c2b56-115">This class and method give consumers the impression that an `IStringLocalizer` instance is expected to be "per-language, per-resource".</span></span> <span data-ttu-id="c2b56-116">实际上，实例应该仅“按资源”。</span><span class="sxs-lookup"><span data-stu-id="c2b56-116">In reality, the instance should only be "per-resource".</span></span> <span data-ttu-id="c2b56-117">在运行时，<xref:System.Globalization.CultureInfo.CurrentUICulture%2A?displayProperty=nameWithType> 属性确定要使用的语言。</span><span class="sxs-lookup"><span data-stu-id="c2b56-117">At run time, the <xref:System.Globalization.CultureInfo.CurrentUICulture%2A?displayProperty=nameWithType> property determines the language to be used.</span></span>

#### <a name="recommended-action"></a><span data-ttu-id="c2b56-118">建议操作</span><span class="sxs-lookup"><span data-stu-id="c2b56-118">Recommended action</span></span>

<span data-ttu-id="c2b56-119">停止使用 `ResourceManagerWithCultureStringLocalizer` 类和 `ResourceManagerStringLocalizer.WithCulture` 方法。</span><span class="sxs-lookup"><span data-stu-id="c2b56-119">Stop using the `ResourceManagerWithCultureStringLocalizer` class and the `ResourceManagerStringLocalizer.WithCulture` method.</span></span>

#### <a name="category"></a><span data-ttu-id="c2b56-120">类别</span><span class="sxs-lookup"><span data-stu-id="c2b56-120">Category</span></span>

<span data-ttu-id="c2b56-121">ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="c2b56-121">ASP.NET Core</span></span>

#### <a name="affected-apis"></a><span data-ttu-id="c2b56-122">受影响的 API</span><span class="sxs-lookup"><span data-stu-id="c2b56-122">Affected APIs</span></span>

- [<span data-ttu-id="c2b56-123">ResourceManagerWithCultureStringLocalizer</span><span class="sxs-lookup"><span data-stu-id="c2b56-123">ResourceManagerWithCultureStringLocalizer</span></span>](/dotnet/api/microsoft.extensions.localization.resourcemanagerwithculturestringlocalizer?view=dotnet-plat-ext-3.1)
- [<span data-ttu-id="c2b56-124">ResourceManagerStringLocalizer.WithCulture</span><span class="sxs-lookup"><span data-stu-id="c2b56-124">ResourceManagerStringLocalizer.WithCulture</span></span>](/dotnet/api/microsoft.extensions.localization.resourcemanagerstringlocalizer.withculture?view=dotnet-plat-ext-3.1)

<!--

#### Affected APIs

- `T:Microsoft.Extensions.Localization.ResourceManagerWithCultureStringLocalizer`
- `Overload:Microsoft.Extensions.Localization.ResourceManagerStringLocalizer.WithCulture`

-->