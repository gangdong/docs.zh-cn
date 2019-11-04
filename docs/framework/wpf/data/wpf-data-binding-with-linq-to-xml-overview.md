---
title: 使用 LINQ to XML 进行 WPF 数据绑定
ms.date: 10/22/2019
ms.topic: conceptual
ms.openlocfilehash: 53aba3295b98ae4a476b321cb585e1bbbdd45dad
ms.sourcegitcommit: 5a28f8eb071fcc09b045b0c4ae4b96898673192e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/31/2019
ms.locfileid: "73197389"
---
# <a name="overview-of-wpf-data-binding-with-linq-to-xml"></a><span data-ttu-id="5bc8b-102">与 LINQ to XML 的 WPF 数据绑定概述</span><span class="sxs-lookup"><span data-stu-id="5bc8b-102">Overview of WPF data binding with LINQ to XML</span></span>

<span data-ttu-id="5bc8b-103">本文介绍 <xref:System.Xml.Linq> 命名空间中的动态数据绑定功能。</span><span class="sxs-lookup"><span data-stu-id="5bc8b-103">This article introduces the dynamic data binding features in the <xref:System.Xml.Linq> namespace.</span></span> <span data-ttu-id="5bc8b-104">这些功能可用作 Windows Presentation Foundation (WPF) 应用中用户界面 (UI) 元素的数据源。</span><span class="sxs-lookup"><span data-stu-id="5bc8b-104">These features can be used as a data source for user interface (UI) elements in Windows Presentation Foundation (WPF) apps.</span></span> <span data-ttu-id="5bc8b-105">此方案依赖于 <xref:System.Xml.Linq.XAttribute?displayProperty=fullName> 和 <xref:System.Xml.Linq.XElement?displayProperty=fullName> 的特殊动态属性。</span><span class="sxs-lookup"><span data-stu-id="5bc8b-105">This scenario relies upon special *dynamic properties* of <xref:System.Xml.Linq.XAttribute?displayProperty=fullName> and <xref:System.Xml.Linq.XElement?displayProperty=fullName>.</span></span>

## <a name="xaml-and-linq-to-xml"></a><span data-ttu-id="5bc8b-106">XAML 和 LINQ to XML</span><span class="sxs-lookup"><span data-stu-id="5bc8b-106">XAML and LINQ to XML</span></span>

<span data-ttu-id="5bc8b-107">Extensible Application Markup Language (XAML) 是由 Microsoft 创建的用于支持 .NET 技术的 XML 方言。</span><span class="sxs-lookup"><span data-stu-id="5bc8b-107">The Extensible Application Markup Language (XAML) is an XML dialect created by Microsoft to support .NET technologies.</span></span> <span data-ttu-id="5bc8b-108">它在 WPF 中用于表示用户界面元素和相关功能，如事件和数据绑定。</span><span class="sxs-lookup"><span data-stu-id="5bc8b-108">It is used in WPF to represent user interface elements and related features, such as events and data binding.</span></span> <span data-ttu-id="5bc8b-109">在 Windows Workflow Foundation 中，XAML 用于表示程序结构，如程序控制（工作流）。</span><span class="sxs-lookup"><span data-stu-id="5bc8b-109">In Windows Workflow Foundation, XAML is used to represent program structure, such as program control (*workflows*).</span></span> <span data-ttu-id="5bc8b-110">XAML 使技术的声明性方面与相关的过程性代码分离，从而可定义更具个性化的程序行为。</span><span class="sxs-lookup"><span data-stu-id="5bc8b-110">XAML enables the declarative aspects of a technology to be separated from the related procedural code that defines the more individualized behavior of a program.</span></span>

<span data-ttu-id="5bc8b-111">XAML 和 LINQ to XML 的交互有两种主要方式：</span><span class="sxs-lookup"><span data-stu-id="5bc8b-111">There are two broad ways that XAML and LINQ to XML can interact:</span></span>

- <span data-ttu-id="5bc8b-112">由于 XAML 文件是格式良好的 XML，因此可以通过 XML 技术（如 LINQ to XML）查询和操作。</span><span class="sxs-lookup"><span data-stu-id="5bc8b-112">Because XAML files are well-formed XML, they can be queried and manipulated through XML technologies such as LINQ to XML.</span></span>

- <span data-ttu-id="5bc8b-113">由于 LINQ to XML 查询表示数据的源，因此这些查询可用作 WPF UI 元素数据绑定的数据源。</span><span class="sxs-lookup"><span data-stu-id="5bc8b-113">Because LINQ to XML queries represent a source of data, these queries can be used as a data source for data binding for WPF UI elements.</span></span>

