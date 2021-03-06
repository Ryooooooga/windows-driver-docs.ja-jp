---
title: OID_SWITCH_NIC_SAVE_COMPLETE
description: Hyper-v 拡張可能スイッチのプロトコルエッジは、OID_SWITCH_NIC_SAVE_COMPLETE のオブジェクト識別子 (OID) セット要求を発行して、Hyper-v 拡張可能スイッチの拡張機能に対して、実行時データを保存する操作の完了について通知します。
ms.assetid: 75D4C0D5-B4B2-493D-8D1D-400F60613FCA
ms.date: 08/08/2017
keywords: -Windows Vista 以降の OID_SWITCH_NIC_SAVE_COMPLETE ネットワークドライバー
ms.localizationpriority: medium
ms.openlocfilehash: 5f8a137c580e31712ff882044489b5eda4f14d96
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843948"
---
# <a name="oid_switch_nic_save_complete"></a>OID\_\_NIC の切り替え\_保存\_完了


Hyper-v 拡張可能スイッチのプロトコルエッジは、オブジェクト識別子 (OID) セットの OID\_の要求を発行します。これにより\_\_NIC は保存\_完了し、Hyper-v 拡張スイッチの拡張機能に対して、保存する操作の完了について通知します。実行時データ。 この操作により、拡張機能によって、ポートとそれに関連付けられているネットワークアダプター接続のランタイムデータが保存されます。

[**Ndis\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造の**informationbuffer**メンバーには、ndis\_\_スイッチへのポインターが含まれています。これには、 [**NIC\_\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_save_state)構造が保存されます。

<a name="remarks"></a>注釈
-------

Oid の OID セット要求を受信すると\_\_NIC\_保存\_完了すると、拡張機能は次のガイドラインに従う必要があります。

-   拡張機能では、OID 要求に関連付けられている\_状態の構造を[**保存\_\_NIC\_スイッチ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_save_state)を変更することはできません。

-   拡張機能は、 [**NdisFOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequest)を呼び出して、この OID セット要求を拡張可能なスイッチドライバースタック内の基になる拡張機能に転送する必要があります。 拡張機能は OID 要求を失敗させることはできません。

OID\_スイッチ\_NIC に設定されている oid セット要求は、保存\_完了\_、最終的に拡張可能スイッチの基になるミニポートエッジによって処理されます。 この OID メソッド要求がミニポートエッジによって受信された後、NDIS\_STATUS\_SUCCESS による OID 要求を完了します。 これにより、拡張可能スイッチのプロトコルエッジに、拡張スイッチドライバースタックのすべての拡張機能が保存操作を完了したことが通知されます。

拡張可能なスイッチポートのランタイムデータを保存する方法の詳細については、「 [Hyper-v 拡張可能スイッチの実行時データの保存](https://docs.microsoft.com/windows-hardware/drivers/network/saving-hyper-v-extensible-switch-run-time-data)」を参照してください。

### <a name="return-status-codes"></a>ステータスコードを返す

拡張可能スイッチの基になるミニポートエッジは、OID\_スイッチ\_\_NIC の OID クエリ要求を完了します。これにより、保存\_完了し、次のステータスコードのいずれかが返されます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>状態コード</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>NDIS_STATUS_SUCCESS</p></td>
<td><p>OID 要求が正常に完了しました。</p></td>
</tr>
</tbody>
</table>

 

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>バージョン</p></td>
<td><p>NDIS 6.30 以降でサポートされています。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis (Ndis .h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


****
[**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

[**NDIS\_スイッチ\_NIC\_\_の状態を保存する**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_save_state)

 

 




