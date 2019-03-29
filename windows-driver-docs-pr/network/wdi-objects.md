---
title: Wi-fi デバイス モデルとオブジェクト
description: Wi-fi デバイスは、オブジェクトのアダプターとポートの 2 種類のコンテキストでのホストによって使用されます。
ms.assetid: 0F375ED7-CB20-4F32-8ECE-4822D7787327
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6464ee4e0c5a2f7820382b710cd230b1a1caa990
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56538834"
---
# <a name="wi-fi-device-model-and-objects"></a>Wi-fi デバイス モデルとオブジェクト


Wi-fi デバイスは、2 種類のオブジェクトのコンテキストではホストによって使用されます。 アダプターとポート。

![wdi デバイス モデル](images/wdi-object-model.png)

## <a name="adapter"></a>アダプタ


アダプター オブジェクトでは、Wi-fi デバイスで Wi-fi 機能を表します。 コマンド、示しているのでは、このオブジェクトは、Wi-fi インターフェイスに関する状態を示すために使用されます。 Wi-fi の複数のデバイスでシステムの場合は、各アダプター オブジェクトは、別のインスタンスを表します。

## <a name="port"></a>ポート


1 つの Wi-fi アダプターに対して同時に使用複数の接続などのインフラストラクチャのクライアントと Wi-Fi Direct グループの所有者。 このような各接続に関連付けられた状態を示すポート オブジェクトが使用されます。 各ポート、接続の MAC の状態と保持 phy 状態の接続に特定します。

アダプターで複数のポートがあります。 ポートで発行されたコマンドには、そのポートの管理状態のみに影響します。

オペレーティング システムでは、802.11 のステーション、Wi-Fi Direct クライアント、または Wi-Fi Direct グループの所有者などの操作モードと各ポートを構成します。 指定されたポートで処理するために、ファームウェアを準備する必要があります set コマンドは、操作モードとポートの状態によって決定されます。 2 つの状態のいずれかで、ポートを指定できます。INIT と場合 最初に INIT 状態と、オペレーティング システム (クライアントのインフラストラクチャ) の場合に接続する、またはアジア太平洋/移動を開始するコマンドを発行する場合にのみ OP 状態に移行するポート。 ポートを INIT に返します状態[OID\_WDI\_タスク\_DOT11\_リセット](https://msdn.microsoft.com/library/windows/hardware/dn925952)IHV コンポーネントに送信されます。

## <a name="port-availability-requirements"></a>ポートの可用性の要件


| ポートの種類                        | 必要な数        |
|----------------------------------|-----------------------|
| ステーションのポート                     | 1                     |
| Wi-Fi Direct デバイス              | (サポートされている) 場合は 1      |
| Wi-Fi Direct ロール (GO またはクライアント) | 1 または 2 (サポートされている) 場合 |

 

## <a name="port-concurrency-requirements"></a>同時実行のポートの要件


別のポートの種類を次の同時実行要件は次のとおりです。

1.  1 ステーションのポートは常に使用できます。
2.  Wi-Fi Direct デバイス 1 のポートは常に使用できます。
3.  Wi-Fi Direct ロールの 2 つのポートは、次の構成で使用できます。
    1.  1 を移動します。
    2.  1 つのクライアント
    3.  1 に移動して、1 つのクライアント

 

 




