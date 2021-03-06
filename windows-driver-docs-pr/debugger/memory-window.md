---
title: WinDbg でのメモリの表示と編集
description: 、WinDbg では、表示し、コマンドを入力するか、または [メモリ] ウィンドウを使用してメモリを編集します。
ms.assetid: 4ac3b94c-5d92-4074-bf79-6da151ce52c8
keywords:
- デバッグ情報のウィンドウで [メモリ] ウィンドウ
- '[メモリ] ウィンドウ'
- メモリ、メモリ ウィンドウ
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: dc1f6a57867190c3144b344508ac07d70ed35279
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63351816"
---
# <a name="viewing-and-editing-memory-in-windbg"></a>WinDbg でのメモリの表示と編集


、WinDbg では、表示し、コマンドを入力するか、または [メモリ] ウィンドウを使用してメモリを編集します。

## <a name="span-iddebuggercommandwindowspanspan-iddebuggercommandwindowspanspan-iddebuggercommandwindowspandebugger-command-window"></a><span id="Debugger_Command_Window"></span><span id="debugger_command_window"></span><span id="DEBUGGER_COMMAND_WINDOW"></span>デバッガー コマンド ウィンドウ


いずれかを入力してメモリを表示することができます、 [**表示メモリ**](d--da--db--dc--dd--dd--df--dp--dq--du--dw--dw--dyb--dyd--display-memor.md)デバッガー コマンド ウィンドウでコマンド。 いずれかを入力してメモリを編集することができます、 [**入力値**](e--ea--eb--ed--ed--ef--ep--eq--eu--ew--eza--ezu--enter-values-.md)デバッガー コマンド ウィンドウでコマンド。 詳細については、次を参照してください。[仮想アドレスにアクセスするメモリ](accessing-memory-by-virtual-address.md)と[物理アドレスにアクセスするメモリ](accessing-memory-by-physical-address.md)します。

## <a name="span-idddkmemorywindowdbgspanspan-idddkmemorywindowdbgspanopening-a-memory-window"></a><span id="ddk_memory_window_dbg"></span><span id="DDK_MEMORY_WINDOW_DBG"></span>[メモリ] ウィンドウを開く


[メモリ] ウィンドウを開くには、次のように選択します。**メモリ**から、**ビュー**メニュー。 (ALT + 5 キーを押すこともできますかをクリックして、**メモリ**ボタン (![メモリ ボタンのスクリーン ショット](images/tbmem.png))、ツールバーの。 ALT + SHIFT + 5 ウィンドウを閉じる、アクティブなメモリ。)

次のスクリーン ショットでは、[メモリ] ウィンドウの例を示します。

![[メモリ] ウィンドウのスクリーン ショット](images/window-memory.png)

## <a name="span-idusingamemorywindowspanspan-idusingamemorywindowspanspan-idusingamemorywindowspanusing-a-memory-window"></a><span id="Using_a_Memory_Window"></span><span id="using_a_memory_window"></span><span id="USING_A_MEMORY_WINDOW"></span>[メモリ] ウィンドウを使用します。


[メモリ] ウィンドウでは、複数の列でデータを表示します。 ウィンドウの左側にある列には、各行の先頭のアドレスが表示されます。 残りの列には、左から右への要求された情報が表示されます。 選択した場合**バイト**で、**表示形式**メニューで、これらのバイトに対応する ASCII 文字は、ウィンドウの右側に表示されます。

**注**  既定では、[メモリ] ウィンドウには、仮想メモリが表示されます。 この種類のメモリは、ユーザー モードで使用可能なメモリの唯一の種類です。 カーネル モードで使用することができます、**メモリ オプション**ダイアログ ボックスに、他のデータ スペースの物理メモリを表示します。 **メモリ オプション** ダイアログ ボックスはこのトピックの後半で説明します。

 

[メモリ] ウィンドウでは、次の操作を行うことができます。

