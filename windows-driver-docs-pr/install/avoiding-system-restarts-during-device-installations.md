---
title: デバイスのインストールとドライバーの更新プログラムの中に再起動を回避します。
description: デバイスのインストールとドライバーの更新プログラムの中にシステムの再起動を回避します。
ms.assetid: b30c9e5f-85af-4e7f-81aa-67fe2df8a178
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 41bda6a033b69bd16b4cfad289b32fb1354ef9c8
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385301"
---
# <a name="avoiding-system-restarts-during-device-installations-and-driver-updates"></a>デバイスのインストールとドライバーの更新プログラムの中にシステムの再起動を回避します。


デバイスのインストール中にシステムの再起動を回避するために、次の規則を使用します。

-   使用しないでください**再起動**または**再起動**エントリ[ **INF DDInstall セクション**](inf-ddinstall-section.md)します。 これらのディレクティブが最初に提供された Windows 互換性のため 9 x/Me Windows 2000 以降のバージョンの Windows を使用する必要があります。

-   使用して行う COPYFLG_FORCE_FILE_IN_USE を使用してまたは COPYFLG_REPLACE_BOOT_FILE フラグ[ **INF CopyFiles ディレクティブ**](inf-copyfiles-directive.md)がない限り、絶対に必要です。

-   クラスのインストーラーまたは共同インストーラーは、サービスの DLL の新しいバージョンごとに新しいファイル名を割り当てます。 これにより、以前のバージョンを使用している場合、システムの再起動の必要性を回避できます。 (実際には、インストーラーの更新後のクラスまたはクラスの共同インストーラーの新しいファイル名を使用しない場合これらの新しいファイルがする未使用のインストール。)

-   デバイスのドライバーを更新するには、下に記載されている規則に従ってください[ドライバー ファイルの更新](updating-driver-files.md)します。

## <a name="minimizing-restarts-when-updating-file-backed-drivers"></a>ファイルに格納されたドライバーを更新するときに、再起動を最小限に抑える


Windows 10 では、前にすべてのカーネル モード ドライバーがシステムのページング ファイルでサポートされます。 その結果、ドライバーのバイナリは、ドライバーの実行中にも、ディスク上上書きでした。

以降、Windows 10 でパフォーマンスを向上させるためにほとんど非ブート開始ドライバーは、代わりにバックアップ バイナリのドライバーによってディスク上。

ファイル バックアップは今すぐドライバーのスタートアップの種類は次のとおりです。

-   SERVICE_SYSTEM_START (0x00000001)
-   SERVICE_AUTO_START (0x00000002)
-   SERVICE_DEMAND_START (0x00000003)

ブート開始ドライバーは、ページング ファイルによってバックアップされ続けます。

ファイルに格納されたドライバーを更新するには、次のベスト プラクティスを使用します。 それ以外の場合、更新プログラムには、ファイルを新しいバージョンのドライバーを読み込む 2 つ目を置換する 1 つ、2 回の再起動が必要です。

INF ファイルを使用している場合は、次の手順に従います。

1.  ドライバーの INF ファイルの変更**CopyFiles**セクションを使用する**COPYFLG_IN_USE_RENAME**、次のようにします。

    ```cpp
    [MyDriver_Install.NT]
    CopyFiles=MyDriverCopy
     
    [MyDriverCopy]
    MyDriver.sys,,,0x00004000  ; COPYFLG_IN_USE_RENAME
    ```

    このフラグを使用する場合、Windows はディスク上のドライバー ファイルを置換しようとします。 詳細については、次を参照してください。 [INF CopyFiles ディレクティブ](inf-copyfiles-directive.md)します。

2.  PnP ドライバーに対して、INF の場合は、デバイスのインストール中に、Windows が実行中のドライバーをアンロードして、新しいバージョンのドライバーを取得するために使用するデバイスを再起動するしようとします。 失敗した場合、デバイスのインストールはシステムを再起動することを示します。
3.  PnP ドライバーに対して、INF でない場合など、メソッドを使用している[ **InstallHInfSection** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-installhinfsectiona) INF を処理し、手動で停止して、ドライバーを再起動します。
    -   ドライバーのすべての開いているハンドルを閉じるし、次のいずれかを使用してドライバーを停止し。

        -   **sc.exe stop** *&lt;mydriver&gt;*
        -   **ControlService(SERVICE_CONTROL_STOP)**

        詳細については、次を参照してください。 [ **ControlService 関数**](https://docs.microsoft.com/windows/desktop/api/winsvc/nf-winsvc-controlservice)します。

INF ファイルを使用していない場合は、次の手順を使用します。

1.  前述のように、ドライバーを停止します。 古いドライバーのバイナリ ファイルを新しいものに置き換えます。
2.  場合は、ドライバーを停止することはできません、既存のファイルの名前を変更、場所に、新しいファイルをコピーおよび今後削除する既存のファイルを設定 (たとえばを使用して[ **MoveFileEx** ](https://docs.microsoft.com/windows/desktop/api/winbase/nf-winbase-movefileexa)で、 **MOVEFILE_DELAY_UNTIL_REBOOT**フラグ)。 の新しいバージョンのドライバーの使用を開始するには、システムが再起動する必要があります。

## <a name="related-topics"></a>関連トピック


[ファイル バックアップし、ファイルに格納されたページのセクション](https://docs.microsoft.com/windows-hardware/drivers/kernel/file-backed-and-page-file-backed-sections)

[ドライバーが読み込まれるときにどのようにして決まります](https://docs.microsoft.com/windows-hardware/drivers/ifs/what-determines-when-a-driver-is-loaded)

 

 






