---
title: 型拡張
description: 'F # の型拡張機能を使用して、以前に定義したオブジェクト型に新しいメンバーを追加する方法について説明します。'
ms.date: 02/05/2020
ms.openlocfilehash: 8fdb2d5e527643b23d24a6118e8cef6b11f1a546
ms.sourcegitcommit: 8bfeb5930ca48b2ee6053f16082dcaf24d46d221
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/18/2020
ms.locfileid: "88559129"
---
# <a name="type-extensions"></a>型拡張

型拡張機能 ( _拡張_とも呼ばれます) は、以前に定義されたオブジェクト型に新しいメンバーを追加できるようにするための機能ファミリです。 次の3つの機能があります。

- 組み込み型拡張機能
- 省略可能な型拡張
- 拡張メソッド

各は異なるシナリオで使用でき、トレードオフも異なります。

## <a name="syntax"></a>構文

```fsharp
// Intrinsic and optional extensions
type typename with
    member self-identifier.member-name =
        body
    ...

// Extension methods
open System.Runtime.CompilerServices

[<Extension>]
type Extensions() =
    [<Extension>]
    static member self-identifier.extension-name (ty: typename, [args]) =
        body
    ...
```

## <a name="intrinsic-type-extensions"></a>組み込み型拡張機能

組み込み型拡張は、ユーザー定義型を拡張する型の拡張機能です。

