---
title: WPF の EF6 とのデータ バインド
author: divega
ms.date: 2016-10-23
ms.prod: entity-framework
ms.author: divega
ms.manager: avickers
ms.technology: entity-framework-6
ms.topic: article
ms.assetid: e90d48e6-bea5-47ef-b756-7b89cce4daf0
caps.latest.revision: 3
ms.openlocfilehash: 1756ec14fe83d80199b6040bd345dc2fe6294281
ms.sourcegitcommit: f05e7b62584cf228f17390bb086a61d505712e1b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/08/2018
ms.locfileid: "39122307"
---
# <a name="databinding-with-wpf"></a><span data-ttu-id="f619b-102">WPF とのデータ バインド</span><span class="sxs-lookup"><span data-stu-id="f619b-102">Databinding with WPF</span></span>
<span data-ttu-id="f619b-103">このステップ バイ ステップ チュートリアルでは、POCO 型を「マスター/詳細」の形式での WPF コントロールにバインドする方法を示します。</span><span class="sxs-lookup"><span data-stu-id="f619b-103">This step-by-step walkthrough shows how to bind POCO types to WPF controls in a “master-detail" form.</span></span> <span data-ttu-id="f619b-104">アプリケーションでは、Entity Framework の Api を使用して、データベースからデータをオブジェクトに設定、変更の追跡、およびデータベースにデータを保持します。</span><span class="sxs-lookup"><span data-stu-id="f619b-104">The application uses the Entity Framework APIs to populate objects with data from the database, track changes, and persist data to the database.</span></span>

<span data-ttu-id="f619b-105">モデルが一対多のリレーションシップに参加している 2 つの型を定義します。**カテゴリ**(プリンシパル\\マスター) と**製品**(依存\\詳細)。</span><span class="sxs-lookup"><span data-stu-id="f619b-105">The model defines two types that participate in one-to-many relationship: **Category** (principal\\master) and **Product** (dependent\\detail).</span></span> <span data-ttu-id="f619b-106">次に、Visual Studio ツールは、WPF コントロール モデルで定義された型のバインドに使用されます。</span><span class="sxs-lookup"><span data-stu-id="f619b-106">Then, the Visual Studio tools are used to bind the types defined in the model to the WPF controls.</span></span> <span data-ttu-id="f619b-107">WPF データ バインディング フレームワークにより、関連するオブジェクト間のナビゲーション: により、対応する子データで更新する詳細ビューがマスター ビューの行を選択します。</span><span class="sxs-lookup"><span data-stu-id="f619b-107">The WPF data-binding framework enables navigation between related objects: selecting rows in the master view causes the detail view to update with the corresponding child data.</span></span>

<span data-ttu-id="f619b-108">スクリーン ショットとこのチュートリアルで示した各コードは、Visual Studio 2013 から取得されますが、このチュートリアルでは、Visual Studio 2012 または Visual Studio 2010 を行うことができます。</span><span class="sxs-lookup"><span data-stu-id="f619b-108">The screen shots and code listings in this walkthrough are taken from Visual Studio 2013 but you can complete this walkthrough with Visual Studio 2012 or Visual Studio 2010.</span></span>

## <a name="use-the-object-option-for-creating-wpf-data-sources"></a><span data-ttu-id="f619b-109">WPF のデータ ソースを作成するため、'Object' オプションを使用します。</span><span class="sxs-lookup"><span data-stu-id="f619b-109">Use the 'Object' Option for Creating WPF Data Sources</span></span>

<span data-ttu-id="f619b-110">Entity Framework の以前のバージョンを使用して推奨を使用して、**データベース**EF Designer で作成したモデルに基づいて新しいデータ ソースを作成するときのオプションします。</span><span class="sxs-lookup"><span data-stu-id="f619b-110">With previous version of Entity Framework we used to recommend using the **Database** option when creating a new Data Source based on a model created with the EF Designer.</span></span> <span data-ttu-id="f619b-111">これは、ObjectContext から派生したコンテキストとエンティティ クラスを EntityObject から派生したデザイナーが生成するためでした。</span><span class="sxs-lookup"><span data-stu-id="f619b-111">This was because the designer would generate a context that derived from ObjectContext and entity classes that derived from EntityObject.</span></span> <span data-ttu-id="f619b-112">データベース オプションを使用してこの API サーフェスと対話するための最適なコードを記述してくれます。</span><span class="sxs-lookup"><span data-stu-id="f619b-112">Using the Database option would help you write the best code for interacting with this API surface.</span></span>

<span data-ttu-id="f619b-113">Visual Studio 2012 および Visual Studio 2013 用の EF デザイナーでは、単純な POCO エンティティ クラスと DbContext から派生したコンテキストを生成します。</span><span class="sxs-lookup"><span data-stu-id="f619b-113">The EF Designers for Visual Studio 2012 and Visual Studio 2013 generate a context that derives from DbContext together with simple POCO entity classes.</span></span> <span data-ttu-id="f619b-114">Visual Studio 2010 で、このチュートリアルの後半で説明したように DbContext を使用するコード生成テンプレートにスワップをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="f619b-114">With Visual Studio 2010 we recommend swapping to a code generation template that uses DbContext as described later in this walkthrough.</span></span>

<span data-ttu-id="f619b-115">使用する必要があります、DbContext API サーフェスを使用する場合、**オブジェクト**このチュートリアルで示すように、新しいデータ ソースを作成するときのオプションします。</span><span class="sxs-lookup"><span data-stu-id="f619b-115">When using the DbContext API surface you should use the **Object** option when creating a new Data Source, as shown in this walkthrough.</span></span>

<span data-ttu-id="f619b-116">場合は、必要な[ObjectContext に基づくコードの生成に戻す](~/ef6/modeling/designer/codegen/legacy-objectcontext.md)EF Designer で作成されたモデル。</span><span class="sxs-lookup"><span data-stu-id="f619b-116">If needed, you can [revert to ObjectContext based code generation](~/ef6/modeling/designer/codegen/legacy-objectcontext.md) for models created with the EF Designer.</span></span>

## <a name="pre-requisites"></a><span data-ttu-id="f619b-117">前提条件</span><span class="sxs-lookup"><span data-stu-id="f619b-117">Pre-Requisites</span></span>

<span data-ttu-id="f619b-118">Visual Studio 2013 を持っている必要があります、このチュートリアルを完了する、Visual Studio 2012 または Visual Studio 2010 がインストールされています。</span><span class="sxs-lookup"><span data-stu-id="f619b-118">You need to have Visual Studio 2013, Visual Studio 2012 or Visual Studio 2010 installed to complete this walkthrough.</span></span>

