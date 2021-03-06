---
title: ディスプレイ ドライバーの必須関数
description: ディスプレイ ドライバーの必須関数
ms.assetid: 7c1489c9-40de-4b44-95b7-af227c7d8205
keywords:
- グラフィックス DDI 関数 WDK Windows 2000 を表示します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7325a3c8cd6cc651edea8e20e2b0474d06620ec5
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67375030"
---
# <a name="optional-display-driver-functions"></a>ディスプレイ ドライバーの必須関数


## <span id="ddk_optional_display_driver_functions_gg"></span><span id="DDK_OPTIONAL_DISPLAY_DRIVER_FUNCTIONS_GG"></span>


ドライバーのサイズを軽減するためにディスプレイ ドライバー開発者は通常、ビデオ ハードウェアでサポートされるも省略可能な関数のみを追加します。 ディスプレイ ドライバーは、次の表に示す関数を実装できます。 これらの関数は、次のカテゴリに並べ替えられます。

ビットマップの管理機能

描画関数

イメージの色の管理関数

ポインターとウィンドウ管理関数

その他の関数

### <a name="span-idddkbitmapmanagementfunctionsggspanspan-idddkbitmapmanagementfunctionsggspanbitmap-management-functions"></a><span id="ddk_bitmap_management_functions_gg"></span><span id="DDK_BITMAP_MANAGEMENT_FUNCTIONS_GG"></span>ビットマップの管理機能

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">関数</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvcreatedevicebitmap" data-raw-source="[&lt;strong&gt;DrvCreateDeviceBitmap&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvcreatedevicebitmap)"><strong>DrvCreateDeviceBitmap</strong></a></p></td>
<td align="left"><p>作成し、ドライバーの定義済みの形式のビットマップを管理します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvdeletedevicebitmap" data-raw-source="[&lt;strong&gt;DrvDeleteDeviceBitmap&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvdeletedevicebitmap)"><strong>DrvDeleteDeviceBitmap</strong></a></p></td>
<td align="left"><p>デバイス管理のビットマップを削除します。</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idddkdrawingfunctionsggspanspan-idddkdrawingfunctionsggspandrawing-functions"></a><span id="ddk_drawing_functions_gg"></span><span id="DDK_DRAWING_FUNCTIONS_GG"></span>描画関数

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">関数</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvalphablend" data-raw-source="[&lt;strong&gt;DrvAlphaBlend&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvalphablend)"><strong>DrvAlphaBlend</strong></a></p></td>
<td align="left"><p>提供<a href="https://docs.microsoft.com/windows-hardware/drivers/#wdkgloss-bit-block-transfer" data-raw-source="&lt;em&gt;bit-block transfer&lt;/em&gt;"><em>ビット ブロック転送</em></a>機能<a href="https://docs.microsoft.com/windows-hardware/drivers/#wdkgloss-alpha-blending" data-raw-source="&lt;em&gt;alpha blending&lt;/em&gt;"><em>アルファ ブレンド</em></a>します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvbitblt" data-raw-source="[&lt;strong&gt;DrvBitBlt&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvbitblt)"><strong>DrvBitBlt</strong></a></p></td>
<td align="left"><p>一般的なビット ブロック転送間での機能を提供します<a href="https://docs.microsoft.com/windows-hardware/drivers/#wdkgloss-device-managed-surface" data-raw-source="&lt;em&gt;device-managed surfaces&lt;/em&gt;"><em>サーフェスのデバイスで管理された</em></a>、標準形式のビットマップは GDI で管理された、またはデバイス管理の画面と GDI 管理間標準形式のビットマップです。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvdithercolor" data-raw-source="[&lt;strong&gt;DrvDitherColor&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvdithercolor)"><strong>DrvDitherColor</strong></a></p></td>
<td align="left"><p>要求に対しては、ブラシの作成、デバイス、ディザリングを<a href="https://docs.microsoft.com/windows-hardware/drivers/#wdkgloss-device-palette" data-raw-source="&lt;em&gt;device palette&lt;/em&gt;"><em>デバイス パレット</em></a>します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvfillpath" data-raw-source="[&lt;strong&gt;DrvFillPath&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvfillpath)"><strong>DrvFillPath</strong></a></p></td>
<td align="left"><p>デバイス管理の画面を閉じたパスを描画します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvgradientfill" data-raw-source="[&lt;strong&gt;DrvGradientFill&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvgradientfill)"><strong>DrvGradientFill</strong></a></p></td>
<td align="left"><p>指定したプリミティブ網掛けを適用します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvlineto" data-raw-source="[&lt;strong&gt;DrvLineTo&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvlineto)"><strong>DrvLineTo</strong></a></p></td>
<td align="left"><p>1 つ、solid、整数のみの表面的な線を描画します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvplgblt" data-raw-source="[&lt;strong&gt;DrvPlgBlt&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvplgblt)"><strong>DrvPlgBlt</strong></a></p></td>
<td align="left"><p>回転提供<a href="https://docs.microsoft.com/windows-hardware/drivers/#wdkgloss-bit-block-transfer" data-raw-source="&lt;em&gt;bit-block transfer&lt;/em&gt;"><em>ビット ブロック転送</em></a>サーフェス デバイス管理し、GDI 管理の組み合わせ間で機能します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvrealizebrush" data-raw-source="[&lt;strong&gt;DrvRealizeBrush&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvrealizebrush)"><strong>DrvRealizeBrush</strong></a></p></td>
<td align="left"><p>定義されたサーフェイスでの指定したブラシに気付きます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvstretchblt" data-raw-source="[&lt;strong&gt;DrvStretchBlt&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvstretchblt)"><strong>DrvStretchBlt</strong></a></p></td>
<td align="left"><p>デバイス管理し、GDI 管理画面間でのブロックの転送を拡大できます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvstretchbltrop" data-raw-source="[&lt;strong&gt;DrvStretchBltROP&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvstretchbltrop)"><strong>DrvStretchBltROP</strong></a></p></td>
<td align="left"><p>使用して伸縮ビット ブロック転送を実行する<a href="https://docs.microsoft.com/windows-hardware/drivers/#wdkgloss-raster-operation--rop-" data-raw-source="&lt;em&gt;ROP&lt;/em&gt;"> <em>ROP</em></a>します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvstrokeandfillpath" data-raw-source="[&lt;strong&gt;DrvStrokeAndFillPath&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvstrokeandfillpath)"><strong>DrvStrokeAndFillPath</strong></a></p></td>
<td align="left"><p>同時に線し、パスを入力します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvtransparentblt" data-raw-source="[&lt;strong&gt;DrvTransparentBlt&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvtransparentblt)"><strong>DrvTransparentBlt</strong></a></p></td>
<td align="left"><p>透過性のビット ブロック転送機能を提供します。</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idddkimagecolormanagementfunctionsggspanspan-idddkimagecolormanagementfunctionsggspanimage-color-management-functions"></a><span id="ddk_image_color_management_functions_gg"></span><span id="DDK_IMAGE_COLOR_MANAGEMENT_FUNCTIONS_GG"></span>イメージの色の管理関数

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">関数</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvicmcheckbitmapbits" data-raw-source="[&lt;strong&gt;DrvIcmCheckBitmapBits&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvicmcheckbitmapbits)"><strong>DrvIcmCheckBitmapBits</strong></a></p></td>
<td align="left"><p>指定したビットマップのピクセルが、指定した変換のデバイスの色域内にあるかどうかを確認します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvicmcreatecolortransform" data-raw-source="[&lt;strong&gt;DrvIcmCreateColorTransform&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvicmcreatecolortransform)"><strong>DrvIcmCreateColorTransform</strong></a></p></td>
<td align="left"><p>ICM の色変換を作成します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvicmdeletecolortransform" data-raw-source="[&lt;strong&gt;DrvIcmDeleteColorTransform&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvicmdeletecolortransform)"><strong>DrvIcmDeleteColorTransform</strong></a></p></td>
<td align="left"><p>指定した ICM 色変換を削除します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvicmsetdevicegammaramp" data-raw-source="[&lt;strong&gt;DrvIcmSetDeviceGammaRamp&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvicmsetdevicegammaramp)"><strong>DrvIcmSetDeviceGammaRamp</strong></a></p></td>
<td align="left"><p>ハードウェアの設定<a href="https://docs.microsoft.com/windows-hardware/drivers/#wdkgloss-gamma-ramp" data-raw-source="&lt;em&gt;gamma ramp&lt;/em&gt;"><em>ガンマごとの傾斜増加</em></a>の指定した表示デバイス。</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idddkpointerandwindowmanagementfunctionsggspanspan-idddkpointerandwindowmanagementfunctionsggspanpointer-and-window-management-functions"></a><span id="ddk_pointer_and_window_management_functions_gg"></span><span id="DDK_POINTER_AND_WINDOW_MANAGEMENT_FUNCTIONS_GG"></span>ポインターとウィンドウ管理関数

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">関数</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvdescribepixelformat" data-raw-source="[&lt;strong&gt;DrvDescribePixelFormat&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvdescribepixelformat)"><strong>DrvDescribePixelFormat</strong></a></p></td>
<td align="left"><p>PIXELFORMATDESCRIPTOR 構造体へのピクセル形式の説明を記述することで、指定されたデバイス PDEV のピクセル形式を説明します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvmovepointer" data-raw-source="[&lt;strong&gt;DrvMovePointer&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvmovepointer)"><strong>DrvMovePointer</strong></a></p></td>
<td align="left"><p>新しい位置にポインターを移動し、再描画します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvsavescreenbits" data-raw-source="[&lt;strong&gt;DrvSaveScreenBits&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvsavescreenbits)"><strong>DrvSaveScreenBits</strong></a></p></td>
<td align="left"><p>保存または画面の指定した四角形を復元します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvsetpixelformat" data-raw-source="[&lt;strong&gt;DrvSetPixelFormat&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvsetpixelformat)"><strong>DrvSetPixelFormat</strong></a></p></td>
<td align="left"><p>ウィンドウのピクセル形式を設定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvsetpointershape" data-raw-source="[&lt;strong&gt;DrvSetPointerShape&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvsetpointershape)"><strong>DrvSetPointerShape</strong></a></p></td>
<td align="left"><p>ドライバーが引かれて、新しいポインターの形を設定し、場合に、ポインターの画面から削除します。</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idddkmiscellaneousfunctionsggspanspan-idddkmiscellaneousfunctionsggspanmiscellaneous-functions"></a><span id="ddk_miscellaneous_functions_gg"></span><span id="DDK_MISCELLANEOUS_FUNCTIONS_GG"></span>その他の関数

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">関数</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvdestroyfont" data-raw-source="[&lt;strong&gt;DrvDestroyFont&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvdestroyfont)"><strong>DrvDestroyFont</strong></a></p></td>
<td align="left"><p>ドライバーに通知するフォントの実現化が不要になった。ドライバーは、割り当て済みのデータ構造体を解放できます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvdrawescape" data-raw-source="[&lt;strong&gt;DrvDrawEscape&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvdrawescape)"><strong>DrvDrawEscape</strong></a></p></td>
<td align="left"><p>描画型エスケープ関数を実装します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvescape" data-raw-source="[&lt;strong&gt;DrvEscape&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvescape)"><strong>DrvEscape</strong></a></p></td>
<td align="left"><p>デバイス非依存グラフィックス DDI では使用できないデバイスからの情報を照会します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvfree" data-raw-source="[&lt;strong&gt;DrvFree&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvfree)"><strong>DrvFree</strong></a></p></td>
<td align="left"><p>指定されたデータ構造体に関連付けられている記憶域を解放します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvnotify" data-raw-source="[&lt;strong&gt;DrvNotify&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvnotify)"><strong>DrvNotify</strong></a></p></td>
<td align="left"><p>GDI で特定の情報について通知するよう、ディスプレイ ドライバーを使用します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvsynchronize" data-raw-source="[&lt;strong&gt;DrvSynchronize&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvsynchronize)"><strong>DrvSynchronize</strong></a></p></td>
<td align="left"><p>GDI とディスプレイのコプロセッサのドライバーでサポートされているデバイスの間の描画操作の座標<a href="https://docs.microsoft.com/windows-hardware/drivers/#wdkgloss-engine-managed-surface" data-raw-source="&lt;em&gt;engine-managed surfaces&lt;/em&gt;"><em>サーフェスのエンジン管理</em></a>のみです。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvsynchronizesurface" data-raw-source="[&lt;strong&gt;DrvSynchronizeSurface&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvsynchronizesurface)"><strong>DrvSynchronizeSurface</strong></a></p></td>
<td align="left"><p>描画操作の GDI と組み合わせて使用するデバイスのコプロセッサによって実行されるようにします。</p></td>
</tr>
</tbody>
</table>

 

ディスプレイ ドライバーでは、Microsoft DirectDraw または Direct3D インターフェイスを必要に応じても実装できます。 詳細については、次のセクションを参照してください。

[DirectDraw](directdraw.md)

[Direct3D DDI](direct3d.md)

内のすべてのグラフィック ドライバーの省略可能な関数の一覧が表示されます[省略可能なグラフィックス ドライバー関数](optional-graphics-driver-functions.md)します。

 

 





