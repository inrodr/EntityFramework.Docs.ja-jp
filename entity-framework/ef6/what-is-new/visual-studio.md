---
title: Visual Studio のリリース - EF6
author: divega
ms.date: 2018-07-05
ms.prod: entity-framework
ms.author: divega
ms.manager: avickers
ms.technology: entity-framework-6
ms.topic: article
ms.assetid: 028FF890-4EDB-4F03-AE53-72F9C33EC92F
caps.latest.revision: 3
ms.openlocfilehash: 7bd08a46b1d6acc5a565952e834f01546a5262c8
ms.sourcegitcommit: f05e7b62584cf228f17390bb086a61d505712e1b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/08/2018
ms.locfileid: "39121844"
---
# <a name="visual-studio-releases"></a><span data-ttu-id="2c97d-102">Visual Studio のリリース</span><span class="sxs-lookup"><span data-stu-id="2c97d-102">Visual Studio Releases</span></span>

<span data-ttu-id="2c97d-103">.NET、NuGet、および Entity Framework の最新のツールが含まれているため、常に最新バージョンの Visual Studio を使用するをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="2c97d-103">We recommend to always use the latest version of Visual Studio because it contains the latest tools for .NET, NuGet, and Entity Framework.</span></span>
<span data-ttu-id="2c97d-104">実際には、さまざまなサンプルと Entity Framework のドキュメント全体のチュートリアルは、Visual Studio の最新バージョンを使用していることをとします。</span><span class="sxs-lookup"><span data-stu-id="2c97d-104">In fact, the various samples and walkthroughs across the Entity Framework documentation assume that you are using a recent version of Visual Studio.</span></span>

<span data-ttu-id="2c97d-105">ただし、アカウントを使用して、さまざまなバージョンの Entity Framework の以前のバージョンの Visual Studio に限り、いくつかの違いはできます。</span><span class="sxs-lookup"><span data-stu-id="2c97d-105">It is possible however to use older versions of Visual Studio with different versions of Entity Framework as long as you take into account some differences:</span></span>

## <a name="visual-studio-2017-157-and-newer"></a><span data-ttu-id="2c97d-106">Visual Studio 2017 15.7年以降</span><span class="sxs-lookup"><span data-stu-id="2c97d-106">Visual Studio 2017 15.7 and newer</span></span>

