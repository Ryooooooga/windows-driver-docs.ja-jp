---
title: bob デインターレース アルゴリズム
description: bob デインターレース アルゴリズム
ms.assetid: ef3220bd-841d-4187-bc86-11b999eae2bd
keywords:
- bob WDK DirectX va なので、デインター レース アルゴリズム
- WDK DirectX va なので、bob、アルゴリズムをデインター レース
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 739c0516bde72b1358f9b7e1e30a541e47ae4bad
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384625"
---
# <a name="bob-deinterlacing-algorithm"></a>bob デインターレース アルゴリズム


## <span id="ddk_bob_deinterlacing_algorithm_gg"></span><span id="DDK_BOB_DEINTERLACING_ALGORITHM_GG"></span>


ディスプレイ ドライバーは、DXVA を実装している場合[DDI デインター レース](https://docs.microsoft.com/windows-hardware/drivers/display/deinterlace-ddi)、だけでなく、独自のアルゴリズムをデインター レース bob スタイル デインター レース アルゴリズムをサポートする必要があります。 次に、bob スタイル デインター レース アルゴリズムの説明を示します。

入力がフィールド F<sub>で</sub>(i, j) MxN がこのようなサイズの 0 &lt;i = &lt;M-1 と 0 を = &lt;j = &lt;N-1, i と j が行と列のインデックスでは、それぞれを = です。

出力は、フレーム F<sub>アウト</sub>(i, j) のようなサイズ 2xMxN 0 &lt;i = &lt;2 M 1 と 0 を = &lt;j = &lt;N-1, i と j が行と列のインデックスでは、それぞれを =。

場合 F<sub>で</sub>(i, j) は最上位のフィールドです。

![fin(i,j) が一番上のフィールドである場合は、アルゴリズムをデインター レース bob を示す計算](images/bobtop.png)

場合 F<sub>で</sub>(i, j) は下部にあるフィールドです。

![fin(i,j) が下部にあるフィールドである場合は、アルゴリズムをデインター レース bob を示す計算](images/bobbotom.png)

各定義は、長さが 2 K の h インパルス応答を有限インパルス応答 (FIR) フィルターを使用します。 インパルス応答時間は、中点の対称ように h₋₍ₖ₊₁₎ = k の hₖ K-1 に 0 を = し、

![計算のフィルター アルゴリズムを示す](images/firfiltr.png)

K = 2 と h₀ bob スタイル デインター レースの優先形式を使用して = 9/16 (その h₁ = 1/16)。 このフィルターとして実装する必要があります (9\*(b+c)-(a+d)+8)&gt;&gt;4、a、b、c、d は、1 つの出力サンプルを生成するために使用される 4 つの入力サンプル。

 

 





