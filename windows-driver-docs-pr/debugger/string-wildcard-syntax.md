---
title: 文字列のワイルドカードの構文
description: このトピックでは、文字列のワイルドカードの構文について説明します。 いくつかのデバッガー コマンドでは、さまざまなワイルドカード文字をそのまま使用する文字列パラメーターがあります。
ms.assetid: 11e73f81-5d5c-4d9a-8380-ec767b27f603
keywords: コマンドの構文規則は文字列のワイルドカード、式、正規表現を使用
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 12885d5b86ac862c940144d2b558c1535f73dedb
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56579375"
---
# <a name="string-wildcard-syntax"></a>文字列のワイルドカードの構文


## <span id="ddk_string_wildcard_syntax_dbg"></span><span id="DDK_STRING_WILDCARD_SYNTAX_DBG"></span>


いくつかのデバッガー コマンドでは、さまざまなワイルドカード文字をそのまま使用する文字列パラメーターがあります。 これらのパラメーターは、それぞれの参照ページに記載されています。

この種のパラメーターは、次の構文機能をサポートします。

- アスタリスク (\*) 0 個以上の文字を表します。

- 疑問符 (?) は、任意の 1 文字を表します。

- 角かっこ ( \[ \] ) 一連の文字を表す、リスト内の任意の 1 文字を含むです。 一覧で 1 つだけの文字に一致します。 これらのかっこ内には、範囲を指定するのに、ハイフン (-) を使用できます。 たとえば、 **Prog\[er-t7\]います**"Progeam"、"Program"、"Progsam"、"Progtam"および"Prog7am"と一致します。

- シャープ記号 (\#) 0 個以上の前の文字を表します。 たとえば、 **Lo\#p** "Lp"、「除外」、「ループ」、"Looop"、およびなどと一致します。 組み合わせることもできます、番号記号を角かっこ、したがって**m\[ia\]\#n** "mn"、"min"、"man"、"maan"、"main"、"mian"、"miin"、"miain"、およびなどと一致します。

- プラス記号 (+) は、1 つ以上の前の文字を表します。 たとえば、 **Lo + p**と同じ**Lo\#p**ことを除いて、 **Lo + p** "Lp"と一致しません。 同様に、 **m\[ia\]+ n**と同じ**m\[ia\]\#n**ことを除いて、m<strong>\[ia\]+ n</strong> "mn"と一致しません。 **ですか? + b**も同じです **、\*b**ことを除いて、 **、ですか? + b** "ab"と一致しません。

- リテラルの番号記号を指定する必要がある場合 (\#)、疑問符 (?) を開き角かっこ (\[)、閉じかっこ (\])、アスタリスク (\*)、またはプラス記号 (+) 文字で、円記号を追加する必要があります ( \\ ) の前文字。 ハイフンは、角かっこで囲むことはない場合に常にリテラル。 かっこで囲まれたリスト内の文字のハイフンを指定することはできません。

シンボルを指定するパラメーターには、その他の機能もサポートします。 アンダー スコアを使用するだけでなく、標準の文字列のワイルドカード文字 (\_) シンボルの指定に使用するテキスト式の前にします。 シンボルには、この式を照合するときに、デバッガーは任意の分量のアンダー スコア、0 であってもとして、アンダー スコアを扱います。 この機能は、シンボルを照合するときにのみ適用されます。 ワイルドカードの式を文字列に一般的に適用にはされません。 シンボルの構文の詳細については、次を参照してください。[シンボルの構文と一致するシンボル](symbol-syntax-and-symbol-matching.md)します。

 

 




