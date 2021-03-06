---
title: マクロブロック予測
description: マクロブロック予測
ms.assetid: 95e779ab-b110-4636-9475-6881dba89649
keywords:
- MCP WDK DirectX VA
- 動き補正 WDK DirectX VA
- DirectX のビデオ アクセラレータ WDK Windows 2000 の表示、ビデオのデコード
- ビデオ アクセラレータの WDK DirectX のビデオのデコード
- VA WDK DirectX、ビデオのデコード
- ビデオの WDK DirectX va なので、マクロ ブロック予測のデコード
- ビデオのデコード WDK DirectX va なので、マクロ ブロックの予測
- WDK の DirectX va なので、予測をマクロ ブロック
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2452e2bc5027d89aee452a9a358442024ff1b8c8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380421"
---
# <a name="macroblock-prediction"></a>マクロブロック予測


## <span id="ddk_macroblock_prediction_gg"></span><span id="DDK_MACROBLOCK_PREDICTION_GG"></span>


動き補償予測 (MCP) を通じてマクロ ブロック予測の形成には、手順と次の図に示すように、一連の不連続のステージとしてする必要があります。

![動き補償予測 (mcp) を通じてマクロ ブロックの予測を作成するかを示す図](images/preddata.png)

マクロ ブロックの予測を作成することで、次の 4 つの手順が含まれます。

1.  フォームの参照フレーム

    参照フレームは、前の画像のデコードすることによって、またはビデオ アクセラレータの圧縮されていない画面に直接書き込みによって既に作成されている非圧縮の画面です。

2.  参照ブロックを抽出します。

    参照ブロックは必ずしも予測ブロックと同じです。 ほとんどの場合のステージをフィルター処理、予測のために必要な追加のサンプルで構成されます。 メモリ単位の半分サンプル フィルタ リングを実行しない限り、ブロックの要素のピクセル データの 8 列で、8 行で構成される各ブロックの 17 x 17 マトリックスを 16 x 16 半分サンプル フィルター選択されたマクロ ブロックの参照のブロックがあります。 参照ブロックのサイズは、予測のブロック サイズの関数と予測のブロックのフィルター属性の両方です。 参照をブロックする必要がありますで使用するための参照をフレーム バッファーから抽出されたデータのブロックを参照してください[動き補償予測](motion-compensated-prediction.md)(MCP)。

    **注**  参照ブロックに対して定義されていない DirectX VA のため、画像のバッファーを維持するための実装に固有の意味を反映するためのプロパティがあります。

     

3.  予測のブロックを形成する参照ブロックのフィルター処理します。

    参照ブロックは、予測のブロックを生成するために 3 番目の段階でフィルター処理できます。

4.  フォームのマクロ ブロック予測する予測のブロックを結合します。

    マクロ ブロックのサンプルの最終的な予測を形成する 1 つ以上の予測のブロックが結合されます。 ブロックは、1 つまたは複数の予測平面内の対応するブロックまでのピクセル値の平均を計算し、(小数部のデータが 0.5 以上の場合) それぞれ、最も近い整数に丸め処理して結合されます。 P の画像のブロックを組み合わせると一時的に最も近い以前はまたは P 図のブロック。 図の b 要素は、P 画像ブロックして、最も近い前および将来と結合されます。

次の図は、ビデオのデコード マクロ ブロックの予測を作成するときに発生する処理で、追加の手順を示します。 (実線で、要素を示しています、モーションの補正プロセス点線でブロックは、ビデオ デコーディングの他の側面を示しています。 中に。)

![予測ブロックの動き補正のシグナルのフローを示す図](images/sigflowmo3.png)

 

 





