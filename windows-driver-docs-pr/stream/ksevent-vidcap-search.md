---
title: KSEVENT\_VIDCAP\_検索
description: 検索が完了すると、KSEVENT\_VIDCAP\_AUTO\_UPDATE イベントがトリガーされます。
ms.assetid: 07c7ef26-4f88-40cf-84f2-14cc702f37d5
keywords:
- KSEVENT_VIDCAP_SEARCH ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSEVENT_VIDCAP_SEARCH
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: f851fad3c8f03c0d98649610d55572a5b7c93b8b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843673"
---
# <a name="ksevent_vidcap_search"></a>KSEVENT\_VIDCAP\_検索


検索が完了すると、KSEVENT\_VIDCAP\_AUTO\_UPDATE イベントがトリガーされます。

## <span id="ddk_ksevent_vidcap_search_ks"></span><span id="DDK_KSEVENT_VIDCAP_SEARCH_KS"></span>


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
<td><p>フィルター</p></td>
<td><p><a href="https://docs.microsoft.com/previous-versions/ff561744(v=vs.85)" data-raw-source="[&lt;strong&gt;KSEVENT&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/ff561744(v=vs.85))"><strong>KSEVENT</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kseventdata" data-raw-source="[&lt;strong&gt;KSEVENTDATA&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kseventdata)"><strong>KSEVENTDATA</strong></a></p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

クライアントは、特定のトラックを検索するときに、たとえば、検索が完了したことを通知するために、このイベントに登録できます。

DirectShow フィルターと Ksk プロキシの詳細については、「[カーネルストリーミングプロキシ](https://docs.microsoft.com/windows-hardware/drivers/ddi/_stream/index)」を参照してください。

 

 





