---
title: WinDbg でのコマンド ブラウザー ウィンドウの使用
description: WinDbg でのコマンド ブラウザー ウィンドウの使用
ms.assetid: b895f463-38ec-451a-8c0a-0deb8650a904
keywords:
- デバッグ情報のウィンドウでコマンドのブラウザー ウィンドウ
- コマンドのブラウザー ウィンドウ
- デバッガー コマンド ウィンドウ、コマンドのブラウザー ウィンドウ
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2fd0e489b10125f6ef2174aa80c65a8a7a1a8bca
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63375088"
---
# <a name="using-the-command-browser-window-in-windbg"></a>WinDbg でのコマンド ブラウザー ウィンドウの使用


コマンドのブラウザー ウィンドウでは、表示し、デバッガー コマンドの結果をテキストを格納します。 このウィンドウは、コマンドのリファレンス、コマンドを再入力しなくても、特定のコマンドの結果を表示することができますを作成します。 コマンドのブラウザー ウィンドウには、ストアドのコマンドを使用してナビゲーションも用意されていますとよりコマンドにすばやくアクセスの詳細はできるように、[デバッガー コマンド ウィンドウ](debugger-command-window.md)します。

### <a name="span-idopeningthecommandbrowserwindowspanspan-idopeningthecommandbrowserwindowspanopening-the-command-browser-window"></a><span id="opening_the_command_browser_window"></span><span id="OPENING_THE_COMMAND_BROWSER_WINDOW"></span>コマンドのブラウザー ウィンドウを開く

一度に複数のコマンドのブラウザー ウィンドウを開くことができます。 コマンドのブラウザー ウィンドウを開くには、次のように選択します。**コマンド ブラウザー**から、**ビュー**メニュー。 (Ctrl キーを押しながら N キーを押してまたは をクリックすることができますも、**コマンド ブラウザー**ボタン (![コマンド、ブラウザーのボタンのスクリーン ショット](images/window-command-browser-icon.png))、ツールバーの。 ALT + SHIFT + N コマンド ブラウザ ウィンドウを閉じる。)

入力してコマンドのブラウザー ウィンドウを開くことができますも[ **.browse (ブラウザーで表示コマンド)** ](-browse--display-command-in-browser-.md)正規のデバッガー コマンド ウィンドウにします。

次のスクリーン ショットでは、コマンドのブラウザー ウィンドウの例を示します。

![コマンドのブラウザー ウィンドウのスクリーン ショット](images/window-commandbrowser.png)

### <a name="span-idusingthecommandbrowserwindowspanspan-idusingthecommandbrowserwindowspanusing-the-command-browser-window"></a><span id="using_the_command_browser_window"></span><span id="USING_THE_COMMAND_BROWSER_WINDOW"></span>コマンドのブラウザー ウィンドウを使用します。

コマンドのブラウザーのウィンドウでは、次の操作を行うことができます。

-   コマンドを入力しでの入力、**コマンド**ボックス。

-   以前に入力したコマンドの結果を表示する、**開始**、 **Prev**と**次**コマンドの一覧をスクロールまたは前の 20 のいずれかを選択するボタンコマンドから、**コマンド**メニュー。 前の 20 のコマンドではないコマンドを確認する、**次**ボタンをクリックします。

コマンドのブラウザー ウィンドウには、その他のコマンドをショートカット メニューがあります。 メニューにアクセスするタイトル バーを右クリックするか、ウィンドウ (右上隅のアイコンをクリックします。![コマンドのブラウザー ウィンドウのツールバーのショートカット メニューを表示するボタンのスクリーン ショット](images/window-command-browser-icon.png)). 次の一覧では、メニュー コマンドの一部について説明します。

-   **開始**、 **Prev**と**次**カーソルまたはへ移動コマンド履歴の開始前または次のコマンドをそれぞれします。

-   **最新のコマンドを追加**に現在のコマンドを配置、**最新コマンド**のメニュー、**ビュー** WinDbg ウィンドウのメニュー。 最新のコマンドは、ワークスペースに保存されます。

-   **ツールバー**オンとオフは、ツールバーをオンにします。

-   **新しいドッキングするのには移動**コマンド ブラウザー ウィンドウを閉じるし、新しいドッキング ステーションで開かれます。

-   **常に浮動**によって、ウィンドウをドッキング場所にドラッグされる場合でも、ドッキングされていないままにします。

-   **フレームを使用して移動**によって、ウィンドウに、ウィンドウがドッキングされていない場合でも、WinDbg フレームが移動したときに移動します。 Windows のドッキング、タブ、および浮動小数点の詳細については、次を参照してください。 [、Windows の位置づけ](positioning-the-windows.md)します。

コマンドのブラウザー ウィンドウに入力するコマンドは、WinDbg のユーザー インターフェイスではなく、デバッガー エンジンによって実行されます。 つまりなどのユーザー インターフェイスのコマンドを入力することはできません[ **.cls** ](-cls--clear-screen-.md)コマンド ブラウザーのウィンドウでします。 ユーザー インターフェイスがリモート クライアントの場合、サーバー (クライアントではなく) は、コマンドを実行します。

コマンドのブラウザー ウィンドウに入力したコマンドは、これが完了するまで、出力は表示されず、同期的に実行します。

ブラウザー ウィンドウのコマンドは、WinDbg ワークスペースで、保存されますが、コマンド履歴は保存されません。 各コマンドのブラウザー ウィンドウの現在のコマンドのみは、ワークスペースに保存されます。

 

 