<span data-ttu-id="f619b-119">Visual Studio 2010 を使用している場合は、NuGet をインストールする必要があります。</span><span class="sxs-lookup"><span data-stu-id="f619b-119">If you are using Visual Studio 2010, you also have to install NuGet.</span></span> <span data-ttu-id="f619b-120">詳細については、次を参照してください。[をインストールする NuGet](http://docs.nuget.org/docs/start-here/installing-nuget)します。</span><span class="sxs-lookup"><span data-stu-id="f619b-120">For more information, see [Installing NuGet](http://docs.nuget.org/docs/start-here/installing-nuget).</span></span>  

## <a name="create-the-application"></a><span data-ttu-id="f619b-121">アプリケーションを作成する</span><span class="sxs-lookup"><span data-stu-id="f619b-121">Create the Application</span></span>

-   <span data-ttu-id="f619b-122">Visual Studio を開く</span><span class="sxs-lookup"><span data-stu-id="f619b-122">Open Visual Studio</span></span>
-   <span data-ttu-id="f619b-123">**ファイル -&gt;新機能 -&gt;プロジェクト.**</span><span class="sxs-lookup"><span data-stu-id="f619b-123">**File -&gt; New -&gt; Project….**</span></span>
-   <span data-ttu-id="f619b-124">選択**Windows**左側のウィンドウで、 **WPFApplication**右側のウィンドウで</span><span class="sxs-lookup"><span data-stu-id="f619b-124">Select **Windows** in the left pane and **WPFApplication** in the right pane</span></span>
-   <span data-ttu-id="f619b-125">入力**WPFwithEFSample**名として</span><span class="sxs-lookup"><span data-stu-id="f619b-125">Enter **WPFwithEFSample** as the name</span></span>
-   <span data-ttu-id="f619b-126">**[OK]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="f619b-126">Select **OK**</span></span>

## <a name="install-the-entity-framework-nuget-package"></a><span data-ttu-id="f619b-127">Entity Framework NuGet パッケージをインストールします。</span><span class="sxs-lookup"><span data-stu-id="f619b-127">Install the Entity Framework NuGet package</span></span>

-   <span data-ttu-id="f619b-128">ソリューション エクスプ ローラーを右クリックし、 **WinFormswithEFSample**プロジェクト</span><span class="sxs-lookup"><span data-stu-id="f619b-128">In Solution Explorer, right-click on the **WinFormswithEFSample** project</span></span>
-   <span data-ttu-id="f619b-129">選択**NuGet パッケージを管理しています.**</span><span class="sxs-lookup"><span data-stu-id="f619b-129">Select **Manage NuGet Packages…**</span></span>
-   <span data-ttu-id="f619b-130">NuGet パッケージの管理 ダイアログ ボックスで、、**オンライン** タブで選択し、 **EntityFramework**パッケージ</span><span class="sxs-lookup"><span data-stu-id="f619b-130">In the Manage NuGet Packages dialog, Select the **Online** tab and choose the **EntityFramework** package</span></span>
-   <span data-ttu-id="f619b-131">クリックして**インストール**</span><span class="sxs-lookup"><span data-stu-id="f619b-131">Click **Install**</span></span>  
    >[!NOTE]
    > <span data-ttu-id="f619b-132">EntityFramework アセンブリだけでなく System.ComponentModel.DataAnnotations への参照も追加されます。</span><span class="sxs-lookup"><span data-stu-id="f619b-132">In addition to the EntityFramework assembly a reference to System.ComponentModel.DataAnnotations is also added.</span></span> <span data-ttu-id="f619b-133">System.Data.Entity への参照をプロジェクトには場合、は、EntityFramework パッケージがインストールされている場合、削除するされます。</span><span class="sxs-lookup"><span data-stu-id="f619b-133">If the project has a reference to System.Data.Entity, then it will be removed when the EntityFramework package is installed.</span></span> <span data-ttu-id="f619b-134">System.Data.Entity アセンブリは Entity Framework 6 アプリケーションは使用されません。</span><span class="sxs-lookup"><span data-stu-id="f619b-134">The System.Data.Entity assembly is no longer used for Entity Framework 6 applications.</span></span>

## <a name="define-a-model"></a><span data-ttu-id="f619b-135">モデルを定義します。</span><span class="sxs-lookup"><span data-stu-id="f619b-135">Define a Model</span></span>

<span data-ttu-id="f619b-136">できます、このチュートリアルでは、Code First または EF Designer を使用してモデルを実装するために選択しました。</span><span class="sxs-lookup"><span data-stu-id="f619b-136">In this walkthrough you can chose to implement a model using Code First or the EF Designer.</span></span> <span data-ttu-id="f619b-137">2 つのセクションでは、次のいずれかを完了します。</span><span class="sxs-lookup"><span data-stu-id="f619b-137">Complete one of the two following sections.</span></span>

### <a name="option-1-define-a-model-using-code-first"></a><span data-ttu-id="f619b-138">オプション 1: Code First を使用してモデルを定義します。</span><span class="sxs-lookup"><span data-stu-id="f619b-138">Option 1: Define a Model using Code First</span></span>

<span data-ttu-id="f619b-139">このセクションでは、モデルおよび関連する Code First を使用してデータベースを作成する方法を示します。</span><span class="sxs-lookup"><span data-stu-id="f619b-139">This section shows how to create a model and its associated database using Code First.</span></span> <span data-ttu-id="f619b-140">次のセクションにスキップ (**オプション 2: Database First を使用してモデルを定義)** エンジニア リング EF designer を使用してデータベースからモデルを使用する場合は、データベースの最初を逆にします。</span><span class="sxs-lookup"><span data-stu-id="f619b-140">Skip to the next section (**Option 2: Define a model using Database First)** if you would rather use Database First to reverse engineer your model from a database using the EF designer</span></span>

<span data-ttu-id="f619b-141">Code First の開発を使用する場合に、(ドメイン) の概念モデルを定義する .NET Framework クラスを記述することで、通常で開始します。</span><span class="sxs-lookup"><span data-stu-id="f619b-141">When using Code First development you usually begin by writing .NET Framework classes that define your conceptual (domain) model.</span></span>

-   <span data-ttu-id="f619b-142">新しいクラスを追加、 **WPFwithEFSample:**</span><span class="sxs-lookup"><span data-stu-id="f619b-142">Add a new class to the **WPFwithEFSample:**</span></span>
    -   <span data-ttu-id="f619b-143">プロジェクト名を右クリックします。</span><span class="sxs-lookup"><span data-stu-id="f619b-143">Right-click on the project name</span></span>
    -   <span data-ttu-id="f619b-144">選択**追加**、し**新しい項目**</span><span class="sxs-lookup"><span data-stu-id="f619b-144">Select **Add**, then **New Item**</span></span>
    -   <span data-ttu-id="f619b-145">選択**クラス**入力**製品**クラス名</span><span class="sxs-lookup"><span data-stu-id="f619b-145">Select **Class** and enter **Product** for the class name</span></span>
-   <span data-ttu-id="f619b-146">置換、**製品**クラス定義を次のコード。</span><span class="sxs-lookup"><span data-stu-id="f619b-146">Replace the **Product** class definition with the following code:</span></span>

``` csharp
    namespace WPFwithEFSample
    {
        public class Product
        {
            public int ProductId { get; set; }
            public string Name { get; set; }

            public int CategoryId { get; set; }
            public virtual Category Category { get; set; }
        }
    }

-   Add a **Category** class with the following definition:

    using System.Collections.ObjectModel;

    namespace WPFwithEFSample
    {
        public class Category
        {
            public Category()
            {
                this.Products = new ObservableCollection<Product>();
            }

            public int CategoryId { get; set; }
            public string Name { get; set; }

            public virtual ObservableCollection<Product> Products { get; private set; }
        }
    }
```

<span data-ttu-id="f619b-147">**製品**プロパティを**カテゴリ**クラスと**カテゴリ**プロパティを**製品**クラスは、ナビゲーション プロパティ。</span><span class="sxs-lookup"><span data-stu-id="f619b-147">The **Products** property on the **Category** class and **Category** property on the **Product** class are navigation properties.</span></span> <span data-ttu-id="f619b-148">Entity Framework では、ナビゲーション プロパティは、2 つのエンティティ型間のリレーションシップを移動する方法を提供します。</span><span class="sxs-lookup"><span data-stu-id="f619b-148">In Entity Framework, navigation properties provide a way to navigate a relationship between two entity types.</span></span>

<span data-ttu-id="f619b-149">エンティティを定義するだけでなくを DbContext から派生し、DbSet を公開するクラスを定義する必要があります。&lt;TEntity&gt;プロパティ。</span><span class="sxs-lookup"><span data-stu-id="f619b-149">In addition to defining entities, you need to define a class that derives from DbContext and exposes DbSet&lt;TEntity&gt; properties.</span></span> <span data-ttu-id="f619b-150">DbSet&lt;TEntity&gt;プロパティは、モデルに追加する型も把握してコンテキストを使用します。</span><span class="sxs-lookup"><span data-stu-id="f619b-150">The DbSet&lt;TEntity&gt; properties let the context know which types you want to include in the model.</span></span>

<span data-ttu-id="f619b-151">DbContext 派生型のインスタンスがデータベースからデータを使用してオブジェクトの設定が含まれています。 ランタイム処理中に、エンティティ オブジェクトを管理、追跡、および永続化するデータをデータベースに変更します。</span><span class="sxs-lookup"><span data-stu-id="f619b-151">An instance of the DbContext derived type manages the entity objects during run time, which includes populating objects with data from a database, change tracking, and persisting data to the database.</span></span>

-   <span data-ttu-id="f619b-152">新しい追加**ProductContext**クラスをプロジェクトに次の定義。</span><span class="sxs-lookup"><span data-stu-id="f619b-152">Add a new **ProductContext** class to the project with the following definition:</span></span>

``` csharp
    using System.Data.Entity;

    namespace WPFwithEFSample
    {
        public class ProductContext : DbContext
        {
            public DbSet<Category> Categories { get; set; }
            public DbSet<Product> Products { get; set; }
        }
    }
```

<span data-ttu-id="f619b-153">プロジェクトをコンパイルします。</span><span class="sxs-lookup"><span data-stu-id="f619b-153">Compile the project.</span></span>

### <a name="option-2-define-a-model-using-database-first"></a><span data-ttu-id="f619b-154">オプション 2: Database First を使用してモデルを定義します。</span><span class="sxs-lookup"><span data-stu-id="f619b-154">Option 2: Define a model using Database First</span></span>

<span data-ttu-id="f619b-155">このセクションでは、EF designer を使用してデータベースからモデルをリバース エンジニア リング Database First を使用する方法を示します。</span><span class="sxs-lookup"><span data-stu-id="f619b-155">This section shows how to use Database First to reverse engineer your model from a database using the EF designer.</span></span> <span data-ttu-id="f619b-156">前のセクションを完了している場合 (**オプション 1: Code First を使用してモデルを定義)**、このセクションをスキップし、すぐに進んで、 **Lazy Loading**セクション。</span><span class="sxs-lookup"><span data-stu-id="f619b-156">If you completed the previous section (**Option 1: Define a model using Code First)**, then skip this section and go straight to the **Lazy Loading** section.</span></span>

#### <a name="create-an-existing-database"></a><span data-ttu-id="f619b-157">既存のデータベースを作成します。</span><span class="sxs-lookup"><span data-stu-id="f619b-157">Create an Existing Database</span></span>

<span data-ttu-id="f619b-158">通常それは既に作成されて、既存のデータベースを対象としているときに、このチュートリアルではアクセスするデータベースを作成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="f619b-158">Typically when you are targeting an existing database it will already be created, but for this walkthrough we need to create a database to access.</span></span>

<span data-ttu-id="f619b-159">Visual Studio と共にインストールされているデータベース サーバーは、インストールした Visual Studio のバージョンによって異なります。</span><span class="sxs-lookup"><span data-stu-id="f619b-159">The database server that is installed with Visual Studio is different depending on the version of Visual Studio you have installed:</span></span>

-   <span data-ttu-id="f619b-160">Visual Studio 2010 を使用している場合は、SQL Express データベースを作成するがします。</span><span class="sxs-lookup"><span data-stu-id="f619b-160">If you are using Visual Studio 2010 you'll be creating a SQL Express database.</span></span>
-   <span data-ttu-id="f619b-161">Visual Studio 2012 を使用しているかどうかは、作成する、 [LocalDB](https://msdn.microsoft.com/library/hh510202.aspx)データベース。</span><span class="sxs-lookup"><span data-stu-id="f619b-161">If you are using Visual Studio 2012 then you'll be creating a [LocalDB](https://msdn.microsoft.com/library/hh510202.aspx) database.</span></span>

<span data-ttu-id="f619b-162">データベースを生成してみましょう。</span><span class="sxs-lookup"><span data-stu-id="f619b-162">Let's go ahead and generate the database.</span></span>

-   <span data-ttu-id="f619b-163">**ビュー -&gt;サーバー エクスプ ローラー**</span><span class="sxs-lookup"><span data-stu-id="f619b-163">**View -&gt; Server Explorer**</span></span>
-   <span data-ttu-id="f619b-164">右クリックして**データ接続 -&gt;接続の追加.**</span><span class="sxs-lookup"><span data-stu-id="f619b-164">Right click on **Data Connections -&gt; Add Connection…**</span></span>
-   <span data-ttu-id="f619b-165">場合、まだデータベースに接続して、サーバー エクスプ ローラーから前に、データ ソースとして Microsoft SQL Server を選択する必要があります。</span><span class="sxs-lookup"><span data-stu-id="f619b-165">If you haven’t connected to a database from Server Explorer before you’ll need to select Microsoft SQL Server as the data source</span></span>

    ![ChangeDataSource](~/ef6/media/changedatasource.png)

-   <span data-ttu-id="f619b-167">LocalDB または SQL Express をインストールしたものに応じてのいずれかに接続し、入力**製品**データベース名として</span><span class="sxs-lookup"><span data-stu-id="f619b-167">Connect to either LocalDB or SQL Express, depending on which one you have installed, and enter **Products** as the database name</span></span>

    ![AddConnectionLocalDB](~/ef6/media/addconnectionlocaldb.png)

    ![AddConnectionExpress](~/ef6/media/addconnectionexpress.png)

-   <span data-ttu-id="f619b-170">選択**OK**かどうかは、新しいデータベースを作成するように要求がある **[はい]**</span><span class="sxs-lookup"><span data-stu-id="f619b-170">Select **OK** and you will be asked if you want to create a new database, select **Yes**</span></span>

    ![CreateDatabase](~/ef6/media/createdatabase.png)

-   <span data-ttu-id="f619b-172">新しいデータベースがサーバー エクスプ ローラーに表示されますを右クリックして選択**新しいクエリ**</span><span class="sxs-lookup"><span data-stu-id="f619b-172">The new database will now appear in Server Explorer, right-click on it and select **New Query**</span></span>
-   <span data-ttu-id="f619b-173">新しいクエリに、次の SQL をコピーし、クエリを選択します右クリックし、 **Execute**</span><span class="sxs-lookup"><span data-stu-id="f619b-173">Copy the following SQL into the new query, then right-click on the query and select **Execute**</span></span>

``` SQL
    CREATE TABLE [dbo].[Categories] (
        [CategoryId] [int] NOT NULL IDENTITY,
        [Name] [nvarchar](max),
        CONSTRAINT [PK_dbo.Categories] PRIMARY KEY ([CategoryId])
    )

    CREATE TABLE [dbo].[Products] (
        [ProductId] [int] NOT NULL IDENTITY,
        [Name] [nvarchar](max),
        [CategoryId] [int] NOT NULL,
        CONSTRAINT [PK_dbo.Products] PRIMARY KEY ([ProductId])
    )

    CREATE INDEX [IX_CategoryId] ON [dbo].[Products]([CategoryId])

    ALTER TABLE [dbo].[Products] ADD CONSTRAINT [FK_dbo.Products_dbo.Categories_CategoryId] FOREIGN KEY ([CategoryId]) REFERENCES [dbo].[Categories] ([CategoryId]) ON DELETE CASCADE
```

#### <a name="reverse-engineer-model"></a><span data-ttu-id="f619b-174">リバース エンジニア リング モデル</span><span class="sxs-lookup"><span data-stu-id="f619b-174">Reverse Engineer Model</span></span>

<span data-ttu-id="f619b-175">Visual Studio の一部として含まれている Entity Framework デザイナーを使用してモデルを作成することになります。</span><span class="sxs-lookup"><span data-stu-id="f619b-175">We’re going to make use of Entity Framework Designer, which is included as part of Visual Studio, to create our model.</span></span>

-   <span data-ttu-id="f619b-176">**プロジェクト -&gt;新しい項目を追加しています.**</span><span class="sxs-lookup"><span data-stu-id="f619b-176">**Project -&gt; Add New Item…**</span></span>
-   <span data-ttu-id="f619b-177">選択**データ**左側のメニューをクリックし**ADO.NET Entity Data Model**</span><span class="sxs-lookup"><span data-stu-id="f619b-177">Select **Data** from the left menu and then **ADO.NET Entity Data Model**</span></span>
-   <span data-ttu-id="f619b-178">入力**ProductModel**名をクリックします**OK**</span><span class="sxs-lookup"><span data-stu-id="f619b-178">Enter **ProductModel** as the name and click **OK**</span></span>
-   <span data-ttu-id="f619b-179">これにより、起動、 **Entity Data Model ウィザード**</span><span class="sxs-lookup"><span data-stu-id="f619b-179">This launches the **Entity Data Model Wizard**</span></span>
-   <span data-ttu-id="f619b-180">選択**データベースから生成**クリック **[次へ]**</span><span class="sxs-lookup"><span data-stu-id="f619b-180">Select **Generate from Database** and click **Next**</span></span>

    ![ChooseModelContents](~/ef6/media/choosemodelcontents.png)

-   <span data-ttu-id="f619b-182">最初のセクションで作成したデータベース接続を選択して、入力**ProductContext**をクリックして、接続文字列の名前として **[次へ]**</span><span class="sxs-lookup"><span data-stu-id="f619b-182">Select the connection to the database you created in the first section, enter **ProductContext** as the name of the connection string and click **Next**</span></span>

    ![ChooseYourConnection](~/ef6/media/chooseyourconnection.png)

-   <span data-ttu-id="f619b-184">すべてのテーブルをインポートし、[完了] をクリックします。 'テーブル' の横にあるチェック ボックスをクリックします。</span><span class="sxs-lookup"><span data-stu-id="f619b-184">Click the checkbox next to ‘Tables’ to import all tables and click ‘Finish’</span></span>

    ![ChooseYourObjects](~/ef6/media/chooseyourobjects.png)

<span data-ttu-id="f619b-186">リバース エンジニア リング プロセスが完了すると、新しいモデルがプロジェクトに追加しを開いて、Entity Framework デザイナーで表示することです。</span><span class="sxs-lookup"><span data-stu-id="f619b-186">Once the reverse engineer process completes the new model is added to your project and opened up for you to view in the Entity Framework Designer.</span></span> <span data-ttu-id="f619b-187">App.config ファイルが、データベースの接続詳細を含むプロジェクトにも追加されました。</span><span class="sxs-lookup"><span data-stu-id="f619b-187">An App.config file has also been added to your project with the connection details for the database.</span></span>

#### <a name="additional-steps-in-visual-studio-2010"></a><span data-ttu-id="f619b-188">Visual Studio 2010 で追加の手順</span><span class="sxs-lookup"><span data-stu-id="f619b-188">Additional Steps in Visual Studio 2010</span></span>

<span data-ttu-id="f619b-189">Visual Studio 2010 で作業している場合は、EF6 コード生成を使用する EF designer を更新する必要があります。</span><span class="sxs-lookup"><span data-stu-id="f619b-189">If you are working in Visual Studio 2010 then you will need to update the EF designer to use EF6 code generation.</span></span>

-   <span data-ttu-id="f619b-190">EF Designer でのモデルの空いている場所を右クリックして**コード生成項目の追加.**</span><span class="sxs-lookup"><span data-stu-id="f619b-190">Right-click on an empty spot of your model in the EF Designer and select **Add Code Generation Item…**</span></span>
-   <span data-ttu-id="f619b-191">選択**オンライン テンプレート**、左側のメニューと検索から**DbContext**</span><span class="sxs-lookup"><span data-stu-id="f619b-191">Select **Online Templates** from the left menu and search for **DbContext**</span></span>
-   <span data-ttu-id="f619b-192">選択、 **EF 6.x C 用 DbContext ジェネレーター\#、** 入力**ProductsModel**名として追加 をクリック</span><span class="sxs-lookup"><span data-stu-id="f619b-192">Select the **EF 6.x DbContext Generator for C\#,** enter **ProductsModel** as the name and click Add</span></span>

#### <a name="updating-code-generation-for-data-binding"></a><span data-ttu-id="f619b-193">データ バインディングの更新のコード生成</span><span class="sxs-lookup"><span data-stu-id="f619b-193">Updating code generation for data binding</span></span>

<span data-ttu-id="f619b-194">EF では、T4 テンプレートを使用して、モデルからコードを生成します。</span><span class="sxs-lookup"><span data-stu-id="f619b-194">EF generates code from your model using T4 templates.</span></span> <span data-ttu-id="f619b-195">Visual Studio に付属のか、Visual Studio ギャラリーからダウンロードしたテンプレートは、一般的な用途に使用されるもの。</span><span class="sxs-lookup"><span data-stu-id="f619b-195">The templates shipped with Visual Studio or downloaded from the Visual Studio gallery are intended for general purpose use.</span></span> <span data-ttu-id="f619b-196">つまり、これらのテンプレートから生成されたエンティティがある単純な ICollection&lt;T&gt;プロパティ。</span><span class="sxs-lookup"><span data-stu-id="f619b-196">This means that the entities generated from these templates have simple ICollection&lt;T&gt; properties.</span></span> <span data-ttu-id="f619b-197">ただし、データを実施する際に WPF を使用したバインドが使用することが望ましい**ObservableCollection**コレクションのプロパティを WPF の追跡できる、コレクションに加えられた変更のためにします。</span><span class="sxs-lookup"><span data-stu-id="f619b-197">However, when doing data binding using WPF it is desirable to use **ObservableCollection** for collection properties so that WPF can keep track of changes made to the collections.</span></span> <span data-ttu-id="f619b-198">我々 はこれに対応する ObservableCollection を使用するテンプレートを変更します。</span><span class="sxs-lookup"><span data-stu-id="f619b-198">To this end we will to modify the templates to use ObservableCollection.</span></span>

-   <span data-ttu-id="f619b-199">開く、**ソリューション エクスプ ローラー**を見つけて**ProductModel.edmx**ファイル</span><span class="sxs-lookup"><span data-stu-id="f619b-199">Open the **Solution Explorer** and find **ProductModel.edmx** file</span></span>
-   <span data-ttu-id="f619b-200">検索、 **ProductModel.tt** ProductModel.edmx ファイルの下で入れ子にはファイル</span><span class="sxs-lookup"><span data-stu-id="f619b-200">Find the **ProductModel.tt** file which will be nested under the ProductModel.edmx file</span></span>

    ![WpfProductModelTemplate](~/ef6/media/wpfproductmodeltemplate.png)

-   <span data-ttu-id="f619b-202">Visual Studio エディターで開く ProductModel.tt ファイルをダブルクリックします</span><span class="sxs-lookup"><span data-stu-id="f619b-202">Double-click on the ProductModel.tt file to open it in the Visual Studio editor</span></span>
-   <span data-ttu-id="f619b-203">検索し、置換の 2 つの出現回数"**ICollection**"with"**ObservableCollection**"。</span><span class="sxs-lookup"><span data-stu-id="f619b-203">Find and replace the two occurrences of “**ICollection**” with “**ObservableCollection**”.</span></span> <span data-ttu-id="f619b-204">これらは、約 296 および 484 行にあります。</span><span class="sxs-lookup"><span data-stu-id="f619b-204">These are located approximately at lines 296 and 484.</span></span>
-   <span data-ttu-id="f619b-205">検索し、置換の最初に見つかった"**HashSet**"with"**ObservableCollection**"。</span><span class="sxs-lookup"><span data-stu-id="f619b-205">Find and replace the first occurrence of “**HashSet**” with “**ObservableCollection**”.</span></span> <span data-ttu-id="f619b-206">この状況の発生が約 50 行に配置されています。</span><span class="sxs-lookup"><span data-stu-id="f619b-206">This occurrence is located approximately at line 50.</span></span> <span data-ttu-id="f619b-207">**しない**HashSet は後で、コードの 2 番目に出現を置換します。</span><span class="sxs-lookup"><span data-stu-id="f619b-207">**Do not** replace the second occurrence of HashSet found later in the code.</span></span>
-   <span data-ttu-id="f619b-208">検索し、置換のみ出現"**System.Collections.Generic**"with"**System.Collections.ObjectModel**"。</span><span class="sxs-lookup"><span data-stu-id="f619b-208">Find and replace the only occurrence of “**System.Collections.Generic**” with “**System.Collections.ObjectModel**”.</span></span> <span data-ttu-id="f619b-209">これは約 424 の行にあります。</span><span class="sxs-lookup"><span data-stu-id="f619b-209">This is located approximately at line 424.</span></span>
-   <span data-ttu-id="f619b-210">ProductModel.tt ファイルを保存します。</span><span class="sxs-lookup"><span data-stu-id="f619b-210">Save the ProductModel.tt file.</span></span> <span data-ttu-id="f619b-211">これは、再生成するエンティティのコードで発生する必要があります。</span><span class="sxs-lookup"><span data-stu-id="f619b-211">This should cause the code for entities to be regenerated.</span></span> <span data-ttu-id="f619b-212">コードは自動的に再生成しない場合は、ProductModel.tt を右クリックし、「カスタム ツールの実行」を選択します。</span><span class="sxs-lookup"><span data-stu-id="f619b-212">If the code does not regenerate automatically, then right click on ProductModel.tt and choose “Run Custom Tool”.</span></span>

<span data-ttu-id="f619b-213">かどうか (これは ProductModel.tt 下で入れ子になった) Category.cs ファイルを開くようになりましたし、製品のコレクションが、型を持つことを確認する必要があります**ObservableCollection&lt;製品&gt;** します。</span><span class="sxs-lookup"><span data-stu-id="f619b-213">If you now open the Category.cs file (which is nested under ProductModel.tt) then you should see that the Products collection has the type **ObservableCollection&lt;Product&gt;**.</span></span>

<span data-ttu-id="f619b-214">プロジェクトをコンパイルします。</span><span class="sxs-lookup"><span data-stu-id="f619b-214">Compile the project.</span></span>

## <a name="lazy-loading"></a><span data-ttu-id="f619b-215">遅延読み込み</span><span class="sxs-lookup"><span data-stu-id="f619b-215">Lazy Loading</span></span>

<span data-ttu-id="f619b-216">**製品**プロパティを**カテゴリ**クラスと**カテゴリ**プロパティを**製品**クラスは、ナビゲーション プロパティ。</span><span class="sxs-lookup"><span data-stu-id="f619b-216">The **Products** property on the **Category** class and **Category** property on the **Product** class are navigation properties.</span></span> <span data-ttu-id="f619b-217">Entity Framework では、ナビゲーション プロパティは、2 つのエンティティ型間のリレーションシップを移動する方法を提供します。</span><span class="sxs-lookup"><span data-stu-id="f619b-217">In Entity Framework, navigation properties provide a way to navigate a relationship between two entity types.</span></span>

<span data-ttu-id="f619b-218">EF では、関連エンティティを読み込む、データベースから自動的に初めてナビゲーション プロパティにアクセスするの選ぶことができます。</span><span class="sxs-lookup"><span data-stu-id="f619b-218">EF gives you an option of loading related entities from the database automatically the first time you access the navigation property.</span></span> <span data-ttu-id="f619b-219">この種類の読み込み (遅延読み込みと呼ばれます) にするには、初めての各ナビゲーション プロパティにアクセスする別のクエリが実行されること、データベースに対して、内容が既にコンテキストでない場合あります。</span><span class="sxs-lookup"><span data-stu-id="f619b-219">With this type of loading (called lazy loading), be aware that the first time you access each navigation property a separate query will be executed against the database if the contents are not already in the context.</span></span>

<span data-ttu-id="f619b-220">POCO エンティティ型を使用する場合、EF は実行時にプロキシの派生型のインスタンスを作成し、読み込み用のフックを追加するクラスの仮想プロパティをオーバーライドして遅延読み込みを実現します。</span><span class="sxs-lookup"><span data-stu-id="f619b-220">When using POCO entity types, EF achieves lazy loading by creating instances of derived proxy types during runtime and then overriding virtual properties in your classes to add the loading hook.</span></span> <span data-ttu-id="f619b-221">関連オブジェクトの遅延読み込みを取得する必要がありますを宣言するナビゲーション プロパティの getter として**パブリック**と**仮想**(**Overridable** Visual Basic で)、およびするクラスがすることはできません**シール**(**NotOverridable** Visual Basic で)。</span><span class="sxs-lookup"><span data-stu-id="f619b-221">To get lazy loading of related objects, you must declare navigation property getters as **public** and **virtual** (**Overridable** in Visual Basic), and you class must not be **sealed** (**NotOverridable** in Visual Basic).</span></span> <span data-ttu-id="f619b-222">データベースを使用して最初のナビゲーション プロパティは自動的遅延読み込みを有効にするための仮想になります。</span><span class="sxs-lookup"><span data-stu-id="f619b-222">When using Database First navigation properties are automatically made virtual to enable lazy loading.</span></span> <span data-ttu-id="f619b-223">コードの最初のセクションで同じ理由から仮想ナビゲーション プロパティを作成することにしました</span><span class="sxs-lookup"><span data-stu-id="f619b-223">In the Code First section we chose to make the navigation properties virtual for the same reason</span></span>

## <a name="bind-object-to-controls"></a><span data-ttu-id="f619b-224">オブジェクトをコントロールにバインドします。</span><span class="sxs-lookup"><span data-stu-id="f619b-224">Bind Object to Controls</span></span>

<span data-ttu-id="f619b-225">この WPF アプリケーションのデータ ソースとしてモデルに定義されているクラスを追加します。</span><span class="sxs-lookup"><span data-stu-id="f619b-225">Add the classes that are defined in the model as data sources for this WPF application.</span></span>

-   <span data-ttu-id="f619b-226">ダブルクリック**MainWindow.xaml**メイン フォームを開くためのソリューション エクスプ ローラー</span><span class="sxs-lookup"><span data-stu-id="f619b-226">Double-click **MainWindow.xaml** in Solution Explorer to open the main form</span></span>
-   <span data-ttu-id="f619b-227">メイン メニューで、次のように選択します**プロジェクト -&gt;新しいデータ ソースを追加しています.。**</span><span class="sxs-lookup"><span data-stu-id="f619b-227">From the main menu, select **Project -&gt; Add New Data Source …**</span></span>
    <span data-ttu-id="f619b-228">(Visual Studio 2010 では、選択する必要があります**データ -&gt;新しいデータ ソースの追加...**)</span><span class="sxs-lookup"><span data-stu-id="f619b-228">(in Visual Studio 2010, you need to select **Data -&gt; Add New Data Source…**)</span></span>
-   <span data-ttu-id="f619b-229">データ ソースの Typewindow 選択で、次のように選択します**オブジェクト**クリック**次へ。**</span><span class="sxs-lookup"><span data-stu-id="f619b-229">In the Choose a Data Source Typewindow, select **Object** and click **Next**</span></span>
-   <span data-ttu-id="f619b-230">選択、データ オブジェクト ダイアログ ボックスで、展開、 **WPFwithEFSample** 2 つの時刻と選択**カテゴリ**</span><span class="sxs-lookup"><span data-stu-id="f619b-230">In the Select the Data Objects dialog, unfold the **WPFwithEFSample** two times and select **Category**</span></span>  
    <span data-ttu-id="f619b-231">*選択する必要はありません、**製品**を通じていたしますので、データ ソース、**製品**のプロパティを**カテゴリ**データ ソース*</span><span class="sxs-lookup"><span data-stu-id="f619b-231">*There is no need to select the **Product** data source, because we will get to it through the **Product**’s property on the **Category** data source*</span></span>  

    ![SelectDataObjects](~/ef6/media/selectdataobjects.png)

-   <span data-ttu-id="f619b-233">クリックして**完了します。**</span><span class="sxs-lookup"><span data-stu-id="f619b-233">Click **Finish.**</span></span>
-   <span data-ttu-id="f619b-234">MainWindow.xaml のウィンドウの横にあるデータ ソース ウィンドウが開かれる*データ ソース ウィンドウが表示されていない場合は、選択**ビュー -&gt;その他の Windows-&gt;データ ソース***</span><span class="sxs-lookup"><span data-stu-id="f619b-234">The Data Sources window is opened next to the MainWindow.xaml window *If the Data Sources window is not showing up, select **View -&gt; Other Windows-&gt; Data Sources***</span></span>
-   <span data-ttu-id="f619b-235">キーを押して、データ ソース ウィンドウが自動しないように、ピン アイコンを非表示にします。</span><span class="sxs-lookup"><span data-stu-id="f619b-235">Press the pin icon, so the Data Sources window does not auto hide.</span></span> <span data-ttu-id="f619b-236">ウィンドウが表示された場合は、更新ボタンをクリックする必要があります。</span><span class="sxs-lookup"><span data-stu-id="f619b-236">You may need to hit the refresh button if the window was already visible.</span></span>

    ![DataSources](~/ef6/media/datasources.png)

-   <span data-ttu-id="f619b-238">選択、* * カテゴリ * * データ ソースをフォームにドラッグします。</span><span class="sxs-lookup"><span data-stu-id="f619b-238">Select the **Category **data source and drag it on the form.</span></span>

<span data-ttu-id="f619b-239">このソースがドラッグされると、次のメッセージが発生しました。</span><span class="sxs-lookup"><span data-stu-id="f619b-239">The following happened when we dragged this source:</span></span>

-   <span data-ttu-id="f619b-240">**CategoryViewSource**リソースと * * * * categoryDataGrid コントロールが XAML に追加されました。</span><span class="sxs-lookup"><span data-stu-id="f619b-240">The **categoryViewSource** resource and the** categoryDataGrid** control were added to XAML.</span></span> <span data-ttu-id="f619b-241">DataViewSources の詳細については、次を参照してください。http://bea.stollnitz.com/blog/?p=387します。</span><span class="sxs-lookup"><span data-stu-id="f619b-241">For more information about DataViewSources, see http://bea.stollnitz.com/blog/?p=387.</span></span>
-   <span data-ttu-id="f619b-242">親グリッド要素の DataContext プロパティに設定されました"{StaticResource **categoryViewSource** }"。</span><span class="sxs-lookup"><span data-stu-id="f619b-242">The DataContext property on the parent Grid element was set to "{StaticResource **categoryViewSource** }".</span></span>  <span data-ttu-id="f619b-243">**CategoryViewSource**リソースは、外側のバインディング ソースとして機能\\親グリッド要素。</span><span class="sxs-lookup"><span data-stu-id="f619b-243">The **categoryViewSource** resource serves as a binding source for the outer\\parent Grid element.</span></span> <span data-ttu-id="f619b-244">内部のグリッド要素は、親 (categoryDataGrid の ItemsSource プロパティは"{binding}"に設定) をグリッドから DataContext 値を継承します。</span><span class="sxs-lookup"><span data-stu-id="f619b-244">The inner Grid elements then inherit the DataContext value from the parent Grid (the categoryDataGrid’s ItemsSource property is set to "{Binding}").</span></span> 

``` xml
    <Window.Resources>
        <CollectionViewSource x:Key="categoryViewSource"
                                d:DesignSource="{d:DesignInstance {x:Type local:Category}, CreateList=True}"/>
    </Window.Resources>
    <Grid DataContext="{StaticResource categoryViewSource}">
        <DataGrid x:Name="categoryDataGrid" AutoGenerateColumns="False" EnableRowVirtualization="True"
                    ItemsSource="{Binding}" Margin="13,13,43,191"
                    RowDetailsVisibilityMode="VisibleWhenSelected">
            <DataGrid.Columns>
                <DataGridTextColumn x:Name="categoryIdColumn" Binding="{Binding CategoryId}"
                                    Header="Category Id" Width="SizeToHeader"/>
                <DataGridTextColumn x:Name="nameColumn" Binding="{Binding Name}"
                                    Header="Name" Width="SizeToHeader"/>
            </DataGrid.Columns>
        </DataGrid>
    </Grid>
```

## <a name="adding-a-details-grid"></a><span data-ttu-id="f619b-245">詳細グリッドを追加します。</span><span class="sxs-lookup"><span data-stu-id="f619b-245">Adding a Details Grid</span></span>

<span data-ttu-id="f619b-246">あるので、みましょうカテゴリを表示するグリッドは、関連付けられている製品を表示する詳細グリッドを追加します。</span><span class="sxs-lookup"><span data-stu-id="f619b-246">Now that we have a grid to display Categories let's add a details grid to display the associated Products.</span></span>

-   <span data-ttu-id="f619b-247">選択、* * 製品 * * の下にあるプロパティ、* * カテゴリ * * データ ソースをフォームにドラッグします。</span><span class="sxs-lookup"><span data-stu-id="f619b-247">Select the **Products **property from under the **Category **data source and drag it on the form.</span></span>
    -   <span data-ttu-id="f619b-248">**CategoryProductsViewSource**リソースと**productDataGrid**グリッドが XAML に追加されます</span><span class="sxs-lookup"><span data-stu-id="f619b-248">The **categoryProductsViewSource** resource and **productDataGrid** grid are added to XAML</span></span>
    -   <span data-ttu-id="f619b-249">製品には、このリソースのバインド パスを設定してください。</span><span class="sxs-lookup"><span data-stu-id="f619b-249">The binding path for this resource is set to Products</span></span>
    -   <span data-ttu-id="f619b-250">WPF データ バインディング フレームワークでは、製品だけが選択したカテゴリに関連する表示ことにより、 **productDataGrid**</span><span class="sxs-lookup"><span data-stu-id="f619b-250">WPF data-binding framework ensures that only Products related to the selected Category show up in **productDataGrid**</span></span>
-   <span data-ttu-id="f619b-251">ツールボックスからドラッグ**ボタン**フォームにログオンします。</span><span class="sxs-lookup"><span data-stu-id="f619b-251">From the Toolbox, drag **Button** on to the form.</span></span> <span data-ttu-id="f619b-252">設定、**名前**プロパティを**buttonSave**と**コンテンツ**プロパティを**保存**します。</span><span class="sxs-lookup"><span data-stu-id="f619b-252">Set the **Name** property to **buttonSave** and the **Content** property to **Save**.</span></span>

<span data-ttu-id="f619b-253">フォームは、次のようになります。</span><span class="sxs-lookup"><span data-stu-id="f619b-253">The form should look similar to this:</span></span>

![Designer](~/ef6/media/designer.png) 

## <a name="add-code-that-handles-data-interaction"></a><span data-ttu-id="f619b-255">データの対話を処理するコードを追加します。</span><span class="sxs-lookup"><span data-stu-id="f619b-255">Add Code that Handles Data Interaction</span></span>

<span data-ttu-id="f619b-256">メイン ウィンドウにいくつかのイベント ハンドラーを追加する時間になります。</span><span class="sxs-lookup"><span data-stu-id="f619b-256">It's time to add some event handlers to the main window.</span></span>

-   <span data-ttu-id="f619b-257">XAML ウィンドウで、クリックして、 **&lt;ウィンドウ**要素、これは、メイン ウィンドウを選択します。</span><span class="sxs-lookup"><span data-stu-id="f619b-257">In the XAML window, click on the **&lt;Window** element, this selects the main window</span></span>
-   <span data-ttu-id="f619b-258">**プロパティ**ウィンドウ選択**イベント**右側の上部にあるテキスト ボックスの右側をダブルクリックし、 **Loaded**ラベル</span><span class="sxs-lookup"><span data-stu-id="f619b-258">In the **Properties** window choose **Events** at the top right, then double-click the text box to right of the **Loaded** label</span></span>

    ![MainWindowProperties](~/ef6/media/mainwindowproperties.png)

-   <span data-ttu-id="f619b-260">追加も、 ** をクリックして**イベントを**保存**デザイナーの Save ボタンをダブルクリックしてボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="f619b-260">Also add the **Click** event for the **Save** button by double-clicking the Save button in the designer.</span></span> 

<span data-ttu-id="f619b-261">分離コードをフォームの表示、ProductContext を使用して、データ アクセスを実行するコードを編集しますようになりました。</span><span class="sxs-lookup"><span data-stu-id="f619b-261">This brings you to the code behind for the form, we'll now edit the code to use the ProductContext to perform data access.</span></span> <span data-ttu-id="f619b-262">次に示すように、MainWindow のコードを更新します。</span><span class="sxs-lookup"><span data-stu-id="f619b-262">Update the code for the MainWindow as shown below.</span></span>

<span data-ttu-id="f619b-263">コードの実行時間の長いインスタンス**ProductContext**します。</span><span class="sxs-lookup"><span data-stu-id="f619b-263">The code declares a long-running instance of **ProductContext**.</span></span> <span data-ttu-id="f619b-264">**ProductContext**オブジェクトを照会し、データベースにデータを保存に使用されます。</span><span class="sxs-lookup"><span data-stu-id="f619b-264">The **ProductContext** object is used to query and save data to the database.</span></span> <span data-ttu-id="f619b-265">**Dispose**() を**ProductContext**インスタンスが呼び出され、オーバーライドされたから**OnClosing**メソッド。</span><span class="sxs-lookup"><span data-stu-id="f619b-265">The **Dispose**() on the **ProductContext** instance is then called from the overridden **OnClosing** method.</span></span> <span data-ttu-id="f619b-266">コード コメントでは、コードの動作について詳しく説明します。</span><span class="sxs-lookup"><span data-stu-id="f619b-266">The code comments provide details about what the code does.</span></span>

``` csharp
    using System.Data.Entity;
    using System.Linq;
    using System.Windows;

    namespace WPFwithEFSample
    {
        public partial class MainWindow : Window
        {
            private ProductContext _context = new ProductContext();
            public MainWindow()
            {
                InitializeComponent();
            }

            private void Window_Loaded(object sender, RoutedEventArgs e)
            {
                System.Windows.Data.CollectionViewSource categoryViewSource =
                    ((System.Windows.Data.CollectionViewSource)(this.FindResource("categoryViewSource")));

                // Load is an extension method on IQueryable,
                // defined in the System.Data.Entity namespace.
                // This method enumerates the results of the query,
                // similar to ToList but without creating a list.
                // When used with Linq to Entities this method
                // creates entity objects and adds them to the context.
                _context.Categories.Load();

                // After the data is loaded call the DbSet<T>.Local property
                // to use the DbSet<T> as a binding source.
                categoryViewSource.Source = _context.Categories.Local;
            }

            private void buttonSave_Click(object sender, RoutedEventArgs e)
            {
                // When you delete an object from the related entities collection
                // (in this case Products), the Entity Framework doesn’t mark
                // these child entities as deleted.
                // Instead, it removes the relationship between the parent and the child
                // by setting the parent reference to null.
                // So we manually have to delete the products
                // that have a Category reference set to null.

                // The following code uses LINQ to Objects
                // against the Local collection of Products.
                // The ToList call is required because otherwise the collection will be modified
                // by the Remove call while it is being enumerated.
                // In most other situations you can use LINQ to Objects directly
                // against the Local property without using ToList first.
                foreach (var product in _context.Products.Local.ToList())
                {
                    if (product.Category == null)
                    {
                        _context.Products.Remove(product);
                    }
                }

                _context.SaveChanges();
                // Refresh the grids so the database generated values show up.
                this.categoryDataGrid.Items.Refresh();
                this.productsDataGrid.Items.Refresh();
            }

            protected override void OnClosing(System.ComponentModel.CancelEventArgs e)
            {
                base.OnClosing(e);
                this._context.Dispose();
            }
        }

    }
```

## <a name="test-the-wpf-application"></a><span data-ttu-id="f619b-267">WPF アプリケーションをテストします。</span><span class="sxs-lookup"><span data-stu-id="f619b-267">Test the WPF Application</span></span>

-   <span data-ttu-id="f619b-268">アプリケーションをコンパイルして実行します。</span><span class="sxs-lookup"><span data-stu-id="f619b-268">Compile and run the application.</span></span> <span data-ttu-id="f619b-269">Code First を使用したかどうかは、ことがわかりますが、 **WPFwithEFSample.ProductContext**データベースが作成されます。</span><span class="sxs-lookup"><span data-stu-id="f619b-269">If you used Code First, then you will see that a **WPFwithEFSample.ProductContext** database is created for you.</span></span>
-   <span data-ttu-id="f619b-270">下部のグリッドに上位のグリッドと製品の名前でカテゴリ名を入力*は何も入力しない ID の列に主キーがデータベースによって生成されるため、*</span><span class="sxs-lookup"><span data-stu-id="f619b-270">Enter a category name in the top grid and product names in the bottom grid *Do not enter anything in ID columns, because the primary key is generated by the database*</span></span>

    ![画面 1](~/ef6/media/screen1.png)

-   <span data-ttu-id="f619b-272">キーを押して、**保存**データベースにデータを保存するボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="f619b-272">Press the **Save** button to save the data to the database</span></span>

<span data-ttu-id="f619b-273">DbContext の呼び出しの後**SaveChanges**()、Id はデータベースで生成された値が格納されます。</span><span class="sxs-lookup"><span data-stu-id="f619b-273">After the call to DbContext’s **SaveChanges**(), the IDs are populated with the database generated values.</span></span> <span data-ttu-id="f619b-274">呼び出したため、**更新**後 () **SaveChanges**()、 **DataGrid**コントロールも、新しい値で更新します。</span><span class="sxs-lookup"><span data-stu-id="f619b-274">Because we called **Refresh**() after **SaveChanges**() the **DataGrid** controls are updated with the new values as well.</span></span>

![Screen2](~/ef6/media/screen2.png)