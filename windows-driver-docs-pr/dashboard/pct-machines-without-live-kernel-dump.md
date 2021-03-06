---
title: ライブ カーネル ダンプなしのマシンの割合
description: この測定値は、ライブ カーネル ダンプが発生しなかったマシンの割合として、14 日間のスライディング ウィンドウからのテレメトリを集計したものです
ms.topic: article
ms.date: 05/20/2019
ms.localizationpriority: medium
ms.openlocfilehash: 0d02ee5456656e9d39f5c49cb93301f3a9958e4c
ms.sourcegitcommit: b33dff0fc9b5b90ee8bd07f62713c58c5f60b40f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/16/2019
ms.locfileid: "71017017"
---
# <a name="percent-of-machines-without-a-live-kernel-dump"></a>ライブ カーネル ダンプなしのマシンの割合

## <a name="description"></a>説明

ライブ カーネル ダンプ (LKD) は、カーネル エラーが原因で発生し、クラッシュすることなくマシンを回復できます。 LKD が発生すると、アプリケーションがハングしたりクラッシュしたりする可能性があります。 一般的な種類の LKD は、タイムアウトの検出と回復 (TDR) で、グラフィックス ドライバーがクラッシュし、ドライバーが回復するまで表示が少しの間黒くなります。

## <a name="measure-attributes"></a>測定値の属性

|属性|Value|
|----|----|
|**オーディエンス**|標準|
|**期間**|14 日間のスライディング ウィンドウ|
|**測定基準**|マシンの集計|
|**最小母集団**|100 台のマシン|
|**合格基準**|LKD が発生しなかったマシンが 90% 以上|
|**測定 ID**|19888731|

## <a name="calculation"></a>計算

1. この測定値は、**LKD が発生しなかったマシンの割合**として、14 日間のスライディング ウィンドウからのテレメトリを集計したものです
2. "*LKD が発生しなかったマシンの台数 = LKD が発生せずにドライバーがインストールされたマシンの台数*"
3. "*総マシン数 = ドライバーが正常にインストールされたマシンの台数*"

### <a name="final-calculation"></a>最終的な計算

"*LKD が発生しなかったマシンの割合 = LKD が発生しなかったマシンの台数 / 総マシン数*"
