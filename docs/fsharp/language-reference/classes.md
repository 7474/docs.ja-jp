---
title: クラス (F#)
description: F# クラスのプロパティ、メソッド、およびイベントを持つことができるオブジェクトを表す型の方法について説明します。
ms.date: 05/16/2016
ms.openlocfilehash: 67164bd9f91c14f465bf05630259ad70cb8d90e5
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/04/2018
ms.locfileid: "33565887"
---
# <a name="classes"></a>クラス

*クラス*プロパティ、メソッド、およびイベントを持つことができるオブジェクトを表す型。


## <a name="syntax"></a>構文

```fsharp
// Class definition:
type [access-modifier] type-name [type-params] [access-modifier] ( parameter-list ) [ as identifier ] =
[ class ]
[ inherit base-type-name(base-constructor-args) ]
[ let-bindings ]
[ do-bindings ]
member-list
...
[ end ]
// Mutually recursive class definitions:
type [access-modifier] type-name1 ...
and [access-modifier] type-name2 ...
...
```

## <a name="remarks"></a>コメント
クラスは、.NET オブジェクト型以外の基本的な記述を表します。クラスは、f# のオブジェクト指向プログラミングをサポートする主な型の概念です。

上記の構文では、`type-name`任意の有効な識別子です。 `type-params`省略可能なジェネリック型パラメーターについて説明します。 型パラメーター名と山かっこで囲まれた制約で構成されます (`<`と`>`)。 詳細については、次を参照してください。[ジェネリック](generics/index.md)と[制約](generics/constraints.md)です。 `parameter-list`コンス トラクターのパラメーターについて説明します。 型に関連する最初のアクセス修飾子2 つ目は、プライマリ コンス トラクターに関連します。 どちらの場合、既定値を`public`です。

クラスの基底クラスを使用して指定する、`inherit`キーワード。 基本クラスのコンス トラクターをかっこでの引数を指定する必要があります。

フィールドを宣言するか、関数値を使用して、クラスに対してローカルな`let`バインディング、およびするが、一般的な規則に従う必要があります`let`バインドします。 `do-bindings`セクションには、オブジェクトの構築時に実行されるコードが含まれています。

`member-list`追加のコンス トラクター、インスタンスと静的メソッドの宣言、インターフェイスの宣言で抽象バインディング、およびプロパティとイベントの宣言で構成されます。 これらは「[メンバー](members/index.md)です。

`identifier`オプションと共に使用される`as`キーワードは、インスタンス変数、または型のインスタンスを参照する種類の定義で使用できる、自己識別子に名前を提供します。 詳細については、このトピックで後述する「自己識別子を参照してください。

キーワード`class`と`end`開始をマークして、定義の最後は省略可能です。

と共に、相互に参照型である再帰型が相互に参加している、`and`キーワードと同じように、再帰関数は、同時に指定します。 例については、「相互再帰型」を参照してください。


## <a name="constructors"></a>コンストラクター
コンス トラクターは、クラス型のインスタンスを作成するコードです。 クラスのコンス トラクターは、他の .NET 言語では f# の少し異なる方法で機能します。 F# クラスでは常にプライマリ コンス トラクターの引数に記載されて、 `parameter-list` 、型名、および本体を持つから成るに依存している、 `let` (および`let rec`) と、クラス宣言の開始時にバインディング`do`に従ってバインドします。 プライマリ コンス トラクターの引数は、クラス宣言全体のスコープ内です。

使用して追加のコンス トラクターを追加することができます、`new`キーワードを次のように、メンバーを追加します。

`new`(`argument-list`) = `constructor-body`

新しいコンス トラクターの本体は、クラス宣言の上部にある指定されたプライマリ コンス トラクターを呼び出す必要があります。

次の例では、この概念を示します。 次のコードに`MyClass`2 つのコンス トラクターを持つ、2 つの引数と別のコンス トラクターを受け取り、プライマリ コンス トラクターは引数を受け取りません。

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-1/snippet2401.fs)]
    
## <a name="let-and-do-bindings"></a>let および do 束縛

`let`と`do`クラス定義内のバインディングが、主要なクラスのコンス トラクターの本体を構成および実行するクラスのインスタンスが作成されるたびにします。 場合、`let`バインディングは、関数、メンバーにコンパイルされます。 場合、`let`バインド関数またはメンバーで使用されていない値は、そのコンス トラクターへのローカル変数にコンパイルされます。 それ以外の場合、クラスのフィールドにコンパイルされます。 `do`後に続く式は、プライマリ コンス トラクターにコンパイルされ、すべてのインスタンスの初期化コードを実行します。 追加のコンス トラクターが常に、プライマリ コンス トラクターを呼び出すので、`let`バインドと`do`バインドが常にコンス トラクターの呼び出しに関係なくを実行します。

によって作成されたフィールド`let`バインディング メソッドとクラスのプロパティを通じてアクセスできます。 ただし、それらにアクセスできません、静的メソッドから静的メソッドは、パラメーターとしてインスタンス変数を受け取る場合でもです。 1 つが存在する場合、自己識別子を使用して、アクセスできません。


## <a name="self-identifiers"></a>自己識別子

A*自己識別子*を現在のインスタンスを表す名前を指定します。 自己識別子のように、 `this` c# または C++ のキーワードまたは`Me`Visual Basic でします。 自己識別子定義については、クラス全体または個々 のメソッドのためだけのスコープ内にあるかどうかに応じて、2 つの方法では、自己識別子を定義できます。

クラス全体の個人識別子を定義するのには、使用、`as`キーワードのコンス トラクターのパラメーターの右かっこの後に一覧表示、および識別子の名前を指定します。

