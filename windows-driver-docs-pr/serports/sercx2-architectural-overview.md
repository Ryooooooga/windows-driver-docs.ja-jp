---
title: SerCx2 アーキテクチャの概要
description: SerCx2 は周辺機器のドライバーと逐次的に接続されている周辺機器のデバイス間の通信を有効にするシリアル コント ローラー ドライバーと共に動作します。
ms.assetid: BA5D8966-ACC5-44ED-8CB8-61D1BCF39522
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b568e09c87923ac88c4b80725d66fa8748e60b81
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558732"
---
# <a name="sercx2-architectural-overview"></a>SerCx2 アーキテクチャの概要


SerCx2 は周辺機器のドライバーと逐次的に接続されている周辺機器のデバイス間の通信を有効にするシリアル コント ローラー ドライバーと共に動作します。 通常、シリアル コント ローラーは SoC チップの外部にあるが、同じプリント回路基板をはんだ付けは周辺機器のデバイスとのピン数の少ない通信を提供するには、チップ (SoC) チップをシステムに統合します。

次の図は、逐次的に接続されている周辺機器とこのデバイスのドライバーの間の通信パスを示します。 この周辺のドライバーでは、カーネル モードまたはユーザー モードのいずれかで実行され、周辺機器が接続されているシリアル ポートへの I/O 要求を送信します。

![sercx2 と関連コンポーネントのブロック図](images/sercx2modules.png)

SerCx2 とシリアル コント ローラー ドライバー カーネル モードで実行して SerCx2 デバイス ドライバー インターフェイス (DDI) を介して相互に通信します。 シリアル コント ローラー ドライバーは SerCx2 によって実装されるドライバー サポート メソッドを呼び出します。 SerCx2 は、イベント シリアル コント ローラー ドライバーによって実装されるコールバック関数を呼び出します。

通常、シリアル コント ローラーのハードウェア レジスタは、メモリ マップトは。 シリアル コント ローラー ドライバーには、これらのレジスタをシリアル ポートを構成し、シリアル ポートに接続されている周辺機器とデータの転送を直接にアクセスします。 長いデータ転送、SerCx2 は通常 DMA の転送 (前の図に示されていません) を使用します。

呼び出されるハードウェア リソースの特別な種類に周辺機器のデバイスへの論理接続を開く、周辺機器のドライバーが必要な情報がカプセル化、*接続 ID*します。 詳細については、次を参照してください。[周辺機器を逐次的に接続されている接続 Id](connection-ids-for-serially-connected-peripheral-devices.md)します。

通常、ドライバーのみがシリアルのコント ローラーに直接 I/O 要求を送信します。 ときに、ユーザー モード アプリケーションでは、アプリケーションとデバイス間の媒介としてデバイス機能の周辺機器のドライバーを逐次的に接続されている周辺機器と通信する必要があります。 アプリケーションが書き込みを送信する場合は、アプリケーションは、周辺機器のデバイス間でデータを転送する必要がある、([**IRP\_MJ\_書き込み**](https://msdn.microsoft.com/library/windows/hardware/ff546904)) 要求または読み取り ([ **IRP\_MJ\_読み取り**](https://msdn.microsoft.com/library/windows/hardware/ff546883)) 周辺のドライバーでは、およびシリアル コント ローラーに対応する書き込みまたは読み取り要求を送信して周辺のドライバーが応答を要求します。 さらに、周辺機器のドライバーでは、シリアル ポートを構成するデバイス I/O 制御要求 (Ioctl) を送信できます。 Ioctl SerCx2 でサポートされているの一覧は、次を参照してください。[シリアル I/O 要求インターフェイス](serial-i-o-request-interface.md)します。

シリアル コント ローラーに I/O 要求を送信する周辺のドライバーを使用するか、カーネル モード ドライバーは、[カーネル モード ドライバー フレームワーク](https://msdn.microsoft.com/library/windows/hardware/ff544296)(KMDF)、またはユーザー モード ドライバーを使用する、[ユーザー モード ドライバー フレームワーク](https://msdn.microsoft.com/library/windows/hardware/ff560442) (UMDF)。 SerCx2 周辺のドライバーによってシリアル コント ローラーに送信された I/O 要求のキューを管理します。

読み取りまたは書き込み要求に応答して、SerCx2 シリアル コント ローラーと、要求のデータ バッファーの間でデータを移動する 1 つまたは複数の I/O トランザクションを開始します。 I/O の各トランザクションでは、下手順の I/O (PIO)、または DMA を使用して、シリアル コント ローラーと、要求のデータ バッファー間でデータを転送します。 シリアル コント ローラー ドライバーでサポートされている I/O トランザクションの種類は、シリアル コント ローラーのハードウェア機能に依存します。 詳細については、次を参照してください。 [SerCx2 I/O トランザクションの概要](overview-of-sercx2-i-o-transactions.md)します。

 

 



