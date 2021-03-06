---
title: SerCx2 で管理されるシリアル ポートからデータを読み取る
description: シリアルコントローラー (または UART) には、通常、受信 FIFO が含まれます。
ms.assetid: 36522E60-3616-4431-8C8C-3EAC4A6E4422
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 071dc00a8b9a2dd3feac89e0c2783926db7feb87
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844942"
---
# <a name="reading-data-from-a-sercx2-managed-serial-port"></a>SerCx2 で管理されるシリアル ポートからデータを読み取る

シリアルコントローラー (または UART) には、通常、受信 FIFO が含まれます。 この FIFO は、シリアルポートに接続されている周辺機器から受信したデータのハードウェア制御のバッファリングを提供します。 受信 FIFO からデータを読み取るために、このデバイスの周辺機器ドライバーは、読み取り ([**IRP\_MJ\_読み取り**](https://docs.microsoft.com/previous-versions/ff546883(v=vs.85))) 要求をシリアルポートに送信します。

シリアルポートが、周辺ドライバーがデータを読み取るよりも高速にデータを受信する場合、受信 FIFO がオーバーフローする可能性があります。 オーバーフローが原因でデータが失われないようにするには、通常、周辺機器ドライバーでハードウェアフロー制御を使用するようにシリアルポートを構成する必要があります。 フロー制御では、受信 FIFO がほぼいっぱいになったときに、シリアルコントローラーハードウェアが周辺機器に自動的にデータの送信を停止するように通知します。 ルールとして、SerCx2 によって管理されるシリアルポートでは、ハードウェアフロー制御を使用する必要があります。 詳細については、「[フロー制御の詳細](#flow-control-details)」を参照してください。

ただし、フロー制御を使用して、周辺機器が長時間にデータを送信できないようにしたり、デバイスが正常に動作しなくなったりしないようにする必要があります。 たとえば、周辺機器には、デバイスでこのバッファーからシリアルポートへのデータの送信が長すぎるとオーバーフローする内部データバッファーが含まれている場合があります。

**このページのもの**

- [非同期読み取り要求の使用](#using-asynchronous-read-requests)
- [間隔のタイムアウトの詳細](#interval-time-out-details)
- [フロー制御の詳細](#flow-control-details)

## <a name="using-asynchronous-read-requests"></a>非同期読み取り要求の使用

不適切な操作やデータ損失の可能性を回避するために、周辺ドライバーはシリアルコントローラーの受信 FIFO からデータを適時に読み取る役割を担います。 通常、データを受信する前に、周辺機器からのデータの到着を見越して、周辺ドライバーがシリアルポートに非同期読み取り要求を送信します。 この読み取り要求は、receive FIFO からデータを読み取ることができるようになるまで、SerCx2 i/o キューで保留状態のままになります。

ほとんどのハードウェアプラットフォームでは、周辺機器のドライバーは、一度に複数の読み取り要求を保留している必要はありません。 まれに、データを受信した後に、データのバックアップによって周辺機器のデータが失われたり、それ以外の動作が発生したりする可能性がある場合に、1つのドライバーに複数の未処理の読み取り要求が必要になることがあります。な.

周辺機器ドライバーで一度に保留される読み取り要求が1つだけであると仮定すると、この要求で必要なデータバッファーのサイズは、周辺機器の既知の動作によって異なります。 たとえば、ドライバーがデバイスから予想されるデータのバイト数を事前に認識している場合、ドライバーは要求のバッファーサイズをこのバイト数に設定します。 読み取り要求は、受信 FIFO からのデータがバッファーに格納されるとすぐに完了します。 応答として、ドライバーは新しい読み取り要求を非同期的に送信して、次のデータブロックを待機することができます。

ただし、周辺機器ドライバーは、周辺機器から予想されるデータ量を事前に把握していない可能性があります。 この場合、ドライバーは読み取り要求のデータバッファーを適切なサイズに設定し、その後、間隔タイムアウトを利用して周辺機器からのデータの末尾を識別します。 読み取りバッファーに適切なサイズを選択するには、周辺機器の動作に関する詳細な知識が必要になることがあります。 読み取りバッファーが小さすぎる場合、ドライバーはデータの読み取りを完了するために1つ以上の追加の読み取り要求を送信する必要があります。

## <a name="interval-time-out-details"></a>間隔のタイムアウトの詳細


読み取り要求と書き込み要求のタイムアウトパラメーターを設定するために、周辺ドライバーは、シリアル[ **\_設定\_タイムアウト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_set_timeouts)要求をシリアルポートに送信する IOCTL\_を送信できます。 読み取りのタイムアウトは、この要求の**Readintervaltimeout**、 **ReadTotalTimeoutMultiplier**、および**ReadTotalTimeoutConstant**パラメーター値によって制御されます。 **Readintervaltimeout**は、受信トランザクションの2つの連続するバイト間で許容される最大時間間隔を指定します。 **ReadTotalTimeoutMultiplier**と**ReadTotalTimeoutConstant**の両方がゼロで、シリアルコントローラーの受信 FIFO が空である場合、読み取り要求がシリアルポートに送信されたときに、この要求はタイムアウトしません (そのため、SerCx2 i/o で保留中のままになります)。queue) が、ポートが少なくとも1バイトの新しいデータを受信するまで待ちます。 詳細については、「 [**SERIAL\_のタイムアウト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddser/ns-ntddser-_serial_timeouts)」を参照してください。

チップ (SoC) 統合回線上のシステムのシリアルポートは、周辺機器から、数メガビット/秒以上のピーク速度で周辺機器からデータを受信できる場合があります。 このデバイスの周辺機器ドライバーの開発者は、( **Readintervaltimeout**パラメーターで指定されている) 間隔のタイムアウト値をミリ秒以下に設定しようとしている可能性がありますが、この値は望ましい効果が得られない可能性があります。 これは、間隔のタイムアウトを検出するために使用されるタイマーの精度が、システムクロックの粒度によって制限されるためです。

たとえば、システムクロック期間が15ミリ秒であり、ドライバーによって**Readintervaltimeout**値が1ミリ秒に設定されている場合、0からわずか15ミリ秒の範囲内の任意の場所にあるバイト対バイトの間隔によってタイムアウトが発生する可能性があります。この設定によっては、周辺機器からのデータ転送中にタイムアウトが発生することがあります。 この転送が終了した後にのみタイムアウトが発生するようにするために、ドライバーは**Readintervaltimeout**を15ミリ秒を超える値に設定できます。 たとえば、 **Readintervaltimeout**が20ミリ秒に設定されている場合、30ミリ秒のバイト対バイトの間隔では、タイムアウトを確実にトリガーし、15ミリ秒以下の間隔でタイムアウトをトリガーしません。

タイマー精度がシステムクロックにどのように依存しているかの詳細については、「[タイマー精度](https://docs.microsoft.com/windows-hardware/drivers/kernel/timer-accuracy)」を参照してください。

## <a name="flow-control-details"></a>フロー制御の詳細


ベストプラクティスとして、SerCx2 で管理されているシリアルポートを使用する周辺機器では、これらのポートがハードウェアフロー制御を使用して受信 FIFO のオーバーフローを防ぐように構成する必要があります。 保留中の読み取り要求が存在しない場合、SerCx2 は、受信 FIFO の容量を超える受信データのソフトウェアバッファーを提供しません。 この FIFO のオーバーフローが許容される場合、データは失われます。

ハードウェアフロー制御を有効にするために、周辺ドライバーは、シリアルポートのハンドシェイクとフロー制御の設定を設定するために、フローの要求\_のフロー要求を送信して、 [**IOCTL\_シリアル\_設定**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_set_handflow)します。 または、ドライバーは、既定の\_構成要求\_適用して、ハードウェアフロー制御を含む既定のハードウェア設定のセットを使用するようにシリアルポートを構成するために、 [**IOCTL\_シリアル\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_apply_default_configuration)送信します。 **IOCTL\_serial\_SET\_のフロー**要求では、[**直列\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddser/ns-ntddser-_serial_handflow)のフローの構造を使用してフロー制御の設定を記述します。 **IOCTL\_シリアル\_適用\_既定の\_構成**要求には、ベンダーが指定したデータ形式で類似した情報が含まれている場合があります。

周辺ドライバーが**IOCTL\_シリアル\_** を使用して、ハードウェアフロー制御を有効にする\_のフロー要求を設定した場合、ドライバーは、この要求の**シリアル\_実行フロー**構造に次のフラグを設定する必要があります。

- 構造体の**Controlhandshake**メンバーのシリアル\_CTS\_ハンドシェイクフラグ。 このフラグにより、シリアルポートで受信操作にフロー制御を使用できるようになります。
- **Flowreplace**メンバーの SERIAL\_RTS\_CONTROL および SERIAL\_RTS\_ハンドシェイクフラグ。 これらのフラグにより、シリアルポートで送信操作のフロー制御を使用できるようになります。
