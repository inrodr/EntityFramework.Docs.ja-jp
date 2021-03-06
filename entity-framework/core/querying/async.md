---
title: 非同期クエリ - EF Core
author: rowanmiller
ms.date: 01/24/2017
ms.assetid: b6429b14-cba0-4af4-878f-b829777c89cb
uid: core/querying/async
ms.openlocfilehash: de00e25279e29355a4eb3e55597a8578ceccecb6
ms.sourcegitcommit: dadee5905ada9ecdbae28363a682950383ce3e10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2018
ms.locfileid: "42993566"
---
# <a name="asynchronous-queries"></a>非同期クエリ

非同期クエリでは、クエリがデータベースで実行されている間の、スレッドのブロックを回避します。 これは、シック クライアント アプリケーションの UI の凍結を防止するために役立つ場合があります。 また、非同期操作では、データベース操作が完了している間に、他の要求を処理するためにスレッドを解放できるので、Web アプリケーションでのスループットを向上させることができます。 詳細については、「[C# での非同期プログラミング](https://docs.microsoft.com/dotnet/csharp/async)」を参照してください。

> [!WARNING]  
> EF Core は、同じコンテキスト インスタンス上での複数の並列操作の実行をサポートしていません。 次の操作を開始する前に、操作が完了するまで常に待機する必要があります。 これは通常、各同期操作において `await` キーワードを使用することで行われます。

Entity Framework Core では、クエリを実行して結果を返すための LINQ メソッドの代替として使用できる、一連の非同期拡張メソッドを提供しています。 例として、`ToListAsync()`、`ToArrayAsync()`、`SingleAsync()` などがあります。`Where(...)`、`OrderBy(...)` などの LINQ 演算子の非同期バージョンはありません。これらのメソッドでは LINQ 式のツリーのみをビルドし、データベースでのクエリの実行は発生しないためです。

> [!IMPORTANT]  
> EF Core の非同期拡張メソッドは、`Microsoft.EntityFrameworkCore` 名前空間で定義されています。 メソッドを使用可能にするには、この名前空間がインポートされている必要があります。

[!code-csharp[Main](../../../samples/core/Querying/Querying/Async/Sample.cs#Sample)]
