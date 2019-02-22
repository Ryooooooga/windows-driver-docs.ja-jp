---
title: ソフトウェア専用のドライバーでの PnP や電源管理のサポート
description: ソフトウェア専用のドライバーでの PnP や電源管理のサポート
ms.assetid: bcfca8b2-68d6-4875-8687-27351becd6f4
keywords:
- PnP WDK KMDF、ソフトウェアのみのドライバー
- プラグ アンド プレイ WDK KMDF、ソフトウェアのみのドライバー
- 電源管理 WDK KMDF、ソフトウェアのみのドライバー
- ソフトウェア専用のドライバー WDK KMDF
- フィルター ドライバー WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: eeb96e085cbb0c3c087b24c8410465204174ea47
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56552896"
---
# <a name="supporting-pnp-and-power-management-in-software-only-drivers"></a>ソフトウェア専用のドライバーでの PnP や電源管理のサポート


*ソフトウェア専用のドライバー*ドライバーは、ハードウェアにアクセスしません。 一部のソフトウェア専用のドライバーは、ハードウェアにアクセスしないドライバー スタック内に存在します。 これらのドライバーはハードウェアにアクセスしないため、通常がない PnP または電源管理操作を実行します。

その他のソフトウェア専用のドライバーは、フィルター: ハードウェアへのアクセスはドライバーのスタック内に存在するが、フィルター ドライバーはハードウェアにアクセスできません。 フィルター ドライバー、PnP を指定する I/O 要求を受信した場合、または電源管理操作、ドライバー通常だけに要求を渡します次のドライバーです。 フレームワークは、これらの要求のインターセプトを framework ベースのドライバーが要求を確認しないように、渡します。

ソフトウェア専用ドライバーでは、ドライバーを記述するかどうかは[デバイス オブジェクトを作成します。](creating-a-framework-device-object.md)が通常は必要ありません PnP または電源管理イベントを処理するコールバック関数のすべてのイベントを提供します。 ドライバーで使用する場合[framework キュー オブジェクト](framework-queue-objects.md)、設定する必要があります、 **PowerManaged**のキューのメンバー [ **WDF\_IO\_キュー\_CONFIG** ](https://msdn.microsoft.com/library/windows/hardware/ff552359)構造体を**WdfFalse**または**WdfUseDefault**します。

いくつかのソフトウェア専用のドライバーを[関数ドライバー](supporting-pnp-and-power-management-in-function-drivers.md)します。 つまり、1 つのドライバーは可能性があります、ハードウェアにアクセスしない仮想デバイスをサポートするソフトウェア専用のドライバーとハードウェア デバイスをサポートする機能のドライバーとして機能します。

 

 