<span data-ttu-id="5bc8b-114">本文档说明第二种情况。</span><span class="sxs-lookup"><span data-stu-id="5bc8b-114">This documentation describes the second scenario.</span></span>

## <a name="data-binding-in-the-windows-presentation-foundation"></a><span data-ttu-id="5bc8b-115">Windows Presentation Foundation 中的数据绑定</span><span class="sxs-lookup"><span data-stu-id="5bc8b-115">Data binding in the Windows Presentation Foundation</span></span>

<span data-ttu-id="5bc8b-116">WPF 数据绑定可使 UI 元素将其一个属性与一个数据源相关联。</span><span class="sxs-lookup"><span data-stu-id="5bc8b-116">WPF data binding enables a UI element to associate one of its properties with a data source.</span></span> <span data-ttu-id="5bc8b-117">这种情况的一个简单示例是 <xref:System.Windows.Controls.Label>，其文本表示用户定义对象中一个公共属性的值。</span><span class="sxs-lookup"><span data-stu-id="5bc8b-117">A simple example of this is a <xref:System.Windows.Controls.Label> whose text presents the value of a public property in a user-defined object.</span></span> <span data-ttu-id="5bc8b-118">WPF 数据绑定依赖于下列组件：</span><span class="sxs-lookup"><span data-stu-id="5bc8b-118">WPF data binding relies on the following components:</span></span>

|<span data-ttu-id="5bc8b-119">组件</span><span class="sxs-lookup"><span data-stu-id="5bc8b-119">Component</span></span>|<span data-ttu-id="5bc8b-120">描述</span><span class="sxs-lookup"><span data-stu-id="5bc8b-120">Description</span></span>|
|---------------|-----------------|
|<span data-ttu-id="5bc8b-121">绑定目标</span><span class="sxs-lookup"><span data-stu-id="5bc8b-121">Binding target</span></span>|<span data-ttu-id="5bc8b-122">要与数据源关联的 UI 元素。</span><span class="sxs-lookup"><span data-stu-id="5bc8b-122">The UI element to be associated with the data source.</span></span> <span data-ttu-id="5bc8b-123">WPF 中的可视元素是从 <xref:System.Windows.UIElement> 类派生的。</span><span class="sxs-lookup"><span data-stu-id="5bc8b-123">Visual elements in WPF are derived from the <xref:System.Windows.UIElement> class.</span></span>|
|<span data-ttu-id="5bc8b-124">目标属性</span><span class="sxs-lookup"><span data-stu-id="5bc8b-124">Target property</span></span>|<span data-ttu-id="5bc8b-125">绑定目标的依赖项属性，反映数据绑定源的值。</span><span class="sxs-lookup"><span data-stu-id="5bc8b-125">The *dependency property* of the binding target that reflects the value of the data-binding source.</span></span> <span data-ttu-id="5bc8b-126">从中派生 <xref:System.Windows.DependencyObject> 的 <xref:System.Windows.UIElement> 类直接支持依赖项属性。</span><span class="sxs-lookup"><span data-stu-id="5bc8b-126">Dependency properties are directly supported by the <xref:System.Windows.DependencyObject> class, which <xref:System.Windows.UIElement> derives from.</span></span>|
|<span data-ttu-id="5bc8b-127">绑定源</span><span class="sxs-lookup"><span data-stu-id="5bc8b-127">Binding source</span></span>|<span data-ttu-id="5bc8b-128">提供给 UI 元素以便进行显示的一个或多个值的源对象。</span><span class="sxs-lookup"><span data-stu-id="5bc8b-128">The source object for one or more values that are supplied to the UI element for presentation.</span></span> <span data-ttu-id="5bc8b-129">WPF 自动支持以下类型作为绑定源：CLR 对象、ADO.NET 数据对象、XML 数据（来自 XPath 或 LINQ to XML 查询）或其他 <xref:System.Windows.DependencyObject>。</span><span class="sxs-lookup"><span data-stu-id="5bc8b-129">WPF automatically supports the following types as binding sources: CLR objects, ADO.NET data objects, XML data (from XPath or LINQ to XML queries), or another <xref:System.Windows.DependencyObject>.</span></span>|
|<span data-ttu-id="5bc8b-130">源路径</span><span class="sxs-lookup"><span data-stu-id="5bc8b-130">Source path</span></span>|<span data-ttu-id="5bc8b-131">绑定源的属性，可解析为要绑定的一个或一组值。</span><span class="sxs-lookup"><span data-stu-id="5bc8b-131">The property of the binding source that resolves to the value or set of values that is to be bound.</span></span>|

