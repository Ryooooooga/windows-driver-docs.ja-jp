---
title: 停止 IRP の処理 (Windows 98/Me)
description: 停止 IRP の処理 (Windows 98/Me)
ms.assetid: 98eefb69-e321-4cc5-8b4d-79335cd8b06e
keywords:
- Irp WDK PnP 停止します。
- WDK PnP Irp
- I/O 要求パケット PnP WDK
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: b42219126bd11733e3854e33b17980a7ef8230e5
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67353792"
---
# <a name="handling-stop-irps-windows-98me"></a>停止 IRP の処理 (Windows 98/Me)





Windows 98 で/PnP マネージャーが送信できる、次のような理由の Irp を停止します。

-   リソースを再調整中にデバイスを一時停止するには

-   デバイス マネージャーを無効にするときに、デバイスを停止するには

-   失敗した後、デバイスを停止する[ **IRP\_MN\_開始\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)要求

ドライバーは IRP が送信された理由を判断できません。 その結果、Windows 98 で実行される WDM ドライバー/場合と、デバイスを無効に、すべて停止 Irp Me 処理する必要があります。 簡単に言えば、つまり、受信 I/O 要求ではなく (Windows 2000 以降) としてキューに入れ、このようなドライバーが失敗します。

次のトピックでは、各停止 Irp の処理詳細な手順について説明します。

[IRP の処理\_MN\_クエリ\_停止\_デバイス要求 (Windows 98/Me)](handling-an-irp-mn-query-stop-device-request--windows-98-me-.md)

[IRP の処理\_MN\_停止\_デバイス要求 (Windows 98/Me)](handling-an-irp-mn-stop-device-request--windows-98-me-.md)

[IRP の処理\_MN\_キャンセル\_停止\_デバイス要求 (Windows 98/Me)](handling-an-irp-mn-cancel-stop-device-request--windows-98-me-.md)

 

 




