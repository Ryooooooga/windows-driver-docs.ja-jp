---
title: KSEVENT\_VIDCAPTOSTI\_EXT\_トリガー
description: KSEVENT\_VIDCAPTOSTI\_EXT\_TRIGGER イベントは、カーネルモードのビデオキャプチャミニドライバーからユーザーモードの DirectShow に、ビデオキャプチャデバイスでトリガーボタンが押されたときなどのアクションを伝達します。
ms.assetid: 97f67d22-20c4-460c-9022-04e55e74f6f9
keywords:
- KSEVENT_VIDCAPTOSTI_EXT_TRIGGER ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSEVENT_VIDCAPTOSTI_EXT_TRIGGER
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: d233530c7baa845dc5929e5bd99db384a37078c0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843669"
---
# <a name="ksevent_vidcaptosti_ext_trigger"></a>KSEVENT\_VIDCAPTOSTI\_EXT\_トリガー


KSEVENT\_VIDCAPTOSTI\_EXT\_TRIGGER イベントは、カーネルモードのビデオキャプチャミニドライバーからユーザーモードの DirectShow に、ビデオキャプチャデバイスでトリガーボタンが押されたときなどのアクションを伝達します。

## <span id="ddk_ksevent_vidcaptosti_ext_trigger_ks"></span><span id="DDK_KSEVENT_VIDCAPTOSTI_EXT_TRIGGER_KS"></span>


### <a name="span-idusage_summary_tablespanspan-idusage_summary_tablespanusage-summary-table"></a><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用状況の概要テーブル

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th>[購入]</th>
<th>設定</th>
<th>対象</th>
<th>イベント記述子の種類</th>
<th>イベント値の種類</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>必須ではない</p></td>
<td><p>[はい]</p></td>
<td><p>Pin</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kse_node" data-raw-source="[&lt;strong&gt;KSE_NODE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kse_node)"><strong>KSE_NODE</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kseventdata" data-raw-source="[&lt;strong&gt;KSEVENTDATA&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kseventdata)"><strong>KSEVENTDATA</strong></a></p></td>
</tr>
</tbody>
</table>

 

DirectShow フィルターと Ksk プロキシの詳細については、「[カーネルストリーミングプロキシ](https://docs.microsoft.com/windows-hardware/drivers/ddi/_stream/index)」を参照してください。

 

 





