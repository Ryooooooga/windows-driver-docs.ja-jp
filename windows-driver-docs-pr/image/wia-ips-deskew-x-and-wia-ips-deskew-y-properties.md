---
title: WIA_IPS_DESKEW_X と WIA_IPS_DESKEW_Y プロパティ
description: WIA_IPS_DESKEW_X と WIA_IPS_DESKEW_Y プロパティ
ms.assetid: 748b08f7-e838-4df8-abcb-4ff1cdd20f7e
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3524f80b8c6ebeeb2641b0d6929b0c5225499006
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67365476"
---
# <a name="wiaipsdeskewx-and-wiaipsdeskewy-properties"></a>WIA\_IP\_DESKEW\_X と WIA\_IP\_DESKEW\_Y プロパティ





[ **WIA\_IP\_DESKEW\_X** ](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-deskew-x)と[ **WIA\_IP\_DESKEW\_Y** ](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-deskew-y)デスキュー ドライバーがサポートしている場合、プロパティは、スキャナー ドライバーによって実装されます。 これら 2 つのプロパティの説明、傾斜したイメージの 2 つの上端がによって定義された外接する四角形内にある[ **WIA\_IP\_XPOS**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-xpos)、 [**WIA\_IP\_YPOS**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-ypos)、 [ **WIA\_IP\_XEXTENT**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-xextent)、および[**WIA\_IP\_YEXTENT** ](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-yextent)プロパティ。

WIA の有効な値\_IP\_DESKEW\_X が 0 の間である必要があり、(WIA\_IP\_XEXTENT − 1)。 WIA の有効な値\_IP\_DESKEW\_Y が 0 の間である必要があり、(WIA\_IP\_YEXTENT − 1)。 両方のプロパティに対して 0 の値は、スキューの修正を実行しないことを意味します。

これら 2 つの値が一意にする deskewed するイメージの位置を定義するため、スキャンの長方形の領域のみがサポートされます。 Deskew 角度は、これら 2 つの値から計算できます。

 

 




