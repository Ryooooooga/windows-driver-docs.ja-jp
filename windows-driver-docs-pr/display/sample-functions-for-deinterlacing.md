---
title: デインターレースのサンプル関数
description: デインターレースのサンプル関数
ms.assetid: a91c0267-7a3e-4206-8680-6e87778a329d
keywords:
- デインター レースの WDK DirectX va なので、サンプル関数
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 385cae818c80ccfbb938ce4e13f7ffaaf9091ed6
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67365615"
---
# <a name="sample-functions-for-deinterlacing"></a>デインターレースのサンプル関数


## <span id="ddk_sample_functions_for_deinterlacing_gg"></span><span id="DDK_SAMPLE_FUNCTIONS_FOR_DEINTERLACING_GG"></span>


このセクションのサンプル デインター レース関数は、デインター レース、フレーム レートの変換機能を実装する方法を示します。 サンプル関数にマップ、[補正コールバック関数のモーション](motion-compensation-callbacks.md)で定義されている、 [ **DD\_MOTIONCOMPCALLBACKS** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-dd_motioncompcallbacks)構造体。 各サンプル関数を実装し、実装の完成に動き補正コード テンプレートを使用できます。 詳細については、次を参照してください。 [DirectX VA デバイス用のコード例](example-code-for-directx-va-devices.md)します。

### <a name="span-iddeinterlacecontainerdeviceclasssamplefunctionsspanspan-iddeinterlacecontainerdeviceclasssamplefunctionsspanspan-iddeinterlacecontainerdeviceclasssamplefunctionsspandeinterlace-container-device-class-sample-functions"></a><span id="Deinterlace_Container_Device_Class_Sample_Functions"></span><span id="deinterlace_container_device_class_sample_functions"></span><span id="DEINTERLACE_CONTAINER_DEVICE_CLASS_SAMPLE_FUNCTIONS"></span>コンテナーのデバイス クラスのサンプル関数のインター レースを解除します。

次の表にサンプルのインター レース解除関数は、メンバー関数の*DXVA\_DeinterlaceContainerDeviceClass* (つまり、それらと呼ばれるインター コンテナーのデバイスを使用して)。 詳細については、次を参照してください。[インター レースを解除するコンテナー デバイス クラスを定義する](defining-the-deinterlace-container-device-class.md)と[ProcAmp コントロールを実行すると操作のデインター レース](performing-procamp-control-and-deinterlacing-operations.md)します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">メンバー関数</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/display/dxva-deinterlacecontainerdeviceclass-deinterlacequeryavailablemodes" data-raw-source="[&lt;strong&gt;DeinterlaceQueryAvailableModes&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/display/dxva-deinterlacecontainerdeviceclass-deinterlacequeryavailablemodes)"><strong>DeinterlaceQueryAvailableModes</strong></a></p></td>
<td align="left"><p>使用可能なデインター レース、フレーム レートの変換モードを照会します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/display/dxva-deinterlacecontainerdeviceclass-deinterlacequerymodecaps" data-raw-source="[&lt;strong&gt;DeinterlaceQueryModeCaps&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/display/dxva-deinterlacecontainerdeviceclass-deinterlacequerymodecaps)"><strong>DeinterlaceQueryModeCaps</strong></a></p></td>
<td align="left"><p>デインター レース、フレーム レートの変換モードを特定の機能を照会します。</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-iddeinterlacebobdeviceclasssamplefunctionsspanspan-iddeinterlacebobdeviceclasssamplefunctionsspanspan-iddeinterlacebobdeviceclasssamplefunctionsspandeinterlace-bob-device-class-sample-functions"></a><span id="Deinterlace_Bob_Device_Class_Sample_Functions"></span><span id="deinterlace_bob_device_class_sample_functions"></span><span id="DEINTERLACE_BOB_DEVICE_CLASS_SAMPLE_FUNCTIONS"></span>Bob のデバイス クラスのサンプル関数のインター レースを解除します。

