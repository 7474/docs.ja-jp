---
title: into (C# リファレンス)
ms.date: 07/20/2015
f1_keywords:
- into_CSharpKeyword
- into
helpviewer_keywords:
- into keyword [C#]
ms.assetid: 81ec62c1-f0b1-4755-8a31-959876e77f65
ms.openlocfilehash: 9bc7d50b77fe42861f92cc5bec946678d11d73d8
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/04/2018
ms.locfileid: "33266865"
---
# <a name="into-c-reference"></a>into (C# リファレンス)
`into` コンテキスト キーワードは、[group](../../../csharp/language-reference/keywords/group-clause.md)、[join](../../../csharp/language-reference/keywords/join-clause.md)、または [select](../../../csharp/language-reference/keywords/select-clause.md) 句の結果を新しい識別子に保存するための一時的な識別子を作成するために使用できます。 この識別子自体を追加のクエリ コマンドのジェネレーターにすることができます。 `group` または `select` 句で使用する場合、新しい識別子の使用は*継続*と呼ばれることもあります。  
  
## <a name="example"></a>例  
 次の例では、`into` キーワードを使用して、推定の型 `IGrouping` を持つ一時的な識別子 `fruitGroup` を有効にする方法を示します。 識別子を使用すると、各グループに対して <xref:System.Linq.Enumerable.Count%2A> メソッドを呼び出し、2 つ以上の単語を含むグループのみを選択することができます。  
  
 [!code-csharp[cscsrefQueryKeywords#18](../../../csharp/language-reference/keywords/codesnippet/CSharp/into_1.cs)]  
  
 `group` 句での `into` の使用は、各グループに対して追加のクエリ操作を実行する場合にのみ必要です。 詳しくは、「[group 句](../../../csharp/language-reference/keywords/group-clause.md)」をご覧ください。  
  
 `join` 句での `into` の使用例については、「[join 句](../../../csharp/language-reference/keywords/join-clause.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [クエリ キーワード (LINQ)](../../../csharp/language-reference/keywords/query-keywords.md)  
 [LINQ クエリ式](../../../csharp/programming-guide/linq-query-expressions/index.md)  
 [group 句](../../../csharp/language-reference/keywords/group-clause.md)
