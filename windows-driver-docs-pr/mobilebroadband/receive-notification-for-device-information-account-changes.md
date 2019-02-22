---
title: デバイス情報のアカウントの変更の通知を受け取る
description: デバイス情報のアカウントの変更の通知を受け取る
ms.assetid: 67d96f61-57dc-4e4b-a6c1-5c3da28e8aaf
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b9732c1c3412adcfe49f419645e0d9220402c87d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56560927"
---
# <a name="receive-notification-for-device-information-account-changes"></a>デバイス情報のアカウントの変更の通知を受け取る


デバイス情報のアカウントの変更の通知を受信するには、使用、 [ **AccountUpdated** ](https://msdn.microsoft.com/library/windows/apps/hh770601)のイベント[ **MobileBroadbandAccountWatcher** ](https://msdn.microsoft.com/library/windows/apps/hh770597)ここで説明します。

1.  インスタンスを作成、 [ **MobileBroadbandAccountWatcher** ](https://msdn.microsoft.com/library/windows/apps/hh770597)オブジェクト。

2.  追加、 [ **AccountUpdated** ](https://msdn.microsoft.com/library/windows/apps/hh770601)イベント ハンドラー。

3.  呼び出す[**開始**](https://msdn.microsoft.com/library/windows/apps/hh770604)ウォッチャーにします。

4.  クエリ、 [ **HasDeviceInformationChanged** ](https://msdn.microsoft.com/library/windows/apps/hh770594)のプロパティ、 [ **MobileBroadbandAccountUpdatedEventArgs** ](https://msdn.microsoft.com/library/windows/apps/hh770593) 内のオブジェクト[**AccountUpdated** ](https://msdn.microsoft.com/library/windows/apps/hh770601)イベント ハンドラー。

5.  デバイスの情報が変更された場合は、アカウントを照会[ **CurrentDeviceInformation.TelephoneNumbers** ](https://msdn.microsoft.com/library/windows/apps/br207373)電話番号のプロパティ。

    次に、例を示します。

    ``` syntax
    if (account.currentDeviceInformation.TelephoneNumbers.length > 0)
    {
      // there is now at least one telephone number
    }
    ```

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[モバイル ブロード バンドの Windows ランタイム Api の一般的なタスク](common-tasks-for-mobile-broadband-windows-runtime-apis.md)

 

 





