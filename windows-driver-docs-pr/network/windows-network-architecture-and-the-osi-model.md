---
title: Windows ネットワーク アーキテクチャと OSI モデル
description: Windows ネットワーク アーキテクチャと OSI モデル
ms.assetid: d57cadc7-c443-441d-b693-d85ffabe9f7f
keywords:
- OSI 参照モデルの WDK ネットワーク
- トランスポート層の WDK ネットワーク
- データ リンク層 WDK ネットワーク
- MAC のレイヤーの WDK ネットワーク
- WDK のネットワークを物理レイヤー
- Windows ネットワーク アーキテクチャ WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e5da7810ac500c4458e9eb55344fa3270ceacd63
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56559053"
---
# <a name="windows-network-architecture-and-the-osi-model"></a>Windows ネットワーク アーキテクチャと OSI モデル


## 概要 <a href="" id="ddk-windows-network-architecture-and-the-osi-model-ng"></a>


Microsoft Windows オペレーティング システムでは、国際標準化機構 (ISO) によって開発された 7 層のネットワーク モデルに基づくネットワーク アーキテクチャを使用します。 1978 年に導入された、ISO 開放型システム (OSI) 参照モデルは"一連のプロトコル レイヤーの各レイヤーに割り当てられている関数の特定のセットを持つとしてネットワークについて説明します。 各レイヤーは、これらの層のサービスを実装する方法の詳細を把握している上位のレイヤーを特定のサービスを提供します。 隣接するレイヤーの各ペアの間で適切に定義されたインターフェイス定義より高いものとそれらのサービスへのアクセス方法には、下位層から提供されるサービスです。" 次の図は、OSI 参照モデルを示しています。

![osi 参照モデルを示す図](images/101osi.png)

Microsoft Windows ネットワーク ドライバーは、OSI 参照モデルの下部にある 4 つのレイヤーを実装します。

## <a name="physical-layer"></a>物理レイヤー  
物理レイヤーでは、OSI モデルの最下位の層です。 このレイヤーは、物理メディア上で受信し、構造化されていない生のビット ストリームの転送を管理します。 これには、物理メディアに電気/光、機械的、および機能のインターフェイスについて説明します。 物理レイヤーでは、上位層のすべての信号伝達されます。 、Windows では、物理層は、ネットワーク インターフェイス カード (NIC)、そのトランシーバー、および NIC がアタッチされているメディアで実装されます。

## <a name="data-link-layer"></a>データ リンク層  
さらにそのデータ リンク層を分割 Institute の Electrical and Electronics Engineers (IEEE) で 2 つのサブレイヤーに: の論理リンク コントロール (LLC) とメディア アクセス制御 (MAC)。

### <a name="llc"></a>LLC

LLC 副層では、エラーのない転送データ フレームの 1 つのノードから別に提供します。 LLC 副層を確立および論理リンクを終了します、フレームのフローを制御、フレームのシーケンス、フレームを確認および未確認のフレームを再送信します。 LLC 副層では、フレームの受信確認と再送信を使用して、上位のレイヤーにリンク経由でほとんどのエラーのない伝送を提供します。

### <a name="mac"></a>MAC

MAC 副層は、物理層へのアクセスを管理、フレームのエラーをチェックし、受信フレームのアドレスを認識を管理します。

Windows ネットワーク アーキテクチャで LLC 副層は、トランスポート ドライバーに実装されてし、NIC の MAC 副層が実装されています。 NIC と呼ばれるソフトウェアのデバイス ドライバーによって制御されます、[ミニポート ドライバー](ndis-miniport-drivers2.md)します。 Windows は、ミニポート ドライバーが WDM ミニポート ドライバー、ミニポート コール マネージャー (MCMs) ミニポートなどのいくつかのバリエーションをサポートしている[ドライバーの中間](ndis-miniport-drivers.md)します。

## <a name="network-layer"></a>ネットワーク層
ネットワーク層では、サブネットの操作を制御します。 このレイヤーは、次の条件に基づいて、データが実行する物理パスを決定します。

-   ネットワークの状態。

-   サービスの優先順位。

-   ルーティング、トラフィック制御、フレームの断片化と再構築、論理と物理アドレスのマッピング、および使用状況のアカウンティングなどその他の要因

## <a name="transport-layer"></a>トランスポート層

トランスポート層によりメッセージが配信されたこと、エラーのないシーケンスで、損失や重複がないようになります。 このレイヤーは、それらとピアの間のデータの転送に何も気から上位層プロトコルを解放します。 信頼性の高いネットワークまたは仮想回線機能を提供する LLC 副層を含むプロトコル スタックで必要な最小限のトランスポート層が必要です。 たとえば、NetBEUI は、OSI 準拠 LLC の副層、Windows のドライバーをトランスポート、ため、そのトランスポート層の機能はわずかです。 プロトコル スタックには、LLC 副層が含まれていない場合、フレームのシーケンス処理と受信確認は、トランスポート層を含める必要があります、ネットワーク レイヤーの信頼性が低いや (と同様 TCP/IP の IP レイヤー、または NWLink の IPX レイヤー) データグラムをサポートしているだけでなく未確認のフレームを再送信します。

呼ばれるソフトウェア ドライバーによって Windows のネットワーク アーキテクチャ、LLC、ネットワーク、およびトランスポート層が実装されている[プロトコル ドライバー](ndis-protocol-drivers.md)、これとも呼ば*トランスポート ドライバー*します。

 

 




