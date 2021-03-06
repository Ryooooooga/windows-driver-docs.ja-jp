---
title: Bug Check 0xF6 PCI_VERIFIER_DETECTED_VIOLATION
description: PCI_VERIFIER_DETECTED_VIOLATION のバグ チェックでは、0x000000F6 の値を持ちます。 これは、BIOS または PCI ドライバーによって検証されている別のデバイスでエラーが発生したことを示します。
ms.assetid: 8d2be46d-52fd-41dc-b33c-67fea7e0e501
keywords:
- Bug Check 0xF6 PCI_VERIFIER_DETECTED_VIOLATION
- PCI_VERIFIER_DETECTED_VIOLATION
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- PCI_VERIFIER_DETECTED_VIOLATION
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 7c9d6a37a235cfc0150583d46f8577970487c59f
ms.sourcegitcommit: d03b44343cd32b3653d0471afcdd3d35cb800c0d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2019
ms.locfileid: "67518741"
---
# <a name="bug-check-0xf6-pciverifierdetectedviolation"></a>バグ チェック 0xF6:PCI\_VERIFIER\_検出\_違反


PCI\_VERIFIER\_検出\_違反のバグ チェックが 0x000000F6 の値を持ちます。 これは、BIOS または PCI ドライバーによって検証されている別のデバイスでエラーが発生したことを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://www.windows.com/stopcode)します。


## <a name="pciverifierdetectedviolation-parameters"></a>PCI\_VERIFIER\_検出\_違反パラメーター


パラメーター 1 が; 関心のある唯一のパラメーターこれは、検出されたエラーの性質を識別します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">パラメーター 1</th>
<th align="left">エラーの原因</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x01</p></td>
<td align="left"><p>Active のブリッジは、ドッキング イベント中に、BIOS で行ったりでした。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x02</p></td>
<td align="left"><p>PMCSR レジスタが仕様で指定された時間内に更新されませんでした。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x03</p></td>
<td align="left"><p>ドライバーは、PCI デバイスの構成領域の部分を Windows コントロールに書き込まれます。</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

PCI ドライバは、デバイスまたは BIOS の検証中にエラーを検出します。

 

 




