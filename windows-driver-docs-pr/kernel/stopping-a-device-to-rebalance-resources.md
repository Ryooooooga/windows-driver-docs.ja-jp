---
title: リソースを再調整するためのデバイスの停止
description: リソースを再調整するためのデバイスの停止
ms.assetid: eed28d41-8a9d-4b9e-90d7-ea4ddeeaad2d
keywords:
- PnP WDK リソースを再調整
- PnP WDK 再均衡化リソース
- PnP デバイスの一時停止
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: a5dd80d3981f3f7bece37a14f35ae8f4b100ad61
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382979"
---
# <a name="stopping-a-device-to-rebalance-resources"></a>リソースを再調整するためのデバイスの停止





次の図で停止してリソースを再調整するデバイスを再起動する Irp のシーケンスを示します。

![リソースを再調整するデバイスを停止するかを示す図](images/stop-irps.png)

次のノートは、前の図の丸の番号に対応しています。

1.  PnP マネージャーの問題、 [ **IRP\_MN\_クエリ\_停止\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-stop-device)リリースとデバイスのデバイス ドライバーを停止できるかどうかを確認する、ハードウェア リソース。

    デバイス スタック内のすべてのドライバーが状態を返すかどうか\_成功すると、ドライバーがデバイスに (停止待ち) の状態をデバイスすばやく停止できるからです。

    PnP マネージャーでは、必要なリソースを再調整する必要に応じて、同数のデバイス スタックを照会します。

2.  PnP マネージャーの問題、 [ **IRP\_MN\_停止\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-stop-device)デバイスを停止します。

    Windows 2000 と Windows の以降のバージョンでは、PnP マネージャーは、停止の場合のみ、デバイスが正常に完了の前のクエリ停止 IRP IRP を送信します。 停止 IRP に応答してでは、ドライバーは、(その I/O ポート) など、デバイスのハードウェア リソースを解放し、デバイスへのアクセスを必要とする任意の Irp を保持します。

3.  PnP マネージャーの発行後、リソースが正常に再調整、 [ **IRP\_MN\_開始\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)要求中に停止しているすべてのデバイスを再起動するには再調整します。

4.  それ以外の場合、PnP マネージャーが送信することによってクエリ停止 IRP を取り消します、 [ **IRP\_MN\_キャンセル\_停止\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-cancel-stop-device)。

    応答、 **IRP\_MN\_キャンセル\_停止\_デバイス**デバイスのドライバーがデバイスを開始状態に戻すし、デバイスの I/O 要求の処理を再開します。

    PnP マネージャーは、スタック内の 1 つのドライバーには、要求が失敗した場合、または全体の再調整操作に失敗し、すべてのクエリの停止要求をキャンセルは場合、デバイス スタックのクエリの停止をキャンセルします。 送信 PnP マネージャーでは、1 つのデバイス スタックでクエリ停止をキャンセルしたときに、 **IRP\_MN\_キャンセル\_停止\_デバイス**ドライバー上すべてのドライバーが接続されているため、要求クエリに失敗した保留中の停止の状態で、デバイスを所有します。 ときに、 **IRP\_MN\_キャンセル\_停止\_デバイス**成功すると、ドライバーには開始状態に、デバイスが返されます。

5.  ドライバーは、リソースを再調整した後、デバイスの再起動に失敗した場合、PnP マネージャー送信は Irp を (Windows 2000 以降のバージョンの Windows で) デバイス スタックを削除します。

    PnP マネージャーの最初の送信、 [ **IRP\_MN\_突然\_削除**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-surprise-removal)要求。 送信し、 [ **IRP\_MN\_削除\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-remove-device)要求がデバイスにのみ後は、すべての開いているハンドルは閉じられます。

PnP デバイスのハードウェア リソースを再調整は、アプリケーションとエンドユーザーに対して透過的に実行する必要があります。 ユーザー操作では、一時的な遅延が発生する可能性がありますが、データが失われたできないする必要があります。 考慮事項に処理するときに停止する Irp を行う必要があります。

 

 




