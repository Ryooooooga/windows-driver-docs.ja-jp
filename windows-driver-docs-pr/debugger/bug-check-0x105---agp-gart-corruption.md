---
title: バグ チェック 0x105 AGP_GART_CORRUPTION
description: AGP_GART_CORRUPTION のバグ チェックでは、0x00000105 の値を持ちます。 これは、グラフィックス Aperture 再マップ テーブル (GART) が壊れていることを示します。
ms.assetid: efc39d1f-666d-4377-a262-ed5164357b52
keywords:
- バグ チェック 0x105 AGP_GART_CORRUPTION
- AGP_GART_CORRUPTION
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- AGP_GART_CORRUPTION
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: ad547578ae3ac1204b4db987401d7fc7e3c959eb
ms.sourcegitcommit: d03b44343cd32b3653d0471afcdd3d35cb800c0d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2019
ms.locfileid: "67521607"
---
# <a name="bug-check-0x105-agpgartcorruption"></a>バグ チェック 0x105:AGP\_GART\_破損


AGP\_GART\_破損バグ チェックが 0x00000105 の値を持ちます。 これは、グラフィックス Aperture 再マップ テーブル (GART) が壊れていることを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://www.windows.com/stopcode)します。


## <a name="agpgartcorruption-parameters"></a>AGP\_GART\_破損パラメーター


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">パラメーター</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>1</p></td>
<td align="left"><p>GART のベース アドレス (仮想)</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>破損が発生した GART オフセット</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>GART キャッシュ (GART のコピー) のベース アドレス (仮想)</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>0</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

このバグ チェックは、ドライバーによって不適切なダイレクト メモリ アクセス (DMA) が通常発生します。

<a name="resolution"></a>解決方法
----------

署名されていないドライバーのドライバーの検証を有効にします。 それらを削除するか、エラーが発生したドライバーが特定されるまで、1 つずつを無効にします。

 

 




