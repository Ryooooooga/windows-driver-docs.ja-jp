---
title: OID_WWAN_PACKET_SERVICE
description: OID_WWAN_PACKET_SERVICE を使用すると、GSM ベースし、CDMA ベースの両方の MB デバイスの場合、現在登録されているプロバイダーのネットワークでパケット サービスのアタッチ/デタッチ操作を実行するミニポート ドライバーに指示します。
ms.assetid: 97bb9324-8052-437c-baa5-fb9a8176c779
ms.date: 08/08/2017
keywords: -OID_WWAN_PACKET_SERVICE ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: c83ca3648779e5bef04503c4f30f5b73c34a6c81
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56572284"
---
# <a name="oidwwanpacketservice"></a>OID\_WWAN\_パケット\_サービス


OID\_WWAN\_パケット\_サービスを使用すると、GSM ベースし、CDMA ベースの両方の MB デバイスの場合、現在登録されているプロバイダーのネットワークでパケット サービスのアタッチ/デタッチ操作を実行するミニポート ドライバーに指示します。 パケット サービスのアタッチ/デタッチ状態だけでなくこの OID を使用して、データ クラスの可用性と現在使用されているデータ クラス情報を決定します。

ミニポート ドライバー セットを処理する必要があり、クエリ要求が最初に、非同期に返す NDIS\_状態\_を示す値\_元の要求とそれ以降の送信に必要な[ **NDIS\_ステータス\_WWAN\_パケット\_サービス**](ndis-status-wwan-packet-service.md)状態通知を含む、 [ **NDIS\_WWAN\_パケット\_サービス\_状態**](https://msdn.microsoft.com/library/windows/hardware/ff567910)または要求のクエリ セットの完了に関係なく、現在のパケット サービス状態に関する情報を指定する構造体。

呼び出し元のパケット サービスの現在の状態を設定する要求を提供する[ **NDIS\_WWAN\_設定\_パケット\_サービス**](https://msdn.microsoft.com/library/windows/hardware/ff567921)構造体を適切な情報のミニポート ドライバー。

<a name="remarks"></a>コメント
-------

参照してください[WWAN パケット サービスのアタッチ操作](https://msdn.microsoft.com/library/windows/hardware/ff559092)詳細については、この OID を使用します。

ミニポート ドライバーは、処理するときに、プロバイダーのネットワークにアクセスできるクエリまたはの集合演算、Subscriber Identity Module (SIM カード) にアクセスしないでください。

CDMA ベースのデバイスがこれを使用して機会として可能であれば、ネットワーク リソースの割り当てを解放します。

SIM カードの中には、パケットのドメインと回線交換ドメイン以外でのみ登録する MB デバイスが有効にします。 データの呼び出しを終了、VAN UI 送信 OID\_WWAN\_パケット\_パケット サービスをデタッチするサービス セットの要求。 これにより、パケットのドメインから切断する MB デバイスです。 MB デバイスのネットワークから登録を解除し、電力には、モードを保存します。 その結果、デバイスは、登録を解除する、結果として、VAN UI が表示されなくなり、再起動にのみ復元できます。 このシナリオでミニポート ドライバーは、MB デバイスをこのようなモードに設定しなくても正の値のデータを返すことによって、パケットのアタッチ/デタッチ操作を偽装する必要があります。

パケット アタッチをサポートしていないテクノロジ、ミニポート ドライバーは MB サービス コンテキストのアクティブ化を続行することを把握できるようにする、接続状態を偽装する必要があります。 ミニポート ドライバー セット OID のスプーフィングもする必要があります\_WWAN\_パケット\_ミニポート ドライバーでのサービス要求します。 ミニポート ドライバーに送信する必要があります[ **NDIS\_状態\_WWAN\_パケット\_サービス**](ndis-status-wwan-packet-service.md)通知クエリ操作と要請していません。イベント。 デバイスのパケット サービスの状態に設定されていない場合、ミニポート ドライバーの PDP アクティブ化が失敗する*WwanPacketServiceStateAttached*します。

コンテキストのアクティブ化では、パケット サービスの状態に到達するまで MB サービスは続行されません*WwanPacketServiceStateAttached*します。

<a name="requirements"></a>必要条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>バージョン</p></td>
<td><p>Windows 7 および Windows の以降のバージョンで使用できます。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis.h (include Ndis.h)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NDIS\_WWAN\_設定\_パケット\_サービス**](https://msdn.microsoft.com/library/windows/hardware/ff567921)

[**NDIS\_状態\_WWAN\_パケット\_サービス**](ndis-status-wwan-packet-service.md)

[WWAN パケット サービス アタッチの操作](https://msdn.microsoft.com/library/windows/hardware/ff559092)

 

 



