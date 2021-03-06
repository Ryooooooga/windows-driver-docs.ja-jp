---
title: KSK プロパティ\_ストリームの\_品質
description: KSK プロパティ\_STREAM\_QUALITY プロパティは、品質管理の不満を生成する場合に実装する必要があるオプションのプロパティです。
ms.assetid: ed4d9baa-967a-41b3-b8b9-910b86230254
keywords:
- KSPROPERTY_STREAM_QUALITY ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_STREAM_QUALITY
api_location:
- ks.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5eb4a077c67c2325bc90ec33163fda86ff9850fa
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837943"
---
# <a name="ksproperty_stream_quality"></a>KSK プロパティ\_ストリームの\_品質


KSK プロパティ\_STREAM\_QUALITY プロパティは、品質管理の不満を生成する場合に実装する必要があるオプションのプロパティです。

## <span id="ddk_ksproperty_stream_quality_ks"></span><span id="DDK_KSPROPERTY_STREAM_QUALITY_KS"></span>


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
<td><p>必須ではない</p></td>
<td><p>[はい]</p></td>
<td><p>Pin</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksquality_manager" data-raw-source="[&lt;strong&gt;KSQUALITY_MANAGER&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksquality_manager)"><strong>KSQUALITY_MANAGER</strong></a></p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

この要求が行われると、ピン接続によって、指定されたコンテキストパラメーターを使用して[**Ksk 品質**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksquality)構造が提供され、品質マネージャーに通知されます。

Pin が品質の問題を報告しない場合は、ストリームの\_品質に\_KSK プロパティをサポートする必要はありません。

「[品質管理](https://docs.microsoft.com/windows-hardware/drivers/stream/quality-management)」も参照してください。

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
<td>Ks (Ks を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)

[**KSQUALITY\_MANAGER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksquality_manager)

[**KSK 品質**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksquality)

 

 






