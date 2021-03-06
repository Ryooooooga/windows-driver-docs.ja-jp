---
title: UDP ESP SA およびパーサー エントリ
description: UDP ESP SA およびパーサー エントリ
ms.assetid: 1682b077-07ba-4b2e-9c01-fd7662f3f189
keywords:
- WDK の IPsec ESP パケットを UDP カプセル化オフロード、パーサーのエントリ
- パーサーのエントリの WDK IPsec オフロード
- WDK の IPsec ESP パケットを UDP カプセル化オフロード、セキュリティ アソシエーション
- セキュリティ アソシエーション WDK IPsec オフロードします。
- SAs の WDK IPsec オフロード
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4f9eb2cd03a893a4287c796dcc93eb6248501863
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355440"
---
# <a name="udp-esp-sas-and-parser-entries"></a>UDP ESP SA およびパーサー エントリ

\[IPsec タスク オフロード機能は非推奨し、は使用できません。\]




UDP ESP カプセル化をサポートしているミニポート ドライバーでは、パーサーのエントリの一覧を保持する必要があります。 パーサーのエントリには、NIC にオフロードされたセキュリティ アソシエーション (Sa) に対して受信 UDP ESP パケットの解析に必要な情報が含まれています。

パーサーのエントリには、次の情報が含まれています。

-   UDP ESP カプセル化の種類。

    現時点では、1 つだけのカプセル化の種類がサポートされています。 基本的な UDP ESP カプセル化型の説明は、次を参照してください。 [UDP ESP カプセル化型](udp-esp-encapsulation-types.md)します。

-   接続先のカプセル化ポート。

    NIC は、オフロードされた SAs で処理される受信の UDP カプセル化パケットの UDP ヘッダーの宛先ポートを探してください。 現時点では、ESP パケットの UDP カプセル化は、ポート 4500 でのみサポートされます。

TCP/IP トランスポートは、負荷がミニポート ドライバーにオフロードするパーサー エントリのリストを保持しています。 追加または削除 UDP ESP SA、トランスポートおよびミニポートのドライバーは、パーサーが特定のエントリを識別するために、ハンドルを使用します。

必要に応じて、さまざまなカプセル化の種類やカプセル化の種類ごとに 1 つ以上のポートに対応するパーサーのエントリを UDP ESP 機能拡張するで許可することに注意してください。

### <a name="adding-a-udp-esp-sa-and-parser-entry"></a>UDP ESP SA とパーサーのエントリを追加します。

TCP/IP トランスポートは要求を発行して、これらの SAs の 1 つまたは複数の UDP ESP SAs とパーサーのエントリを追加するためのミニポート ドライバー、 [OID\_TCP\_タスク\_IPSEC\_追加\_UDPESP\_SA](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-task-ipsec-add-udpesp-sa)要求。 **EncapTypeEntry** 、オフロードのメンバー\_IPSEC\_追加\_UDPESP\_SA 構造体には、パーサーのエントリの情報が含まれています。

OID を発行する前に\_TCP\_タスク\_IPSEC\_追加\_UDPESP\_SA 要求、TCP/IP トランスポートは、オフロードされている SAs のパーサーのエントリがかどうかを決定しますその。指定された IP インターフェイスのパーサー エントリの一覧。

-   トランスポートが独自のエントリとセットのコピーを作成、トランスポートの一覧で、パーサーのエントリがない場合、 **EncapTypeEntryOffloadHandle** 、オフロードのメンバー\_IPSEC\_追加\_UDPESP\_SA の構造体を**NULL**します。 トランスポートは、発行、 [OID\_TCP\_タスク\_IPSEC\_追加\_UDPESP\_SA](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-task-ipsec-add-udpesp-sa)要求。 要求を受信した後、ミニポート ドライバーを決定するかどうか、パーサーのエントリを**EncapTypeEntry** NIC のパーサー エントリの一覧には、指定しました。

    -   ミニポート ドライバーがカプセル化の種類を使用して、パーサーのエントリを作成しで指定された宛先ポート、NIC のパーサー エントリの一覧に指定されたパーサーのエントリがない場合**EncapTypeEntry** NIC にパーサーのエントリを追加します。パーサーのエントリの一覧。 ミニポート ドライバーが、OID で指定された SAs をオフロードし\_TCP\_タスク\_IPSEC\_追加\_UDPESP\_SA 要求。 OID 要求を正常に完了した後は、ミニポート ドライバーのハンドルを返します。 **EncapTypeEntryOffloadHandle**パーサーを新しく作成されたエントリを識別します。 ミニポート ドライバーもでオフロードされた SAs を識別するハンドルを返します、 **OffloadHandle** 、オフロードのメンバー\_IPSEC\_追加\_UDPESP\_SA 構造体。
    -   ミニポート ドライバーがだけでハンドルを返しますパーサーの指定したエントリが、NIC のパーサー エントリの一覧に既に場合**EncapTypeEntryOffloadHandle**の既存のパーサー エントリ。 ミニポート ドライバーもでオフロードされた SAs を識別するハンドルを返します、 **OffloadHandle** 、オフロードのメンバー\_IPSEC\_追加\_UDPESP\_SA 構造体。

    ミニポート ドライバーには、OID が完了すると\_TCP\_タスク\_IPSEC\_追加\_UDPESP\_SA の要求を正常には、トランスポート、新しいパーサーのエントリのコピーを独自のパーサー エントリに追加します特定の IP インターフェイスの一覧です。 さらに、トランスポートは、いずれかでパーサー エントリの参照カウントをインクリメントします。 トランスポートの使用数のオフロード UDP ESP SAs を列挙するには、この参照カウントは、パーサーのエントリに関連付けられます。

    ミニポート ドライバーが失敗すると、OID\_TCP\_タスク\_IPSEC\_追加\_UDPESP\_SA 要求、トランスポートは、パーサーのエントリのコピーを破棄します。 ミニポート ドライバーには、このような要求が失敗した場合、ことが、実際には、パーサーのエントリを追加し、SAs をオフロード、ことを確認する必要があります。