<span data-ttu-id="5bc8b-132">依赖项属性是特定于 WPF 的概念，它表示 UI 元素的动态计算的属性。</span><span class="sxs-lookup"><span data-stu-id="5bc8b-132">A dependency property is a concept specific to WPF that represent a dynamically computed property of a UI element.</span></span> <span data-ttu-id="5bc8b-133">例如，依赖项属性通常具有默认值或具有由父元素提供的值。</span><span class="sxs-lookup"><span data-stu-id="5bc8b-133">For example, dependency properties often have default values or values that are provided by a parent element.</span></span> <span data-ttu-id="5bc8b-134"><xref:System.Windows.DependencyProperty> 类的实例（而不是支持标准属性的字段）支持这些特殊属性。</span><span class="sxs-lookup"><span data-stu-id="5bc8b-134">These special properties are backed by instances of the <xref:System.Windows.DependencyProperty> class (and not fields as with standard properties).</span></span> <span data-ttu-id="5bc8b-135">有关详细信息，请参阅[依赖项属性概述](../advanced/dependency-properties-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="5bc8b-135">For more information, see [Dependency Properties Overview](../advanced/dependency-properties-overview.md).</span></span>

### <a name="dynamic-data-binding-in-wpf"></a><span data-ttu-id="5bc8b-136">WPF 中的动态数据绑定</span><span class="sxs-lookup"><span data-stu-id="5bc8b-136">Dynamic data binding in WPF</span></span>

<span data-ttu-id="5bc8b-137">默认情况下，仅在初始化目标 UI 元素时，才会发生数据绑定。</span><span class="sxs-lookup"><span data-stu-id="5bc8b-137">By default, data binding occurs only when the target UI element is initialized.</span></span> <span data-ttu-id="5bc8b-138">这称为“一次性”绑定。</span><span class="sxs-lookup"><span data-stu-id="5bc8b-138">This is called *one-time* binding.</span></span> <span data-ttu-id="5bc8b-139">这不能满足多数用途的需要；通常，数据绑定解决方案要求使用以下方式之一在运行时动态传播更改：</span><span class="sxs-lookup"><span data-stu-id="5bc8b-139">For most purposes, this is insufficient; typically, a data-binding solution requires that the changes be dynamically propagated at run time using one of the following:</span></span>

- <span data-ttu-id="5bc8b-140">单向绑定，这种方式会自动传播对一侧所做的更改。</span><span class="sxs-lookup"><span data-stu-id="5bc8b-140">*One-way* binding causes the changes to one side to be propagated automatically.</span></span> <span data-ttu-id="5bc8b-141">最常见的情况是对源所做的更改会反映在目标中，但有时需要相反的情况。</span><span class="sxs-lookup"><span data-stu-id="5bc8b-141">Most commonly, changes to the source are reflected in the target, but the reverse can sometimes be useful.</span></span>

- <span data-ttu-id="5bc8b-142">双向绑定，在这种方式中，对源所做的更改会自动传播到目标，而且对目标的更改也会自动传播到源。</span><span class="sxs-lookup"><span data-stu-id="5bc8b-142">In *two-way* binding, changes to the source are automatically propagated to the target, and changes to the target are automatically propagated to the source.</span></span>

<span data-ttu-id="5bc8b-143">为了进行单向或双向绑定，源必须实现一种更改通知机制，例如通过实现 <xref:System.ComponentModel.INotifyPropertyChanged> 接口或通过对支持的每个属性使用 PropertyNameChanged 模式。</span><span class="sxs-lookup"><span data-stu-id="5bc8b-143">For one-way or two-way binding to occur, the source must implement a change notification mechanism, for example by implementing the <xref:System.ComponentModel.INotifyPropertyChanged> interface or by using a *PropertyNameChanged* pattern for each property supported.</span></span>

<span data-ttu-id="5bc8b-144">有关 WPF 中数据绑定的详细信息，请参阅[数据绑定 (WPF)](/dotnet/framework/wpf/data/data-binding-wpf)。</span><span class="sxs-lookup"><span data-stu-id="5bc8b-144">For more information about data binding in WPF, see [Data Binding (WPF)](/dotnet/framework/wpf/data/data-binding-wpf).</span></span>

## <a name="dynamic-properties-in-linq-to-xml-classes"></a><span data-ttu-id="5bc8b-145">LINQ to XML 类中的动态属性</span><span class="sxs-lookup"><span data-stu-id="5bc8b-145">Dynamic properties in LINQ to XML classes</span></span>

<span data-ttu-id="5bc8b-146">大多数 LINQ to XML 类都不适合作为适当的 WPF 动态数据源。</span><span class="sxs-lookup"><span data-stu-id="5bc8b-146">Most LINQ to XML classes do not qualify as proper WPF dynamic data sources.</span></span> <span data-ttu-id="5bc8b-147">一些最有用的信息只能通过方法（而不是属性）提供，并且这些类中的属性不实现更改通知。</span><span class="sxs-lookup"><span data-stu-id="5bc8b-147">Some of the most useful information is available only through methods, not properties, and properties in these classes do not implement change notifications.</span></span> <span data-ttu-id="5bc8b-148">为了支持 WPF 数据绑定，LINQ to XML 公开了一组动态属性。</span><span class="sxs-lookup"><span data-stu-id="5bc8b-148">To support WPF data binding, LINQ to XML exposes a set of *dynamic properties*.</span></span>

<span data-ttu-id="5bc8b-149">这些动态属性是特殊的运行时属性，它们重复 <xref:System.Xml.Linq.XAttribute> 和 <xref:System.Xml.Linq.XElement> 类中现有方法和属性的功能。</span><span class="sxs-lookup"><span data-stu-id="5bc8b-149">These dynamic properties are special run-time properties that duplicate the functionality of existing methods and properties in the <xref:System.Xml.Linq.XAttribute> and <xref:System.Xml.Linq.XElement> classes.</span></span> <span data-ttu-id="5bc8b-150">将这些属性添加到这些类中只是为了使这些类能够充当 WPF 的动态数据源。</span><span class="sxs-lookup"><span data-stu-id="5bc8b-150">They were added to these classes solely to enable them to act as dynamic data sources for WPF.</span></span> <span data-ttu-id="5bc8b-151">为了满足这一要求，所有这些动态属性都要实现更改通知。</span><span class="sxs-lookup"><span data-stu-id="5bc8b-151">To meet this need, all these dynamic properties implement change notifications.</span></span> <span data-ttu-id="5bc8b-152">下一节 [LINQ to XML 动态属性](linq-to-xml-dynamic-properties.md)中提供有关这些动态属性的详细参考。</span><span class="sxs-lookup"><span data-stu-id="5bc8b-152">A detailed reference for these dynamic properties is provided in the next section, [LINQ to XML Dynamic Properties](linq-to-xml-dynamic-properties.md).</span></span>

> [!NOTE]
> <span data-ttu-id="5bc8b-153"><xref:System.Xml.Linq> 命名空间的各个类中的很多标准公共属性都可用于一次性数据绑定。</span><span class="sxs-lookup"><span data-stu-id="5bc8b-153">Many of the standard public properties, found in the various classes in the <xref:System.Xml.Linq> namespace, can be used for one-time data binding.</span></span> <span data-ttu-id="5bc8b-154">但请记住，在这种方案下，源和目标都不会动态更新。</span><span class="sxs-lookup"><span data-stu-id="5bc8b-154">However, remember that neither the source nor the target will be dynamically updated under this scheme.</span></span>

### <a name="access-dynamic-properties"></a><span data-ttu-id="5bc8b-155">访问动态属性</span><span class="sxs-lookup"><span data-stu-id="5bc8b-155">Access dynamic properties</span></span>

<span data-ttu-id="5bc8b-156">不能像访问标准属性那样访问 <xref:System.Xml.Linq.XAttribute> 和 <xref:System.Xml.Linq.XElement> 类中的动态属性。</span><span class="sxs-lookup"><span data-stu-id="5bc8b-156">The dynamic properties in the <xref:System.Xml.Linq.XAttribute> and <xref:System.Xml.Linq.XElement> classes cannot be accessed like standard properties.</span></span> <span data-ttu-id="5bc8b-157">例如，在符合 CLR 的语言（如 C#）中，动态属性不能：</span><span class="sxs-lookup"><span data-stu-id="5bc8b-157">For example, in CLR-compliant languages such as C#, they cannot be:</span></span>

- <span data-ttu-id="5bc8b-158">在编译时直接访问。</span><span class="sxs-lookup"><span data-stu-id="5bc8b-158">Accessed directly at compile time.</span></span> <span data-ttu-id="5bc8b-159">动态属性对于编译器和 Visual Studio IntelliSense 是不可见的。</span><span class="sxs-lookup"><span data-stu-id="5bc8b-159">Dynamic properties are invisible to the compiler and to Visual Studio IntelliSense.</span></span>

- <span data-ttu-id="5bc8b-160">在运行时使用 .NET 反射来发现或访问。</span><span class="sxs-lookup"><span data-stu-id="5bc8b-160">Discovered or accessed at run time using .NET reflection.</span></span> <span data-ttu-id="5bc8b-161">即使在运行时，它们也不是基本 CLR 意义上的属性。</span><span class="sxs-lookup"><span data-stu-id="5bc8b-161">Even at run time, they are not properties in the basic CLR sense.</span></span>

<span data-ttu-id="5bc8b-162">在 C# 中，动态属性只能在运行时通过 <xref:System.ComponentModel> 命名空间提供的功能进行访问。</span><span class="sxs-lookup"><span data-stu-id="5bc8b-162">In C#, dynamic properties can only be accessed at run time through facilities provided by the <xref:System.ComponentModel> namespace.</span></span>

<span data-ttu-id="5bc8b-163">但相比之下，在 XML 源中，可以通过下面形式的简洁表示法访问动态属性：</span><span class="sxs-lookup"><span data-stu-id="5bc8b-163">In contrast, however, in an XML source dynamic properties can be accessed through a straightforward notation in the following form:</span></span>

```xml
<object>.<dynamic-property>
```

<span data-ttu-id="5bc8b-164">这两个类的动态属性或者解析为可以直接使用的值，或者解析为必须与索引一起提供的索引器，以便获取结果值或值的集合。</span><span class="sxs-lookup"><span data-stu-id="5bc8b-164">The dynamic properties for these two classes either resolve to a value that can be used directly, or to an indexer that must be supplied with an index to obtain the resulting value or collection of values.</span></span> <span data-ttu-id="5bc8b-165">后一种语法采用的格式为：</span><span class="sxs-lookup"><span data-stu-id="5bc8b-165">The latter syntax takes the form:</span></span>

```xml
<object>.<dynamic-property>[<index-value>]
```

<span data-ttu-id="5bc8b-166">有关详细信息，请参阅 [LINQ to XML 动态属性](linq-to-xml-dynamic-properties.md)。</span><span class="sxs-lookup"><span data-stu-id="5bc8b-166">For more information, see [LINQ to XML Dynamic Properties](linq-to-xml-dynamic-properties.md).</span></span>

<span data-ttu-id="5bc8b-167">为了实现 WPF 动态绑定，需要与 <xref:System.Windows.Data> 命名空间提供的功能（特别是 <xref:System.Windows.Data.Binding> 类）一起使用动态属性。</span><span class="sxs-lookup"><span data-stu-id="5bc8b-167">To implement WPF dynamic binding, dynamic properties will be used with facilities provided by the <xref:System.Windows.Data> namespace, most notably the <xref:System.Windows.Data.Binding> class.</span></span>

## <a name="see-also"></a><span data-ttu-id="5bc8b-168">请参阅</span><span class="sxs-lookup"><span data-stu-id="5bc8b-168">See also</span></span>

- [<span data-ttu-id="5bc8b-169">使用 LINQ to XML 进行 WPF 数据绑定</span><span class="sxs-lookup"><span data-stu-id="5bc8b-169">WPF Data Binding with LINQ to XML</span></span>](wpf-data-binding-with-linq-to-xml-overview.md)
- [<span data-ttu-id="5bc8b-170">LINQ to XML 动态属性</span><span class="sxs-lookup"><span data-stu-id="5bc8b-170">LINQ to XML Dynamic Properties</span></span>](linq-to-xml-dynamic-properties.md)
- [<span data-ttu-id="5bc8b-171">WPF 中的 XAML</span><span class="sxs-lookup"><span data-stu-id="5bc8b-171">XAML in WPF</span></span>](../advanced/xaml-in-wpf.md)
- [<span data-ttu-id="5bc8b-172">数据绑定 (WPF)</span><span class="sxs-lookup"><span data-stu-id="5bc8b-172">Data Binding (WPF)</span></span>](/dotnet/framework/wpf/data/data-binding-wpf)
- [<span data-ttu-id="5bc8b-173">使用工作流标记</span><span class="sxs-lookup"><span data-stu-id="5bc8b-173">Using Workflow Markup</span></span>](https://go.microsoft.com/fwlink/?LinkId=98685)