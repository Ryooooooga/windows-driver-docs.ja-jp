---
title: NDIS_STATUS_WDI_INDICATION_ASSOCIATION_PARAMETERS_REQUEST
description: ミニポート ドライバーは、ホストから Bssid の一連の要求関連のパラメーターの NDIS_STATUS_WDI_INDICATION_ASSOCIATION_PARAMETERS_REQUEST を使用します。
ms.assetid: 2c8aef86-bb4a-47c6-a839-eb14eb430a31
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_WDI_INDICATION_ASSOCIATION_PARAMETERS_REQUEST ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 59c88edddb64bb4e6002b4bfe91205f57fc46b07
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382188"
---
# <a name="ndisstatuswdiindicationassociationparametersrequest"></a>NDIS\_状態\_WDI\_INDICATION\_アソシエーション\_パラメーター\_要求


ミニポート ドライバーを使用して、NDIS\_状態\_WDI\_を示す値\_アソシエーション\_パラメーター\_Bssid の一連の関連パラメーターをホストから要求を要求します。

| オブジェクト |
|--------|
| ポート   |

 

現在の設定に基づくアソシエーションの候補となる BSS エントリを見つけたときに、アダプターによってこのを示す値を送信できます。 この通知を受信すると、ホスト チェック アソシエーション パラメータがある場合とそうである場合に送信しますで[OID\_WDI\_設定\_アソシエーション\_パラメーター](oid-wdi-set-association-parameters.md)します。

## <a name="payload-data"></a>ペイロード データ


| 種類                                                                                                             | 許可されている複数の TLV インスタンス | 省略可能 | 説明                                   |
|------------------------------------------------------------------------------------------------------------------|--------------------------------|----------|-----------------------------------------------|
| [**WDI\_TLV\_アソシエーション\_パラメーター\_要求された\_型**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-association-parameters-requested-type) |                                |          | 要求された関連付けパラメーターの一覧。 |
| [**WDI\_TLV\_BSS\_エントリ**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-bss-entry)                                                           | x                              | x        | Bssid の一覧。                           |

 

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>サポートされている最小のクライアント</p></td>
<td><p>Windows 10</p></td>
</tr>
<tr class="even">
<td><p>サポートされている最小のサーバー</p></td>
<td><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td><p>Header</p></td>
<td>Dot11wdi.h</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[OID\_WDI\_タスク\_接続](oid-wdi-task-connect.md)

 

 




