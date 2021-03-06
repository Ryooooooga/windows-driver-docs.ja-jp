---
title: Devices Using WDF (WDF 使用デバイス) タブ
description: このトピックでは、WDF のページを使用して、WDF Verifier のデバイスについて説明します。
ms.assetid: 06144cf4-bb6f-4b5b-ac0d-f4fae89a04a9
keywords:
- WDF Verifier WDK、KMDF 設定の管理
- WDK WDF KMDF の検証の設定
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c4a1aad9820544f91c4c9be23197bf43db1aca2a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63329661"
---
# <a name="devices-using-wdf-tab"></a>[Devices Using WDF]\(WDF 使用デバイス\) タブ


このトピックで説明 WDF Verifier の**WDF を使用してデバイス**ページ。 このページには、WDF のドライバーを使用しているすべてのデバイスが一覧表示されます。 デバイスを選択すると、強調表示されているデバイスの WDF ドライバー スタックを参照してください。 この画面からの検証の設定を変更することもできます。

このページの上部にあるインストール済みランタイムとドライバーの概要がわかります。 WDF のドライバーに関連付けられているデバイス インスタンスの一覧を次に示します。

![wdf タブを使用してデバイスのスクリーン ショット](images/wdfverifier-tab2.png)

**WDF ドライバーとデバイス**ボックスで、WDF 関連の設定を持つデバイスには前に、+ です。 設定を変更するには、デバイス ID またはノード内の個々 の設定を右クリックします。

デバイスまたは個々 の設定を選択すると、ボックスの右側に、デバイスのフレンドリ名が表示されます。

さらに、すべてのデバイスに WDF ドライバーに表示されます、 **WDF ドライバー スタックのデバイスを**ボックスに、スタックの上から下への順序で。 たとえば、上フィルター上部に表示機能ドライバーを続けてし、フィルターを削減します。

UMDF ドライバーを使用している場合は、カーネル デバイス スタックの適切な場所にスタックの順序でも表示されます。

同様に、ノードを開き、ドライバー スタックで + をクリックし、各ドライバーの値を変更するを右クリックし、できます。

変更する場合、 **WDF を使用してデバイス** ページで、その変更反映された表示されます、 **WDF ドライバー**ページ。

 

 





