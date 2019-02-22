---
title: DirectX 5.0 インターフェイス
description: DirectX 5.0 インターフェイス
ms.assetid: 416a9187-d64f-48a4-8868-fd5158d58a25
keywords:
- ジョイスティックに WDK を非表示にインターフェイス
- 仮想ジョイスティックのドライバー WDK を非表示にインターフェイス
- VJoyD WDK HID、インターフェイス
- WDK ジョイスティック インターフェイス
- ジョイスティックに WDK を非表示にコールバック
- 仮想ジョイスティックのドライバー WDK を非表示にコールバック
- VJoyD WDK HID、コールバック
- WDK ジョイスティックのコールバック
- WDK ジョイスティックのポーリング
- ジョイスティックに WDK を非表示にバージョン
- VJoyD WDK HID のバージョン
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 45280843a3e3900821a27bb363a2a1e4d4bba022
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530938"
---
#  <a name="directx-50-interface"></a>DirectX 5.0 インターフェイス





DirectX 5.0 およびそれ以降のインターフェイス VJoyD とその以前のバージョンのいずれかを認識できません。 そのため、登録を試みる前に、ミニドライバーは VJoyD のバージョンを確認します。 必要があります。 VJoyD は標準のバージョンのメッセージをサポートしていません。 そのため、これを手動で実装する VJoyD のデバイス記述子ブロック (DDB) を取得し、DDB でマークされているバージョンを確認しください。 これを実装する方法の詳細については、例については、ドライバーのサンプルを参照してください。 バージョン リソースでマーク バージョンと同じ、DDB でマークされているバージョンがないに注意してください。

ミニドライバーがそのコールバックを登録するプロセスが大幅に拡張し、DirectX 5.0 でを開始します。

以前のように、VJoyD または HID スタック) などの外部の所有者は、ミニドライバーを読み込むことができます。 VJoyD VJOYD を使用して自身を登録するようにミニドライバーに要する VJoyD にデバイスが読み込まれる\_登録\_デバイス\_ドライバー サービス。 ただし、ミニドライバーは、登録するようにメッセージを表示する 3 つのシステム コントロール メッセージを受信する可能性があります。 1 つは、SYS\_動的\_デバイス\_ミニドライバーを受け取る VJoyD で読み込まれる前に、VxD が読み込まれていない場合、INIT メッセージ。 これは、登録に使用される元のインターフェイスとして同じメカニズムを使用します。 VxD の最新の負荷であるため、定義されている INIT セクションを利用できます。 このメッセージの受信後は、VxD は内部の初期化を実行し、VJoyD に登録されます。

アプリケーションには、(たとえば、プライベートの IOCTL インターフェイスを使用するように、アプリケーションが読み込まれている場合) のミニドライバーが既に読み込まれている場合にメッセージは表示されませんこのもう一度 VJoyD で読み込まれる。 このような場合は、Windows 98 の問題、SYS\_動的\_デバイス\_REINIT メッセージと応答で、ミニドライバーは VJoyD を登録する必要があります。 これは、VxD の最新の負荷ではないため、INIT のセクションでは利用できなくします。 Windows 98 が動作しないミニドライバー、VJoyD かかりますとしてのミニドライバーの負荷に応じての欠如 VxD が既に読み込まれています。 VJoyD 発行有向システム コントロール メッセージ BEGIN\_予約済み\_プライベート\_システム\_コントロール、応答をミニドライバーを登録する必要があります。

読み込み時の登録だけでなく VJoyD では、ドライバーでは、それを駆動するデバイスの状態の変更を検出時に新しい種類の登録がようになりました受け入れます。 だけでなく、コールバックは、DirectX 5.0 インターフェイスは、さまざまな制御パラメーターと登録に設定するデバイスの説明をによりします。 これには、検出されたその他のデバイスに合わせて変更できるデバイス (調整情報を含む完全)、完全な説明が含まれます。

DirectX 5.0 およびそれ以降のインターフェイスのジョイスティック ミニドライバー コールバックは、コントロールのコールバック、ポーリング、コールバック、およびフォース フィードバック コールバックで構成されます。 これらの変更を VJoyD VJOYD への対応\_登録\_デバイス\_EAX が使用されて、新しい登録と、ECX を保持する構造体へのポインターを保持することを示す 0 xffffffff を保持するために、ドライバー サービスが過負荷、パラメーター。 EBX および EDX の値が定義されていると、ドライバーが EBX がして呼び出しから返されることを想定します。

