---
title: アーキテクチャと I²C トランスポート経由で HID の概要
description: このセクションでは、HID を I²C トランスポート経由でサポートするデバイスのドライバー スタックについて説明します。
ms.assetid: 99384729-552C-4847-AA35-E0D413018104
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d22cf5684dbb295f292c8b009041f64caae77f3c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67375789"
---
# <a name="architecture-and-overview-for-hid-over-the-ic-transport"></a>アーキテクチャと I²C トランスポート経由で HID の概要


このセクションでは、HID を I²C トランスポート経由でサポートするデバイスのドライバー スタックについて説明します。

## <a name="architecture-and-overview"></a>アーキテクチャと概要


HID I²C ドライバー スタックは、既存および新規コンポーネント、Microsoft によって提供されるだけでなく I²C シリコンの製造元によって提供されるコンポーネントで構成されます。 次の図は、スタックとこれらのコンポーネントを示しています。

![i2c ドライバー スタックの上を非表示](images/hid-i2c-arch.png)

Windows 8 は、オペレーティング システムを効率的に通信する低電力、単純なバスのインターフェイスを提供します。 このインターフェイスはシンプルな周辺機器バス (SPB) と呼ばれます Inter-Integrated 回線 (I²C) とシリアル ペリフェラル インターフェイス (SPI) のようにバスをサポートしています。 SPB の詳細については、単純な周辺機器のバスのトピックを参照してください。

Windows 8 では、I²C 経由で HID のプロトコルの仕様のバージョン 1.0 を実装する KMDF ベース HID ミニポート ドライバーを提供します。 このドライバーは、HIDI2C.sys という名前です。 Windows では、Advanced Configuration and Power Interface (ACPI) によって公開されている互換性のある ID 一致に基づくこのドライバーを読み込みます。 ドライバーにより HID Ioctl アプリケーションを使用するアプリを非表示の Ioctl と API のセットを利用するソフトウェアの互換性のレベルします。 注意が必要ですが、またはデータがあるとき、デバイスは、ホストをアサートします。 ただし、アサーションが発生する前に、GPIO 接続が存在する必要があります。

**注**  HIDI2C.sys デバイス ドライバーが I²C バスのみをサポートしています。 Windows 8 の SPI、sm バス、または他の低電力のバスをサポートしてはありません。

 

## <a name="the-ic-controller-driver"></a>I²C コント ローラーのドライバー


I²C コント ローラーのドライバーでは、読み取りおよび実行する書き込み操作のシリアル周辺バス (SPB) IOCTL インターフェイスを公開します。 このドライバーは、実際のコント ローラーの組み込み関数 (たとえば、I²C) を提供します。 コント ローラーのドライバーに代わって、SPB クラスの拡張は、リソース ハブのすべての対話を処理し、同時のターゲットを管理するために必要なキューを実装します。

**注**  SPB プラットフォームと互換性がある I²C バスがないシステムでは、HID I²C ドライバーは機能しません。 デバイスのシステム I²C バスが SPB プラットフォームと互換性のあるかどうかを判断する、システムの製造元に問い合わせてください。

 

## <a name="the-gpio-controller-driver"></a>GPIO コント ローラーのドライバー


一般的な目的の入出力 (GPIO) コント ローラーは、GPIO 経由でデバイスからの割り込みを提供します。 これは、多くの場合、Windows の新しいデータまたはその他のイベントを信号に GPIO ピンを使用する単純なスレーブ コンポーネントです。 GPIO は、I²C チャネル以外の方法でデバイスを制御できます。

## <a name="the-resource-hub"></a>リソース ハブ


SoC のプラットフォームでの接続は、SoC. で使用されているバス上のデバイス列挙の標準がないために、通常検出不可能です、します。 その結果、Advanced Configuration and Power Interface (ACPI) でこれらのデバイスを静的に定義する必要があります。 さらに、コンポーネントでは、多くの場合、厳密な分岐ツリー構造ではなく、複数のバスにまたがる複数の依存関係があります。

リソースのハブは、すべてのデバイスとコント ローラー間の接続を管理するプロキシです。 HIDI²C ドライバーでは、リソース ハブを使用して、適切なコント ローラー ドライバーへのデバイスを開く要求を再ルーティングします。 リソースのハブの詳細についてを参照してください、 [SPB 接続デバイス用の接続 Id](https://docs.microsoft.com/windows-hardware/drivers/spb/connection-ids-for-spb-connected-peripheral-devices)トピック。

 

 




