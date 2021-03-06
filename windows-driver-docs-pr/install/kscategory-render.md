---
title: KSCATEGORY_RENDER
description: KSCATEGORY_RENDER
ms.assetid: 467e3192-46c4-4ef4-88cf-0a870efc1725
keywords:
- KSCATEGORY_RENDER デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- KSCATEGORY_RENDER
api_location:
- Ks.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: b16972d6c10d39e5b7e51f6b76edc2d5066bdf6d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67366714"
---
# <a name="kscategoryrender"></a>KSCATEGORY_RENDER


KSCATEGORY_RENDER[デバイス インターフェイス クラス](https://docs.microsoft.com/windows-hardware/drivers/install/device-interface-classes)が定義されている、[カーネル ストリーミング](https://docs.microsoft.com/windows-hardware/drivers/stream/streaming-minidrivers2)wave と MIDI データ ストリームを表示します (KS) 機能のカテゴリ。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">属性</th>
<th align="left">設定</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>識別子</p></td>
<td align="left"><p>KSCATEGORY_RENDER</p></td>
</tr>
<tr class="even">
<td align="left"><p>クラス GUID</p></td>
<td align="left"><p>{65E8773E-8F56-11D0-A3B9-00A0C9223196}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

KS オーディオ アダプター デバイス用のドライバーでは、デバイスが KSCATEGORY_RENDER 機能カテゴリをサポートすることを示す KSCATEGORY_RENDER のインスタンスを登録します。

INF ファイルでこの機能のカテゴリを登録する方法については、INF ファイルを参照してください。 *Ac97smpl.inf*に含まれる、 [AC'97 サンプル ドライバー](https://go.microsoft.com/fwlink/p/?linkid=256075) WDK に含まれています。

オーディオのアダプターのインターフェイス クラスのデバイスについては、次を参照してください。[オーディオのアダプターのデバイスのインターフェイスをインストールする](https://docs.microsoft.com/windows-hardware/drivers/audio/installing-device-interfaces-for-an-audio-adapter)と[ **KSPROPERTY_TOPOLOGY_CATEGORIES**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-topology-categories)します。

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
<td align="left">Ks.h (Ks.h を含む)</td>
</tr>
</tbody>
</table>

 

 





