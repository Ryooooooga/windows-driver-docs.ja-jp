---
title: SR-IOV の合成データ パス
description: SR-IOV の合成データ パス
ms.assetid: FB7E57F6-AA99-421D-8344-B76615BD20ED
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c7ab27fbe1e04a4518925bc08891f24574df8f13
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56552163"
---
# <a name="sr-iov-synthetic-data-path"></a>SR-IOV の合成データ パス


HYPER-V 子パーティションを起動し、ゲスト オペレーティング システムが実行されている、仮想化スタックでは、ネットワーク仮想サービス クライアント (NetVSC) が開始されます。 NetVSC、ミニポート ドライバーの端、ゲスト オペレーティング システムで実行されているプロトコル スタックを提供する仮想マシン (VM) ネットワーク アダプターを公開します。

NetVSC は、HYPER-V 親パーティションの管理オペレーティング システムで実行されている HYPER-V 拡張可能スイッチとも通信します。 拡張可能スイッチのコンポーネントは、ネットワーク仮想サービス プロバイダー (NetVSP) として動作します。 NetVSC と NetVSP 間のインターフェイスと呼ばれるソフトウェアのデータ パスを提供する、*合成データ パス*します。

次の図は、SR-IOV 対応のネットワーク アダプタ上での合成データ パスのコンポーネントを示します。

![ゲスト オペレーティング システムが含まれる子パーティションを vmbus 経由で通信の管理の親パーティションの下に、sr-iov アダプターを示すスタックの図](images/sriovsynthetic-datapaths.png)

基になる、SR-IOV ネットワーク アダプターでは、PCI Express (PCIe) 仮想機能 (Vf) のリソースを割り当て、仮想化スタックは、HYPER-V 子パーティションを VF がアタッチされます。 アタッチされると、子パーティション内のトラフィックのパケットが合成データ パスの代わりのハードウェアに最適化された VF データのパス経由で発生します。 VF のデータ パスの詳細については、次を参照してください。 [SR-IOV データ パス](sr-iov-data-paths.md)します。

仮想化スタックには、次の条件のいずれかが true の場合、HYPER-V 子パーティションの合成データ パスが有効にも可能性があります。

-   開始された HYPER-V 子パーティションのすべてに対応する VF リソースが不足しています、SR-IOV ネットワーク アダプター すべての VFs ネットワーク アダプターでは、子パーティションに関連付けられている後の残りのパーティションは、合成データ パスを使用します。

    合成データ パスに VF のデータ パスからのフェイル オーバーのプロセスと呼びます*VF フェールオーバー*します。

-   VF は、HYPER-V 子パーティションに接続されていたがデタッチ済みになります。 たとえば、仮想化スタックは、VF 1 つの子パーティションからのデタッチし、もう 1 つの子パーティションにアタッチします。 基になる、SR-IOV ネットワーク アダプターの VF リソースがより多くを実行している HYPER-V 子パーティションがある場合があります。

-   HYPER-V 子パーティションは、別のホストに移行、ライブでことです。

SR-IOV 対応のネットワーク アダプタ上での合成データ パスは VF のデータ パスほど効率的ではありませんが、最適化されたハードウェアをできます。 たとえば、1 つまたは複数の仮想ポート (拡張) は構成されている、PCIe 物理機能 (PF) に接続されている場合、データ パスは、仮想マシン キュー (VMQ) インターフェイスのようなオフロード機能を提供できます。 詳細については、次を参照してください。[既定以外の仮想ポートおよび VMQ](nondefault-virtual-ports-and-vmq.md)します。

 

 




