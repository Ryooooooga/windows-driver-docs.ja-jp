---
title: Windows コンポーネントにおけるユーザー モードの信頼性を示すクラッシュ数を母集団で正規化した値がベースライン目標と同じかそれより小さい
description: この測定値は、年単位の総実行時間について、グラフィックス ドライバーに起因する Microsoft コンポーネントのクラッシュの割合として、7 日間のスライディング ウィンドウからのテレメトリを集計したものです
ms.topic: article
ms.date: 08/08/2019
ms.localizationpriority: medium
ms.openlocfilehash: 84c09cc623b49d7c5aba506da836ca5f95ed39c4
ms.sourcegitcommit: b33dff0fc9b5b90ee8bd07f62713c58c5f60b40f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/16/2019
ms.locfileid: "71016918"
---
# <a name="number-of-user-mode-reliability-for-crashes-in-windows-components-photos-app-normalized-by-population-is-less-than-or-equal-to-the-baseline-goal"></a>Windows コンポーネント フォト アプリにおけるユーザー モードの信頼性を示すクラッシュ数を母集団で正規化した値がベースライン目標と同じかそれより小さい

## <a name="description"></a>説明

この測定値では、ドライバーが使用されるすべてのマシンの数に関連して、ディスプレイ ドライバーで Windows コンポーネント (dwm.exe、シェル、ログオン UI など) がクラッシュする頻度を監視します。 Windows コンポーネントがクラッシュした場合、再び使用できる状態になるまで、ユーザーはそのアプリケーションの回復を待機する必要があります。

## <a name="measure-attributes"></a>測定値の属性

|属性|Value|
|----|----|
|**オーディエンス**|展開|
|**期間**|7 日間のスライディング ウィンドウ|
|**測定基準**|マシンの集計|
|**最小インスタンス**|10,000 台のマシン|
|**合格基準**|10,000 台のマシンあたりのクラッシュが 15 回以下|
|**測定 ID**|22725967|

## <a name="calculation"></a>計算

1. この測定値は、**ドライバーがインストールされているすべてのマシンに対する、グラフィックス ドライバーに起因する Windows コンポーネントのクラッシュの割合**として、7 日間のスライディング ウィンドウからのテレメトリを集計したものです
2. "*Windows コンポーネントの総クラッシュ回数 = ドライバーがインストールされているマシンで Windows コンポーネントがクラッシュした回数*"
3. "*デバイスの総数 = ドライバーがインストールされているマシンの合計*"

### <a name="final-calculation"></a>最終的な計算 

4. "*デバイス数で正規化された Windows コンポーネントのクラッシュ回数 = Windows コンポーネントの総クラッシュ回数 * 10,000 / デバイスの総数*"
