---
title: Source Code (ソース コード) ウィンドウの使用
description: Source Code (ソース コード) ウィンドウの使用
ms.assetid: da8d16cd-583f-42b0-857f-64e5103aa379
keywords:
- Static Driver Verifier レポート WDK、ソース コード ウィンドウ
- ソース コード ウィンドウ WDK Static Driver Verifier
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 47019afe6ed0997e368d570f9551106607d59e4c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63327340"
---
# <a name="using-the-source-code-pane"></a>[Source Code]\(ソース コード\) ウィンドウの使用


使用して、**ソース コード**規則違反へのパス内のコードの各行の起点を特定するウィンドウ。

内のコード要素をステップ実行すると、[トレース ツリー ウィンドウ](trace-tree-pane.md)にカーソルを置き、**ソース コード**ペインに自動的に移動元の行のコード ファイルを必要に応じてすばやく間の切り替え。 どのファイルが表示されているかを判断する最上位タブでファイル名を検索、**ソース コード**ウィンドウ、または使用して、[色分け](color-coding-in-the-source-code-pane.md)視覚的な合図として。

実行されたドライバーのソース コードの行の検証の状態またはトレースの効果を確認するには、まずそのコードの行をクリックして、**ソース コード**ウィンドウ、でその行のコード要素が強調表示されているように**トレース ツリー**ウィンドウ。 次に、使用、**トレース ツリー**ウィンドウ内の値を変更するために見ているときに、後続のコード行をステップ実行する、[状態ウィンドウ](state-pane.md)します。

ルールの SDV を監視している関数を見つけて、内の値が変わる可能性があるアクションを識別する、[の状態 ウィンドウ](state-pane.md)、規則のソース コードを読み取ることができます (*RuleName*.slic) ファイルで、 **ソース コード**ウィンドウ。

使用することができます、**ソース コード**を読み取る任意のファイルが、カーソルの手順により、コードを 1 行ずつ; 実行の順序ではなくウィンドウ。

任意のタブから、コードをコピーすることも、**ソース コード**ウィンドウと Microsoft Word やワードパッドなどのリッチ テキスト形 (式 RTF) をサポートするアプリケーションにファイルを貼り付けます。 コードをコピーする、**編集**メニューの **すべて選択**し、**編集**メニューの **コピー**します。 または、CTRL + A (すべて選択) し (コピー) を ctrl キーを押しながら C キーを押します。

 

 





