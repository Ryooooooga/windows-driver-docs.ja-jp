---
title: ビデオ コンテンツのインターとフレーム レートの変換
description: ビデオ コンテンツのインターとフレーム レートの変換
ms.assetid: 627b394e-c2e1-4327-adaa-0c3436ba3d1a
keywords:
- WDK DirectX VA デインター レース、ビデオ コンテンツを受信しました
- フレーム レート変換 WDK DirectX VA
- ビデオ コンテンツ WDK DirectX VA を受け取りました。
- WDK DirectX VA デインター レースのビデオ コンテンツ
- フレーム レート変換 WDK DirectX VA のビデオ コンテンツ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7bd9bbf34e0176d2f8fc38e42b1f32fd7b7b3ba6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56552734"
---
# <a name="video-content-for-deinterlace-and-frame-rate-conversion"></a>ビデオ コンテンツのインターとフレーム レートの変換


## <span id="ddk_video_content_for_deinterlace_and_frame_rate_conversion_gg"></span><span id="DDK_VIDEO_CONTENT_FOR_DEINTERLACE_AND_FRAME_RATE_CONVERSION_GG"></span>


ドライバーは、それがどのようにノンインター レース化かを判断できますか、フレーム レートは、このようなコンテンツを変換できるように、ビデオ コンテンツの説明を受け取ります。 ドライバーでは、このビデオの内容を受け取るへのポインターとして、 [ **DXVA\_VideoDesc** ](https://msdn.microsoft.com/library/windows/hardware/ff564070)次の関数呼び出しで構造体。

-   [**DeinterlaceQueryAvailableModes**](https://msdn.microsoft.com/library/windows/hardware/ff563943)

-   [**DeinterlaceQueryModeCaps**](https://msdn.microsoft.com/library/windows/hardware/ff563946)

-   [**DeinterlaceOpenStream**](https://msdn.microsoft.com/library/windows/hardware/ff563935)

次の例では、ドライバーが受信したビデオ コンテンツのデインター レース、フレーム レートの変換を実行する方法を示しています。

### <a name="span-iddeinterlacing720x480icontentexamplespanspan-iddeinterlacing720x480icontentexamplespanspan-iddeinterlacing720x480icontentexamplespandeinterlacing-720-x-480i-content-example"></a><span id="Deinterlacing_720_x_480i_Content_Example"></span><span id="deinterlacing_720_x_480i_content_example"></span><span id="DEINTERLACING_720_X_480I_CONTENT_EXAMPLE"></span>デインター レース x 720 480i コンテンツの例

DXVA\_29.97 Hz の頻度でサンプルごとの 2 つのフィールドとしてに属している x 720 480i コンテンツをインター レース解除するドライバーに出力するため VideoDesc 構造は次のように入力されます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">メンバー</th>
<th align="left">Value</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>SampleWidth</strong></p></td>
<td align="left"><p>720</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>SampleHeight</strong></p></td>
<td align="left"><p>480</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>SampleFormat</strong></p></td>
<td align="left"><p><strong>DXVA_SampleFieldInterleavedOddFirst</strong>で列挙子<a href="https://msdn.microsoft.com/library/windows/hardware/ff564045" data-raw-source="[&lt;strong&gt;DXVA_SampleFormat&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564045)"> <strong>DXVA_SampleFormat</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>d3dFormat</strong></p></td>
<td align="left"><p>定義されている D3DFMT_YUY2、 <em>d3d8types.h</em>と<em>d3d9types.h</em>ヘッダー ファイル</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>InputSampleFreq.Numerator</strong></p></td>
<td align="left"><p>30000 (29.97 Hz モニター頻度)</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>InputSampleFreq.Denominator</strong></p></td>
<td align="left"><p>1001</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>OutputFrameFreq.Numerator</strong></p></td>
<td align="left"><p>60000 (59.94 Hz モニター頻度)</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>OutputFrameFreq.Denominator</strong></p></td>
<td align="left"><p>1001</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-iddeinterlacingandframe-rateconversionof720x480icontentexamplespanspan-iddeinterlacingandframe-rateconversionof720x480icontentexamplespanspan-iddeinterlacingandframe-rateconversionof720x480icontentexamplespandeinterlacing-and-frame-rate-conversion-of-720-x-480i-content-example"></a><span id="Deinterlacing_and_Frame-Rate_Conversion_of_720_x_480i_Content_Example"></span><span id="deinterlacing_and_frame-rate_conversion_of_720_x_480i_content_example"></span><span id="DEINTERLACING_AND_FRAME-RATE_CONVERSION_OF_720_X_480I_CONTENT_EXAMPLE"></span>デインター レース、720 x 480i コンテンツの例のフレーム レートの変換

**OutputFrameFreq**メンバーは、DXVA の\_720 x 480i コンテンツのインター レース解除するドライバーとフレーム レート変換に出力するため VideoDesc 構造は次のように入力されます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">メンバー</th>
<th align="left">Value</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>OutputFrameFreq.Numerator</strong></p></td>
<td align="left"><p>85 (85 Hz モニター頻度)</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>OutputFrameFreq.Denominator</strong></p></td>
<td align="left"><p>1</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-iddeinterlacingasinglefieldtoaprogressiveframeexamplespanspan-iddeinterlacingasinglefieldtoaprogressiveframeexamplespanspan-iddeinterlacingasinglefieldtoaprogressiveframeexamplespandeinterlacing-a-single-field-to-a-progressive-frame-example"></a><span id="Deinterlacing_a_Single_Field_to_a_Progressive_Frame_Example"></span><span id="deinterlacing_a_single_field_to_a_progressive_frame_example"></span><span id="DEINTERLACING_A_SINGLE_FIELD_TO_A_PROGRESSIVE_FRAME_EXAMPLE"></span>プログレッシブ フレームの例の 1 つのフィールドをデインター レース

**OutputFrameFreq**メンバーは、DXVA の\_以降 MPEG エンコード プログレッシブのフレームに 1 つのフィールドをインター レース解除するドライバーに出力するため VideoDesc 構造は次のように入力されます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">メンバー</th>
<th align="left">Value</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>OutputFrameFreq.Numerator</strong></p></td>
<td align="left"><p>30000 (29.97 Hz モニター頻度)</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>OutputFrameFreq.Denominator</strong></p></td>
<td align="left"><p>1001</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idframe-rateconversionof480pcontentexamplespanspan-idframe-rateconversionof480pcontentexamplespanspan-idframe-rateconversionof480pcontentexamplespanframe-rate-conversion-of-480p-content-example"></a><span id="Frame-Rate_Conversion_of__480p_Content_Example"></span><span id="frame-rate_conversion_of__480p_content_example"></span><span id="FRAME-RATE_CONVERSION_OF__480P_CONTENT_EXAMPLE"></span>480 p コンテンツの例のフレーム レートの変換

DXVA\_480 p コンテンツのフレーム レートの変換を実行して、モニターの一致するように、ドライバーに出力するため次のように表示頻度として VideoDesc 構造が入力されます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">メンバー</th>
<th align="left">Value</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>SampleWidth</strong></p></td>
<td align="left"><p>720</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>SampleHeight</strong></p></td>
<td align="left"><p>480</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>SampleFormat</strong></p></td>
<td align="left"><p><strong>DXVA_SampleProgressiveFrame</strong>で列挙子、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff564045" data-raw-source="[&lt;strong&gt;DXVA_SampleFormat&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564045)"> <strong>DXVA_SampleFormat</strong> </a>列挙型</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>d3dFormat</strong></p></td>
<td align="left"><p>D3DFMT_YUY2 d3d8types.h と d3d9types.h ヘッダー ファイルで定義されています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>InputSampleFreq.Numerator</strong></p></td>
<td align="left"><p>60 (60 Hz モニター頻度)</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>InputSampleFreq.Denominator</strong></p></td>
<td align="left"><p>1</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>OutputFrameFreq.Numerator</strong></p></td>
<td align="left"><p>85 (85 Hz モニター頻度)</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>OutputFrameFreq.Denominator</strong></p></td>
<td align="left"><p>1</p></td>
</tr>
</tbody>
</table>

 

 

 




