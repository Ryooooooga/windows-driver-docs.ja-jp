---
title: グラフィックス カーネルのクラッシュによってブルー スクリーンが表示されたマシンの数
description: この測定値は、グラフィックス カーネルにおけるクラッシュが原因でブルースクリーンが発生した個別のマシンのミリアドとして、7 日間のスライディング ウィンドウからのテレメトリを集計したものです。
ms.topic: article
ms.date: 05/20/2019
ms.localizationpriority: medium
ms.openlocfilehash: e421c489a67692d8afcde9b51dc4ccf6804a448c
ms.sourcegitcommit: b33dff0fc9b5b90ee8bd07f62713c58c5f60b40f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/16/2019
ms.locfileid: "71016978"
---
# <a name="number-of-machines-that-had-a-blue-screen-caused-by-a-crash-in-the-graphics-kernel"></a>グラフィックス カーネルのクラッシュによってブルー スクリーンが表示されたマシンの数

## <a name="description"></a>説明

ユーザーのセッション中、ディスプレイ カーネルにおけるクラッシュが原因でブルー スクリーンが発生します。それによってマシンが再起動され、ユーザーのワークフローが中断されることがあります。 この測定では、ドライバーがインストールされたマシンのうち、グラフィックス カーネルにおけるクラッシュが生じたマシンの数が評価されます。

## <a name="measure-attributes"></a>測定値の属性

|属性|Value|
|----|----|
|**オーディエンス**|標準|
|**期間**|7 日間のスライディング ウィンドウ|
|**測定基準**|マシンの集計|
|**最小母集団**|5,000 台のマシン|
|**合格基準**|ディスプレイ カーネルのクラッシュが生じたマシンが 10,000 台中 10 台以下|
|**測定 ID**|7533022|

## <a name="calculation"></a>計算

1. この測定値は、**特定の母集団について、グラフィックス カーネルにおけるクラッシュが原因でブルースクリーンが発生した個別のマシン**の**ミリアド**として、7 日間のスライディング ウィンドウからのテレメトリを集計したものです。
2. "*ブルー スクリーンが発生したマシン = ドライバーがインストールされているマシンのうち、ブルー スクリーンが発生したマシンの台数*"
3. "*総マシン数 = ドライバーがインストールされているマシンの台数*"
4. "*ブルー スクリーン発生マシンの割合 = ブルー スクリーン発生マシン / 総マシン数*"

### <a name="final-calculation"></a>最終的な計算

5. "*母集団におけるブルー スクリーン発生マシン数 = ブルー スクリーン発生マシンの割合 * 10,000*"
6. 結果は 10,000 台のマシンに正規化され、最終的な計算は次のようになります。

   i. [母集団におけるブルー スクリーン発生マシン数] 10,000 台のマシンのうち、グラフィックス ドライバーのバイナリにおけるクラッシュが原因のブルー スクリーンに遭遇した個別のマシン