---
title: KSK プロパティ\_SOUNDDETECTOR\_
description: "\"取り組ま\" プロパティ\\_には、\"\" プロパティ\\_\"武装\" プロパティは、検出の現在の状態を示します。"
ms.assetid: 3B9B43C0-31EE-4490-AD29-98DA81D1664F
keywords:
- KSPROPERTY_SOUNDDETECTOR_ARMED オーディオデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_SOUNDDETECTOR_ARMED
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 09/26/2019
ms.localizationpriority: medium
ms.openlocfilehash: 9e3f22ad31dc11c235343f1d63acea132b32dbb3
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72830587"
---
# <a name="ksproperty_sounddetector_armed"></a>KSK プロパティ\_SOUNDDETECTOR\_


"取り組ま" プロパティ\_には、"" プロパティ **\_"武装**" プロパティは、検出の現在の状態を示します。

### <a name="span-idusage_summary_tablespanspan-idusage_summary_tablespanspan-idusage_summary_tablespanusage-summary-table---kspropsetid_sounddetector"></a><span id="Usage_Summary_Table"></span><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用状況の概要テーブル-KSPROPSETID_SoundDetector

この使用状況テーブルでは、 [KSPROPSETID_SoundDetector](kspropsetid-sounddetector.md)を使用して\_\_の KSPROPERTY に sounddetector 器が呼び出されるタイミングをまとめます。

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
<th align="left">[購入]</th>
<th align="left">設定</th>
<th align="left">対象</th>
<th align="left">プロパティ記述子の型</th>
<th align="left">プロパティ値の型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>[はい]</p></td>
<td align="left"><p>[はい]</p></td>
<td align="left"><p>フィルター</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/ff564262(v=vs.85)" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/ff564262(v=vs.85))"><strong>KSPROPERTY</strong></a></p></td>
<td align="left"><p>型</p></td>
</tr>
</tbody>
</table>

[KSPROPSETID_SoundDetector](kspropsetid-sounddetector.md)によって呼び出された場合、ドライバーは次の場合にこの値を false にリセットします。

-   フィルターインターフェイスが無効になっています。
-   [ **\_SOUNDDETECTOR\_PATTERNS**](ksproperty-sounddetector-patterns.md)プロパティが設定されています。
-   キーワードが検出されました。


### <a name="span-idusage_summary_tablespanspan-idusage_summary_tablespanspan-idusage_summary_tablespanusage-summary-table---kspropsetid_sounddetector2"></a><span id="Usage_Summary_Table"></span><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用状況の概要テーブル-KSPROPSETID_SoundDetector2


この使用状況テーブルでは、 [KSPROPSETID_SoundDetector2](kspropsetid-sounddetector2.md)を使用して\_\_の KSPROPERTY に sounddetector 器が呼び出されるタイミングをまとめます。

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
<th align="left">[購入]</th>
<th align="left">設定</th>
<th align="left">対象</th>
<th align="left">プロパティ記述子の型</th>
<th align="left">プロパティ値の型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>[はい]</p></td>
<td align="left"><p>[はい]</p></td>
<td align="left"><p>フィルター</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-kssounddetectorproperty" data-raw-source="[&lt;strong&gt;KSSOUNDDETECTORPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-kssounddetectorproperty"><strong>KSSOUNDDETECTORPROPERTY</strong></a></p></td>
<td align="left"><p>型</p></td>
</tr>
</tbody>
</table>

[KSPROPSETID_SoundDetector2](kspropsetid-sounddetector2.md)で呼び出された場合、キーワードが検出されても arm 状態はリセットされません。

次の場合は false にリセットされます。
- フィルターインターフェイスが無効になっています。
- [**Ksproperty\_SOUNDDETECTOR\_PATTERNS**](ksproperty-sounddetector-patterns.md)プロパティが設定されています


### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

プロパティ値は、検出機能の取り組ま状態を示すブール値です。

<a name="remarks"></a>注釈
-------

OS は、検出機能を利用するためにこの true を設定します。

キーワードパターンが設定されていないときにこの true を設定した場合 ([**Ksk プロパティ\_SOUNDDETECTOR\_パターン**](ksproperty-sounddetector-patterns.md)が空の場合)、効果はありません。

注: このプロパティが true の場合、次に[**ksk\_プロパティ**](ksproperty-sounddetector-patterns.md)を設定すると、前に説明したように、\_パターンによってこの値が自動的に false にリセットされます。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>サポートされている最小のクライアント</p></td>
<td align="left"><p>Windows 10</p></td>
</tr>
<tr class="even">
<td align="left"><p>サポートされている最小のサーバー</p></td>
<td align="left"><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">Ksmedia.h</td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目

[**KSK プロパティ\_SOUNDDETECTOR\_パターン**](ksproperty-sounddetector-patterns.md)

[**KSPROPERTY**](https://docs.microsoft.com/previous-versions/ff564262(v=vs.85))

[**KSSOUNDDETECTORPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-kssounddetectorproperty)
