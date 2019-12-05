---
title: BodyToString 方法（System.servicemodel. 通道）
author: mairaw
ms.author: mairaw
ms.date: 11/01/2019
topic_type:
- apiref
api_name:
- System.ServiceModel.Channels.Message.BodyToString
api_location:
- system.servicemodel.dll
api_type:
- Assembly
ms.openlocfilehash: 7b0b56bfda1c0c37f43f95e9684d3b4042c1b97c
ms.sourcegitcommit: 9a39f2a06f110c9c7ca54ba216900d038aa14ef3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/23/2019
ms.locfileid: "74451310"
---
# <a name="messagebodytostring-method"></a><span data-ttu-id="87b2f-102">BodyToString 方法</span><span class="sxs-lookup"><span data-stu-id="87b2f-102">Message.BodyToString Method</span></span>

<span data-ttu-id="87b2f-103">通过调用 <xref:System.ServiceModel.Channels.Message.OnBodyToString%2A?displayProperty=nameWithType> 方法，将消息正文转换为字符串。</span><span class="sxs-lookup"><span data-stu-id="87b2f-103">Converts the message body into a string by calling the <xref:System.ServiceModel.Channels.Message.OnBodyToString%2A?displayProperty=nameWithType> method.</span></span>

```csharp
internal void BodyToString(XmlDictionaryWriter writer);
```

## <a name="parameters"></a><span data-ttu-id="87b2f-104">参数</span><span class="sxs-lookup"><span data-stu-id="87b2f-104">Parameters</span></span>

- <span data-ttu-id="87b2f-105">`writer` <xref:System.Xml.XmlDictionaryWriter></span><span class="sxs-lookup"><span data-stu-id="87b2f-105">`writer` <xref:System.Xml.XmlDictionaryWriter></span></span>\
  <span data-ttu-id="87b2f-106">用于将消息正文转换为字符串的编写器。</span><span class="sxs-lookup"><span data-stu-id="87b2f-106">The writer that is used to convert the message body to a string.</span></span>

## <a name="remarks"></a><span data-ttu-id="87b2f-107">备注</span><span class="sxs-lookup"><span data-stu-id="87b2f-107">Remarks</span></span>

> [!WARNING]
> <span data-ttu-id="87b2f-108">`Message.BodyToString` 方法是内部的，不应在代码中直接使用。</span><span class="sxs-lookup"><span data-stu-id="87b2f-108">The `Message.BodyToString` method is internal and is not meant to be used directly in your code.</span></span>
>
> <span data-ttu-id="87b2f-109">在任何情况下，Microsoft 不支持在生产应用程序中使用此方法。</span><span class="sxs-lookup"><span data-stu-id="87b2f-109">Microsoft does not support the use of this method in a production application under any circumstance.</span></span>

## <a name="requirements"></a><span data-ttu-id="87b2f-110">要求</span><span class="sxs-lookup"><span data-stu-id="87b2f-110">Requirements</span></span>

<span data-ttu-id="87b2f-111">**命名空间：** <xref:System.ServiceModel.Channels></span><span class="sxs-lookup"><span data-stu-id="87b2f-111">**Namespace:** <xref:System.ServiceModel.Channels></span></span>

<span data-ttu-id="87b2f-112">**程序集：** System.servicemodel .dll</span><span class="sxs-lookup"><span data-stu-id="87b2f-112">**Assembly:** System.ServiceModel.dll</span></span>

<span data-ttu-id="87b2f-113">**.NET Framework 版本：** 自3.0 起可用。</span><span class="sxs-lookup"><span data-stu-id="87b2f-113">**.NET Framework versions:** Available since 3.0.</span></span>