- <span data-ttu-id="2c97d-107">このバージョンの Visual Studio は、Entity Framework のツールと、EF 6.2 ランタイムの最新リリースを含み、追加のセットアップ手順は必要ありません。</span><span class="sxs-lookup"><span data-stu-id="2c97d-107">This version of Visual Studio includes the latest release of Entity Framework tools and the EF 6.2 runtime, and does not require additional setup steps.</span></span>
<span data-ttu-id="2c97d-108">参照してください[新](~/ef6/what-is-new/index.md)これらのリリースの詳細についてはします。</span><span class="sxs-lookup"><span data-stu-id="2c97d-108">See [What's New](~/ef6/what-is-new/index.md) for more details on these releases.</span></span>
- <span data-ttu-id="2c97d-109">Entity Framework の EF ツールを使用して新しいプロジェクトに追加すると、EF 6.2 NuGet パッケージが自動的に追加します。</span><span class="sxs-lookup"><span data-stu-id="2c97d-109">Adding Entity Framework to new projects using the EF tools will automatically add the EF 6.2 NuGet package.</span></span>
<span data-ttu-id="2c97d-110">手動でインストールまたは使用可能な任意の EF の NuGet パッケージをオンラインでアップグレードすることができます。</span><span class="sxs-lookup"><span data-stu-id="2c97d-110">You can manually install or upgrade to any EF NuGet package available online.</span></span>
- <span data-ttu-id="2c97d-111">既定では、このバージョンの Visual Studio で使用可能な SQL Server インスタンスは、MSSQLLocalDB と呼ばれる LocalDB インスタンスです。</span><span class="sxs-lookup"><span data-stu-id="2c97d-111">By default, the SQL Server instance available with this version of Visual Studio is a LocalDB instance called MSSQLLocalDB.</span></span>
<span data-ttu-id="2c97d-112">必要がありますを使用する接続文字列のサーバーのセクションは、"(localdb)\\MSSQLLocalDB"。</span><span class="sxs-lookup"><span data-stu-id="2c97d-112">The server section of connection string you should use is "(localdb)\\MSSQLLocalDB".</span></span>
<span data-ttu-id="2c97d-113">付いて逐語的文字列を使用して、忘れず`@`または二重バック スラッシュ"\\\\"とする C# コードで接続文字列を指定する場合。</span><span class="sxs-lookup"><span data-stu-id="2c97d-113">Remember to use a verbatim string prefixed with `@` or double back-slashes "\\\\" when specifying a connection string in C# code.</span></span>  


## <a name="visual-studio-2015-to-visual-studio-2017-156"></a><span data-ttu-id="2c97d-114">Visual Studio 2015 を Visual Studio 2017 15.6</span><span class="sxs-lookup"><span data-stu-id="2c97d-114">Visual Studio 2015 to Visual Studio 2017 15.6</span></span>

- <span data-ttu-id="2c97d-115">これらのバージョン Visual Studio にはでは、Entity Framework のツールとランタイム 6.1.3 が含まれます。</span><span class="sxs-lookup"><span data-stu-id="2c97d-115">These versions of Visual Studio include Entity Framework tools and runtime 6.1.3.</span></span>
<span data-ttu-id="2c97d-116">参照してください[過去解放](~/ef6/what-is-new/past-releases.md#ef-613)これらのリリースの詳細についてはします。</span><span class="sxs-lookup"><span data-stu-id="2c97d-116">See [Past Releases](~/ef6/what-is-new/past-releases.md#ef-613) for more details on these releases.</span></span>
- <span data-ttu-id="2c97d-117">Entity Framework を EF ツールを使用して新しいプロジェクトに追加すると、EF 6.1.3 が自動的に追加 NuGet パッケージ。</span><span class="sxs-lookup"><span data-stu-id="2c97d-117">Adding Entity Framework to new projects using the EF tools will automatically add the EF 6.1.3 NuGet package.</span></span>
<span data-ttu-id="2c97d-118">手動でインストールまたは使用可能な任意の EF の NuGet パッケージをオンラインでアップグレードすることができます。</span><span class="sxs-lookup"><span data-stu-id="2c97d-118">You can manually install or upgrade to any EF NuGet package available online.</span></span>
- <span data-ttu-id="2c97d-119">既定では、このバージョンの Visual Studio で使用可能な SQL Server インスタンスは、MSSQLLocalDB と呼ばれる LocalDB インスタンスです。</span><span class="sxs-lookup"><span data-stu-id="2c97d-119">By default, the SQL Server instance available with this version of Visual Studio is a LocalDB instance called MSSQLLocalDB.</span></span>
<span data-ttu-id="2c97d-120">必要がありますを使用する接続文字列のサーバーのセクションは、"(localdb)\\MSSQLLocalDB"。</span><span class="sxs-lookup"><span data-stu-id="2c97d-120">The server section of connection string you should use is "(localdb)\\MSSQLLocalDB".</span></span>
<span data-ttu-id="2c97d-121">付いて逐語的文字列を使用して、忘れず`@`または二重バック スラッシュ"\\\\"とする C# コードで接続文字列を指定する場合。</span><span class="sxs-lookup"><span data-stu-id="2c97d-121">Remember to use a verbatim string prefixed with `@` or double back-slashes "\\\\" when specifying a connection string in C# code.</span></span>  


## <a name="visual-studio-2013"></a><span data-ttu-id="2c97d-122">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="2c97d-122">Visual Studio 2013</span></span>
- <span data-ttu-id="2c97d-123">このバージョン Visual Studio にはが含まれていて、古いバージョンの Entity Framework のツールとランタイム。</span><span class="sxs-lookup"><span data-stu-id="2c97d-123">This version of Visual Studio includes and older version of Entity Framework tools and runtime.</span></span>
<span data-ttu-id="2c97d-124">Entity Framework Tools 6.1.3 にアップグレードすることをお勧めを使用して[インストーラー](https://www.microsoft.com/en-us/download/details.aspx?id=40762) Microsoft ダウンロード センターで使用できます。</span><span class="sxs-lookup"><span data-stu-id="2c97d-124">It is recommended that you upgrade to Entity Framework Tools 6.1.3, using [the installer](https://www.microsoft.com/en-us/download/details.aspx?id=40762) available in the Microsoft Download Center.</span></span>
<span data-ttu-id="2c97d-125">参照してください[過去解放](~/ef6/what-is-new/past-releases.md#ef-613)これらのリリースの詳細についてはします。</span><span class="sxs-lookup"><span data-stu-id="2c97d-125">See [Past Releases](~/ef6/what-is-new/past-releases.md#ef-613) for more details on these releases.</span></span>
- <span data-ttu-id="2c97d-126">Entity Framework をアップグレード後の EF ツールを使用して新しいプロジェクトに追加すると、EF 6.1.3 が自動的に追加 NuGet パッケージ。</span><span class="sxs-lookup"><span data-stu-id="2c97d-126">Adding Entity Framework to new projects using the upgraded EF tools will automatically add the EF 6.1.3 NuGet package.</span></span>
<span data-ttu-id="2c97d-127">手動でインストールまたは使用可能な任意の EF の NuGet パッケージをオンラインでアップグレードすることができます。</span><span class="sxs-lookup"><span data-stu-id="2c97d-127">You can manually install or upgrade to any EF NuGet package available online.</span></span>
- <span data-ttu-id="2c97d-128">既定では、このバージョンの Visual Studio で使用可能な SQL Server インスタンスは、MSSQLLocalDB と呼ばれる LocalDB インスタンスです。</span><span class="sxs-lookup"><span data-stu-id="2c97d-128">By default, the SQL Server instance available with this version of Visual Studio is a LocalDB instance called MSSQLLocalDB.</span></span>
<span data-ttu-id="2c97d-129">必要がありますを使用する接続文字列のサーバーのセクションは、"(localdb)\\MSSQLLocalDB"。</span><span class="sxs-lookup"><span data-stu-id="2c97d-129">The server section of connection string you should use is "(localdb)\\MSSQLLocalDB".</span></span>
<span data-ttu-id="2c97d-130">付いて逐語的文字列を使用して、忘れず`@`または二重バック スラッシュ"\\\\"とする C# コードで接続文字列を指定する場合。</span><span class="sxs-lookup"><span data-stu-id="2c97d-130">Remember to use a verbatim string prefixed with `@` or double back-slashes "\\\\" when specifying a connection string in C# code.</span></span>  

## <a name="visual-studio-2012"></a><span data-ttu-id="2c97d-131">Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="2c97d-131">Visual Studio 2012</span></span>

- <span data-ttu-id="2c97d-132">このバージョン Visual Studio にはが含まれていて、古いバージョンの Entity Framework のツールとランタイム。</span><span class="sxs-lookup"><span data-stu-id="2c97d-132">This version of Visual Studio includes and older version of Entity Framework tools and runtime.</span></span>
<span data-ttu-id="2c97d-133">Entity Framework Tools 6.1.3 にアップグレードすることをお勧めを使用して[インストーラー](https://www.microsoft.com/en-us/download/details.aspx?id=40762) Microsoft ダウンロード センターで使用できます。</span><span class="sxs-lookup"><span data-stu-id="2c97d-133">It is recommended that you upgrade to Entity Framework Tools 6.1.3, using [the installer](https://www.microsoft.com/en-us/download/details.aspx?id=40762) available in the Microsoft Download Center.</span></span>
<span data-ttu-id="2c97d-134">参照してください[過去解放](~/ef6/what-is-new/past-releases.md#ef-613)これらのリリースの詳細についてはします。</span><span class="sxs-lookup"><span data-stu-id="2c97d-134">See [Past Releases](~/ef6/what-is-new/past-releases.md#ef-613) for more details on these releases.</span></span>
- <span data-ttu-id="2c97d-135">Entity Framework をアップグレード後の EF ツールを使用して新しいプロジェクトに追加すると、EF 6.1.3 が自動的に追加 NuGet パッケージ。</span><span class="sxs-lookup"><span data-stu-id="2c97d-135">Adding Entity Framework to new projects using the upgraded EF tools will automatically add the EF 6.1.3 NuGet package.</span></span>
<span data-ttu-id="2c97d-136">手動でインストールまたは使用可能な任意の EF の NuGet パッケージをオンラインでアップグレードすることができます。</span><span class="sxs-lookup"><span data-stu-id="2c97d-136">You can manually install or upgrade to any EF NuGet package available online.</span></span>
- <span data-ttu-id="2c97d-137">既定では、このバージョンの Visual Studio で使用可能な SQL Server インスタンスは、v11.0 と呼ばれる LocalDB インスタンスです。</span><span class="sxs-lookup"><span data-stu-id="2c97d-137">By default, the SQL Server instance available with this version of Visual Studio is a LocalDB instance called v11.0.</span></span>
<span data-ttu-id="2c97d-138">必要がありますを使用する接続文字列のサーバーのセクションは、"(localdb)\\v11.0"。</span><span class="sxs-lookup"><span data-stu-id="2c97d-138">The server section of connection string you should use is "(localdb)\\v11.0".</span></span>
<span data-ttu-id="2c97d-139">付いて逐語的文字列を使用して、忘れず`@`または二重バック スラッシュ"\\\\"とする C# コードで接続文字列を指定する場合。</span><span class="sxs-lookup"><span data-stu-id="2c97d-139">Remember to use a verbatim string prefixed with `@` or double back-slashes "\\\\" when specifying a connection string in C# code.</span></span>  

## <a name="visual-studio-2010"></a><span data-ttu-id="2c97d-140">Visual Studio 2010</span><span class="sxs-lookup"><span data-stu-id="2c97d-140">Visual Studio 2010</span></span>

- <span data-ttu-id="2c97d-141">このバージョンの Visual Studio で使用できるエンティティ フレームワーク ツールのバージョンでは、Entity Framework 6 のランタイムと互換性がないと、アップグレードできません。</span><span class="sxs-lookup"><span data-stu-id="2c97d-141">The version of Entity Framework Tools available with this version of Visual Studio is not compatible with the Entity Framework 6 runtime and cannot be upgraded.</span></span>
- <span data-ttu-id="2c97d-142">既定では、Entity Framework ツールは、プロジェクトに Entity Framework 4.0 を追加します。</span><span class="sxs-lookup"><span data-stu-id="2c97d-142">By default, the Entity Framework tools will add Entity Framework 4.0 to your projects.</span></span>
<span data-ttu-id="2c97d-143">すべての新しいバージョンの EF を使用してアプリケーションを作成するために必要がありますをインストールする、 [NuGet パッケージ マネージャー拡張機能](https://marketplace.visualstudio.com/items?itemName=NuGetTeam.NuGetPackageManager)します。</span><span class="sxs-lookup"><span data-stu-id="2c97d-143">In order to create applications using any newer versions of EF, you will first need to install the [NuGet Package Manager extension](https://marketplace.visualstudio.com/items?itemName=NuGetTeam.NuGetPackageManager).</span></span>
- <span data-ttu-id="2c97d-144">既定では、EF ツールのバージョンですべてのコード生成を EntityObject および Entity Framework 4 に基づきます。</span><span class="sxs-lookup"><span data-stu-id="2c97d-144">By default, all code generation in the version of EF tools is based on EntityObject and Entity Framework 4.</span></span>
<span data-ttu-id="2c97d-145">DbContext と Entity Framework 5、に基づいて用 DbContext のコード生成テンプレートをインストールすることによって、コード生成を切り替えることをお勧めします。 [c#](https://marketplace.visualstudio.com/items?itemName=EntityFrameworkTeam.EF5xDbContextGeneratorforC)または[Visual Basic](https://marketplace.visualstudio.com/items?itemName=EntityFrameworkTeam.EF5xDbContextGeneratorforVBNET)します。</span><span class="sxs-lookup"><span data-stu-id="2c97d-145">We recommend that you switch the code generation to be based on DbContext and Entity Framework 5, by installing the DbContext code generation templates for [C#](https://marketplace.visualstudio.com/items?itemName=EntityFrameworkTeam.EF5xDbContextGeneratorforC) or [Visual Basic](https://marketplace.visualstudio.com/items?itemName=EntityFrameworkTeam.EF5xDbContextGeneratorforVBNET).</span></span>
- <span data-ttu-id="2c97d-146">NuGet パッケージ マネージャー拡張機能をインストールすると、手動でインストールまたはオンラインで利用可能な任意の EF の NuGet パッケージをアップグレードでき EF6 を使用して、デザイナーが必要としない Code First で使用できます。</span><span class="sxs-lookup"><span data-stu-id="2c97d-146">Once you have installed the NuGet Package Manager extensions, you can manually install or upgrade to any EF NuGet package available online and use EF6 with Code First, which does not require a designer.</span></span>
- <span data-ttu-id="2c97d-147">既定では、このバージョンの Visual Studio で使用可能な SQL Server インスタンスは、SQL Server Express SQLEXPRESS という名前です。</span><span class="sxs-lookup"><span data-stu-id="2c97d-147">By default, the SQL Server instance available with this version of Visual Studio is SQL Server Express named SQLEXPRESS.</span></span>
<span data-ttu-id="2c97d-148">必要がありますを使用する接続文字列のサーバーのセクションは、"。\\SQLEXPRESS"。</span><span class="sxs-lookup"><span data-stu-id="2c97d-148">The server section of connection string you should use is ".\\SQLEXPRESS".</span></span>
<span data-ttu-id="2c97d-149">付いて逐語的文字列を使用して、忘れず`@`または二重バック スラッシュ"\\\\"とする C# コードで接続文字列を指定する場合。</span><span class="sxs-lookup"><span data-stu-id="2c97d-149">Remember to use a verbatim string prefixed with `@` or double back-slashes "\\\\" when specifying a connection string in C# code.</span></span>