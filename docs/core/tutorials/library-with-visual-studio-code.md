---
title: 在 Visual Studio Code 中创建 .NET Standard 类库
description: 了解如何使用 Visual Studio Code 创建 .NET Standard 类库。
ms.date: 05/29/2020
ms.openlocfilehash: 5720ac374d50ef27a07d463e57af1bd95a352d83
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/05/2020
ms.locfileid: "84446947"
---
# <a name="tutorial-create-a-net-standard-library-in-visual-studio-code"></a>教程：在 Visual Studio Code 中创建 .NET Standard 库

类库定义的是可以由应用程序调用的类型和方法。 借助面向 .NET Standard 2.0 的类库，任何支持相应 .NET Standard 版本的 .NET 实现都可以调用库。 完成类库时，可以决定是要将其作为 NuGet 包进行分布，还是要将其作为与一个或多个应用程序捆绑在一起的组件进行添加。

> [!NOTE]
> 有关 .NET Standard 版本及其支持的平台列表，请参阅 [.NET Standard](../../standard/net-standard.md)。

在本教程中，将创建包含一个字符串处理方法的简单实用工具库。 我们把它作为[扩展方法](../../csharp/programming-guide/classes-and-structs/extension-methods.md)进行实现，这样就可以把它作为 <xref:System.String> 类成员进行调用。

## <a name="prerequisites"></a>先决条件

