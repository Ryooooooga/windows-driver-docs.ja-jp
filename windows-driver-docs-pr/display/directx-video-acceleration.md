---
title: DirectX ビデオ アクセラレータ
description: DirectX ビデオ アクセラレータ
ms.assetid: e25407a3-be5c-4509-a3e7-d9688958e3d4
keywords:
- DirectX ビデオ アクセラレータ WDK Windows 2000 の表示
- ビデオ アクセラレータ WDK DirectX
- 動き補正 WDK
- VA WDK DirectX
- WDK の DirectX のアクセラレータ
- ドライバー モデル WDK Windows 2000 では、DirectX ビデオ アクセラレータの表示します。
- Windows 2000 ディスプレイ ドライバー モデル WDK、DirectX ビデオ アクセラレータ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 52645fba6a3eb7aec1f26bd689a7966b759ddb9d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67380003"
---
# <a name="directx-video-acceleration"></a>DirectX ビデオ アクセラレータ


## <span id="ddk_directx_video_acceleration_gg"></span><span id="DDK_DIRECTX_VIDEO_ACCELERATION_GG"></span>


このセクションには、Microsoft DirectX ビデオ アクセラレータ (DirectX VA) に関する情報が含まれています。 これは、アプリケーション プログラミング インターフェイス (API) と、対応する[補正のモーション](motion-compensation.md)デジタル ビデオ デコーディングのアクセラレータのデバイス ドライバー インターフェイス (DDI)。 次の追加 Ddi は、DirectX VA の一部として提供されるも示します。

-   A [DDI デインター レース](https://docs.microsoft.com/windows-hardware/drivers/display/deinterlace-ddi)ビデオ コンテンツのデインター レース、フレーム レートの変換。

-   A [ProcAmp DDI](https://docs.microsoft.com/windows-hardware/drivers/display/procamp-control-ddi) ProcAmp コントロールおよびビデオ コンテンツの後処理をサポートします。

-   A [COPP DDI](sample-functions-for-copp.md)ビデオ コンテンツを保護するためです。

Microsoft Windows XP Service Pack 1 (SP1) 以降を使用する必要があります、DirectX VA ドライバーを作成しているドライバーの作成者、 *dxva.h*ヘッダー ファイル。 これには、構造体とビデオ アクセラレータとデインター レース、フレーム レート変換に使用する列挙体が含まれます。

ここでは、次のトピックについて説明します。

[DirectX VA の概要](introduction-to-directx-va.md)

[ビデオのデコード](video-decoding.md)

[デインター レース、フレーム レートの変換](deinterlacing-and-frame-rate-conversion.md)

[ProcAmp コントロールの処理](procamp-control-processing.md)

[COPP 処理](copp-processing.md)

[DirectX VA デバイス用のコード例](example-code-for-directx-va-devices.md)

[DirectX VA データ フローの管理](directx-va-data-flow-management.md)

[DirectX VA 操作](directx-va-operations.md)

[アクセラレータの機能を定義します。](defining-accelerator-capabilities.md)