-   パーサーのエントリのトランスポートのパーサーのエントリの一覧が既にいる場合、ミニポート ドライバーは既に追加パーサー エントリ前 OID への応答で\_TCP\_タスク\_IPSEC\_追加\_UDPESP\_SA 要求。 セットによって、トランスポートがパーサー エントリの参照カウントをインクリメントするこの例では、 **EncapTypeEntryOffloadHandle**ミニポート ドライバーが以前に返される値にします。 トランスポートが、OID を発行\_TCP\_タスク\_IPSEC\_追加\_UDPESP\_SA 要求が要求される追加の SAs のパーサーの既存のエントリを使用するミニポート ドライバーオフロードされます。 この場合、ミニポート ドライバーを返すだけ、 **OffloadHandle**オフロードされた SAs を識別します。 場合、OID\_TCP\_タスク\_IPSEC\_追加\_UDPESP\_SA 要求が失敗した場合は、パーサーのエントリの参照カウント トランスポートをデクリメントします。

### <a name="deleting-a-udp-esp-sa-and-parser-entry"></a>UDP ESP SA およびパーサーのエントリの削除

TCP/IP トランスポートは要求を発行してこれらの SAs の 1 つ以上の SAs またはパーサーのエントリを削除するミニポート ドライバー、 [OID\_TCP\_タスク\_IPSEC\_削除\_UDPESP\_SA](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-task-ipsec-delete-udpesp-sa)要求。

この要求を発行する前に、TCP/IP は、パーサーのエントリを削除する SAs に関連付けられているは、参照カウントをデクリメントを転送します。 トランスポートは、参照カウントがゼロかどうかをテストします。

-   パーサーのエントリが 1 つまたは複数の他の Sa を NIC にオフロードが現在に関連付けられて、参照カウントがゼロでない場合 この場合は、トランスポートの設定、 **EncapTypeEntryOffldHandle** 、オフロードのメンバー\_IPSEC\_削除\_UDPESP\_SA 構造体を**NULL**. OID を受け取った後\_TCP\_タスク\_IPSEC\_削除\_UDPESP\_SA 要求、ミニポート ドライバーが削除されるだけで、OID で指定されている SAs\_TCP\_タスク\_IPSEC\_削除\_UDPESP\_SA 要求。

-   パーサーのエントリが NIC にオフロードされている他のすべての SAs に関連付けられていない参照カウントがゼロの場合 この場合は、トランスポートの設定、 **EncapTypeEntryOffldHandle**ミニポート ドライバーが以前から返されたパーサー エントリ ハンドルの値のメンバー。 ミニポート ドライバーでは、指定したパーサー エントリと、指定された SAs の両方を削除します。

ミニポート ドライバーが、OID が失敗した場合\_TCP\_タスク\_IPSEC\_削除\_UDPESP\_SA 要求と、指定された SAs をマークする必要があり、必要に応じて、指定したパーサーのエントリ削除し、後で削除を実行します。 着信パケットを処理するには、パーサーのエントリまたは削除対象としてマーク SA ミニポート ドライバーを使用できません。

トランスポートが要求する、SA を削除するミニポート ドライバーまたはミニポート ドライバーの前に、パーサーのエントリ (または両方) の完了 (またはその両方) をその SA またはパーサーのエントリを追加することに注意してください。 ミニポート ドライバーは、加算演算で削除操作をシリアル化したがって必要があります。

 

 





