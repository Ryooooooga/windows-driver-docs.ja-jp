---
title: パケット結合の概要
description: パケット結合の概要
ms.assetid: E406E89C-247B-4DCB-B309-B742BF0A27E9
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 11484f48a4687719c9ca2553d983791aa5483e99
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843728"
---
# <a name="overview-of-packet-coalescing"></a>パケット結合の概要


特定の IP バージョン 4 (IPv4) と IP version 6 (IPv6) のネットワークプロトコルでは、ブロードキャストまたはマルチキャストアドレスにパケットを送信します。 これらのパケットは、IPv4/IPv6 サブネット内の複数のホストによって受信されます。 ほとんどの場合、これらのパケットを受信するホストは、これらのパケットに対して何も実行しません。 そのため、これらの不要なマルチキャストまたはブロードキャストパケットを受信すると、受信ホスト内で不要な処理と電力消費が発生します。

たとえば、ホスト A は、IPv6 サブネット上でマルチキャストリンクローカルマルチキャスト名前解決 (LLMNR) 要求を送信して、ホスト B の名前を解決します。 ホスト A を除き、この LLMNR 要求は、サブネット上のすべてのホストによって受信されます。 ホスト B を除き、他のホスト上で実行される TCP/IP プロトコルスタックはパケットを検査し、パケットが意図したものではないと判断します。 したがって、プロトコルスタックはパケットを拒否し、 [**NdisReturnNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisreturnnetbufferlists)を呼び出してミニポートドライバーにパケットを返します。

NDIS 6.30 以降では、ネットワークアダプターは NDIS パケット合体をサポートできます。 ランダムなブロードキャストまたはマルチキャストパケットの結合によって受信割り込みの数を減らすことで、システムの処理のオーバーヘッドと電力消費が大幅に減少します。

パケット合体には、次の手順が含まれます。

1.  TCP/IP プロトコルスタックなどのその他のドライバーは、ブロードキャストおよびマルチキャストパケットを表示するために使用される NDIS 受信フィルターを定義します。 このドライバーは、パケット合体をサポートする基になるミニポートドライバーにこれらのフィルターをダウンロードします。 ダウンロードが完了すると、ミニポートドライバーは、パケット合体受信フィルターを使用してネットワークアダプターを構成します。

    これらのフィルターの詳細については、「[パケット合体受信フィルター](packet-coalescing-receive-filters.md)」を参照してください。

2.  受信フィルターに一致する受信パケットは、ネットワークアダプター上にキャッシュされるか、または*結合*されます。 アダプターは、結合されたパケットの受信割り込みを生成しません。 代わりに、別のハードウェアイベントが発生したときに、アダプターによってホストが中断されます。

    この割り込みが生成された場合、アダプターは、割り込みを持つ受信イベントを示す必要があります。 これにより、ネットワークアダプターがネットワークアダプターによって受信された、結合されたパケットを処理できるようになります。

    たとえば、パケット合体をサポートするネットワークアダプターは、次のいずれかのイベントが発生したときに受信割り込みを生成できます。

    -   有効期限が一致する受信フィルターの最大合体遅延値に設定されているハードウェアタイマーの有効期限。

    -   ハードウェア合体バッファー内で使用可能な領域が、アダプターによって指定された下限のマークに達します。

    -   結合フィルターに一致しないパケットを受信しました。

    -   送信完了イベントなどの別の割り込みイベントが発生しました。

    このプロセスの詳細については、「[パケット合体受信フィルターの処理](handling-packet-coalescing-receive-filters.md)」を参照してください。

NDIS によるパケット合体のサポートには、次の点が適用されます。

-   NDIS では、物理ネットワークアダプターに割り当てられた既定の NDIS ポート (ポート 0) で受信したパケットのパケット合体がサポートされています。 NDIS では、仮想ネットワークアダプターに割り当てられている NDIS ポートでのパケット合体はサポートされていません。 詳細については、「 [NDIS Ports](ndis-ports.md)」を参照してください。

-   NDIS では、ネットワークアダプターの既定の受信キューで受信したパケットのパケット結合がサポートされています。 この受信キューには、NDIS\_既定\_受信\_キュー\_ID の識別子が設定されています。
