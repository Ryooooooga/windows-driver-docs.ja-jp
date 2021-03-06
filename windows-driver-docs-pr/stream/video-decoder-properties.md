---
title: ビデオ デコーダーのプロパティ
description: ビデオ デコーダーのプロパティ
ms.assetid: 671a310b-52a6-49f0-8848-e586a37c25ff
keywords:
- ビデオ デコーダー プロパティ WDK ビデオのキャプチャします。
- デコーダーの WDK ビデオのプロパティをキャプチャします。
- PROPSETID_VIDCAP_VIDEODECODER
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 488c8668d3287f452a7aa789cc0450fb101a58be
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385369"
---
# <a name="video-decoder-properties"></a>ビデオ デコーダーのプロパティ


[PROPSETID\_しました\_VIDEODECODER](https://docs.microsoft.com/windows-hardware/drivers/stream/propsetid-vidcap-videodecoder)プロパティ セットには、標準や時間の送信通知などのアナログ ビデオ デコーダーのデバイスの操作に関連するプロパティが含まれます。 次の表に、プロパティ、PROPSETID の一部である\_しました\_VIDEODECODER プロパティ セット。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>PROPSETID_VIDCAP_VIDEODECODER KS プロパティ</th>
<th>プロパティの説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-videodecoder-caps" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEODECODER_CAPS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-videodecoder-caps)"><strong>KSPROPERTY_VIDEODECODER_CAPS</strong></a></p></td>
<td><p>時間のうちは落ち着かないのビデオ デコーダーなどのデバイス標準信号 (NTSC、PAL、SECAM) の機能情報を返します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-videodecoder-standard" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEODECODER_STANDARD&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-videodecoder-standard)"><strong>KSPROPERTY_VIDEODECODER_STANDARD</strong></a></p></td>
<td><p>現在のアナログ ビデオ標準を制御します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-videodecoder-status" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEODECODER_STATUS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-videodecoder-status)"><strong>KSPROPERTY_VIDEODECODER_STATUS</strong></a></p></td>
<td><p>ビデオのビデオ信号内の行の数などのデバイスと、シグナルがロックされているかどうかをデコードの状態を返します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-videodecoder-output-enable" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEODECODER_OUTPUT_ENABLE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-videodecoder-output-enable)"><strong>KSPROPERTY_VIDEODECODER_OUTPUT_ENABLE</strong></a></p></td>
<td><p>ビデオのデコーダーの 3 つの状態の出力を制御します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-videodecoder-vcr-timing" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEODECODER_VCR_TIMING&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-videodecoder-vcr-timing)"><strong>KSPROPERTY_VIDEODECODER_VCR_TIMING</strong></a></p></td>
<td><p>ビデオ デコーダーが VCR のタイミングまたはブロードキャストのタイミングを使用するかどうかを制御します。</p></td>
</tr>
</tbody>
</table>

 

 

 




