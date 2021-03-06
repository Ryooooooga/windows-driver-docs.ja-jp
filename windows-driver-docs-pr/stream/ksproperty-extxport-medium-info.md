---
title: KSK プロパティ\_EXTXPORT\_中\_情報
description: KSK プロパティ\_EXTXPORT\_MEDIUM\_INFO プロパティは、外部デバイスのメディアに関する情報を取得します。
ms.assetid: 04b98c50-ebb0-4224-b476-d261b7c5dd79
keywords:
- KSPROPERTY_EXTXPORT_MEDIUM_INFO ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_EXTXPORT_MEDIUM_INFO
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3466e28f22a9c3e3ebf749f7079efebfd0460c81
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838061"
---
# <a name="ksproperty_extxport_medium_info"></a>KSK プロパティ\_EXTXPORT\_中\_情報


KSK プロパティ\_EXTXPORT\_MEDIUM\_INFO プロパティは、外部デバイスのメディアに関する情報を取得します。

## <span id="ddk_ksproperty_extxport_medium_info_ks"></span><span id="DDK_KSPROPERTY_EXTXPORT_MEDIUM_INFO_KS"></span>


### <a name="usage-summary-table"></a>使用状況の概要テーブル

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
<th>プロパティ記述子の型</th>
<th>プロパティ値の型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>[はい]</p></td>
<td><p>必須ではない</p></td>
<td><p>デバイス</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_extxport_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_EXTXPORT_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_extxport_s)"><strong>KSPROPERTY_EXTXPORT_S</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-medium_info" data-raw-source="[&lt;strong&gt;MEDIUM_INFO&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-medium_info)"><strong>MEDIUM_INFO</strong></a></p></td>
</tr>
</tbody>
</table>

 

プロパティ値 (操作データ) は、外部デバイスに読み込まれるメディアを記述する中\_の情報構造です。 たとえば、カセットテープ、テープグレード、書き込み保護などです。

<a name="remarks"></a>注釈
-------

KSK プロパティ\_EXTXPORT\_S 構造体の**MediumInfo**メンバーは、情報を指定します。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Ksmedia .h (Ksk を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)

[**KSK プロパティ\_EXTXPORT\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_extxport_s)

[**中程度の\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-medium_info)

 

 






