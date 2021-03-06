---
title: GDL 構成
description: GDL 構成
ms.assetid: ce698737-c9d8-4502-8823-e249820a06fa
keywords:
- GDL WDK の構成
- WDK GDL の構成
- WDK GDL、例の構成
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 990c4483698ead05304389900fe9b0bbe1bf4076
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63392167"
---
# <a name="gdl-configurations"></a>GDL 構成


GDL では、データの依存関係を定義することができます。 クライアントが依存関係を意識する必要はありません。代わりに、クライアントは、スナップショットを要求して、パーサーは、その構成に対応するスナップショットを生成時に、関心のある構成を指定します。

たとえば、電話の呼び出しに対して課金される価格は、送信元と送信先のポイントや、電話がかけ、呼び出し元のプランが使用されている週の曜日と時間に依存します。 すべての考えられる結果の価格は、大きな多次元配列で表現できます。 このデータは、送信元と送信先のポイント、日、呼び出し元のプランの時間など、さまざまな変数を表すパラメーターを定義する GDL ディレクティブを使用して表現できます。 これらのパラメーターに使用できる値を定義する他のディレクティブを使用できます。 まだ他のディレクティブは、データを定義するパラメーターの値に依存する方法を指定します。 電話 (次の例では CostOfCall) のコストを表すデータが GDL ソース ファイルとして表現されている、解析できるし、任意のクライアントが必要な va を代入する構成を作成するだけで電話をかけるのコストを取得できます。ロ、GDL で定義されている各パラメーターにします。

たとえば、クライアントは可能性がありますを次のデータを含む構成を作成します。

```cpp
OriginationPoint: Seattle
DestinationPoint: SanFrancisco
LengthOfCall: 10minutes
TimeOfDay: Night
CallingPlan: OneRate
```

生成されたスナップショットが 1 つの例を次のように見える可能性があります (すべての可能な組み合わせの) 外のデータが格納されます。

```cpp
CostOfCall: $0.49
```

GDL スナップショットは、何千もの項目または 1 つだけを持つ複雑なデータ構造体を含めることができます。 スナップショット内の各項目は、構成によって、クライアントは認識しません、独自の依存関係のセットを持つことができます。 クライアントは、関心のある構成を指定する必要があり、GDL パーサーはその構成に対応するデータを表すスナップショットに戻ります。

GDL により除外する選択した構成、さらに、「許可されていません」とします。 たとえば、印刷デバイスでは、透過的なメディアで両面印刷を許可する希望可能性があります。 GDL パーサー インターフェイスが、指定された構成が許可されたかを使用できないかどうかを検出する方法構成が許可されていない場合は、ことができるように、メソッドは最低限の構成が変更されます。 除外された構成を定義するためのディレクティブと競合を解決するのには、構成を修正できるし、変更を行って、元の意図が維持されますので可能な限りように、パラメーターの相対的な重要度を指定するディレクティブがあります。

データの作成の詳細については、構成に依存するを参照してください。 [GDL 構成に依存するデータを作成する](creating-gdl-configuration-dependent-data.md)します。

 

 




