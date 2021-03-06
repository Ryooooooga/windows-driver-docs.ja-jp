---
title: 電源管理
description: 電源管理
ms.assetid: b47ed463-2292-419a-af16-196382dbd3f1
keywords:
- 電源管理の WDK プリンター
- 重大なシャット ダウンの WDK プリンター
- シャット ダウンの電源管理の WDK プリンター
- スタンバイ テスト WDK プリンター
- テストの WDK プリンターを休止状態します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1c6543333369ee51fa4a6452035ee08c4b2b3c68
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373808"
---
# <a name="power-management"></a>電源管理


いくつかのポートに接続されたデバイスの最も一般的なエラーは、システムは、さまざまなスリープ状態を循環すると、デバイスには、デバイスの電源状態を正しく設定またはさまざまなデバイスの電源の状態からを返すが失敗した場合に発生します。 システムを完全に電源オフ状態 (「コールド ブート」) から起動した場合、常に機能する必要があります。 入力するか、スリープ状態から復帰する一意の特別な動作は、ほとんどの場合、バグです。

デバイスが正しく動作しているかどうかを確認するこれらの基本的な規則に従います。

1.  デバイス、ポート、およびそのドライバーをしないブロックまたはシステムのスリープ状態にならないようにします。

2.  進行中の印刷ジョブでは、低電力状態に移動する要求をブロックしないでください。

3.  システムがスリープ状態から戻る、低電力状態が開始されたときに、進行中のある印刷ジョブを正常に再開する必要があります。

4.  重大なシャット ダウンの要求試行はすべて拒否する電源状態の変更が上書きされます。

詳細については、次を参照してください。[システム電源の状態](https://docs.microsoft.com/windows-hardware/drivers/kernel/system-power-states)WDK ドキュメントと[システム電源の状態](https://go.microsoft.com/fwlink/p/?linkid=51899)、Microsoft Windows SDK ドキュメント。

### <a name="testing-port-connected-devices-across-various-power-states"></a>さまざまな電源状態の間でのポートに接続されたデバイスのテスト

さまざまな電源状態の前後に、デバイスのテストを開始するには、まず、デバイスの基準を確認[プラグ アンド プレイ](https://docs.microsoft.com/windows-hardware/drivers/kernel/implementing-plug-and-play)(PnP) 機能です。 次に、テスト環境を入力してすべての電源状態から復帰ことを確認します。

1 つのデバイスが接続されており、正しくインストールされているには、各電源状態 S0 s5 までからの前後に、その動作をテストには、次のように。

-   **スタンバイ テスト (S1、S3)**
    1.  入力し、接続されたデバイスのスタンバイ状態と進行中のジョブからの復帰します。 システムでは、各スリープおよびウェイク状態が入力適切にする必要があります。
    2.  デバイスが正しく機能する前に両方を確認し、状態、スリープ状態にします。 インストールされているデバイスがなくても、同じテストを繰り返します。
    3.  スタンバイ状態から復帰した後、デバイスをインストールしてください。 デバイスが正常にインストールする必要があります。
    4.  入力して、進行中の印刷ジョブでスタンバイ状態からスリープ解除することを確認します。 スリープ解除時に進行中のジョブを再開する必要があります。
    5.  ジョブのキャンセルから、回復し、入力して、スタンバイ状態から復帰後に再起動をできること、を確認します。
    6.  デバイスで説明されているエラー状態のそれぞれに[デバイスのエラー状態](device-error-states.md)します。 ジョブのキャンセルから、回復し、入力して、スタンバイ状態から復帰後に再起動をできること、を確認します。
-   **テスト (S4) を休止状態します。**
    1.  入力し、接続されているデバイスで休止状態と進行中のジョブからの復帰します。 システムでは、各スリープおよびウェイク状態が入力適切にする必要があります。
    2.  デバイスが正しく機能する前に両方を確認し、状態、スリープ状態にします。 インストールされているデバイスがなくても、同じテストを繰り返します。
    3.  休止状態から復帰した後、デバイスをインストールしてください。 デバイスが正常にインストールする必要があります。
    4.  入力して、進行中の印刷ジョブを休止状態から復帰を確認します。 スリープ解除時に進行中のジョブを再開する必要があります。
    5.  デバイスで説明されているエラー状態のそれぞれに[デバイスのエラー状態](device-error-states.md)します。 ジョブのキャンセルから、回復し、入力して、休止状態から復帰し、後に再起動をできること、を確認します。
-   **シャット ダウン/再起動 (S5)**
    1.  シャット ダウンされたシステム、デバイスが接続されているし、ジョブの進行状況ではありません。 正常にする必要があります、システムをシャット ダウンします。
    2.  デバイスが正しく機能する両方の検証前に、と後、システムのシャット ダウンします。 インストールされているデバイスがなくても、同じテストを繰り返します。
    3.  シャット ダウンし、システムを再起動した後、デバイスをインストールしてください。
    4.  シャット ダウンし、進行中の印刷ジョブを使用してシステムを再起動します。 再起動時に進行中のジョブを再開する必要があります。
    5.  デバイスで説明されているエラー状態のそれぞれに[デバイスのエラー状態](device-error-states.md)します。 ジョブのキャンセルから、回復し、システムのシャット ダウンまたは再起動からが返された後に再起動をできることを確認します。 シャット ダウンまたは再起動を使用して、キューで印刷ジョブがエラー状態にしておくし、シャット ダウンまたは再起動した後、エラー状態がクリアされた後、印刷ジョブを再開する必要があります。
-   **重大なシャット ダウン**
    1.  コンピューターは、(S0-S4) ときに重大なシャット ダウン イベントの状態を要求できます (たとえば、バッテリ レベルに達している) 場合、上記のアクティブな電源のいずれかにできます。 デバイスが正しく機能する両方の確認、重大なシャット ダウン イベントの前後にします。 インストールされているデバイスがなくても、同じテストを繰り返します。
    2.  重大なシャット ダウン イベント後にデバイスをインストールしてください。
    3.  デバイスの使用中で重大なシャット ダウン イベントは、電源マネージャーによって開始され、デバイス ドライバーがスリープ状態を拒否していないときに条件をテストします。
    4.  進行中の印刷ジョブには、重大なシャット ダウン イベントを開始します。 システムがスリープ解除時に、印刷ジョブが再起動し、適切な回復する必要があります。
    5.  デバイスで説明されているエラー状態のそれぞれに[デバイスのエラー状態](device-error-states.md)します。 ジョブのキャンセルから、回復し、重大なシャット ダウン イベントから返された後に再起動をできることを確認します。 シャット ダウンまたは再起動を使用して、キューで印刷ジョブがエラー状態にしておくし、シャット ダウンまたは再起動した後、エラー状態がクリアされた後、印刷ジョブを再開する必要があります。
    6.  デバイスがインストールされ、アイドル状態、使用、**電源オプション**アプリケーション、コントロール パネル から取得したシステムのスリープ状態を開始します。 システムは特定の時点で適切なスリープ状態の入力を確認します。 インストールされているデバイスがなくてもこのテストを繰り返すし、システム スリープ状態を解除した後、デバイスにインストールできることを確認します。

 

 




