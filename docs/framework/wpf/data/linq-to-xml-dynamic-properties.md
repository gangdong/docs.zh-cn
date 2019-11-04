---
title: LINQ to XML 动态属性引用
ms.date: 10/22/2019
ms.topic: reference
ms.openlocfilehash: 48b51e92eb78786b2cc189e3e7daa00875b41585
ms.sourcegitcommit: 5a28f8eb071fcc09b045b0c4ae4b96898673192e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/31/2019
ms.locfileid: "73197051"
---
# <a name="linq-to-xml-dynamic-properties"></a><span data-ttu-id="86eac-102">LINQ to XML 动态属性</span><span class="sxs-lookup"><span data-stu-id="86eac-102">LINQ to XML dynamic properties</span></span>

<span data-ttu-id="86eac-103">本节提供有关 LINQ to XML 中动态属性的参考信息。</span><span class="sxs-lookup"><span data-stu-id="86eac-103">This section provides reference information about the dynamic properties in LINQ to XML.</span></span> <span data-ttu-id="86eac-104">具体地说，这些属性由 <xref:System.Xml.Linq.XAttribute> 命名空间中的 <xref:System.Xml.Linq.XElement> 和 <xref:System.Xml.Linq> 类公开。</span><span class="sxs-lookup"><span data-stu-id="86eac-104">Specifically, these properties are exposed by the <xref:System.Xml.Linq.XAttribute> and <xref:System.Xml.Linq.XElement> classes, which are in the <xref:System.Xml.Linq> namespace.</span></span>

<span data-ttu-id="86eac-105">如 [使用 LINQ to XML 进行 WPF 数据绑定概述](wpf-data-binding-with-linq-to-xml-overview.md) 主题中所述，每个动态属性都等效于同一类中的标准公共属性或方法。</span><span class="sxs-lookup"><span data-stu-id="86eac-105">As explained in the topic [Overview of WPF data binding with LINQ to XML](wpf-data-binding-with-linq-to-xml-overview.md), each of the dynamic properties is equivalent to a standard public property or method in the same class.</span></span> <span data-ttu-id="86eac-106">多数情况下应使用这些标准成员；动态属性是专门为 LINQ to XML 数据绑定方案提供的。</span><span class="sxs-lookup"><span data-stu-id="86eac-106">These standard members should be used for most purposes; dynamic properties are provided specifically for LINQ to XML data binding scenarios.</span></span> <span data-ttu-id="86eac-107">有关这些类的标准成员的更多信息，请参见 <xref:System.Xml.Linq.XAttribute> 和 <xref:System.Xml.Linq.XElement> 参考主题。</span><span class="sxs-lookup"><span data-stu-id="86eac-107">For more information about the standard members of these classes, see the <xref:System.Xml.Linq.XAttribute> and <xref:System.Xml.Linq.XElement> reference topics.</span></span>

<span data-ttu-id="86eac-108">就其解析值而论，本节中的动态属性可分为两类：</span><span class="sxs-lookup"><span data-stu-id="86eac-108">With respect to their resolved values, the dynamic properties in this section fall into two categories:</span></span>

- <span data-ttu-id="86eac-109">解析为单个值的简单动态属性，如 `Value` 和 <xref:System.Xml.Linq.XAttribute> 类中的 <xref:System.Xml.Linq.XElement> 属性。</span><span class="sxs-lookup"><span data-stu-id="86eac-109">Simple ones, such as the `Value` properties in the <xref:System.Xml.Linq.XAttribute> and <xref:System.Xml.Linq.XElement> classes, that resolve to a single value.</span></span>

- <span data-ttu-id="86eac-110">解析为索引器类型的索引值，如 [Elements](elements-xelement-dynamic-property.md) 和 <xref:System.Xml.Linq.XElement> 的 [Descendants](descendants-xelement-dynamic-property.md) 属性。</span><span class="sxs-lookup"><span data-stu-id="86eac-110">Indexed values, such as the [Elements](elements-xelement-dynamic-property.md) and [Descendants](descendants-xelement-dynamic-property.md) properties of <xref:System.Xml.Linq.XElement>, that resolve into an indexer type.</span></span> <span data-ttu-id="86eac-111">对于要解析为所需值或集合的索引器类型，必须为其传递展开名称参数。</span><span class="sxs-lookup"><span data-stu-id="86eac-111">For indexer types to be resolved to the desired value or collection, an expanded name parameter must be passed to them.</span></span>

<span data-ttu-id="86eac-112">返回 <xref:System.Collections.Generic.IEnumerable%601> 类型索引值的所有动态属性都使用延迟执行。</span><span class="sxs-lookup"><span data-stu-id="86eac-112">All the dynamic properties that return an indexed value of type <xref:System.Collections.Generic.IEnumerable%601> use deferred execution.</span></span> <span data-ttu-id="86eac-113">有关延迟执行的详细信息，请参阅 [LINQ 查询简介 (C#)](../../../csharp/programming-guide/concepts/linq/introduction-to-linq-queries.md)。</span><span class="sxs-lookup"><span data-stu-id="86eac-113">For more information about deferred execution, see [Introduction to LINQ queries (C#)](../../../csharp/programming-guide/concepts/linq/introduction-to-linq-queries.md).</span></span>

## <a name="reference"></a><span data-ttu-id="86eac-114">参考</span><span class="sxs-lookup"><span data-stu-id="86eac-114">Reference</span></span>

- <xref:System.Xml.Linq>
- <xref:System.Xml.Linq.XElement?displayProperty=fullName>
- <xref:System.Xml.Linq.XAttribute?displayProperty=fullName>

## <a name="see-also"></a><span data-ttu-id="86eac-115">请参阅</span><span class="sxs-lookup"><span data-stu-id="86eac-115">See also</span></span>

- [<span data-ttu-id="86eac-116">使用 LINQ to XML 进行 WPF 数据绑定</span><span class="sxs-lookup"><span data-stu-id="86eac-116">WPF data binding with LINQ to XML</span></span>](wpf-data-binding-with-linq-to-xml-overview.md)
- [<span data-ttu-id="86eac-117">使用 LINQ to XML 进行 WPF 数据绑定概述</span><span class="sxs-lookup"><span data-stu-id="86eac-117">WPF data binding with LINQ to XML overview</span></span>](wpf-data-binding-with-linq-to-xml-overview.md)
- [<span data-ttu-id="86eac-118">LINQ 查询简介 (C#)</span><span class="sxs-lookup"><span data-stu-id="86eac-118">Introduction to LINQ queries (C#)</span></span>](../../../csharp/programming-guide/concepts/linq/introduction-to-linq-queries.md)