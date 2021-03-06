---
title: Visual Studio でのソース コードのデバッグ
description: プロシージャでは、Visual Studio でソース コードのデバッグについて説明します。
ms.assetid: C2E5BAA8-913A-4B0E-8ADF-E2758CCFEC84
ms.date: 05/11/2018
ms.localizationpriority: medium
ms.openlocfilehash: 1e85abe6cefa91d4e2b2fb2bc01cebcd3f426f6b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67369460"
---
# <a name="source-code-debugging-in-visual-studio"></a>Visual Studio でのソース コードのデバッグ

> [!IMPORTANT]
> この機能は、Windows 10 バージョン 1507、以降のバージョンの WDK でご利用いただけません。
>

このトピックで示す手順では、Visual Studio に統合された Windows Driver Kit が必要です。 統合環境を取得するには、最初に、Microsoft Visual Studio をインストールし、Windows Driver Kit (WDK) をインストールします。 詳細については、次を参照してください。 [Windows ドライバー開発](https://docs.microsoft.com/windows-hardware/drivers/)します。

使用するソースのデバッグ、する必要がありますが、コンパイラまたはリンカーのシンボル ファイル (.pdb ファイル) を作成、バイナリが構築されます。 これらのシンボル ファイルは、バイナリの命令がソース行に対応させる方法をデバッガーに表示します。 また、デバッガーは、実際のソース ファイルにアクセスできる必要があります。 詳細については、次を参照してください。[ソース パス](source-path.md)します。

対象のコンピューターに侵入するか、ターゲット コンピューターで実行されているコードがブレークポイントにヒットされると、Visual Studio は、ソース ファイルが見つかった場合のソース コードを表示します。 いずれかを選択して、ソース コードをステップスルー、**手順**からコマンドを**デバッグ**メニュー。 ソース ウィンドウの左の列をクリックして、ブレークポイントを設定することもできます。 次のスクリーン ショットでは、Visual Studio デバッガーでソース コード ウィンドウを示しています。

![visual studio デバッガーでのソース コードのスクリーン ショット](images/sourcecodedebuggingvs01.png)

 

 





