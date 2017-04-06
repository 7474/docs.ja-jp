---
title: "イベントの概要"
description: "イベントの概要"
keywords: .NET, .NET Core
author: BillWagner
ms.author: wiwagn
ms.date: 06/20/2016
ms.topic: article
ms.prod: .net
ms.technology: devlang-csharp
ms.devlang: csharp
ms.assetid: 9b8d2a00-1584-4a5b-8994-5003d54d8e0c
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: a2eb8daef0883b78769a185be7d64e43c88b1d15
ms.lasthandoff: 03/13/2017

---

# <a name="introduction-to-events"></a>イベントの概要

[前へ](delegates-patterns.md)

デリゲートのようなイベントは*遅延バインディング* メカニズムになっています。 実際、イベントはデリゲートの言語サポートに基づいて構築されます。

イベントは、何かが起こったことをオブジェクトが (システム内のあらゆる関連コンポーネントに) ブロードキャストする方法です。 他のコンポーネントはイベントを受信登録できます。イベントが発生すると通知されます。

プログラミングにイベントを利用した経験があることでしょう。 グラフィカル システムの多くには、ユーザー操作を報告するイベント モデルがあります。 そのようなイベントは、マウスが動いた、ボタンが押されたなどの動作を報告します。 それは最も一般的なイベントの 1 つですが、イベントが利用されるシナリオはこれだけではありません。

クラスに対して発生させるイベントを定義できます。 イベントを使用するときに考慮するべき重要なことは、特定のイベントに登録されていないオブジェクトの可能性です。 リスナーが構成されていないときはイベントを発生させないようにコードを記述する必要があります。

イベントを受信登録すると、2 つのオブジェクト (イベント ソースとイベント シンク) の間に結合も生成されます。 イベント シンクにイベントに対する関心がなくなったとき、イベント ソースの受信登録を解除する必要があります。

## <a name="design-goals-for-event-support"></a>イベント サポートのデザイン目標

イベントの言語デザインには次のような目標があります。

最初の目標は、イベント ソースとイベント シンクの間で最小限の結合を有効にすることです。 これら 2 つのコンポーネントは、別々の組織に記述されることがあります。まったく異なる日程で更新されることもあります。

2 つ目の目標は、イベントの受信登録と登録解除を非常にシンプルにすることです。

最後の目標は、イベント ソースで複数のイベント サブスクライバーに対応することです。 イベント サブスクライバーをアタッチしないことにも対応する必要があります。

イベントの目標はデリゲートの目標とよく似ています。
そのような理由から、イベント言語サポートはデリゲート言語サポートに基づいて構築されます。

## <a name="language-support-for-events"></a>イベントの言語サポート

イベントの定義、受信登録、登録解除の構文は、デリゲートの構文の拡張になります。

イベントを定義するには、`event` キーワードを使用します。

```csharp
public event EventHandler<FileListArgs> Progress;
```

イベントの種類 (この例の `EventHandler<FileListArgs>`) はデリゲート型にする必要があります。 イベントを宣言するときはさまざまな決まりごとを守る必要があります。 通常、イベント デリゲート型には戻り値 void があります。
イベント宣言は動詞または動詞句にする必要があります。
何かが起こったことをイベントが報告するときは (この例のように) 過去時制を使用します。 何かが起こりそうなことを報告するには、現在時制の動詞 (たとえば、`Closing`) を使用します。 多くの場合、現在時制の使用は、お使いのクラスで何らかのカスタマイズ動作をサポートしていることを示します。 最も一般的なシナリオの 1 つがキャンセルのサポートです。 たとえば、`Closing` イベントには、close 操作を続行するかどうかを示す引数が含まれることがあります。  イベント引数のプロパティを更新することで呼び出し元が動作を変更するシナリオもあります。 アルゴリズムに実行させる次のアクションを提案するイベントを発生させることもできます。 イベント ハンドラーは、イベント引数のプロパティを変更することで、別のアクションを命令することもあります。

イベントが発生させるとき、デリゲート呼び出し構文を利用してイベント ハンドラーを呼び出します。

```csharp
Progress?.Invoke(this, new FileListArgs(file));
```

[デリゲート](delegates-patterns.md)に関するセクションで説明したように、
?. 演算子を利用すると、イベントのサブスクライバーが存在しないとき、そのイベントの発生を試行しないように容易に確保できます。
 
`+=` 演算子を利用し、イベントを受信登録します。

```csharp
EventHandler<FileListArgs> onProgress = (sender, eventArgs) => 
    Console.WriteLine(eventArgs.FoundFile);
lister.Progress += OnProgress;
```

上の画像のように、一般的にハンドラー メソッドはプレフィックス 'On' の後にイベント名を続けたものになります。

`-=` 演算子を利用して受信登録を解除します。

```csharp
lister.Progress -= onProgress;
```

イベント ハンドラーを表す式にローカル変数が宣言されたことに注目してください。 これで受信登録解除によりハンドラーが削除されます。
代わりにラムダ式の本文を使用した場合、アタッチされたことがないハンドラーの削除が試行され、何も起こりません。

次回の記事では、一般的なイベント パターンと今回のサンプルのさまざまなバリエーションについて学習します。

[次へ](event-pattern.md)