-   メモリに書き込むには、新しいデータがメモリ ウィンドウ内をクリックします。 16 進数のデータのみを編集することができます-ASCII および Unicode 文字を直接編集することはできません。 変更は、新しい情報を入力するとすぐに反映されます。

-   メモリの他のセクションを表示するには、使用、**前**と**次**ボタン メモリ ウィンドウのツールバー、またはキーを押して、PAGE UP または PAGE DOWN キー。 これらのボタンとキーは、メモリのすぐ前または後のセクションを表示します。 無効なページを要求すると、エラー メッセージが表示されます。

-   ウィンドウ内で移動するには、右矢印、左方向、上方向および下方向キーを使用します。 これらのキーを使用して、ページから移動する場合は、新しいページが表示されます。 これらのキーを使用する前に、スクロール バーがあるないように、[メモリ] ウィンドウがサイズ変更する必要があります。 このサイズでは、実際のページの端とカットオフのウィンドウとを区別することができます。

-   表示されているメモリの場所を変更するには、[メモリ] ウィンドウの上部にある [アドレス] ボックスに新しいアドレスを入力します。 アドレスを入力が完了する前に、エラー メッセージを取得することに、アドレスを入力するときに、[メモリ] ウィンドウは表示を更新します。 注意してください。
    **注**  ボックスに入力したアドレスは現在の基数で解釈されます。 16 進数のアドレスのプレフィックスにする必要があります、現在の基数が 16 でない場合**0 x**します。 既定の基数を変更するには、使用、 [**n (設定数の基本)**](n--set-number-base-.md)デバッガー コマンド ウィンドウでコマンド。 メモリ ウィンドウ自体内での表示は現在の基数の影響を受けません。

     

-   ウィンドウを使用してメモリを表示するデータ型を変更するには、使用、**表示形式**メモリ ウィンドウのツールバー メニュー。 サポートされているデータ型には、短い単語やダブル ワード、クアッド単語; が含まれます。short、long、およびクアッド整数と符号なし整数。10 バイト、16 バイト、32 バイト、64 バイトの実数。ASCII 文字。Unicode 文字。16 進数のバイト数。 16 進数のバイトの表示には、同様の ASCII 文字が含まれます。

[メモリ] ウィンドウは、2 つのボタン、メニューのおよびボックスを含み、その他のコマンドのショートカット メニューを持つツールバーがあります。 メニューにアクセスするタイトル バーを右クリックするか、ウィンドウ (右上隅のアイコンをクリックします。![メモリ ウィンドウのツールバーのショートカット メニューを表示するボタンのスクリーン ショット](images/tbmem.png)). ツールバーとショートカット メニューには、次の選択肢が含まれます。

-   (ツールバー)[アドレス] ボックスでは、新しいアドレスまたはオフセットを指定することができます。 このボックスの正確な意味は、表示しているメモリの種類によって異なります。 たとえば、仮想メモリを表示している場合、ボックスでは、新しい仮想アドレスまたはオフセットを指定します。

-   (ツールバー)**表示形式**新しい表示形式を選択することができます。

-   (ツールバーとメニュー)**前**(ツールバー) と**前ページ**(ショートカット メニュー) で表示されるメモリの前のセクションが発生します。

-   (ツールバーとメニュー)**次**(ツールバー) と**次のページ**(ショートカット メニュー) で表示されるメモリの次のセクションが発生します。

-   (メニューのみ)**ツールバー**オンとオフは、ツールバーをオンにします。

-   (メニューのみ)**自動調整列**[メモリ] ウィンドウに表示される列の数が [メモリ] ウィンドウの幅を調整します。

-   (メニューのみ)**ドッキング**または**ドッキング解除**によって、ウィンドウに入力するか、ドッキング状態のままにします。

-   (メニューのみ)**新しいドッキングするのには移動**[メモリ] ウィンドウを閉じ、新しいドッキング ステーションで開かれます。

