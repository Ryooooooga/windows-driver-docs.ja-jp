---
title: グラフィックス ドライバー バイナリのクラッシュによってブルー スクリーンが表示されたディスクリート GPU の無数のマシン
description: この測定では、グラフィックス ドライバーのバイナリにおけるクラッシュが原因でブルー スクリーンが発生したディスクリート GPU の個別のマシンのミリアドとして、7 日間のスライディング ウィンドウからのテレメトリが集計されます
ms.topic: article
ms.date: 10/28/2019
ms.localizationpriority: medium
ms.openlocfilehash: 49e8753557fc5229f659f8d6b237ffcce20767c2
ms.sourcegitcommit: 6e839d8f12eafd93d357b6896e0671cb69f7ecfa
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/26/2019
ms.locfileid: "72962186"
---
# <a name="myriad-of-machines-with-discrete-gpu-that-had-a-blue-screen-caused-by-a-crash-in-the-graphics-driver-binary"></a>グラフィックス ドライバー バイナリのクラッシュによってブルー スクリーンが表示されたディスクリート GPU の無数のマシン

## <a name="description"></a>説明

ユーザーのセッション中、グラフィックス ドライバーのバイナリにおけるクラッシュが原因でブルー スクリーンが発生し、その結果マシンが再起動されて、ユーザーのワークフローが中断されることがあります。 この測定では、グラフィックス ドライバーのバイナリにおけるクラッシュが原因でブルー スクリーンが生じているドライバーが存在するディスクリート GPU のマシンのミリアド (10,000 台から) が評価されます。 

これは、[グラフィックス ドライバーのバイナリにおけるクラッシュによってブルー スクリーンが表示された、ディスクリート GPU のマシンのミリアド](https://docs.microsoft.com/windows-hardware/drivers/dashboard/myriad-of-machines-that-had-blue-screen-caused-by-crash-in-graphics-driver-binary-discrete-standard)の測定のエコシステムに対応するものです。

## <a name="measure-attributes"></a>測定値の属性

|属性|Value|
|----|----|
|**オーディエンス**|エコシステム|
|**期間**|7 日間のスライディング ウィンドウ|
|**測定基準**|マシンの集計|
|**最小母集団**|20,000 台のマシン|
|**合格基準**|ブルー スクリーンの発生したマシンが 10,000 台中 30 台以下|
|**測定 ID**|16507562|

## <a name="calculation"></a>計算

この測定では、**グラフィックス ドライバーのバイナリにおけるクラッシュが原因でブルー スクリーンが発生したディスクリート GPU の個別のマシン**の**ミリアド**として、7 日間のスライディング ウィンドウからのテレメトリが集計されます。
1. *ブルー スクリーンが発生したマシン = ドライバーが入れられており、ブルー スクリーンが発生したディスクリート GPU のマシンの台数*
2. *総マシン数 = ドライバーが入れられているディスクリート GPU のマシンの台数*
3. *ブルー スクリーンが発生したマシンの割合 = ブルー スクリーンが発生したマシン/総マシン数*

### <a name="final-calculation"></a>最終的な計算

*母集団に対する個別のデバイス ヒット数 (DHoP) = ブルー スクリーンが発生したマシンの割合 * 10,000*

上記の計算では、結果は 10,000 台のマシンに正規化され、最終的な結果は次のようになります。   
[母集団に対する個別のデバイス ヒット数 (DHoP)] 10,000 台のマシンのうち、グラフィックス ドライバーのバイナリにおけるクラッシュが原因でブルー スクリーンが発生した個別のマシン