次の例では、ジョイスティックを表示するミニドライバー登録シーケンス。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>mov</p></td>
<td><p>eax、0ffffffffh</p></td>
</tr>
<tr class="even">
<td><p>mov</p></td>
<td><p>ecx に offset32 RegData</p></td>
</tr>
<tr class="odd">
<td><p>VxDcall</p></td>
<td><p>VJOYD_Register_Device_Driver</p></td>
</tr>
</tbody>
</table>

 

[ **VJREGDRVINFO** ](https://msdn.microsoft.com/library/windows/hardware/ff543581)構造体は、新しい登録に渡されます。

**DwFunction** VJREGDRVINFO 構造体のメンバーは VJRT である必要があります\_読み込まれたその他のすべての値は予約されています。 VJRT\_LOADED は登録を使用する元のインターフェイスでは、読み込まれているようにミニドライバーに応答 VJoyD にコールバックを渡すと同様に、新しいインターフェイスで使用します。

コントロールのコールバックとポーリング コールバック、すべてのドライバーは、コントロールのコールバックを指定する必要があり、非常に少数のデバイスが出力のみであるために、1 つのテーブルにマージされます (およびしたがってポーリング コールバックを必要はありません)。 使用してこれらのコールバックが登録されて、 [ **VJPOLLREG** ](https://msdn.microsoft.com/library/windows/hardware/ff543577)構造体。

**LpCfg** VJPOLLREG 構造体のメンバーは、元のインターフェイスで CfgRoutine とまったく同じように、標準の構成マネージャー コールバックをポイントします。 主な違いは、VJoyD が適切な configuration manager のコールバックを呼び出します。 VJoyD はドライバーをインストール済みのデバイス ノードにリンクし、configuration manager アクティビティのドライバーに通知するには、このコールバックを呼び出します。 以前のインターフェイスでは、各 configuration manager のコールバック、DirectX 5.0 の読み込まれているすべてのドライバーと呼ばれ、以降のインターフェイスのみ呼び出しを 1 つのドライバーが、変更されてデバイス ノードにリンクします。 また、ドライバーが読み込まれていないときに、configuration manager のアクティビティが発生する可能性があります、ためにが読み込まれるときに、このデバイス ノードのドライバーを通知する場合は、[デバイス] ノードが開始されて VJoyD プリミティブ キャッシュ システムは実装します。

ドライバーは常に呼び出されるため、リソースの割り当てを必要なリソースを検索する既定のポートが確認しません。 残念ながら、前のインターフェイスを使用する方法を検索する必要があったドライバーは、従来の方法で引き続き動作します。 つまり、こと VJoyD は、一連のリソースを 1 つのドライバーのみを割り当てます、すべての古いドライバーが読み込まれるを引き続き使用できますに割り当てられていないポート。 リソースが割り当てられると、ドライバーは、デバイスとデバイスの状態を判断するために必要なすべてのハンドシェイクを実行する必要があります。

[*初期化*](https://msdn.microsoft.com/library/windows/hardware/ff541025)コールバック (によって示される、 **fpInitialize** VJPOLLREG 構造体のメンバー) が置き換えられます、 *JoyId*でのコールバック前のインターフェイスです。 主な違いは、ドライバーは、1 つ以上のデバイスをサポートしている場合、インスタンスを識別できるように VJoyD にデバイスが登録時に渡されるデバイス インスタンスの識別のドライバーに戻る VJoyD が渡します。

**注**  使用する必要があるレジストリ キーを開く必要がある場合、 [VJOYD\_OpenConfigKey\_サービス](https://msdn.microsoft.com/library/windows/hardware/ff543545)と[VJOYD\_OpenTypeKey\_サービス](https://msdn.microsoft.com/library/windows/hardware/ff543549)レジストリ キーを直接開く代わりにマクロ。 これらのサービスのマクロの使用により、適切なレジストリ ブランチが開かれています。 さらに、マクロがありますが、サービス サポートされる将来のバージョン DirectInput の基になるレジストリ データは異なる方法で構造化可能性があります。

 

 

 



