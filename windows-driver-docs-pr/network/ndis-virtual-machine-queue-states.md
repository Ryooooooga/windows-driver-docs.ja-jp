---
title: NDIS 仮想マシン キューの状態
description: NDIS 仮想マシン キューの状態
ms.assetid: 69a301ac-71f4-4591-80ff-356c32187aa8
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ad6d98f0fbe865471f6e792db96dd29362c023cf
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63369037"
---
# <a name="ndis-virtual-machine-queue-states"></a>NDIS 仮想マシン キューの状態





このトピックでは、NDIS 仮想マシン キュー (VMQs) の操作状態の概要を示します。 キューの状態の詳細については、次を参照してください。、[キューの状態と操作](queue-states-and-operations.md)でトピック、[書き込み VMQ ドライバー](writing-vmq-drivers.md)セクション。

キューごとにネットワーク アダプターは、次の操作状態のセットをサポートする必要があります。

-   未定義

-   割り当てられました。

-   Set

-   一時停止

-   実行中

-   DMA を停止します。

-   解放します。

次の図は、これらの状態間の関係を示します。

![ndis vm キューの状態とイベントを示す図します。](images/queuestate.png)

次に、アダプターの状態を定義します。

<a href="" id="undefined"></a>未定義  
*未定義*はキューの初期状態です。 この状態では、キューは割り当てられません。 ミニポート ドライバーは、キューの割り当て要求を受信するまで、(常に存在する既定のキュー) を除く、キューは定義されません。 また、これは定義されません解放操作が完了し、いずれかが表示される起動したことを示すものが完了です。

<a href="" id="allocated"></a>割り当てられました。  
キューは、*割り当て済み*状態、割り当て要求の後、およびが前にすべてのフィルターをキューに設定します。 フィルターは、状態の設定に、キューがあり、キューの最後のフィルターがオフになっている場合にも、割り当てられている状態に入力できます。 ミニポート ドライバーは、ミニポート ドライバーが割り当てられている状態に割り当ての完全な要求を受信した場合、キューは一時停止状態になります。 ミニポート ドライバーは、無料のキューの要求を受信した場合、キューは DMA の停止状態になります。

<a href="" id="set"></a>設定  
*設定*状態では、キューが割り当てられていると、少なくとも 1 つのフィルターがキューに設定が、ミニポート ドライバーでは、割り当ては受信しませんでした OID をまだ完了します。 キューは、割り当ての完全な要求を受信した場合、実行中の状態を入力します。 キューの最後のフィルターをオフにした場合、キューは割り当てられている状態になります。 キューにフィルターのセットがあるときに、キューを解放することはできませんに注意してください。

<a href="" id="paused"></a>一時停止  
*Paused*状態では、キューが割り当てられますが、キューに設定されているフィルターが存在しないため、ミニポート ドライバーは受信したパケットを示しません。 ミニポート ドライバーは、割り当て済み状態から、または実行中の状態から一時停止状態を入力できます。 キューは、フィルターのセット要求を受信すると、実行中の状態を入力します。 無料のキューの要求を受信すると、キューは DMA の停止状態になります。

<a href="" id="running"></a>実行しています。  
*を実行している*状態キューにフィルターを設定、キューの割り当てが完了したら、およびネットワーク アダプターでは、パケットの受信を示します。 キューの最後のフィルターをオフにした場合、キューは一時停止状態になります。 キューにフィルターのセットがあるときに、キューを解放することはできませんに注意してください。 また、最後のフィルターがオフの場合は、ミニポート ドライバーは、DMA を停止できます。 しかし、ミニポート ドライバーでは、DMA が停止状態の表示がここでは送信しない必要があります。

<a href="" id="stop-dma"></a>DMA を停止します。  
*停止 DMA*状態では、ミニポート ドライバーが無料のキューの要求を受信し、DMA アクティビティを停止する必要があります。 ミニポート ドライバーでは、DMA が停止状態の表示を送信する必要があります。 ミニポート ドライバーが、状態を示す値を送信した後、キューは、解放状態です。 最後のフィルターがオフにすると、DMA が停止おそらく既にことに注意してください。 ただし、ミニポート ドライバーのみを送信する状態の表示、無料のキューの要求を受信するとします。

<a href="" id="freeing"></a>解放します。  
*解放*状態では、ミニポート ドライバーが、未処理のすべての受信を完了にキューに表示するを待機していると、キューに関連付けられているリソースを解放します。 すべてのリソースを解放すると、キューが定義されていない状態になります。

 

 





