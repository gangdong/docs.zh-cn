---
ms.openlocfilehash: f4ff938b2d0e9ead481fdf239aed8a6b918a99b0
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2020
ms.locfileid: "85619889"
---
### <a name="listboxitem-isselected-binding-issue-with-observablecollectionlttgtmove"></a>ObservableCollection&lt;T&gt;.Move 的 ListBoxItem IsSelected 绑定问题

#### <a name="details"></a>详细信息

在绑定到有选中项的 <xref:System.Windows.Controls.ListBox?displayProperty=fullName> 的集合上调用 <xref:System.Collections.ObjectModel.ObservableCollection%601.Move(System.Int32,System.Int32)> 或 <xref:System.Collections.ObjectModel.ObservableCollection%601.MoveItem(System.Int32,System.Int32)> 可能导致未来选择或不选 <xref:System.Windows.Controls.ListBox?displayProperty=fullName> 项的不稳定行为。

#### <a name="suggestion"></a>建议

调用 <xref:System.Collections.ObjectModel.Collection%601.Remove(%600)?displayProperty=fullName> 和 <xref:System.Collections.ObjectModel.Collection%601.Insert(System.Int32,%600)?displayProperty=fullName>（而不是 <xref:System.Collections.ObjectModel.ObservableCollection%601.Move(System.Int32,System.Int32)>）将解决此问题。 此外，此问题已在 .NET Framework 4.6 中解决，因此升级到该版本的 .NET Framework 即可解决该问题。

| “属性”    | “值”       |
|:--------|:------------|
| 范围   |次要|
|Version|4.5|
|类型|运行时

#### <a name="affected-apis"></a>受影响的 API

-<xref:System.Collections.ObjectModel.ObservableCollection%601.Move(System.Int32,System.Int32)?displayProperty=nameWithType></li><li><xref:System.Collections.ObjectModel.ObservableCollection%601.MoveItem(System.Int32,System.Int32)?displayProperty=nameWithType></li></ul>|
