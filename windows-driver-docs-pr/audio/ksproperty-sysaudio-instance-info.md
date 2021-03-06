---
title: KSK プロパティ\_SYSAUDIO\_インスタンス\_情報
description: KSK プロパティ\_SYSAUDIO\_INSTANCE\_INFO プロパティによって、仮想オーディオデバイスが開き、そのデバイスの構成フラグが指定されます。
ms.assetid: ef60c188-704f-4dbb-bf6d-cdf3152c209b
keywords:
- KSPROPERTY_SYSAUDIO_INSTANCE_INFO オーディオデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_SYSAUDIO_INSTANCE_INFO
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2394f3cfcf648967cc2bee7c6ec122b7e4716cbd
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72830485"
---
# <a name="ksproperty_sysaudio_instance_info"></a>KSK プロパティ\_SYSAUDIO\_インスタンス\_情報


KSK プロパティ\_SYSAUDIO\_INSTANCE\_INFO プロパティによって、仮想オーディオデバイスが開き、そのデバイスの構成フラグが指定されます。

## <span id="ddk_ksproperty_sysaudio_instance_info_ks"></span><span id="DDK_KSPROPERTY_SYSAUDIO_INSTANCE_INFO_KS"></span>


### <a name="span-idusage_summary_tablespanspan-idusage_summary_tablespanspan-idusage_summary_tablespanusage-summary-table"></a><span id="Usage_Summary_Table"></span><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用状況の概要テーブル

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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-sysaudio_instance_info" data-raw-source="[&lt;strong&gt;SYSAUDIO_INSTANCE_INFO&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-sysaudio_instance_info)"><strong>SYSAUDIO_INSTANCE_INFO</strong></a></p></td>
<td align="left"><p>なし</p></td>
</tr>
</tbody>
</table>

 

プロパティ記述子 (インスタンスデータ) は、オープンする仮想オーディオデバイスを指定する SYSAUDIO\_インスタンス\_INFO 型の構造体であり、そのデバイスの構成フラグも指定します。

プロパティ値 (操作データ) がこのプロパティに対して定義されていません。 プロパティ値のポインターを**NULL**として指定し、プロパティ値のサイズを0として指定します。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSK プロパティ\_SYSAUDIO\_インスタンス\_INFO プロパティ要求は、正常に完了したことを示すステータス\_成功を返します。 それ以外の場合、要求は適切なエラー状態コードを返します。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">Ksmedia .h (Ksk を含む)</td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[**SYSAUDIO\_インスタンス\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-sysaudio_instance_info)

 

 






