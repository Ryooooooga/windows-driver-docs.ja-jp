---
title: カーネル モード クラッシュなしのマシンの割合
description: この測定値は、カーネル モード クラッシュが発生しなかったマシンの割合として、14 日間のスライディング ウィンドウからのテレメトリを集計したものです
ms.topic: article
ms.date: 05/20/2019
ms.localizationpriority: medium
ms.openlocfilehash: 49540d0393a8423721ce9255c636c0f6c0ce29fa
ms.sourcegitcommit: b33dff0fc9b5b90ee8bd07f62713c58c5f60b40f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/16/2019
ms.locfileid: "71016947"
---
# <a name="percent-of-machines-without-a-kernel-mode-crash"></a>カーネル モード クラッシュなしのマシンの割合

## <a name="description"></a>説明

カーネル モード クラッシュ (KMC) は、カーネル エラーが原因で発生し、オペレーティング システムが停止します。 KMC が発生すると、マシンが突然クラッシュし、ブルー スクリーンが表示されます。 この種のクラッシュでは、ユーザーのワークフローが中断され、データが失われる可能性があります。

## <a name="measure-attributes"></a>測定値の属性

|属性|Value|
|----|----|
|**オーディエンス**|標準|
|**期間**|14 日間のスライディング ウィンドウ|
|**測定基準**|マシンの集計|
|**最小母集団**|100 台のマシン|
|**合格基準**|カーネル モード クラッシュが発生しなかったマシンが 96% 以上|
|**測定 ID**|19888712|

## <a name="calculation"></a>計算

1. この測定値は、**KMC が発生しなかったマシンの割合**として、14 日間のスライディング ウィンドウからのテレメトリを集計したものです。
2. "*クラッシュが発生しなかったマシンの台数 = KMC が発生せずにドライバーがインストールされたマシンの台数*"
3. "*総マシン数 = ドライバーが正常にインストールされたマシンの台数*"

### <a name="final-calculation"></a>最終的な計算

"*KMC が発生しなかったマシンの割合 = クラッシュが発生しなかったマシンの台数 / 総マシン数*"