組み込み型拡張は、拡張する型と同じファイル **と** 同じ名前空間またはモジュールで定義されている必要があります。 その他の定義では、 [省略可能な型拡張](type-extensions.md#optional-type-extensions)になります。

組み込み型の拡張機能は、型宣言から機能を分離するために、明確な方法である場合があります。 次の例は、組み込み型拡張を定義する方法を示しています。

```fsharp
namespace Example

type Variant =
    | Num of int
    | Str of string
  
module Variant =
    let print v =
        match v with
        | Num n -> printf "Num %d" n
        | Str s -> printf "Str %s" s

// Add a member to Variant as an extension
type Variant with
    member x.Print() = Variant.print x
```

型拡張を使用すると、次の各項目を分離できます。

- 型の宣言 `Variant`
- `Variant`"Shape" に応じてクラスを印刷する機能
- 印刷機能にオブジェクト形式の表記でアクセスする方法 `.`

これは、すべてをのメンバーとして定義する方法の1つです `Variant` 。 これは本質的には優れたアプローチではありませんが、状況によっては機能が明確に表示される可能性があります。

組み込み型の拡張は、それが拡張する型のメンバーとしてコンパイルされ、リフレクションによって型が検証されるときに型に表示されます。

## <a name="optional-type-extensions"></a>省略可能な型拡張

省略可能な型拡張は、拡張される型の元のモジュール、名前空間、またはアセンブリの外側に表示される拡張機能です。

省略可能な型拡張は、自分で定義していない型を拡張する場合に便利です。 次に例を示します。

```fsharp
module Extensions

type IEnumerable<'T> with
    /// Repeat each element of the sequence n times
    member xs.RepeatElements(n: int) =
        seq {
            for x in xs do
                for _ in 1 .. n -> x
        }
```

これで、使用している `RepeatElements` <xref:System.Collections.Generic.IEnumerable%601> `Extensions` スコープでモジュールが開かれている限り、にアクセスできるようになりました。

リフレクションによってチェックされる場合、拡張型にはオプションの拡張機能は表示されません。 オプションの拡張機能はモジュール内に存在する必要があり、拡張機能を含むモジュールが開いている場合、またはそれ以外の場合はスコープ内にある場合にのみスコープに含まれます。

任意拡張のメンバーはコンパイルされると、静的メンバーになります。このメンバーに対する最初のパラメーターとして、オブジェクト インスタンスが暗黙で渡されます。 ただし、これらは、それらが宣言されている方法に従って、インスタンスメンバーまたは静的メンバーであるかのように動作します。

オプションの拡張メンバーは、C# または Visual Basic コンシューマーにも表示されません。 他の F # コードでのみ使用できます。

## <a name="generic-limitation-of-intrinsic-and-optional-type-extensions"></a>組み込みおよびオプションの型拡張の一般的な制限

型変数が制限されているジェネリック型に対して型拡張を宣言できます。 要件は、拡張宣言の制約が宣言された型の制約と一致することです。

ただし、宣言された型と型拡張の間で制約が一致した場合でも、宣言された型よりも型パラメーターに対して異なる要件を課す拡張メンバーの本体によって制約が推論される可能性があります。 次に例を示します。

```fsharp
open System.Collections.Generic

// NOT POSSIBLE AND FAILS TO COMPILE!
//
// The member 'Sum' has a different requirement on 'T than the type IEnumerable<'T>
type IEnumerable<'T> with
    member this.Sum() = Seq.sum this
```

このコードを取得して、オプションの型拡張機能を使用することはできません。

- そのように、 `Sum` メンバーは、型拡張機能で定義されているものとは異なる制約を `'T` ( `static member get_Zero` および) 持ち `static member (+)` ます。
- と同じ制約を持つように型拡張を変更すると、 `Sum` で定義されている制約とは一致しなくなり `IEnumerable<'T>` ます。
- `member this.Sum`をに変更する `member inline this.Sum` と、型制約が一致しないというエラーが表示されます。

必要なのは、"スペースで浮動小数点" を使用する静的メソッドであり、型を拡張するかのように表示できます。 ここで拡張メソッドが必要になります。

## <a name="extension-methods"></a>拡張メソッド

最後に、拡張メソッド ("C# スタイル拡張メンバー" とも呼ばれます) は、F # でクラスの静的メンバーメソッドとして宣言できます。

拡張メソッドは、型変数を制約するジェネリック型の拡張機能を定義する場合に便利です。 次に例を示します。

```fsharp
namespace Extensions

open System.Collections.Generic
open System.Runtime.CompilerServices

[<Extension>]
type IEnumerableExtensions =
    [<Extension>]
    static member inline Sum(xs: IEnumerable<'T>) = Seq.sum xs
```

このコードを使用すると、 `Sum` が <xref:System.Collections.Generic.IEnumerable%601> 開かれている `Extensions` かスコープ内にある限り、がに定義されているかのように表示されます。

VB.NET code で拡張機能を使用できるようにするに `ExtensionAttribute` は、アセンブリレベルで追加のが必要です。

```fsharp
module AssemblyInfo
open System.Runtime.CompilerServices
[<assembly:Extension>]
do ()
```

## <a name="other-remarks"></a>その他の解説

型拡張には、次の属性もあります。

- アクセス可能なすべての型を拡張できます。
- 組み込みおよびオプションの型拡張では、メソッドだけでなく、 _任意_ のメンバー型を定義できます。 たとえば、拡張機能のプロパティも可能です。
- `self-identifier`[構文](type-extensions.md#syntax)のトークンは、通常のメンバーと同じように、呼び出される型のインスタンスを表します。
- 拡張メンバーは、静的メンバーまたはインスタンスメンバーにすることができます。
- 型の拡張機能の型変数は、宣言された型の制約と一致する必要があります。

型拡張機能には、次の制限もあります。

- 型拡張は、仮想メソッドまたは抽象メソッドをサポートしていません。
- 型拡張は、拡張としてのオーバーライドメソッドをサポートしていません。
- 型拡張は、 [静的に解決される型パラメーター](./generics/statically-resolved-type-parameters.md)をサポートしていません。
- 省略可能な型拡張は、拡張としてのコンストラクターをサポートしていません。
- 型の拡張子を型の [省略形](type-abbreviations.md)に対して定義することはできません。
- 型拡張は、では有効ではありません `byref<'T>` (ただし、宣言することはできます)。
- 型拡張は、属性に対しては有効ではありません (ただし、宣言することはできます)。
- 同じ名前の他のメソッドをオーバーロードする拡張機能を定義できますが、あいまいな呼び出しがある場合は、F # コンパイラによって非拡張メソッドが優先されます。

最後に、1つの型に対して複数の組み込み型拡張が存在する場合は、すべてのメンバーが一意である必要があります。 オプション型拡張の場合は、1 つの型に対する複数の型拡張が存在する場合でも、各メンバーに同じ名前を付けることができます。 クライアント コードで同じメンバー名が定義されている 2 つの異なるスコープを開いている場合にのみ、あいまいさに対するエラーが発生します。

## <a name="see-also"></a>関連項目

- [F# 言語リファレンス](index.md)
- [[メンバー]](./members/index.md)
