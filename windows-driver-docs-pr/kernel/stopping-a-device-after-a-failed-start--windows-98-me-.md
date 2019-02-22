---
title: 失敗した開始後にデバイスを停止する (Windows 98/Me)
description: 失敗した開始後にデバイスを停止する (Windows 98/Me)
ms.assetid: 373a1797-6479-4b99-b577-c74494f1774c
keywords:
- 失敗した開始 PnP WDK
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 392b9b11e3e59f046a6095c106e76c6a619198ba
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56539041"
---
# <a name="stopping-a-device-after-a-failed-start-windows-98me"></a>失敗した開始後にデバイスを停止する (Windows 98/Me)





Windows 98 で PnP マネージャーの問題、/、 [ **IRP\_MN\_停止\_デバイス**](https://msdn.microsoft.com/library/windows/hardware/ff551755)せず、上記のクエリを使用しているデバイスのドライバー、の失敗したときに要求[ **IRP\_MN\_開始\_デバイス**](https://msdn.microsoft.com/library/windows/hardware/ff551749)要求。 (Windows 2000 以降、PnP マネージャー送信削除 Irp このような状況でします。 参照してください[Irp を削除する場合は、発行](understanding-when-remove-irps-are-issued.md))。

IRP の停止への応答、ドライバー (その I/O ポート) など、デバイスのハードウェア リソースを解放、無効にして、ユーザー モード インターフェイスを登録解除およびデバイスへのアクセスを必要とするすべての受信 I/O 要求が失敗します。

 

 



