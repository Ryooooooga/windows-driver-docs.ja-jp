---
title: トレースのエラーをデバッグする方法
description: トレースのエラーをデバッグする方法
ms.assetid: 9f974482-e19d-4bcc-a884-4425741aa465
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7cf79c687a7131fbd90790ebff82bff137459d31
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63360391"
---
# <a name="how-do-i-debug-tracing-failures"></a>トレース エラーをデバッグする方法


トレース メッセージが表示されないのトレース ログ ファイルで、プロバイダーが有効な場合でもですなど、トレースでインストルメント化されたドライバーの問題をデバッグするには追加、 **WppDebug**マクロ定義ソース コードにします。

**WppDebug** WPP をデバッグするためのコードを使用します。 これは、登録および有効/無効にするアクティビティなどのアクションをトレースします。

すべて**WppDebug**定義ディレクティブは機能します。 例:

```
#define WppDebug(a,b) printf b, printf("\n");
```

ルーチンを呼び出すには、次の形式を使用します。

```
WppDebug(level,(format,...));
```

混同しないでください、 **WppDebug**で WPP のアクションを追跡、マクロ、 **WPP\_デバッグ**マクロで、デバッガーにトレース メッセージを送信します。

 

 





