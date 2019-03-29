---
title: KSPROPERTY\_CAMERACONTROL\_PANTILT
description: KSPROPERTY\_CAMERACONTROL\_PANTILT プロパティを絶対指定方向へパンして、傾きの設定。
ms.assetid: d6f151c9-a428-4d76-9854-5064d901643e
keywords:
- KSPROPERTY_CAMERACONTROL_PANTILT ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_CAMERACONTROL_PANTILT
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: fe1fa9526e25ac23f8c3df2dea5d6d7b7535d053
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574779"
---
# <a name="kspropertycameracontrolpantilt"></a>KSPROPERTY\_CAMERACONTROL\_PANTILT


KSPROPERTY\_CAMERACONTROL\_PANTILT プロパティを絶対指定方向へパンして、傾きの設定。

## <span id="ddk_ksproperty_cameracontrol_pantilt_ks"></span><span id="DDK_KSPROPERTY_CAMERACONTROL_PANTILT_KS"></span>


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
<th>取得</th>
<th>Set</th>
<th>移行先</th>
<th>プロパティ記述子の型</th>
<th>プロパティ値の型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>はい</p></td>
<td><p>はい</p></td>
<td><p>フィルターまたはノード</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564451" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_S2&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564451)"><strong>KSPROPERTY_CAMERACONTROL_S2</strong> </a>または<a href="https://msdn.microsoft.com/library/windows/hardware/ff564421" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_NODE_S2&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564421)"> <strong>KSPROPERTY_CAMERACONTROL_NODE_S2</strong> </a>要求をフィルターまたはノードがあるかによって</p></td>
<td><p>長整数のペア</p></td>
</tr>
</tbody>
</table>

 

プロパティの値 (データの操作) は、カメラの絶対パンを指定する設定を傾ける長整数のペアです。 これらの値は、円弧を秒単位で表現されます。

1 つの円弧は、2 つ目はある程度には、1/3600 です。 許容値の範囲 −180 から\*+180 に 3600\*円弧の 3600 秒です。 パンまたは傾きの値が指定されていない場合、既定値は 0 です。

パンの要求を行うときに、右にカメラの回転し、負の値を左にカメラの回転を指定する正の値を指定します。

正の値が、カメラを傾けます傾き要求を行うときに、負の値をカメラを傾けます。

<a name="remarks"></a>コメント
-------

**Value1**のメンバー、 [ **KSPROPERTY\_CAMERACONTROL\_S2** ](https://msdn.microsoft.com/library/windows/hardware/ff564451)または[ **KSPROPERTY\_CAMERACONTROL\_ノード\_S2** ](https://msdn.microsoft.com/library/windows/hardware/ff564421)構造体をパン設定を指定します。 **Value2**メンバー傾きの設定を指定します。

<a name="requirements"></a>必要条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>バージョン</p></td>
<td><p>Windows Vista および Windows オペレーティング システムの以降のバージョンで使用できます。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ksmedia.h (Ksmedia.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**KSPROPERTY\_CAMERACONTROL\_S2**](https://msdn.microsoft.com/library/windows/hardware/ff564451)

[**KSPROPERTY\_CAMERACONTROL\_ノード\_S2**](https://msdn.microsoft.com/library/windows/hardware/ff564421)

 

 





