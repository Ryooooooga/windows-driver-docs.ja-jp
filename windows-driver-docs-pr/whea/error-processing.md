---
title: エラー処理
description: エラー処理
ms.assetid: d9cb2f62-1ccf-4ab6-b547-dc54f6d07820
keywords:
- Windows ハードウェア エラー アーキテクチャ WDK では、エラー処理
- WHEA WDK では、エラー処理
- ハードウェア エラー WDK の WHEA エラー処理
- エラー WDK の WHEA エラー処理
- 修正されたエラー WDK WHEA
- WDK WHEA 未修正のエラー
- ハードウェアの致命的なエラー WDK WHEA
- WDK WHEA の致命的でないハードウェア エラー
- 低レベル ハードウェア エラー ハンドラー WDK WHEA
- LLHEHs WDK WHEA
- プラットフォーム固有のハードウェア エラー ドライバー WDK WHEA
- PSHED WDK WHEA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 59302d85710f1e3ad39c409016e894c79457f691
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67362590"
---
# <a name="error-processing"></a>エラー処理


Windows ハードウェア エラー アーキテクチャ (WHEA) は、エラー状態の分類に応じて異なる方法でハードウェア エラーを処理します。 ハードウェア エラーのさまざまな分類の詳細については、次を参照してください。[ハードウェア エラーとエラーのソース](hardware-errors-and-error-sources.md)します。

ハードウェア エラー条件の種類ごとに応答 WHEA によって実行されたアクションのシーケンスを次に示します。 これらのアクションで参照される WHEA コンポーネントの詳細については、次を参照してください。[コンポーネント、Windows Hardware Error Architecture の](components-of-the-windows-hardware-error-architecture.md)します。

### <a name="corrected-hardware-error"></a>**修正されたハードウェア エラー**

1.  *低レベル ハードウェア エラー ハンドラー* (*LLHEH*) ハードウェアのエラー状態の有無について通知されます。

2.  LLHEH は、ハードウェア エラーの有無を確認します。

3.  LLHEH では、エラーの発生元からハードウェアのエラー情報を取得し、エラー データを使用して、ハードウェアのエラー パケットを入力します。 このパケットとして書式設定、 [WHEA\_エラー\_パケット](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff560465(v=vs.85))構造体。

4.  呼び出しを LLHEH、*プラットフォーム固有のハードウェア エラー ドライバー* (PSHED) 任意のプラットフォーム固有のハードウェア エラー情報を取得します。 PSHED のプラグインがインストールされているし、場合エラー情報の取得、PSHED で参加に登録されているは順番がさらにそのようにプラグイン PSHED への呼び出しを強化、LLHEH に返されるエラー情報。

5.  LLHEH エラー パケットを渡して、Windows オペレーティング システム カーネルを呼び出します。

6.  Windows カーネルの作成、[エラー レコード](error-records.md)LLHEH から受信したエラー パケットからの情報と、エラーの重大度、エラー ソースなど、エラーに関する他の情報を使用して入力して、エラーが発生した回数。

7.  Windows カーネルへの呼び出し、PSHED にエラー レコードにセクションを追加するよう PSHED を許可します。 PSHED のプラグインがインストールされているし、場合エラー情報の取得、PSHED で参加に登録されているはさらに PSHED がさらにそのようにプラグインへの呼び出しを補強エラー レコードの情報。

8.  Windows カーネルへの呼び出し、PSHED にエラーの発生元の状態のレジスタをオフにします。 PSHED のプラグインがインストールされ、さらに、エラー情報の取得、PSHED に参加するが登録されている場合にできるように、プラグインの PSHED 呼び出しオフ エラーの発生元の状態を登録します。

9.  ハードウェア エラーの状態は、エラーの発生元のエラーのしきい値を超えている場合、Windows カーネルは ETW イベントを生成し、システム イベント ログにエラー情報を記録します。

