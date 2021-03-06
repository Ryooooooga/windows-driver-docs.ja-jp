---
title: デバッグ用シンボルへのアクセス
description: デバッグ用シンボルへのアクセス
ms.assetid: a0f52dc3-6903-4d63-b74c-5c16960a7cb6
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 671035d7aa60d6e715552c2cc26b5274e1203f96
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63352602"
---
# <a name="accessing-symbols-for-debugging"></a>デバッグ用シンボルへのアクセス


## <span id="ddk_debugging_user_mode_processes_without_symbols_dbg"></span><span id="DDK_DEBUGGING_USER_MODE_PROCESSES_WITHOUT_SYMBOLS_DBG"></span>


正しくのデバッグのシンボルの設定と、カーネルをデバッグするための困難な作業を指定できます。 名前とすべての製品のリリースをコンピューターにいる多くの場合、必要があります。 デバッガーは、各製品のリリースおよびサービス パックに対応するシンボル ファイルを検索できる必要があります。

これにより、ディレクトリの長い一覧から成るシンボルが非常に長いパスにあります。

シンボル ファイルを調整することでこれらの問題を簡素化するシンボル ファイルを収集することができます、*シンボル ストア*、によってアクセスされますが、*シンボル サーバー*します。

シンボル ストアでは、シンボル ファイル、インデックス、および管理者を追加してファイルを削除するのに使用できるツールのコレクションです。 タイム スタンプとイメージのサイズなどの一意のパラメーターに従って、ファイルのインデックスが作成されます。 シンボル ストアでは、シンボル サーバーを使用して抽出できる実行可能イメージ ファイルも格納できます。 デバッグ ツールの Windows という名前のシンボル ストアの作成ツールが含まれています[SymStore](symstore.md)します。

製品の名前を知らなくても、ユーザーがないシンボルから正しいシンボル ファイルを自動的に取得するデバッガーの格納、シンボル サーバー有効では、リリース、またはビルド番号。 デバッグ ツールの Windows という名前のシンボル サーバーが含まれています[SymSrv](symsrv.md)します。 シンボル パスに特定のテキスト文字列を含めることで、シンボル サーバーがアクティブ化されます。 デバッガーが、新しく読み込まれたモジュールのシンボルを読み込む必要があるたびに、適切なシンボル ファイルを検索するシンボル サーバーを呼び出します。

SymSrv で提供されるより、シンボルの検索のさまざまな方法を使用する場合は、独自のシンボル サーバー DLL を作成できます。 このようなシンボル サーバーの実装について詳しくは、次を参照してください。[その他のシンボル サーバー](other-symbol-servers.md)します。

ユーザー モードのデバッグを実行する場合は、ターゲット アプリケーションのシンボルを必要があります。 カーネル モードのデバッグを実行している場合は、デバッグすると、ドライバーのシンボルと Windows のパブリック シンボルを必要があります。 Microsoft が Microsoft 製品のパブリック シンボルをシンボル ストアを作成します。このシンボル ストアは、インターネットで使用できます。 使用してこれらのシンボルを読み込むことが、 [ **.symfix (シンボル ストア パスの設定)** ](-symfix--set-symbol-store-path-.md)デバッガーの実行中に、インターネットへのアクセスがある限り、コマンドします。 詳細については、またはこれらのシンボルを手動でインストールする方法を決定するを参照してください。 [Windows シンボル ファイルのインストール](installing-windows-symbol-files.md)します。

このセクションの内容:

[Windows シンボル ファイルのインストール](installing-windows-symbol-files.md)

[シンボル ストアとシンボル サーバー](symbol-stores-and-symbol-servers.md)

[シンボルの読み込みの遅延](deferred-symbol-loading.md)

 

 