-   (メニューのみ)**ウィンドウの種類のタブのドッキング先として設定**他のメモリ ウィンドウのタブ ドッキング先として選択されているメモリ ウィンドウを設定します。 1 つがタブ ドッキング ターゲットとして選択した後に開かれているすべてのメモリ ウィンドウは、タブ付きのコレクションでは、そのウィンドウに自動的にグループ化されます。

-   (メニューのみ)**常に浮動**によって、ウィンドウをドッキング場所にドラッグされる場合でも、ドッキングされていないままにします。

-   (メニューのみ)**フレームを使用して移動**によって、ウィンドウに、ウィンドウがドッキングされていない場合でも、WinDbg フレームが移動したときに移動します。 Windows のドッキング、タブ、および浮動小数点の詳細については、次を参照してください。 [、Windows の位置づけ](positioning-the-windows.md)します。

-   (メニューのみ)**プロパティ**開きます、**メモリ オプション**ダイアログ ボックスで、このトピックでは、次のセクションに記載されています。

-   (メニューのみ)**ヘルプ**ツールを Windows のデバッグ ドキュメントのこのトピックを開きます。

-   (メニューのみ)**閉じる**このウィンドウを閉じます。

### <a name="span-idmemoryoptionsdialogboxspanspan-idmemoryoptionsdialogboxspanmemory-options-dialog-box"></a><span id="memory_options_dialog_box"></span><span id="MEMORY_OPTIONS_DIALOG_BOX"></span>メモリ オプション ダイアログ ボックス

クリックすると**プロパティ**、ショートカット メニューで、**メモリ オプション** ダイアログ ボックスが表示されます。

カーネル モードでは 6 つのメモリの種類がこのダイアログ ボックスのタブとして使用できます。**仮想メモリ**、**物理メモリ**、 **Bus データ**、**コントロール データ**、 **I/O** (I/O ポート情報) と**MSR** (モデルに固有の登録情報)。 アクセスに必要な情報に対応するタブをクリックします。

ユーザー モードのみで、**仮想メモリ**タブを使用できます。

各タブには、メモリを表示するを指定することができます。

- **仮想メモリ** タブで、**オフセット**ボックスで、アドレスまたは表示するメモリの範囲の先頭のオフセットを指定します。

- **物理メモリ** タブで、**オフセット**ボックスで、表示するメモリの範囲の先頭の物理アドレスを指定します。 [メモリ] ウィンドウには、説明、キャッシュ可能な物理メモリのみを表示できます。 その他の属性を持つ物理メモリを表示する場合、使用、 [ **d\* (メモリの表示)** ](d--da--db--dc--dd--dd--df--dp--dq--du--dw--dw--dyb--dyd--display-memor.md)コマンドまたは[ **! d\\**  * ](-db---dc---dd---dp---dq---du---dw.md)拡張機能。

- **Bus データ** タブで、 **Bus データ型** メニューの バスのデータ型を指定します。 次に、使用、**バス番号**、**スロット数**と**オフセット**bus データを表示するを指定するボックス。

- **コントロール データ** タブで、使用、**プロセッサ**と**オフセット**テキスト ボックスを表示するコントロールのデータを指定します。

- **I/O**  タブで、**インターフェイス型**メニューで、I/O インターフェイスの種類を指定します。 使用して、**バス番号**、**アドレス空間**、および**オフセット**ボックスを表示するデータを指定します。

- **MSR**  タブで、 **MSR**ボックスで、表示するモデル固有のレジスタを指定します。

各タブにも含まれています、**表示形式**メニュー。 このメニューと同じ効果を持つ、**表示形式** メニューの メモリ ウィンドウ。

をクリックして**OK**で、**メモリ オプション** ダイアログ ボックスを有効にする、変更が発生します。

## <a name="span-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報


メモリの操作とその他のメモリに関連するコマンドの説明の詳細については、次を参照してください。[読み取りと書き込みメモリ](reading-and-writing-memory.md)します。

 

 





