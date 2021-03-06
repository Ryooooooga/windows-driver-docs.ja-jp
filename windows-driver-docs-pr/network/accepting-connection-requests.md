---
title: 接続要求の受け入れ
description: 接続要求の受け入れ
ms.assetid: 2233daa7-c5c5-49be-b76e-61a90a496447
keywords:
- SAN 接続のセットアップ WDK、接続要求の受け入れ
- 受信接続要求が WDK San
- セッションのネゴシエーション WDK San
- リモート ピアの接続要求が WDK San
- WDK の San を要求の接続を受け付ける
- SAN 接続要求を拒否しています
- SAN 接続要求を拒否しています
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e4a3b820419ea71cf26d948819ea54b5df39423f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67378721"
---
# <a name="accepting-connection-requests"></a>接続要求の受け入れ





アプリケーションを呼び出す場合、 **WSAAccept**、**受け入れる**、または**AcceptEx**ソケットの受信接続要求を受け入れるように関数を Windows ソケットは常に切り替えるTCP/IP サービス プロバイダーには、この呼び出しを転送します。 SAN 以外のネットワークから受信接続要求が到着すると、NDIS パスを通過し、TCP/IP サービスのプロバイダーを処理します。 スイッチは、TCP/IP サービス プロバイダーと接続要求を受け入れるかどうかを判断して、アプリケーションのを完了するためにSANサービスプロバイダー間の媒介として機能する場合は、SANでリモートピアからの接続要求を受信した、**WSAAccept**、**受け入れる**、または**AcceptEx**関数。

次の図は、受け入れるか、受信接続要求を拒否するかどうかを決定する Windows Sockets スイッチと SAN サービス プロバイダー間の相互作用の概要を示します。 シーケンスと次のセクションには、さらに詳しく承認決定が説明します。

![windows ソケットのスイッチと san サービス プロバイダー間の相互作用の図の概要](images/apiflow5.png)

 **接続要求を承認または拒否**

1.  」の説明に従って、リモート ピアからの受信接続要求を受け取る SAN サービス プロバイダーがイベント オブジェクトを通知[SAN 上の接続のリッスン](listening-for-connections-on-a-san.md)します。

2.  Windows ソケットは、SAN サービス プロバイダーの呼び出しを切り替える[ **WSPEnumNetworkEvents** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff566284(v=vs.85))関数に、FD\_ACCEPT イベント コード。

3.  受信する、FD\_ACCEPT イベント コードでは、スイッチを呼び出す SAN サービス プロバイダーの[ **WSPAccept** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff566266(v=vs.85))関数の着信接続要求を承認または拒否します。

4.  スイッチの SAN サービス プロバイダーの呼び出しで[ **WSPAccept** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff566266(v=vs.85))関数、スイッチは、条件関数を指定します。 SAN サービス プロバイダーが同じスレッドでこの条件関数を呼び出す必要があります、 **WSPAccept**から戻る前に関数が呼び出された、 **WSPAccept**呼び出します。

5.  スイッチは、CF を返します\_ACCEPT または CF\_を受け入れるか、それぞれに、接続要求を拒否したことを示すためには、この条件関数からコードを拒否します。

### <a name="accepting-a-connection-request-and-creating-an-accepting-socket"></a>接続要求を受け入れると、受け入れソケットを作成します。

アプリケーションが、受信接続要求を受け入れる場合、スイッチは、CF を返します\_スイッチの条件の機能を完了する SAN サービス プロバイダーへの同意コード。 受信する CF\_受け入れるには、SAN サービス プロバイダーが受け入れソケットに関する情報が格納する内部データ構造を初期化します。 SAN サービス プロバイダーの[ **WSPAccept** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff566266(v=vs.85))関数は次に呼び出す必要があります、 **WPUCreateSocketHandle**スイッチからソケットを受け入れる記述子を取得する関数. SAN サービス プロバイダーが受け入れ元のソケットの場合は、その内部データ構造でスイッチの記述子を格納する必要があるし、受け入れ元のソケットを完了するための固有の記述子を返す必要があります、 **WSPAccept**呼び出します。 スイッチは、SAN サービス プロバイダーは、スイッチへの呼び出しをでスイッチのソケット記述子を指定する必要があります中に、サービスのプロバイダーの機能を SAN を呼び出すときに、受け入れ元のソケットの SAN サービス プロバイダーの内部の記述子を指定する必要があります。

正常に完了する前に[ **WSPAccept**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff566266(v=vs.85))、SAN サービス プロバイダーは、Win32 を呼び出す必要があります**ResetEvent**イベント オブジェクトをリセットする機能。 により、Win32 の後で呼び出す SAN サービス プロバイダーを行って**SetEvent**を次の受信接続要求を受け入れるへの切り替えを通知します。

### <a name="rejecting-a-connection-request"></a>接続要求を拒否しています