自己識別子に対して 1 つのメソッドを定義するのには、宣言では、メンバー、メソッド名と区切り記号としてピリオド (.) の前に、自己識別子を提供します。

次のコード例は、自己識別子を作成する 2 つの方法を示しています。 最初の行で、`as`キーワードの使用を自己識別子を定義します。 5 番目の行では、識別子に`this`自己識別子をスコープは、メソッドに制限を定義するために使用`PrintMessage`です。

```fsharp
type MyClass2(dataIn) as self =
    let data = dataIn
    do
        self.PrintMessage()
    member this.PrintMessage() =
        printf "Creating MyClass2 with Data %d" data
```

異なり他の .NET 言語で名前を指定できます、自己識別子が好みに合わせてです。いないに制限されている名前など`self`、 `Me`、または`this`です。

宣言された自己識別子、`as`までキーワードが初期化されていない後、`let`バインドが実行されます。 そのため、これでは使用できません、`let`バインドします。 自己識別子を使用することができます、`do`バインド セクション。


## <a name="generic-type-parameters"></a>ジェネリック型の型パラメーター

山かっこでジェネリック型パラメーターが指定されて (`<`と`>`)、単一引用符の後に識別子の形式でします。 複数のジェネリック型パラメーターは、コンマで区切られます。 ジェネリック型パラメーターは、宣言全体のスコープでです。 次のコード例では、ジェネリック型パラメーターを指定する方法を示します。

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-1/snippet2403.fs)]

型を使用する場合、型引数が推論されます。 次のコードでは、推論された型は、組のシーケンスです。

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-1/snippet24031.fs)]
    
## <a name="specifying-inheritance"></a>継承を指定します。

`inherit`句は、1 つを使用する必要がある場合に、直接基底クラスを指定します。 F# では、直接基底クラスを 1 つだけが許可されます。 クラスが実装するインターフェイスでは、基本クラスは考慮されません。 インターフェイスは、後ほど、[インターフェイス](Interfaces.md)トピックです。

表示するメソッドと基底クラスのプロパティ、派生クラスからを言語キーワードを使用して`base`を識別子としての後にピリオド (.) と、メンバーの名前。

詳細については、「[継承](inheritance.md)」を参照してください。


## <a name="members-section"></a>メンバー セクション
このセクションでは、静的またはインスタンス メソッド、プロパティ、インターフェイスの実装、抽象メンバー、イベントの宣言、および追加のコンス トラクターを定義できます。 できるように、このセクションでバインドに表示できません。 別のトピックで説明していますので、メンバーは、さまざまなクラスのほか、f# の型に追加できる、[メンバー](members/index.md)です。


## <a name="mutually-recursive-types"></a>相互再帰型
循環的に相互に参照型を定義するとき、文字列一緒に種類の定義を使用して、`and`キーワード。 `and`キーワードに置き換えられます、`type`次のように、最初の定義以外のすべてのキーワードです。

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-1/snippet2404.fs)]

出力は、現在のディレクトリ内のすべてのファイルの一覧を示します。


## <a name="when-to-use-classes-unions-records-and-structures"></a>クラス、共用体、レコード、および構造体を使用する場合
指定する、さまざまな種類から選択すると、どのような各型のデザインはの特定の状況に該当する種類を選択するをよく理解する必要があります。 クラスは、オブジェクト指向プログラミングのコンテキストで使用するために設計されます。 オブジェクト指向プログラミングでは、.NET Framework 用に記述されているアプリケーションで使用される基準となるパラダイムです。 F# コードしている場合、.NET Framework または別のオブジェクト指向のライブラリと密接に連携の UI ライブラリなどのオブジェクト指向型システムからを拡張する必要がある場合は特に、クラスは、適切な可能性があります。

いない相互運用密接にしているオブジェクト指向のコードでは、自己完結型とオブジェクト指向のコードで頻繁に行われる操作から保護されているためであるコードを記述する場合や、レコードの使用を検討する必要がありますして判別共用体です。 1 つのも思考アウト適切なパターン一致コードと共に、判別共用体は、オブジェクト階層をさらに簡単に多くの場合、使用できます。 判別共用体の詳細については、次を参照してください。[判別共用体](discriminated-unions.md)です。

レコードが、クラスよりも簡単になるというメリットがあるが、型の要求は、簡単に達成できるを超えた場合にレコードが適切でないです。 レコードは、基本的には単純な集計値、カスタム アクションを実行できる別のコンス トラクターを持たない、非表示のフィールドや継承またはインターフェイスの実装のないのです。 プロパティやメソッドなどのメンバーは、レコードをその動作はより複雑なに追加できる、レコードに格納されているフィールドはまだ値の単純な集計にします。 レコードの詳細については、次を参照してください。[レコード](records.md)です。

構造体も、データの小規模な集約に便利ですが、それらとは異なり、クラスやレコードから .NET 値型では。 クラスやレコードは、.NET 参照型です。 値型と参照型のセマンティクスは、さまざまな値の型が値渡しされます。 つまり、コピーされるビット単位では、パラメーターとして渡されるまたは関数から返されます。 格納されるスタック上か、ヒープ上のそれぞれの場所に格納されている場合は、代わりに親オブジェクト内に埋め込まれた対象のフィールドとして使用されます。 そのため、構造体は、ヒープへのアクセスのオーバーヘッドが問題と頻繁にアクセスされるデータに適しています。 構造体の詳細については、次を参照してください。[構造](structures.md)です。


## <a name="see-also"></a>関連項目
[F# 言語リファレンス](index.md)

[メンバー](members/index.md)

[継承](inheritance.md)

[インターフェイス](interfaces.md)

