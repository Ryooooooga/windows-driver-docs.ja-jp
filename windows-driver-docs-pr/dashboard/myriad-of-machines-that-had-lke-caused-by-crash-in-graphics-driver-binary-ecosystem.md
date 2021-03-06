---
title: グラフィックス ドライバー バイナリのクラッシュによって LKE が発生した無数のマシン
description: この測定値は、グラフィックス ドライバーのバイナリにおけるクラッシュが原因で LKE が発生した個別のマシンのミリアドとして、7 日間のスライディング ウィンドウからのテレメトリを集計したものです。
ms.topic: article
ms.date: 10/28/2019
ms.localizationpriority: medium
ms.openlocfilehash: 3c53dbdb8e3c0678349a926d9c215f817ae33140
ms.sourcegitcommit: fe0b8b8b162c6fc0afd82dd03e83d41be0bc5d12
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/28/2019
ms.locfileid: "72980747"
---
# <a name="myriad-of-machines-that-had-an-lke-caused-by-a-crash-in-the-graphics-driver-binary"></a>グラフィックス ドライバー バイナリのクラッシュによって LKE が発生した無数のマシン

## <a name="description"></a>説明

ユーザーのセッション中、グラフィックス ドライバーのバイナリにおけるクラッシュが原因でライブ カーネル イベント (LKE) が発生する場合があります。それによってマシンが再起動され、ユーザーのワークフローが中断されることがあります。 この測定では、ドライバーが入れられており、グラフィックス ドライバーのバイナリにおけるクラッシュが原因で LKE が生じたマシンの数が評価されます。

これは、[グラフィックス ドライバーのバイナリにおけるクラッシュによって LKE が発生したマシンのミリアド](https://docs.microsoft.com/windows-hardware/drivers/dashboard/myriad-of-machines-that-had-lke-caused-by-crash-in-graphics-driver-binary-standard)の測定のエコシステムに対応するものです。

## <a name="measure-attributes"></a>測定値の属性

|属性|Value|
|----|----|
|**オーディエンス**|エコシステム|
|**期間**|7 日間のスライディング ウィンドウ|
|**測定基準**|マシンの集計|
|**最小母集団**|20,000 台のマシン|
|**合格基準**|LKE イベントの発生したマシンが 10,000 台中 130 台以下|
|**測定 ID**|17361846|

## <a name="calculation"></a>計算

この測定では、**グラフィックス ドライバーのバイナリにおけるクラッシュが原因で LKE が発生した個別のマシン**の**ミリアド**として、7 日間のスライディング ウィンドウからのテレメトリが集計されます。
1. *LKE が発生したマシン = ドライバーが入れられており、LKE が発生したマシンの台数*
2. "*総マシン数 = ドライバーがインストールされているマシンの台数*"
3. *LKE が発生したマシンの割合 = LKE が発生したマシン/総マシン数*

### <a name="final-calculation"></a>最終的な計算

*母集団に対する個別のデバイス ヒット数 (DHoP) = LKE が発生したマシンの割合 * 10,000*

上記の計算では、結果は 10,000 台のマシンに正規化され、最終的な結果は次のようになります。    
[母集団に対する個別のデバイス ヒット数 (DHoP)] 10,000 台のマシンのうち、グラフィックス ドライバーのバイナリにおけるクラッシュが原因で LKE が発生した個別のマシン
