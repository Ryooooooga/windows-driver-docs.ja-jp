---
title: ウィンドウの変更の追跡
description: ウィンドウの変更の追跡
ms.assetid: 76539ee8-439a-4c6a-b16a-3998e341f954
keywords:
- ディスプレイ ドライバー WDK Windows 2000 では、ウィンドウの変更
- ウィンドウの変更の追跡の WDK Windows 2000 の表示
- WNDOBJ
- WDK の Windows 2000 クライアントのリージョンの変更を表示します。
- 表示されているクライアント領域の WDK Windows 2000 を表示します。
- サイズの WDK Windows 2000 の表示
- Windows 2000 の WDK の位置の表示
- Windows 2000 の WDK の表示を変更のトラッキング ウィンドウ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9d8ad5b8bd7c906c3e390cfb44d7297eb6a62bf2
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67353428"
---
# <a name="tracking-window-changes"></a>ウィンドウの変更の追跡


## <span id="ddk_tracking_window_changes_gg"></span><span id="DDK_TRACKING_WINDOW_CHANGES_GG"></span>


1 つを含む、ウィンドウへの変更、[マルチ モニター システム](multiple-monitor-support-in-the-display-driver.md)でデバイス ドライバーによって追跡されることができます、 [ **WNDOBJ**](https://docs.microsoft.com/windows/desktop/api/winddi/ns-winddi-_wndobj)します。 WNDOBJ は、位置、サイズ、およびウィンドウの表示されているクライアント領域に関する情報を含むドライバー レベルのウィンドウ オブジェクトです。 つまり、アプリケーション ウィンドウに対応する WNDOBJ を作成すると、ドライバーを追跡できますサイズ、位置、およびそのウィンドウのクライアント領域の変更点。

アプリケーションでは、Win32 API を使用して、アクセス、 **WNDOBJ\_セットアップ**デバイス ドライバによって実装される機能です。 Win32 アクセス権を得る**ExtEscape**関数。 GDI のデバイス ドライバーには、このエスケープ呼び出しに渡します[ **DrvEscape**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvescape)デバイス ドライバによって実装される、 **WNDOBJ\_セットアップ**の値の*iEsc*します。

アプリケーションを呼び出す<strong>ExtEscape (</strong>hdc、WNDOBJ\_... セットアップします。 **)** をアプリケーションで作成されたウィンドウ ハンドルを渡します (によって作成された**CreateWindow**または同等の Win32 関数がいくつか)、ドライバーに、入力バッファー内。 呼び出す場合は、ドライバーは、ウィンドウを追跡するのには、 [ **EngCreateWnd**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engcreatewnd)のコンテキスト内で、 **ExtEscape**呼び出し、指定されたウィンドウの WNDOBJ 構造を作成します。 その時点からそのウィンドウへの変更は、ドライバーにに渡されます。

ドライバーを処理する必要があります、 **ExtEscape**次のような方法で呼び出します。

```cpp
ULONG DrvEscape(
  SURFOBJ *pso,
  ULONG    iEsc,
  ULONG    cjIn,
  PVOID    pvIn,
  ULONG    cjOut,
  PVOID    pvOut)
{
    WNDOBJ *pwo;
    WNDDATA *pwd;

    if (iEsc == WNDOBJ_SETUP)
    {
        pwo = EngCreateWnd(pso,*((HWND *)pvIn),&DrvVideo,
                           WO_RGN_CLIENT, 0);

    // Allocate space for caching client rects. Remember the pointer
    // in the pvConsumer field.

        pwd = EngAllocMem(0, sizeof(WNDDATA), DRIVER_TAG);
        WNDOBJ_vSetConsumer(pwo,pwd);

    // Update the rectangle list for this wndobj.

        vUpdateRects(pwo);
        return(1);
    }

}
```

そのため、特別なウィンドウのリソースをロックするにはウィンドウ オブジェクトを作成[ **EngCreateWnd** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engcreatewnd)のコンテキストでのみ呼び出す必要があります、 **WNDOBJ\_セットアップ**でエスケープ[ **DrvEscape** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvescape)または[ **DrvSetPixelFormat**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvsetpixelformat)します。

**EngCreateWnd**関数は、複数のドライバーによってウィンドウの追跡をサポートしています。 を通じて**EngCreateWnd**、各ドライバーは、GDI が対応するウィンドウへの変更を呼び出すためには独自のコールバック ルーチンを識別します。 この機能により、ライブのビデオ ドライバー、OpenGL ドライバーが OpenGL の windows に変更を追跡中に、ライブ ビデオ ウィンドウへの変更を追跡します。

GDI は、新規の場合、最新のウィンドウ状態を持つドライバーにコールバック[ **WNDOBJ** ](https://docs.microsoft.com/windows/desktop/api/winddi/ns-winddi-_wndobj)は*DrvSetPixelFormat*または**ExtEscape**. GDI もコールバックにドライバーを WNDOBJ により参照されるウィンドウが破棄されるときにします。

ドライバー、アクセラレータとしてのパブリック メンバーのアクセス可能性があります、 [ **WNDOBJ** ](https://docs.microsoft.com/windows/desktop/api/winddi/ns-winddi-_wndobj)構造体。

ウィンドウの変更を追跡するには、WNDOBJ 構造をサポートするために用意されている 3 つのコールバック関数を使用する必要があります。 呼び出すことによって表示されているクライアント領域を列挙することがあります、 [ **WNDOBJ\_cEnumStart** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-wndobj_cenumstart)と[ **WNDOBJ\_bEnum** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-wndobj_benum)コールバック関数。 ドライバーは、呼び出すことによって、WNDOBJ で独自のデータを関連付ける、 [ **WNDOBJ\_vSetConsumer** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-wndobj_vsetconsumer)コールバック関数。









