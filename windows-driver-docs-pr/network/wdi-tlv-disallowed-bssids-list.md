---
title: WDI_TLV_DISALLOWED_BSSIDS_LIST
description: WDI_TLV_DISALLOWED_BSSIDS_LIST は、関連付けに使用することが許可されていない BSSIDs の一覧を含む TLV です。
ms.assetid: A65A6C05-C4E1-4880-BF83-48B62D0C2FD3
ms.date: 07/18/2017
keywords:
- WDI_TLV_DISALLOWED_BSSIDS_LIST ネットワークドライバー (Windows Vista 以降)
ms.localizationpriority: medium
ms.openlocfilehash: ab7d7620654f29833e98dcee413c3a5f17dbd727
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72834148"
---
# <a name="wdi_tlv_disallowed_bssids_list"></a>WDI\_TLV\_BSSIDS\_リスト\_許可されていません


WDI\_TLV\_許可されていない\_BSSIDS\_LIST は、アソシエーションに使用することが許可されていない BSSIDs の一覧を含む TLV です。

## <a name="tlv-type"></a>TLV 型


0xC3

## <a name="length"></a>長さ


[**WDI\_MAC\_アドレス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_mac_address)構造体の配列のサイズ (バイト単位)。 配列には1つ以上の構造体が含まれている必要があります。

## <a name="values"></a>値


| タスクバーの検索ボックスに                                                  | 説明                                                                                                                                               |
|-------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------|
| [**WDI\_MAC\_アドレス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_mac_address)\[\] | 関連付けに使用することが許可されていない BSSIDs の一覧。 このが指定されている場合、アダプターは、この一覧にない AP に関連付けられていない必要があります。 |

 

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
<td>Wditypes</td>
</tr>
</tbody>
</table>

 

 