次の表にサンプルのインター レース解除関数は、メンバー関数の*DXVA\_DeinterlaceBobDeviceClass* (つまり、それらと呼ばれるインター bob のデバイスを使用して)。 詳細については、次を参照してください。[インター レースを解除する Bob デバイス クラスを定義する](defining-the-deinterlace-bob-device-class.md)します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">メンバー関数</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/display/dxva-deinterlacebobdeviceclass-deinterlaceopenstream" data-raw-source="[&lt;strong&gt;DeinterlaceOpenStream&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/display/dxva-deinterlacebobdeviceclass-deinterlaceopenstream)"><strong>DeinterlaceOpenStream</strong></a></p></td>
<td align="left"><p>ビデオ ストリーム オブジェクトを開きます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/display/dxva-deinterlacebobdeviceclass-deinterlaceblt" data-raw-source="[&lt;strong&gt;DeinterlaceBlt&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/display/dxva-deinterlacebobdeviceclass-deinterlaceblt)"><strong>DeinterlaceBlt</strong></a></p></td>
<td align="left"><p>ビデオ ストリーム オブジェクトのビット ブロックがデインター レースを提供します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/display/dxva-deinterlacebobdeviceclass-deinterlacebltex" data-raw-source="[&lt;strong&gt;DeinterlaceBltEx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/display/dxva-deinterlacebobdeviceclass-deinterlacebltex)"><strong>DeinterlaceBltEx</strong></a></p></td>
<td align="left"><p><strong>Windows Server 2003 SP1 以降および Windows XP SP2 以降のみです。</strong></p>
<div>
 
</div>
ビデオ、およびコンポジット ビデオ サブストリーム ビデオ ストリームの上にインター レースを解除します。</td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/display/dxva-deinterlacebobdeviceclass-deinterlaceclosestream" data-raw-source="[&lt;strong&gt;DeinterlaceCloseStream&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/display/dxva-deinterlacebobdeviceclass-deinterlaceclosestream)"><strong>DeinterlaceCloseStream</strong></a></p></td>
<td align="left"><p>ビデオ ストリーム オブジェクトを閉じます。</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idmappingsamplefunctionstoddmotioncompcallbacksspanspan-idmappingsamplefunctionstoddmotioncompcallbacksspanspan-idmappingsamplefunctionstoddmotioncompcallbacksspanmapping-sample-functions-to-ddmotioncompcallbacks"></a><span id="Mapping_Sample_Functions_to_DD_MOTIONCOMPCALLBACKS"></span><span id="mapping_sample_functions_to_dd_motioncompcallbacks"></span><span id="MAPPING_SAMPLE_FUNCTIONS_TO_DD_MOTIONCOMPCALLBACKS"></span>DD にサンプル関数のマップ\_MOTIONCOMPCALLBACKS

このセクションのサンプル関数は、次の表に示すように、モーション補正のコールバック関数にマップします。 つまり、各関数のサンプルは、それぞれの動き補正コールバック内で呼び出されます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">関数</th>
<th align="left">DD_MOTIONCOMPCALLBACKS メンバー</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/display/dxva-deinterlacecontainerdeviceclass-deinterlacequeryavailablemodes" data-raw-source="[&lt;strong&gt;DeinterlaceQueryAvailableModes&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/display/dxva-deinterlacecontainerdeviceclass-deinterlacequeryavailablemodes)"><strong>DeinterlaceQueryAvailableModes</strong></a></p></td>
<td align="left"><p><strong>RenderMoComp</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/display/dxva-deinterlacecontainerdeviceclass-deinterlacequerymodecaps" data-raw-source="[&lt;strong&gt;DeinterlaceQueryModeCaps&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/display/dxva-deinterlacecontainerdeviceclass-deinterlacequerymodecaps)"><strong>DeinterlaceQueryModeCaps</strong></a></p></td>
<td align="left"><p><strong>RenderMoComp</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/display/dxva-deinterlacebobdeviceclass-deinterlaceopenstream" data-raw-source="[&lt;strong&gt;DeinterlaceOpenStream&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/display/dxva-deinterlacebobdeviceclass-deinterlaceopenstream)"><strong>DeinterlaceOpenStream</strong></a></p></td>
<td align="left"><p><strong>CreateMoComp</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/display/dxva-deinterlacebobdeviceclass-deinterlaceblt" data-raw-source="[&lt;strong&gt;DeinterlaceBlt&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/display/dxva-deinterlacebobdeviceclass-deinterlaceblt)"><strong>DeinterlaceBlt</strong></a></p></td>
<td align="left"><p><strong>RenderMoComp</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/display/dxva-deinterlacebobdeviceclass-deinterlacebltex" data-raw-source="[&lt;strong&gt;DeinterlaceBltEx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/display/dxva-deinterlacebobdeviceclass-deinterlacebltex)"><strong>DeinterlaceBltEx</strong></a></p></td>
<td align="left"><p><strong>RenderMoComp</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/display/dxva-deinterlacebobdeviceclass-deinterlaceclosestream" data-raw-source="[&lt;strong&gt;DeinterlaceCloseStream&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/display/dxva-deinterlacebobdeviceclass-deinterlaceclosestream)"><strong>DeinterlaceCloseStream</strong></a></p></td>
<td align="left"><p><strong>DestroyMoComp</strong></p></td>
</tr>
</tbody>
</table>

 

 

 





