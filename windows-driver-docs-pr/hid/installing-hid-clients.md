---
title: HID クライアントをインストールする
description: このセクションでは、Microsoft Windows に HIDClass デバイスをインストールする場合は、次の要件について説明します。
ms.assetid: 080992B1-AB36-4BA1-BF44-7CF0C9F4EEE3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 391539f4f21323fc27ee4977766954347adbb029
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67375911"
---
# <a name="installing-hid-clients"></a>HID クライアントをインストールする


このセクションでは、Microsoft Windows に HIDClass デバイスをインストールする場合は、次の要件について説明します。

-   ベンダーを使用する必要があります、 [*ハードウェア Id* ](https://docs.microsoft.com/windows-hardware/drivers/install/hardware-ids)として指定されている最上位のコレクションの*ベンダーのハードウェア ID の形式*で[HIDClass ハードウェア Id最上位のコレクション](hidclass-hardware-ids-for-top-level-collections.md)します。

-   親の入力デバイス (HID クラス ドライバー HIDClass デバイスのドライバー スタックで以下がインストールされている) のベンダーから提供されたドライバーは、HID クラス ドライバーは、最上位のコレクションのハードウェア Id の生成に使用するハードウェア情報を指定する必要があります。 (注、HIDClass デバイス用のシステム指定のドライバーが自動的に行います)。

-   Windows Vista および Windows の以降のバージョンでは、ベンダーは USB HID デバイスをセレクティブ サスペンドの機能を有効にできます。 この機能はバージョン 2.0 で定義されている、*ユニバーサル シリアル バス仕様。* Windows で USB のセレクティブをサポートする方法の詳細については、機能を中断しを参照してください[USB のセレクティブ サスペンド](../usbcon/usb-selective-suspend.md)します。

HIDClass デバイスをインストールするには、その他の HIDClass 固有要件はありません。 デバイスをインストールする方法の詳細については、次を参照してください。[デバイス インストールの概要](https://docs.microsoft.com/windows-hardware/drivers/install/overview-of-device-and-driver-installation)します。

 

 




