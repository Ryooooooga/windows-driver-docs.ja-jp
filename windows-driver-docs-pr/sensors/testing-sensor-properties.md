---
title: テストのセンサー データの取得
description: センサー診断ツールを使用して、センサー API でのプロパティを呼び出すことによってデータの取得については、ドライバーとファームウェアのサポートをテストできます。
ms.assetid: A4473253-D4AC-4374-9C5D-919B597FE2F0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3f4d898ff9b4c5983cf4321671cc6fc4460057d7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56527961"
---
# <a name="testing-sensor-data-retrieval"></a>テストのセンサー データの取得


センサー診断ツールを使用して、センサー API でのプロパティを呼び出すことによってデータの取得については、ドライバーとファームウェアのサポートをテストできます。
 

## <a name="configuring-the-sensor-diagnostic-tool-to-retrieve-a-single-sensor-reading"></a>1 つのセンサーからのデータを取得するセンサー診断ツールを構成します。


次の手順では、加速度計の読み取りを取得する診断ツールを構成する方法について説明します。

1.  加速度計センサーの左側のウィンドウでのノードを展開します。 チェック、**接続済み**ボックスにオフにし、**サブスクライブ済み**ボックス。
2.  加速度計を回転し、場所に保持します。
3.  をクリックして、**更新データ/実行**ボタンをクリックし、右側のウィンドウの [データ] セクションで取得したデータを表示します。

右側のウィンドウの [データ] セクションには、センサーの更新されたデータが含まれています。 このデータは、加速度計の静的な位置に対応する必要があります。

## <a name="configuring-the-sensor-diagnostic-tool-for-synchronous-polling"></a>センサー診断ツールの同期のポーリングを構成します。


次の手順では、加速度計の同期のポーリングを実行する診断ツールを構成する方法について説明します。 つまり、これにより、センサーからの読み取りは、一定の間隔でデータを取得することです。

1.  加速度計センサー左側のノードを展開します。チェック、**接続済み**ボックスにオフにし、**サブスクライブ済み**ボックス。
2.  **要求データの自動** ボックスに、ミリ秒単位で、目的のポーリング間隔を入力します。 (0 の間隔が同期のポーリングを無効になるに注意してください)。

右側のペインのデータ セクションは、ポーリング済みデータを表示する開始されます。 加速度計を移動すると、このウィンドウの新しい値が表示されます。

ポーリングされたセンサー データを CSV ファイルにログインすることができます。 参照してください、[センサー イベントのテスト](testing-sensor-events.md)トピックとこれを行う方法の詳細については、「CSV ファイルにログ記録イベントのデータ」セクション。

データが使用して、ツールのデータ セクションに表示する必要がありますを指定することができます、 **Datafield**右側のウィンドウでコントロールの 2 つ目の行に表示されたドロップダウン リスト。

## <a name="related-topics"></a>関連トピック
[センサーの機能をテストします。](testing-sensor-functionality.md)  
[テストのセンサー プロパティのサポート](testing-and-logging-sensor-data.md)  
[テストのセンサー イベント](testing-sensor-events.md)  