アプリケーションでは、受信接続要求を拒否する場合、スイッチは、CF を返します\_スイッチの条件の機能を完了する SAN サービス プロバイダーにコードを拒否します。 CF を受け取る\_REJECT、SAN サービス プロバイダー返す必要があります使いますエラー コードを完了するスイッチに、 [ **WSPAccept** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff566266(v=vs.85))呼び出します。

### <a name="indicating-acceptance-or-refusal-of-a-connection-request-to-a-remote-peer"></a>受け入れまたは拒否するリモート ピアの接続要求を示す

SAN サービス プロバイダーは、受け入れるか、リモート ピアの接続要求を拒否したこと、リモート ピアを指定できます、前に、SAN サービス プロバイダーは、スイッチの条件の関数を呼び出す必要があります。 スイッチの条件の関数によって返される値、によって SAN サービス プロバイダーへを作成する次の問題のいずれかのリモート ピア。

スイッチの条件の関数は、CF を返す場合\_受け入れるには、SAN サービス プロバイダーがリモート ピアの接続要求を受け入れることを示す必要があります。 リモート ピアの SAN サービス プロバイダーによって開始された接続操作を正常に完了できますし、 [ **WSPConnect** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff566275(v=vs.85))呼び出します。

スイッチの条件の関数は、CF を返す場合\_REJECT、SAN サービス プロバイダーが示されます、リモート ピアの接続要求を拒否したことです。 リモート ピアの SAN サービス プロバイダーによって開始された接続操作が失敗する必要があります、 [ **WSPConnect** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff566275(v=vs.85))使いますエラー コードを呼び出します。

### <a name="session-negotiation"></a>セッションのネゴシエーション

スイッチで SAN サービス プロバイダーを使用すると、リモート ピアからの接続要求を受け入れるが正常に、スイッチは、そのピアとのセッションをネゴシエートします。

 **セッションをネゴシエートするには**

1.  リモート ピアにあるスイッチ呼び出し SAN サービス プロバイダーの[ **WSPRecv** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff566309(v=vs.85))受信バッファーのセットを投稿する関数。

2.  リモート ピアにあるスイッチ呼び出し SAN サービス プロバイダーの[ **WSPSend** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff566316(v=vs.85))ローカル受け入れ側のエンドポイントでスイッチにセッションのネゴシエーション メッセージを送信します。 このメッセージには、スイッチ、リモート ピアにポストされた受信バッファーの数が含まれています。

3.  ローカルの受け入れ側のエンドポイントにあるスイッチ呼び出しのローカルの SAN サービス プロバイダーの[ **WSPRecv** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff566309(v=vs.85))独自に投稿する関数の受信バッファーしますが、セッションを受信するまでの時間で実行できない可能性がありますネゴシエーション メッセージ。 -Local スイッチが時間の受信バッファーを投稿していない場合、SAN サービス プロバイダーでローカルの受け入れに基になる NIC がフロー制御をサポートしていない場合、エンドポイントは、独自のプライベートの受信バッファーでリモート スイッチのセッションのネゴシエーション メッセージをバッファーする必要があります。 スイッチの投稿では、バッファーを受信、SAN サービス プロバイダーからデータをコピー プライベート受信バッファーが、一対一のスイッチのバッファーにすべてのデータがコピーされるまで、プライベート バッファーからスイッチのバッファー。

    SAN サービス プロバイダーは通常の受信 - 以降のスイッチのバッファーで処理を実行する、NIC の受信キューにこのようなすべてのスイッチ バッファーのポストバック

    注こと SAN サービス プロバイダーする必要があります、接続を単純に削除しないため、セッションのネゴシエーション メッセージが到着する前に、スイッチは、受信バッファーを通知できませんでした。 セッションのネゴシエーション メッセージの最大長は 256 バイトです。

4.  ローカルの受け入れ側のエンドポイントにあるスイッチは、セッションのネゴシエーション メッセージに応答する前に、受信バッファーを投稿します。 -Local スイッチは、ローカルの SAN サービス プロバイダーを呼び出して[ **WSPSend** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff566316(v=vs.85))セッションのネゴシエーション メッセージに応答する関数。 -Local スイッチの応答には、ローカルのスイッチが投稿された受信バッファーの数が含まれています。 これ以降は、-local スイッチは、受信バッファーのポストされたセットが接続で受信するすべてのメッセージを受信するための十分なサイズのことを保証します。

5.  アプリケーションで、当初の受信バッファーを指定する場合、 **AcceptEx**呼び出し、アプリケーションを完了する前にそのリモート ピアからのデータの最初のメッセージを受信するまでに、スイッチが待機する**AcceptEx**呼び出します。

6.  独自のアプリケーションをキャンセルした場合**受け入れる**、スイッチが呼び出される適切なの SAN サービス プロバイダーの[ **WSPCloseSocket** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff566273(v=vs.85))関数を受け入れ側の SAN のソケットを閉じる.

 

 