### <a name="nonfatal-uncorrected-hardware-error"></a>**未修正ハードウェアの致命的でないエラー**

1.  ハードウェアのエラー状態の有無について、LLHEH に通知されます。

2.  LLHEH は、ハードウェア エラーの有無を確認します。

3.  LLHEH では、エラーの発生元からハードウェアのエラー情報を取得し、エラー データを使用して、ハードウェアのエラー パケットを入力します。

4.  任意のプラットフォーム固有のハードウェア エラー情報を取得、PSHED に LLHEH 呼び出し。 PSHED のプラグインがインストールされているし、場合エラー情報の取得、PSHED で参加に登録されているは順番がさらにそのようにプラグイン PSHED への呼び出しを強化、LLHEH に返されるエラー情報。

5.  LLHEH エラー パケットを渡して、Windows オペレーティング システム カーネルを呼び出します。

6.  Windows カーネルの作成、[エラー レコード](error-records.md)LLHEH から受信したエラー パケットからの情報と、エラーの重大度、エラー ソースなど、エラーに関する他の情報を使用して入力して、エラーが発生した回数。

7.  Windows カーネルへの呼び出し、PSHED にエラー レコードにセクションを追加するよう PSHED を許可します。 PSHED のプラグインがインストールされているし、場合エラー情報の取得、PSHED で参加に登録されているはさらに PSHED がさらにそのようにプラグインへの呼び出しを補強エラー レコードの情報。

8.  Windows カーネルは、ハードウェア エラーの状態を解決しようとして、エラーから回復しようとします。 Windows カーネルは、必要な復旧操作を実行する機会を提供するよう PSHED に呼び出します。 PSHED のプラグインがインストールされへの参加、PSHED は、エラーの回復に PSHED プラグインへの呼び出しエラーを修正または完全に必要な追加の操作を実行するようにが登録されている場合は、エラー条件から回復します。

9.  ハードウェア エラーが修正された正常 Windows カーネルは ETW イベントを生成し、システム イベント ログにエラー情報を記録します。 ハードウェア エラーが正しくない場合、Windows カーネルは、エラー レコードを保存するよう PSHED を呼び出します。 PSHED のプラグインがインストールされ、エラー レコードの永続化に参加するが登録されている場合、PSHED はさらに、PSHED への呼び出しプラグイン エラー レコードを保存できるようにします。 エラー レコードを保存した後、Windows カーネルにバグ チェックが生成されます。

### <a name="fatal-uncorrected-hardware-error"></a>**未修正ハードウェアの致命的なエラー**

1.  ハードウェアのエラー状態の有無について、LLHEH に通知されます。

2.  LLHEH は、ハードウェア エラーの有無を確認します。

3.  LLHEH では、エラーの発生元からハードウェアのエラー情報を取得し、エラー データを使用して、ハードウェアのエラー パケットを入力します。

4.  任意のプラットフォーム固有のハードウェア エラー情報を取得、PSHED に LLHEH 呼び出し。 PSHED のプラグインがインストールされているし、場合エラー情報の取得、PSHED で参加に登録されているは順番がさらにそのようにプラグイン PSHED への呼び出しを強化、LLHEH に返されるエラー情報。

5.  LLHEH エラー パケットを渡して、Windows オペレーティング システム カーネルを呼び出します。

6.  Windows カーネルの作成、[エラー レコード](error-records.md)LLHEH から受信したエラー パケットからの情報と、エラーの重大度、エラー ソースなど、エラーに関する他の情報を使用して入力して、エラーが発生した回数。

7.  Windows カーネルへの呼び出し、PSHED にエラー レコードを保存します。 PSHED のプラグインがインストールされ、エラー レコードの永続化に参加するが登録されている場合、PSHED はさらに、PSHED への呼び出しプラグイン エラー レコードを保存できるようにします。

8.  Windows カーネルには、バグ チェックが生成されます。

 

 




