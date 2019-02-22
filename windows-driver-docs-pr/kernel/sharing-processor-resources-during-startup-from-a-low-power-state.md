---
title: 低電力状態から起動中にプロセッサ リソースの共有
description: 低電力状態から起動中にプロセッサ リソースの共有
ms.assetid: 2b2e6a1b-7c2d-4f38-9407-a417b75daa6a
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: c6faa61189f36e60c0692bc99cf643a5b8fa4427
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529722"
---
# <a name="sharing-processor-resources-during-startup-from-a-low-power-state"></a>低電力状態から起動中にプロセッサ リソースの共有


コンピューターがスタンバイ状態または休止状態 (ウォーム起動) から開始されると、ドライバーは必要がありますよりも長い期間のプロセッサ リソースの使用を避ける必要があります。 最も重要なは、遅延プロシージャ呼び出し (DPC) のルーチンと IRQL で実行されるコード&gt;= ディスパッチ\_レベルは、実行時間を最小限に抑える必要があります。 ドライバーでは、DPC ルーチンを使用してデバイスを初期化します。 ドライバーは、ディスパッチに初期化コードを実行する必要があります\_ポート ミニポート インターフェイス コントラクトの一部としてのレベル。

DPC ルーチンの実行中には、他のスレッド優先順位の低いが、同じプロセッサで実行されているからブロックされます。 さらに、現在の DPC が完了するまで、その他のキューに置かれ、実行する準備ができている DPC ルーチンがブロックされます。 臨機応変に実行するには、他のスレッドを有効にするには、一般的な DPC ルーチンに 100 件未満 (マイクロ秒) の実行する必要があります。

システムの起動時に長時間実行される DPC ルーチンには、他のデバイスの初期化を遅らせることができます。 この遅延は、オペレーティング システムによって、デバイスの初期化フェーズが長いと遅延起動完了をにより、します。

DPC ルーチンを設計するのにには、次のベスト プラクティスを使用します。

-   1 つの DPC ルーチンはする必要がありますの 100 を超える (マイクロ秒) は実行されません。

-   DPC ルーチンを呼び出す、 [ **KeStallExecutionProcessor** ](https://msdn.microsoft.com/library/windows/hardware/ff553295)実行を遅延させるルーチンが 100 を超えるマイクロ秒の遅延を指定する必要があります。

-   タスクが 100 マイクロ秒を超える必要があり、ディスパッチで実行されるかどうか\_レベル、DPC ルーチンが 100 マイクロ秒後に終了およびは後でタスクを完了する 1 つまたは複数の DPC タイマー ルーチンをスケジュールします。

-   DPC ルーチンの実行時間を評価する WDK で説明されているパフォーマンス分析ツールを使用します。

パフォーマンス分析ツールの詳細については、次を参照してください。 [Windows Vista でのシステム再開パフォーマンスの測定](https://go.microsoft.com/fwlink/p/?linkid=69964)します。

 

 



