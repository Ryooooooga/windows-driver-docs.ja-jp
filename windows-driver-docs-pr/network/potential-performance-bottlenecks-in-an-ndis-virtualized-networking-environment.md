---
title: 仮想化されたネットワーク環境でパフォーマンスのボトルネック
description: NDIS 仮想化ネットワーク環境の潜在的なパフォーマンス ボトルネック
ms.assetid: D295E450-C8AF-43A9-B169-5387EB2A2CF0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bf18704287fea57bc8a4aea36c27095c64fa3a0e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63342993"
---
# <a name="potential-performance-bottlenecks-in-an-ndis-virtualized-networking-environment"></a>NDIS 仮想化ネットワーク環境の潜在的なパフォーマンス ボトルネック





ネットワーク環境でデバイスの共有をサポートする独自のメディア アクセス権を持つ仮想インターフェイス コントロール (MAC) アドレスは、各 HYPER-V 子パーティションで公開されます。 これらの仮想インターフェイスでは、基になる仮想マシン バス (VMBus) を使用して、HYPER-V 親パーティションの管理オペレーティング システムで実行されている HYPER-V 拡張可能スイッチ モジュール上のポートに接続します。 拡張可能スイッチは、基になる共有ネットワーク アダプターに送信要求を発行して別のパーティションからの送信のすべてのフレームを送信します。

物理ネットワーク アダプターでは、管理オペレーティング システムで拡張可能スイッチに受信したすべての着信フレームを示します。 拡張可能スイッチは、接続先 MAC アドレスを使用して仮想ネットワーク アダプターに指定された受信フレームを割り当てます。 子パーティションごとに、が関連付けられている子パーティションから事前に割り当てられたセカンダリ バッファーに着信フレーム、管理オペレーティング システムでのネットワーク アダプターのバッファーからコピーする必要があります。 保留中のフレームがある各仮想インターフェイスに通知が送信されます。 各子パーティション内の仮想インターフェイスでは、トランスポート ドライバーに関連する受信のフレームを示します。 アプリケーションを識別するには後、は、トランスポート ドライバーは、セカンダリ バッファーからデータ ペイロードをアプリケーション バッファーにコピーします。

そのため、仮想化環境で入力方向の受信フレームにコピーされます 2 回、まずアダプターのネットワーク バッファーから、子パーティションのターゲットのメモリ アドレス空間から割り当てられたバッファーの一時的なし、この一時からもう一度アプリケーション バッファーをバッファーします。 管理オペレーティング システムで拡張可能スイッチは、CPU サイクルを使用して、着信フレームを解析し、その接続先 MAC アドレスに基づいて別のキューに配置する必要があります。

次の図は、仮想化環境でのパフォーマンスのボトルネックの受信処理を示します。

![仮想化環境での受信処理を図に示すパフォーマンスのボトルネック](images/vmqsyntheticpaths.png)

前の図のパフォーマンスの問題を以下に示します。

-   ターゲットの仮想ネットワーク アダプターを識別するために各着信パケットを検査する必要があります。

-   子パーティションのメモリ アドレス空間を親パーティションのメモリ アドレス空間から受信したデータをコピーする必要があります。

-   割り込みおよび Dpc を同時実行制御の不足。

### <a name="overcoming-performance-bottlenecks-with-vmq"></a>VMQ とパフォーマンスのボトルネックを解消

アドレスのパフォーマンスの問題を仮想マシン キュー (VMQ) インターフェイスを使用します。

-   ネットワーク アダプター MAC アドレスのハードウェアでのフィルター処理を実装することで、ターゲットの子パーティションを決定します。

-   DMA を使用して、子パーティションのメモリ アドレス空間に直接受信パケットを転送するネットワーク アダプター。

-   指定して、割り込みと DPC の同時実行制御を提供するミニポート ドライバーは、異なる Cpu 上の別の子パーティションのパケットを受信しました。

**注**  外部ネットワークから受信したパケットは、管理オペレーティング システムは、ゲスト オペレーティング システムを VMBus 経由で転送できるがあります。

 

VMQ インターフェイスの詳細については、次を参照してください。[仮想マシン キュー (VMQ)](virtual-machine-queue--vmq-.md)します。

### <a name="overcoming-performance-bottlenecks-with-sr-iov"></a>SR-IOV とパフォーマンスのボトルネックを解消

シングル ルート I/O 仮想化 (SR-IOV) インターフェイスでは、複数の子パーティションの PCI Express (PCIe) デバイスを効率的に共有を標準ベースの基盤を提供します。 各デバイスと呼ばれる複数の仮想 I/O インターフェイスを表示するため、PCIe デバイス内で物理 I/O リソースが仮想化*仮想関数*(VFs)。 管理オペレーティング システムは、デバイスで各 VF を構成し、特定の子パーティションを割り当てます。

子パーティションのハードウェア デバイスとして、VF が公開されます。 すべてのデータ パケットは、ゲスト オペレーティング システムと、VF 間で直接フローです。 これにより、管理オペレーティング システムとデータのトラフィックの子パーティションのソフトウェアのパスがなくなります。 子パーティションごとに独立したメモリ領域、割り込みと DMA のストリームを提供することで、データの移動で、管理オペレーティング システムの関与がバイパスします。 フレームは、VF に接続されている内部ポートを使用して、デバイスの物理ポートを使用して外部ネットワークまたは別の子パーティションに送信されます。

すべてのケースで SR-IOV インターフェイス、データ パスで、管理オペレーティング システムの任意の関与の必要はありません。 その結果、SR-IOV インターフェイスは次のよう

-   I/O スループットの向上と CPU 使用率を削減します。

-   低待機時間。

-   スケーラビリティが向上します。

SR-IOV インターフェイスの詳細については、次を参照してください。 [Single Root I/O Virtualization (SR-IOV)](single-root-i-o-virtualization--sr-iov-.md)します。

 

 





