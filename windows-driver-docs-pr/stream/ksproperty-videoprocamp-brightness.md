---
title: KSK プロパティ\_VIDEOPROCAMP\_輝度
description: KSK プロパティ\_VIDEOPROCAMP\_輝度プロパティは、明るさの設定を制御します。 このプロパティは省略可能です。
ms.assetid: 8b099ff1-e64a-4723-9834-8a42450bebd4
keywords:
- KSPROPERTY_VIDEOPROCAMP_BRIGHTNESS ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_VIDEOPROCAMP_BRIGHTNESS
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2065eea045993ffb160142c9f0753f9ba0a89561
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844809"
---
# <a name="ksproperty_videoprocamp_brightness"></a>KSK プロパティ\_VIDEOPROCAMP\_輝度


KSK プロパティ\_VIDEOPROCAMP\_輝度プロパティは、明るさの設定を制御します。 このプロパティは省略可能です。

## <span id="ddk_ksproperty_videoprocamp_brightness_ks"></span><span id="DDK_KSPROPERTY_VIDEOPROCAMP_BRIGHTNESS_KS"></span>


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
<td><p>[はい]</p></td>
<td><p>フィルターまたはノード</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videoprocamp_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEOPROCAMP_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videoprocamp_s)"><strong>KSPROPERTY_VIDEOPROCAMP_S</strong></a>または<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videoprocamp_node_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEOPROCAMP_NODE_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videoprocamp_node_s)"> <strong>KSPROPERTY_VIDEOPROCAMP_NODE_S</strong></a></p></td>
<td><p>長い</p></td>
</tr>
</tbody>
</table>

 

プロパティ値 (操作データ) は、カメラの明るさの設定を指定する LONG です。 この値は、NTSC ソースの場合、IRE 単位で100を乗算した値になります。 NTSC 以外のソースの場合、単位は任意であり、0は、純粋な白を表す、ブランキングと1万を表します。

<a name="remarks"></a>注釈
-------

VIDEOPROCAMP\_S 構造体\_KSK プロパティの**値**メンバーは、明るさを指定します。

明るさは、黒のレベルとも呼ばれます。 明るさの設定を変更すると、すべての明るさの値についてビデオ信号全体が均等に移動します。

すべてのビデオキャプチャミニドライバーで、このプロパティの範囲と既定値を定義する必要があります。 必要な範囲は、-1万 ~ + 1万である必要があります。 既定値は 750 (7.5 IRE) である必要があります。

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

[**KSK プロパティ\_VIDEOPROCAMP\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videoprocamp_s)

 

 






