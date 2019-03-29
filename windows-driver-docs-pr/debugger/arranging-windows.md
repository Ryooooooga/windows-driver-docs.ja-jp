---
title: Windows の配置
description: Windows の配置
ms.assetid: f6c0b778-42a8-4073-8cdb-c4b801e59274
keywords:
- デバッグ情報のウィンドウをドッキングの提案
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: f2fcc6682e4aefeb87675a6a14e24f5c69f8f9e5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56557988"
---
# <a name="arranging-windows"></a>Windows の配置


## <span id="ddk_suggested_configurations_dbg"></span><span id="DDK_SUGGESTED_CONFIGURATIONS_DBG"></span>


1 つの便利なウィンドウの整列はすべての結合には、[ソース windows](source-window.md)タブ付きコレクションを 1 つにします。 これを行う最も簡単な方法は、すべてのソース ウィンドウのタブ ドッキング先として選択して、最初のソース ウィンドウをマークすることによって、**ウィンドウの種類のタブのドッキング先として設定**ソース ウィンドウのショートカット メニューのオプション。 これを完了すると、開かれたすべての将来ソース ウィンドウはこの最初のソース ウィンドウのタブ付きのコレクションに自動的に含まれます。 ソース ウィンドウとしてマークされているタブ ドッキングときにターゲットは削除されません、**ウィンドウ |ソースのすべての Windows を閉じる**メニュー コマンドを選択します。 したがってプレース ホルダーにする場合にのみ閉じることがソース ウィンドウのウィンドウを設定することができます。

このコレクションは WinDbg ウィンドウの半分を占有できるまたは別のドッキング ステーションに配置することができます。

各デバッグ情報 ウィンドウを完全に分離する場合は、各ウィンドウのドッキング ステーションを 1 つを作成できます。 この配置では最小限に抑えるか、個別に各ウィンドウを最大化を行うことができます。

選択する必要がありますすべて配置する、windows の場合**常に浮動**各ウィンドウのショートカット メニューの ドラッグできますしない各ウィンドウ個別に任意の場所にできるようにします。

また、使用することができます、 [MDI エミュレーション](window---mdi-emulation.md)コマンドを**ウィンドウ**メニュー。 このコマンドは、すべてのウィンドウがフローティング ウィンドウは、し、フレーム ウィンドウ内でそれらを制限します。 この動作は、ドッキング モードを導入する前に、WinDbg の動作をエミュレートします。

デュアル モニターを使用している場合は、1 つのモニターと、それ以外の追加の dock に WinDbg ウィンドウを配置できます。

さまざまなデバッグ シナリオのいくつかの標準ウィンドウ配置は、Windows のツールをデバッグ パッケージに含まれます。 これらの並べ替え方法について詳しくは、次を参照してください。 [WinDbg テーマのカスタマイズの使用と](using-and-customizing-windbg-themes.md)します。

 

 




