---
title: システム トレイと SndVol32
description: システム トレイと SndVol32
ms.assetid: 53f8c5be-d0a5-4364-8fac-813cf9f8318c
keywords:
- システム トレイの WDK オーディオ
- SndVol32 WDK オーディオ
- ボリュームのマスター設定の WDK オーディオ
- スピーカー WDK のオーディオ、アイコンの表示
- ボリュームの設定の WDK オーディオ
- アイコンの WDK オーディオ
- スピーカーのアイコンを表示します。
- ボリューム スライダー WDK オーディオ
- スピーカーの非表示のアイコンの WDK オーディオ
- コントロールの WDK オーディオをミュートします。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3c133bebc25bc2209b8b77dfacbadac7cee0f8b4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56552838"
---
# <a name="systray-and-sndvol32"></a>システム トレイと SndVol32


## <span id="systray_and_sndvol32"></span><span id="SYSTRAY_AND_SNDVOL32"></span>


SndVol32 プログラム (Sndvol32.exe) は、(wave、CD、およびシンセサイザー) などのさまざまなサウンド ソース ボリュームの設定と、マスターのボリュームの設定の両方を制御します。 SndVol32 プログラムは、タスク バーで、既定では、Windows 画面の右下隅に表示されるシステム トレイの通知領域に表示される、スピーカーのアイコンとして表されます。

オンにしているときに、スピーカーのアイコンを表示するため、になっている場合は、スピーカーのアイコンを非表示には、システム トレイ (Systray.exe) をプログラムします。 Windows xp の場合、既定では、スピーカーのアイコンは表示されません。 Windows XP SP1 を含む、他のすべての Windows バージョンでは、スピーカー アイコンが既定で表示されます。

Windows XP では、次のタスク バーのスピーカーのアイコンを表示する次の手順を実行します。

1.  コントロール パネル、**サウンドとオーディオ デバイス**アイコン (または単に実行 mmsys.cpl)。

2.  **ボリューム**] タブで、[、**音量アイコンを配置して、タスク バーで**チェック ボックスをオンします。

サウンド カードのボリューム レベルを変更するには、ソフトウェアの管理下にある、タスク バーのスピーカーのアイコンが表示されます。 マスター-ボリュームのアイコンをクリックし、[音量] スライダーを調整することで設定を変更できます。

ログオン時に、システム トレイのクエリ、MIXERLINE の線をミキサーのオーディオ ドライバー\_COMPONENTTYPE\_DST\_スピーカー (スピーカー destination) または MIXERLINE\_COMPONENTTYPE\_DST\_スピーカーのアイコンを表示するかどうかを判断するには、コンポーネントの種類をヘッドホン (ヘッドホンによる立体音響転送先)。 これらのコンポーネントの種類のどちらが見つかると、システム トレイでは、スピーカーのアイコンは表示されません。 行を調べるには、ミュート用のコントロールが含まれるかどうかを確認する行を照会します。 システム トレイには、ログオン時間のミキサー-行の内部的に格納することで処理が完了すると、**ライン ID**と**コントロール ID をミュート**後で参照します。

SndVol32 プログラムには、システム内のすべてのボリューム コントロールを制御するためのユーザー インターフェイスも提供します。 ユーザーがシステム トレイのスピーカーのアイコンをダブルクリック (または Sndvol32.exe を実行するだけです) と SndVol32 には、マスター ボリューム レベルとさまざまなサウンドのソースのボリューム レベルの両方を制御するためのスライダーが含まれています「マスター ボリューム」 ウィンドウが表示されます。 この場合、SndVol32 はさまざまなアルゴリズムを使用して ― 表示内容を確認します。 **マスター音量スライダー**、「マスター」送信先 (たとえば、番号が 0 である送信先) の最初のボリューム コントロールを探します。 これは、通常、スピーカーの変換先です。

SndVol32 を実行すると、認識しているコントロールのセットを検索、ミキサー行ドライバーを照会します。 スライダーのパネルを表示するには、ソース行、次のコントロールの少なくとも 1 つが必要です。

-   ボリューム コントロール

-   ミュート用のコントロール

-   コントロールの詳細 (AGC、低音、または高)

これらのコントロールのいずれもが見つかった場合 SndVol32 では、パネルが表示されません。 単にないコントロールで、MUX の一部であるソース行は、表示するための十分なではありません。 この制限は、簡単に偽のミュートを挿入することで脆弱化コントロールを表示するパネルを取得するトポロジにします。 行は、単に、マルチプレクサーをフィードするとき、**選択**MUXes がミュート用のコントロールを非表示に表示されるボックス。

ミキサー ライン コントロールに適切にマップされていない WDM オーディオ トポロジのノードは、SndVol32 によっては表示されません。 参照してください[トポロジ ノード](topology-nodes.md)詳細についてをノードがミキサー行コントロールに変換されます。 WDM ミキサー行ドライバーによってコントロールにいくつかのノードを変換しますが、SndVol32 が把握しているコントロールのセットのみを表示します。

ボリュームの範囲と、さまざまなバージョンの Windows での既定のボリューム レベルについては、次を参照してください。[既定のオーディオ音量設定](default-audio-volume-settings.md)します。

 

 



