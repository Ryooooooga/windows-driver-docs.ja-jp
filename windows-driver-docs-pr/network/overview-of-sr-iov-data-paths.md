---
title: SR-IOV データ パスの概要
description: SR-IOV データ パスの概要
ms.assetid: C82AEB00-E699-40AB-85E8-064B841B83F4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cb10aeafe3855b9c9288c2158f921e622d0d348b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63381327"
---
# <a name="overview-of-sr-iov-data-paths"></a>SR-IOV データ パスの概要


HYPER-V 子パーティションを起動し、ゲスト オペレーティング システムが実行されている、仮想化スタックでは、ネットワーク仮想サービス クライアント (NetVSC) が開始されます。 NetVSC、ミニポート ドライバーの端、ゲスト オペレーティング システムで実行されているプロトコル スタックを提供することで、仮想マシン (VM) ネットワーク アダプターを公開します。 さらに、NetVSC は、基になるミニポート ドライバーにバインドすることを許可するプロトコル ドライバー エッジを提供します。

NetVSC は、HYPER-V 親パーティションの管理オペレーティング システムで実行されている HYPER-V 拡張可能スイッチとも通信します。 拡張可能スイッチのコンポーネントは、ネットワーク仮想サービス プロバイダー (NetVSP) として動作します。 NetVSC と NetVSP 間のインターフェイスと呼ばれるソフトウェアのデータ パスを提供する、*合成データ パス*します。 このデータ パスの詳細については、次を参照してください。 [SR-IOV 対応の合成データ パス](sr-iov-synthetic-data-path.md)します。

物理ネットワーク アダプターでは、シングル ルート I/O 仮想化 (SR-IOV) インターフェイスをサポートする場合、1 つまたは複数 PCI Express (PCIe) 仮想機能 (Vf) を有効にすることができます。 HYPER-V 子パーティションには、各 VF をアタッチすることができます。 この場合、仮想化スタックは、次の手順を実行します。

1.  仮想化スタックでは、ゲスト オペレーティング システムで VF のネットワーク アダプターを公開します。 これにより、PCI VF ミニポート ドライバーを開始するゲスト オペレーティング システムで実行されています。 このドライバーは、SR-IOV ネットワーク アダプターの独立系ハードウェア ベンダー (IHV) によって提供されます。

2.  VF のミニポート ドライバーが読み込まれ、初期化後、NDIS では、ゲスト オペレーティング システムで、NetVSC のプロトコルの端をドライバーにバインドします。

    **注**NetVSC は VF のミニポート ドライバーにのみバインドします。 VF ミニポート ドライバーにバインドできます、ゲスト オペレーティング システムでは、その他のプロトコル スタックはありません。

ゲスト オペレーティング システム内のネットワーク トラフィックを介した、NetVSC がドライバーに正常にバインドした後、 *VF データ パス*します。 パケットを送信または合成データ パスの代わりに、ネットワーク アダプターの基になる VF 経由で受信しました。

VF のデータ パスの詳細については、次を参照してください。 [SR-IOV VF データ パス](sr-iov-vf-data-path.md)します。

次の図は、SR-IOV ネットワーク アダプター上でサポートされているさまざまなデータ パスを示します。

![親パーティションの管理と、sr-iov アダプターおよびゲスト オペレーティング システムを含む 2 つの子パーティションを示すスタックの図](images/sriovdatapaths.png)

HYPER-V 子パーティションを起動し、VF データの前に、パスが確立されている、ネットワーク トラフィック、合成データ パス経由で送られます。 VF のデータ パスが確立されると、ネットワーク トラフィックは、次の条件に該当する場合、合成データ パスに戻すことができます。

-   VF には、HYPER-V 子パーティションに接続されていないのになります。 たとえば、仮想化スタックは、VF 1 つの子パーティションからのデタッチし、もう 1 つの子パーティションにアタッチします。 基になる、SR-IOV ネットワーク アダプターの VF リソースがより多くを実行している HYPER-V 子パーティションがある場合があります。

    合成データ パスに VF のデータ パスからのフェイル オーバーのプロセスと呼びます*VF フェールオーバー*します。

-   HYPER-V 子パーティションは、別のホストに移行、ライブでことです。

VF のフェールオーバーとライブ マイグレーションの詳細については、次を参照してください。 [SR-IOV VF のフェールオーバーとライブ マイグレーション](sr-iov-vf-failover-and-live-migration-support.md)します。