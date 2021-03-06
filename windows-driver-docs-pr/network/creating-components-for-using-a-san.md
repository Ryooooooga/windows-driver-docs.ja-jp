---
title: SAN を使用するためのコンポーネントの作成
description: SAN を使用するためのコンポーネントの作成
ms.assetid: b7405eda-734e-43f0-b0fe-747a06766291
keywords:
- システム エリア ネットワーク WDK、コンポーネントを作成します。
- SAN の WDK、コンポーネントを作成します。
- トランスポートのドライバー WDK San
- WDK の San のデータを転送します。
- WDK の San のデータを転送します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 816d8bd8a2d5969efcd0302169f03f332c1a81bc
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374902"
---
# <a name="creating-components-for-using-a-san"></a>SAN を使用するためのコンポーネントの作成





Windows ソケット アプリケーションは、システム エリア ネットワーク (SAN) を使用してから利用できます。 SAN を使用するには、これらのアプリケーションが SAN サービス プロバイダーの DLL とプロキシ ドライバーをその dll が必要です。

特定の SAN を使用して、データを転送するは SAN に対する信頼性の高いトランスポートを必要も。 信頼性の高いトランスポートが SAN NIC ハードウェアで完全に実装されていない場合は、SAN のトランスポート ドライバーする必要があります。 必要な場合、SAN トランスポート ドライバーは、SAN の NIC ベンダーによって指定され、その上にある SAN プロキシ ドライバーとプライベート インターフェイスを通じて基になる SAN NIC 通信します。

SAN サービス プロバイダーの DLL とそのプロキシ ドライバーを実装する方法の詳細については、次を参照してください。 [Windows Sockets 直接](windows-sockets-direct.md)します。 ただし、このセクションに SAN 転送のドライバーを作成する方法が指定されていないことに注意してください。

NDIS ミニポート ドライバー イーサネット、ATM、または別の SAN など、特定の SAN 以外のネットワーク経由で送信する必要がありますデータを転送する必要があります。 TCP/IP では、NDIS ミニポート ドライバーを使用して SAN の NIC にし、このようなネットワーク経由でデータを送信します。

ドライバーのミニポートとトランスポートを実装する方法の詳細については、次を参照してください。*ミニポート ドライバー*と[TDI トランスポートとそのクライアント](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff565587(v=vs.85))します。

 

 





