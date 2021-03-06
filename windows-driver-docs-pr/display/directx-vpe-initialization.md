---
title: DirectX VPE の初期化
description: DirectX VPE の初期化
ms.assetid: 1309a302-f9fc-49cf-a6b8-691d0956beab
keywords:
- DirectX VPE サポート WDK DirectDraw, 初期化
- 描画 VPEs WDK DirectDraw, 初期化
- DirectDraw VPEs WDK Windows 2000 の表示、初期化
- 拡張機能のビデオ ポート WDK DirectDraw, 初期化
- VPEs WDK DirectDraw, 初期化
- DirectX VPE 機能を初期化しています
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ad26d95847280080e5ff091b6e05deb5c588014a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379995"
---
# <a name="directx-vpe-initialization"></a>DirectX VPE の初期化


## <span id="ddk_directx_vpe_initialization_gg"></span><span id="DDK_DIRECTX_VPE_INITIALIZATION_GG"></span>


VPE 機能を有効にするには、ドライバーは、次の操作を行う必要があります。

-   ときに[ **DrvGetDirectDrawInfo** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvgetdirectdrawinfo)が呼び出されるの次のメンバーの初期化、 [ **DDCORECAPS** ](https://docs.microsoft.com/windows/desktop/api/ddrawi/ns-ddrawi-_ddcorecaps) に埋め込まれている構造体[**DD\_HALINFO** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_halinfo)構造体、 *pHalInfo*パラメーターが指す。
    -   設定、DDCAPS2\_ビデオ ポート フラグ**dwCaps2**ディスプレイ ハードウェアがハードウェアのビデオ ポートに含まれているかを示す。 ドライバーは、他のハードウェアにも設定する必要がありますビデオ ポート関連 DDCAPS2\_*Xxx* VPE を記述するフラグは、デバイスができることをサポートします。
    -   設定**dwMaxVideoPorts**デバイスでサポートされているハードウェアのビデオ ポートの数。
    -   初期化**dwCurrVideoPorts**をゼロにします。
-   実装を[ **DdGetDriverInfo** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_getdriverinfo)関数を設定、 **GetDriverInfo** 、DD のメンバー\_HALINFO 構造をこの関数を指すとき[ **DrvGetDirectDrawInfo** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvgetdirectdrawinfo)が呼び出されます。 ドライバーの**DdGetDriverInfo**関数は、GUID を解析する必要があります\_VideoPortCallbacks と GUID\_VideoPortCaps Guid。

-   ときに[ **DdGetDriverInfo** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_getdriverinfo) GUID を使用して呼び出した\_VideoPortCallbacks の GUID を入力、 [ **DD\_VIDEOPORTCALLBACKS**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-dd_videoportcallbacks)適切なドライバーのコールバックとフラグのセットを含む構造体。 これらのコールバックは、「 [VPE コールバック関数](vpe-callback-functions.md)します。 ドライバーを DirectDraw に割り当てられたバッファーに、この初期化された構造体をコピーしする必要があります、 **lpvData**のメンバー、 [ **DD\_GETDRIVERINFODATA** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_getdriverinfodata)ポイント、構造体し、をバッファーに書き込まれたバイト数を返す**dwActualSize**します。

-   ときに[ **DdGetDriverInfo** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_getdriverinfo) GUID を使用して呼び出した\_VideoPortCaps の GUID の配列を入力[ **DDVIDEOPORTCAPS** ](https://docs.microsoft.com/windows/desktop/api/dvp/ns-dvp-_ddvideoportcaps)各ハードウェアのビデオ ポートの機能を持つ構造体。 各ハードウェアのビデオ ポートには、ハードウェアのビデオ ポート 0 は最初に、指定されたハードウェアのビデオ ポート次に、指定された 1 つで、配列のエントリがあります。 デバイスは、ハードウェアのビデオ ポートを 1 つだけをサポートする場合はだけ DDVIDEOPORTCAPS 構造体の 1 つ、配列内です。 ドライバーを DirectDraw に割り当てられたバッファーにこのデータをコピーする必要があります、 **lpvData**のメンバー、 [ **DD\_GETDRIVERINFODATA** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_getdriverinfodata)構造体ポイントし、のバッファーに書き込まれたバイト数を返す**dwActualSize**します。

 

 





