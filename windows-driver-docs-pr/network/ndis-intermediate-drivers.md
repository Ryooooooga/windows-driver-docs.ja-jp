---
title: 中間ドライバー
description: 中間ドライバー
ms.assetid: 0c0516b0-1fc4-43b5-8c7c-58255c72a4e7
keywords:
- 中間ドライバー WDK ネットワー キング、アーキテクチャ
- NDIS 中間ドライバー WDK、アーキテクチャ
ms.date: 11/26/2018
ms.localizationpriority: medium
ms.openlocfilehash: 9097dfcd64af18584b8668d855724b579683821f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56577761"
---
# <a name="intermediate-drivers"></a>中間ドライバー

次の図に示すように、中間ドライバーは通常、階層化されているミニポート ドライバーの間とトランスポート プロトコル ドライバー。

![ミニポート ドライバーとトランスポート ドライバー間層、中間のドライバーを示す図](images/id-1.png)

> [!NOTE]
> NDIS ドライバー スタックと 4 つすべての NDIS ドライバーの種類間のリレーションシップを示す図の詳細については、次を参照してください。 [NDIS ドライバー スタック](ndis-driver-stack.md)します。

ドライバー階層の中間の位置のため中間のドライバーは、公開するために上位プロトコル ドライバーと基になるミニポート ドライバーの両方で通信する必要があります。

-   プロトコルのエントリ ポイント。

    NDIS を呼び出してその下端にある、 *ProtocolXxx*関数を基になるミニポート ドライバーからの要求を伝達します。 中間のドライバーは、基になる、ミニポート ドライバーにプロトコル ドライバーと似ています。

-   ミニポート ドライバーのエントリ ポイント。

    NDIS を呼び出し、上端にある、 *MiniportXxx*関数上にあるプロトコル ドライバーが 1 つまたは複数の要求を伝達します。 中間のドライバーは、ミニポート ドライバー、上位のプロトコル ドライバーに似ています。

中間のドライバーのサブセットのエクスポート、 *MiniportXxx*上端で機能します。 1 つまたは複数仮想アダプター、上位のプロトコルのドライバーをバインドすることができますもエクスポートされます。 プロトコル ドライバーに中間のドライバーによってエクスポートされた仮想アダプターは物理 NIC に表示されます。 プロトコル ドライバーは、仮想アダプターにパケットまたは要求を送信するときに、中間のドライバーは、これらのパケットと基になるミニポート ドライバーへの要求を伝達します。 このようなパケット、応答、およびプロトコル ドライバーにバインドされている最大の状態と基になるミニポート ドライバーは、受信したパケットを示します、については、プロトコル ドライバーの要求に応答すると、状態を示します、中間ドライバーが伝達、仮想アダプター。

中間のドライバーを使用できます。

-   別のネットワークのメディア間で変換します。

-   1 つ以上の NIC 間で分散パケットの転送 負荷分散のドライバーは、トランスポート プロトコルに関連する 1 つの仮想アダプターを公開し、送信パケットを 1 つ以上の NIC に分散

## <a name="related-topics"></a>関連トピック

[NDIS 中間ドライバ](ndis-intermediate-drivers2.md)

[NDIS 中間ドライバー リファレンス](https://msdn.microsoft.com/library/windows/hardware/ff565782)