---
title: WDI_TLV_MULTICAST_DATA_ALGORITHM_LIST
description: WDI_TLV_MULTICAST_DATA_ALGORITHM_LIST は、マルチキャストデータアルゴリズムペアの配列を含む TLV です。
ms.assetid: BF07170E-CF4E-4E93-85E1-3276E414BDD9
ms.date: 07/18/2017
keywords:
- Windows Vista 以降のネットワークドライバーの WDI_TLV_MULTICAST_DATA_ALGORITHM_LIST
ms.localizationpriority: medium
ms.openlocfilehash: ff3bd22e3b5848d0e4d3d6730fe1b97cee60063f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837630"
---
# <a name="wdi_tlv_multicast_data_algorithm_list"></a>WDI\_TLV\_マルチキャスト\_データ\_アルゴリズム\_一覧


WDI\_TLV\_マルチキャスト\_データ\_アルゴリズム\_一覧は、マルチキャストデータアルゴリズムペアの配列を含む TLV です。

## <a name="tlv-type"></a>TLV 型


0x14

## <a name="length"></a>長さ


WDI\_ALGO\_組の要素の配列のサイズ (バイト単位)。 配列には1つ以上の要素が含まれている必要があります。

**注**  WDI\_algo\_のペアは、WDI 構造体ではありません。 これは、WDI TLV parser ジェネレーターで定義されており、ドキュメントの目的でのみ使用されます。

 

## <a name="values"></a>値


| 種類                 | 説明                                            |
|----------------------|--------------------------------------------------------|
| WDI\_ALGO\_ペア\[\] | 認証と暗号アルゴリズムのペアの配列。 |

 

WDI\_ALGO\_のペアは、次の要素で構成されています。

| 種類  | 説明                                                                                     |
|-------|-------------------------------------------------------------------------------------------------|
| UINT8 | [**WDI\_AUTH\_アルゴリズム**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_auth_algorithm)で定義されている認証アルゴリズム。 |
| UINT8 | [**WDI\_cipher\_アルゴリズム**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_cipher_algorithm)で定義されている暗号アルゴリズム。     |

 

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

 

 




