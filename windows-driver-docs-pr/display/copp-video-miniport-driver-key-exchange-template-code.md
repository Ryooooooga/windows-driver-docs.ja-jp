---
title: COPP ビデオ ミニポート ドライバーのキー交換テンプレート コード
description: COPP ビデオ ミニポート ドライバーのキー交換テンプレート コード
ms.assetid: 5c0de949-e460-4f01-a762-706eac3abee0
keywords:
- キー交換 WDK COPP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cffbc50947b0358709dd9800c2c8678e752a22f9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63331341"
---
# <a name="copp-video-miniport-driver-key-exchange-template-code"></a>COPP ビデオ ミニポート ドライバーのキー交換テンプレート コード


## <span id="ddk_copp_video_miniport_driver_key_exchange_template_code_gg"></span><span id="DDK_COPP_VIDEO_MINIPORT_DRIVER_KEY_EXCHANGE_TEMPLATE_CODE_GG"></span>


このセクションには、Windows Server 2003 SP1 にのみ以降が適用されますおよび Windows XP SP2 以降。

次のコード例を使用すると、グラフィックス ハードウェア COPP DirectX VA デバイス オブジェクトを使用するデジタル証明書を取得できます。

```cpp
VP_STATUS
IoctlCOPPKeyExchange(
    PHW_DEVICE_EXTENSION pHwDeviceExtension,
    PVIDEO_REQUEST_PACKET pVideoRequestPacket
    )
{
    COPP_IO_InputBuffer* pInBuff = pVideoRequestPacket->InputBuffer;
    COPP_DeviceData* pThis = (COPP_DeviceData*)*pInBuff->ppThis;
    GUID* lpout = (GUID*)pVideoRequestPacket->OutputBuffer;
    BYTE* pCertificate = (BYTE*)pInBuff->InputBuffer;
    HRESULT* phr = pInBuff->phr;
     *phr = COPPKeyExchange(pThis, lpout, pCertificate);
    if (*phr == NO_ERROR) {
        pVideoRequestPacket->StatusBlock->Information = pVideoRequestPacket->OutputBufferLength;
    }
    return NO_ERROR;
}
```

 

 





