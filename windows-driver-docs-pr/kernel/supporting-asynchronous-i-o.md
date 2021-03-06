---
title: 非同期 I/O のサポート
description: 非同期 I/O のサポート
ms.assetid: b4baf1a9-6156-4bbf-b4d9-7205924c637f
keywords:
- 非同期 I/O の WDK カーネル
- I/O WDK カーネルでは、非同期モード
- WDK の I/O 要求の状態情報
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0087723df0b61e2ee506d69325a44bbd530069f8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63330564"
---
# <a name="supporting-asynchronous-io"></a>非同期 I/O のサポート





I/O マネージャーは、(通常ユーザー モード アプリケーションが、場合によって別のドライバー) は、I/O 要求の発信元は、の実行を続行ではなくの I/O 要求が完了するまで待機するために、非同期 I/O のサポートを提供します。 非同期 I/O のサポートは、システム全体のスループットと I/O 要求を作成するすべてのコードのパフォーマンスが向上します。

非同期 I/O のサポート、カーネル モード ドライバーとは限りません処理しない I/O マネージャーに送信された順序での I/O 要求。 I/O マネージャー、またはより高度なドライバーは受信するときに I/O 要求に順序を変更します。 ドライバーは、転送要求の数に大量のデータの転送要求を分割できます。 さらに、ドライバーと重複できる、対称型マルチプロセッサ プラットフォームでは特に、I/O 要求の処理で説明したよう[マルチプロセッサ セーフ](multiprocessor-safe.md)します。

さらに、個々 の I/O 要求のカーネル モード ドライバーの処理は必ずしもシリアル化されません。 ドライバーとは限りませんを処理しない各 IRP の完了を次の受信 I/O 要求の処理を開始する前に。

ドライバーは IRP を受信すると、できるだけ IRP に固有の処理可能な限り実行して応答します。 ドライバーは IRP の非同期をサポートしている場合処理、必要に応じて、次のドライバーには IRP を送信してが完了する 1 つ目を待つことがなく [次へ] の IRP の処理を開始します。 ドライバーは、「完了ルーチンを」I/O マネージャーが別のドライバーが IRP の処理を完了したときに呼び出すを登録できます。 ドライバーは、I/O 要求の状態を確認するその他のドライバーがアクセスできる IRP の I/O 状態ブロックの状態値を提供します。

ドライバーと呼ばれる、そのデバイス オブジェクトの特殊な部分で、現在の I/O 操作に関する状態情報を維持できる、[デバイス拡張機能](device-extensions.md)します。

詳細については、次を参照してください。 [Irp の処理](handling-irps.md)と[入力/出力手法](i-o-programming-techniques.md)します。

 

 




