---
title: デバイスの電源ポリシーを管理する
description: デバイスの電源ポリシーを管理する
ms.assetid: f6f9ab40-4d51-4181-ac11-ff7af42370af
keywords:
- デバイスの電源ポリシー WDK カーネル
- 電源ポリシー WDK カーネル
- デバイスの電源ポリシー所有者 WDK カーネル
- 関数ドライバー WDK の電源管理
- デバイスの電源状態 WDK カーネル
- 初期デバイスの電源状態 WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9a70f368ad346eef28f8d3fc8ecd1251f8572f89
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838555"
---
# <a name="managing-device-power-policy"></a>デバイスの電源ポリシーを管理する





電源マネージャーがシステムの電源ポリシーを維持および管理するのと同じように、各デバイスのデバイススタック内の1つのドライバーによって、デバイスの電源ポリシーが保持および管理されます。 このドライバーは、デバイスの*デバイスの電源ポリシー所有者*です。

デバイスの電源ポリシーの所有者は、デバイスの使用状況と電源の状態に関する情報が最も多いドライバーです。 デバイスの電源をオンまたはオフにするデバイスレジスタを物理的に設定する必要はありませんが、デバイスがいつ使用されているか、アイドル状態になったとき、電源状態を変更する必要があるかどうかを判断できる必要があります。

通常、デバイスの関数ドライバーは、電源ポリシーの所有者です。ただし、デバイスによっては、別のドライバーまたはシステムコンポーネントがこの役割を担います。 電源管理に関連するドライバーの種類の詳細については、「 [WDM ドライバーの種類](types-of-wdm-drivers.md)」を参照してください。

一部のドライバーは、1つのデバイス (FDO を作成する) の関数ドライバーとして機能し、列挙された子デバイスのバスドライバー (PDO を作成) として機能します。 このようなドライバーでは、電源と PnP Irp のディスパッチルーチンで、FDO に送信される Irp と PDO に送信される Irp の処理を区別する必要があります。

たとえば、SCSI アダプターのドライバーは、アダプター自体に対して関数ドライバー (FDO を作成する) の役割と、アダプターに接続されているディスクのバスドライバー (PDO を作成する) を実行する場合があります。 SCSI アダプターの関数ドライバー/ポリシー所有者としての容量では、このドライバーはシステム Irp を受信し、SCSI アダプターのデバイス Irp を要求します。 ディスクのバスドライバーとしての容量では、作成するディスク PDOs を指定するデバイス Irp が処理され、完了します。 ドライバーが1つのデバイス (FDO) の電源ポリシーを所有しているということは、子デバイス (PDO) の電源ポリシーを所有しているという意味ではありません。

デバイスの電源ポリシー所有者は、次のことを担当します。

-   [**PoSetPowerState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-posetpowerstate)を呼び出すことによってデバイスの初期電源状態を D0 に設定します。これは、プラグアンドプレイ Manager の[**IRP\_、\_\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)要求を開始します。

    デバイスは必要に応じて電源をオンにする必要があります。たとえば、デバイスで i/o 要求を処理するには電源をオンにする必要があります。 デバイスの電源ポリシーの所有者は、デバイスがいつ必要になるかを判断し、デバイスの電源がオンになっていることを確認し、適切なデバイスの電源状態を設定します。 通常のデバイスは、PnP の開始デバイスの IRP の完了時に電源がオンになっている必要があります。

    一般的なルールとして、システムが動作中の場合でも、ほとんどのデバイスは使用されていないときに電源をオフにする必要があります。

-   [**PoRequestPowerIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-porequestpowerirp)を呼び出して、システムの電源要求に応答してデバイスの電源要求を送信します。

    たとえば、ポリシー所有者がシステム設定-電源 IRP を受け取ると、デバイスセット-電源 IRP が送信されます。 ほとんどのデバイスは、システムがスリープ状態になると、D3 に入ります。 [**デバイス\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_capabilities)の構造の**devicestate**配列には、デバイスがシステムの電源状態ごとに維持できる最高の状態が一覧表示されます。 (「[レポートデバイスの電源機能](reporting-device-power-capabilities.md)」を参照してください)。

-   デバイスがアイドル状態であることを検出し、エネルギーを節約するためにスリープ状態にします。

    電源マネージャーまたはデバイスポリシーの所有者は、アイドル状態のデバイスを検出し、その状態を変更するためにデバイスの電源 IRP を送信することができます。 詳細については、「[アイドル状態のデバイスの検出](detecting-an-idle-device.md)」を参照してください。

-   必要に応じて、デバイスを動作中の状態に戻します。

    スリープ状態のデバイスに対して i/o 要求が到着すると、デバイスのドライバーから動作中の状態に戻ります。

-   要求されたときのデバイスのウェイクアップを有効または無効にします。

    デバイスの電源ポリシー所有者は、「[ウェイクアップ機能を搭載したデバイスのサポート](supporting-devices-that-have-wake-up-capabilities.md)」で説明されているように、待機/ウェイク irp を送受信します。

 

 