1. 已安装 [C# 扩展](https://marketplace.visualstudio.com/items?itemName=ms-dotnettools.csharp) 的 [Visual Studio Code](https://code.visualstudio.com/)。 有关如何在 Visual Studio Code 上安装扩展的信息，请访问 [VS Code 扩展市场](https://code.visualstudio.com/docs/editor/extension-gallery)。
2. [.NET Core 3.1 SDK 或更高版本](https://dotnet.microsoft.com/download)

## <a name="create-a-solution"></a>创建解决方案

首先，创建一个空白解决方案来放置类库项目。 解决方案用作一个或多个项目的容器。 将其他相关项目添加到同一个解决方案中。

1. 打开 Visual Studio Code。

1. 在主菜单中选择“文件” > “打开文件夹”/“打开…”，创建“ClassLibraryProjects”文件夹，然后单击“选择文件夹”/“打开”   。

1. 在主菜单中选择“视图” > “终端”，从 Visual Studio Code 中打开“终端”  。

   “终端”在“ClassLibraryProjects”文件夹中连同命令提示符一起打开。

1. 在“终端”中输入以下命令：

   ```dotnetcli
   dotnet new sln
   ```

   终端输出如以下示例所示：

   ```
   The template "Solution File" was created successfully.
   ```

## <a name="create-a-class-library-project"></a>创建类库项目

将名为“StringLibrary”的新 .NET Standard 类库项目添加到解决方案。

1. 在终端中，运行以下命令创建库项目：

   ```dotnetcli
   dotnet new classlib -o StringLibrary
   ```

   终端输出如以下示例所示：

   ```
   The template "Class library" was created successfully.
   Processing post-creation actions...
   Running 'dotnet restore' on StringLibrary\StringLibrary.csproj...
     Determining projects to restore...
     Restore completed in 328.13 ms for C:\Projects\ClassLibraryProjects\StringLibrary\StringLibrary.csproj.
   Restore succeeded.
   ```

1. 运行以下命令，向解决方案添加库项目：

   ```dotnetcli
   dotnet sln add StringLibrary/StringLibrary.csproj
   ```

   终端输出如以下示例所示：

   ```
   Project `StringLibrary\StringLibrary.csproj` added to the solution.
   ```

1. 请检查以确保库面向 .NET Standard 的正确版本。 在资源管理器中，打开 StringLibrary/StringLibrary.csproj。

   `TargetFramework` 元素表明项目面向 .NET Standard 2.0。

   ```xml
   <Project Sdk="Microsoft.NET.Sdk">

     <PropertyGroup>
       <TargetFramework>netstandard2.0</TargetFramework>
     </PropertyGroup>

   </Project>
   ```

1. 打开 Class1.cs 并将代码替换为以下代码。

   :::code language="csharp" source="./snippets/library-with-visual-studio/csharp/StringLibrary/Class1.cs":::

   类库 `UtilityLibraries.StringLibrary`包含一个名为 `StartsWithUpper` 的方法。 此方法会返回 <xref:System.Boolean> 值，以指明当前字符串实例是否以大写字符开头。 Unicode 标准会区分大小写字符。 如果为大写字符，<xref:System.Char.IsUpper(System.Char)?displayProperty=nameWithType> 方法返回 `true`。

1. 保存该文件。

1. 运行以下命令以生成解决方案，并验证项目是否正确编译。

   ```dotnetcli
   dotnet build
   ```

   终端输出如以下示例所示：

   ```
   Microsoft (R) Build Engine version 16.6.0 for .NET Core
   Copyright (C) Microsoft Corporation. All rights reserved.
     Determining projects to restore...
     All projects are up-to-date for restore.
     You are using a preview version of .NET Core. See: https://aka.ms/dotnet-core-preview
     StringLibrary -> C:\Projects\ClassLibraryProjects\StringLibrary\bin\Debug\netstandard2.0\StringLibrary.dll
   Build succeeded.
       0 Warning(s)
       0 Error(s)
   Time Elapsed 00:00:02.78
   ```

## <a name="add-a-console-app-to-the-solution"></a>向解决方案添加控制台应用

添加使用类库的控制台应用程序。 应用将提示用户输入字符串，并报告字符串是否以大写字符开头。

1. 在终端中，运行以下命令创建控制台应用项目：

   ```dotnetcli
   dotnet new console -o ShowCase
   ```

   终端输出如以下示例所示：

   ```
   The template "Console Application" was created successfully.
   Processing post-creation actions...
   Running 'dotnet restore' on ShowCase\ShowCase.csproj...  
     Determining projects to restore...
     Restore completed in 210.78 ms for C:\Projects\ClassLibraryProjects\ShowCase\ShowCase.csproj.
   Restore succeeded.
   ```

1. 运行以下命令，向解决方案添加控制台应用项目：

   ```dotnetcli
   dotnet sln add ShowCase/ShowCase.csproj
   ```

   终端输出如以下示例所示：

   ```
   Project `ShowCase\ShowCase.csproj` added to the solution.
   ```

1. 最初，新的控制台应用项目无权访问类库。 若要允许该项目调用类库中的方法，请通过运行以下命令创建对类库项目的项目引用：

   ```dotnetcli
   dotnet add ShowCase/Showcase.csproj reference StringLibrary/StringLibrary.csproj
   ```

   终端输出如以下示例所示：

   ```
   Reference `..\StringLibrary\StringLibrary.csproj` added to the project.
   ```

1. 打开 ShowCase/Program.cs 并将所有代码替换为以下代码。

   :::code language="csharp" source="./snippets/library-with-visual-studio/csharp/ShowCase/Program.cs":::

   该代码使用 `row` 变量来维护写入到控制台窗口的数据行数计数。 如果大于或等于 25，该代码将清除控制台窗口，并向用户显示一条消息。

   该程序会提示用户输入字符串。 它会指明字符串是否以大写字符开头。 如果用户没有输入字符串就按 Enter 键，那么应用程序会终止，控制台窗口会关闭。

1. 保存更改。

1. 运行该程序。

   ```dotnetcli
   dotnet run --project ShowCase/ShowCase.csproj
   ```

1. 输入字符串并按 Enter 以试用程序，然后按 Enter 退出<kbd></kbd><kbd></kbd>。

   终端输出如以下示例所示：

   ```
   Press <Enter> only to exit; otherwise, enter a string and press <Enter>:

   A string that starts with an uppercase letter
   Input: A string that starts with an uppercase letter
   Begins with uppercase? : Yes

   A string that starts with a lowercase letter
   Input: A string that starts with a lowercase letter
   Begins with uppercase? : Yes
   ```

## <a name="additional-resources"></a>其他资源

* [使用 .NET Core CLI 开发库](libraries.md)

## <a name="next-steps"></a>后续步骤

在本教程中，你创建了一个解决方案，添加了一个库项目，并添加了一个使用该库的控制台应用项目。 在下一教程中，将向解决方案中添加单元测试项目。

> [!div class="nextstepaction"]
> [在 Visual Studio Code 中使用 .NET Core 测试 .NET Standard 库](testing-library-with-visual-studio-code.md)