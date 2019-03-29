---
title: ドライバーの機能
description: ドライバーの機能
ms.assetid: 639eff56-655d-4b6a-95f0-daa1daf62fae
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 12e7166ebca9173164eef8988ff5e68555b32d96
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56528176"
---
# <a name="driver-capabilities"></a>ドライバーの機能





すべて WIA ミニドライバーは、通知イベントとコマンドを処理するために、デバイスの機能を定義する必要があります。 このセクションでは、これらのミニドライバー機能について説明します。

WIA ミニドライバーは、すべてのイベントとそれがサポートするコマンドの一覧を表示するテーブルを構築します。 次の図は、WIA ミニドライバーを作成する機能の一覧を示します。

![wia ミニドライバーの機能の一覧を示す図](images/wia-capabilitiestable.png)

機能の表がの配列として定義されている[ **WIA\_DEV\_CAP\_DRV** ](https://msdn.microsoft.com/library/windows/hardware/ff550233)構造体。 ミニドライバーがこの配列を作成し、WIA サービスを呼び出すと、WIA サービスに返す必要があります、 [ **IWiaMiniDrv::drvGetCapabilities** ](https://msdn.microsoft.com/library/windows/hardware/ff543977)メソッド。

### <a name="defining-supported-events-and-commands"></a>イベントとコマンド サポートを定義します。

WIA ミニドライバーは、イベントと、WIA サービスにデバイスをサポートするコマンドについて説明します必要があります。

### <a name="events"></a>イベント

*イベント*ドライバーに報告する必要がありますデバイス レベルでアクションです。 たとえば、スキャナーには、「スキャン」というラベルの付いたフロント パネル ボタンがあります。 ユーザーがこのボタンをクリックすると、スキャン、または少なくともを開始するスキャナーが期待どおり、スキャンを開始するアプリケーションを開始します。

WIA には、2 種類のイベントがサポートされています。

<a href="" id="action-event"></a>操作イベント  
*アクション イベント*がこのようなイベントを処理するために登録されているアプリケーションを起動します。 たとえば、Microsoft のスキャナーとカメラ ウィザードはスキャン イベントの登録済みハンドラー (他のアプリケーションは、このイベントにも登録できます)。 ドライバーは、スキャンのイベントを送信するとき、WIA サービスはこのイベントを処理するには、スキャナーとカメラ ウィザードを開始します。 この種類のイベントと呼ばれるよく、*永続的なイベント*します。

<a href="" id="notification-event"></a>Notification イベント  
A*通知イベント*は既に実行されており、このイベントを受け取る必要がある、WIA サービスに指定されているアプリケーションにのみ送信されます。 アプリケーションが実行されていない場合、このイベントを処理するためには開始されません。

イベントには、アクション イベントおよび notification イベントの両方ができます。

### <a name="commands"></a>コマンド

WIA デバイス コマンドは、いくつかの操作を実行するようにミニドライバーに指示する WIA ミニドライバーに (イメージング アプリケーション) に代わって、WIA サービスを送信する要求です。 WIA カメラのミニドライバーが処理など、**画像の撮影**コマンド。 このコマンドは、新しい写真を撮影するデジタル カメラ デバイスを注文するミニドライバーを指示します。

**注**  スキャナーとカメラ ウィザードはすぐに、ユーザーに応答、バック グラウンドで行うクリーンアップがある場合でもです。 ユーザーがアクションのキャンセルを要求するとすぐに、スキャナーとカメラ ウィザード ウィンドウを閉じますなどただし、スキャナーとカメラ ウィザードには、ウィンドウが閉じられた後に実行を継続する個別の買収スレッドがあります。 この個別のスレッドでは、により、ユーザーの要求をすぐに応答が必要なタスクとユーザー エクスペリエンスに影響を与えることがなく完了する中断できないタスクをことができます。

 

 

 



