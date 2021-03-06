---
title: ドライバーの読み込み順序の指定
description: ドライバーの読み込み順序の指定
ms.assetid: 2e06671a-5664-4042-bc7a-e8ab12938cea
keywords:
- INF ファイル WDK デバイスのインストール、ドライバーの読み込み順序
- ドライバーの読み込み順序 WDK INF ファイル
- 読み込み順序 WDK INF ファイル
- サービス-インストール-セクション WDK INF ファイル
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 402ee452d5ba77b73b8c85bc46ae4492d232898b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72828700"
---
# <a name="specifying-driver-load-order"></a>ドライバーの読み込み順序の指定





ほとんどのデバイスでは、コンピューター上のデバイスの物理階層によって、Windows と PnP マネージャーがドライバーを読み込む順序が決まります。 Windows と PnP マネージャーは、システムルートデバイスで開始されるデバイスを構成してから、ルートデバイス (PCI アダプターなど) の子デバイス、それらのデバイスの子デバイスなどを構成します。 PnP マネージャーは、デバイスが構成されているときに、別のデバイス用にドライバーが読み込まれていない場合、各デバイスのドライバーを読み込みます。

INF ファイルの設定は、ドライバーの読み込み順序に影響を与える可能性があります。 このトピックでは、ドライバーの[**INF AddService ディレクティブ**](inf-addservice-directive.md)によって参照される*サービスインストールセクション*でベンダーが指定する関連の値について説明します。 具体的には、このトピックでは、 **Starttype**、 **bootflags**、 **loadordergroup**、および**Dependencies**の各エントリについて説明します。

ドライバーは、 **Starttype**を指定するために次の規則に従う必要があります。

-   PnP ドライバー

    Pnp ドライバーのスタートアップの種類は SERVICE_DEMAND_START (0x3) である必要があります。 pnp マネージャーがドライバーサービスによってデバイスを検出したときにドライバーを読み込むことができるように指定します。

-   コンピューターを起動するために必要なデバイスのドライバー

    デバイスでコンピューターを起動する必要がある場合は、デバイスのドライバーの開始の種類が SERVICE_BOOT_START (0x0) になっている必要があります。

-   PnP で列挙できないデバイスを検出する非*ブート開始ドライバー*

    PnP で列挙されていないデバイスの場合、ドライバーは[**IoReportDetectedDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-ioreportdetecteddevice)を呼び出すことによってデバイスを pnp マネージャーに報告します。 このようなドライバーには、システムの初期化中に Windows によってドライバーが読み込まれるように、開始の種類が SERVICE_SYSTEM_START (0x01) である必要があります。

    PnP 以外のハードウェアを報告するドライバーのみが、この開始の種類を設定する必要があります。 ドライバーが PnP デバイスと非 PnP デバイスの両方をサービスしている場合、この開始の種類を設定する必要があります。

-   サービスコントロールマネージャーによって起動される必要がある、PnP 以外のドライバー

    このようなドライバーには、SERVICE_AUTO_START (0x02) という開始の種類が必要です。 PnP ドライバーでは、この開始の種類を設定しないでください。

PnP ドライバーは、Windows がドライバーサービスによってデバイスを構成するときに読み込むことができるように書き込む必要があります。 逆に、ドライバーは、ドライバーサービスが使用していないデバイスが存在しないと判断した場合はいつでもアンロードできる必要があります。 PnP ドライバーが依存するドライバーの負荷順序は、次のようになります。

1.  子デバイスのドライバーは、親デバイスのドライバーが読み込まれるという事実によって異なる場合があります。

2.  デバイススタック内のドライバーは、その下にあるすべてのドライバーが読み込まれるという事実に依存します。

    たとえば、関数ドライバーは、下位フィルタードライバーが読み込まれていることを特定できます。

    ただし、デバイススタック内のドライバーは、他のデバイスが構成されているときに既に読み込まれている可能性があるため、デバイスの下位のドライバーの後に順番に読み込まれることに依存することはできないことに注意してください。

フィルターグループ内のフィルタードライバーは、その負荷の順序を予測できません。 たとえば、デバイスに3つの上位フィルタードライバーが登録されている場合、これら3つのドライバーはすべて、関数ドライバーの後に読み込まれますが、上位フィルターグループ内の任意の順序で読み込むことができます。

ドライバーが別のドライバーに対して明示的な負荷順序の依存関係を持っている場合、その依存関係は親子関係を通じて実装する必要があります。 子デバイスのドライバーは、子ドライバーが読み込まれる前に、読み込まれている親デバイスのドライバーによって異なる場合があります。

正しい**starttype**値を設定することの重要性を高めるために、次の一覧では、Windows と PnP マネージャーが INF ファイルの**starttype**エントリをどのように使用するかを説明します。

1.  システムの起動時に、オペレーティングシステムローダーは、カーネルに制御を転送する前に、SERVICE_BOOT_START タイプのドライバーを読み込みます。 これらのドライバーは、カーネルが制御を取得するときにメモリ内にあります。

    ブート開始ドライバーは、INF **Loadordergroup**エントリを使用して、読み込みの順序を付けることができます。 (ブート開始ドライバーは、ほとんどのデバイスが構成される前に読み込まれます。そのため、デバイス階層によって負荷の順序を決定することはできません)。オペレーティングシステムは、ブート開始ドライバーの INF**依存関係**エントリを無視します。

2.  PnP マネージャーは、SERVICE_BOOT_START ドライバーの**Driverentry**ルーチンを呼び出して、ドライバーがブートデバイスにサービスを実行できるようにします。

    ブートデバイスに子デバイスがある場合は、それらのデバイスが列挙されます。 子デバイスは、ドライバーがブート開始ドライバーでもある場合に構成され、開始されます。 デバイスのドライバーがすべてのブート開始ドライバーでない場合、PnP マネージャーはデバイスのデバイスノード (*devnode*) を作成しますが、デバイスはまだ起動しません。

3.  すべてのブートドライバーが読み込まれ、ブートデバイスが起動すると、pnp マネージャーによって残りの PnP デバイスが構成され、ドライバーが読み込まれます。

    PnP マネージャーは、まだ開始されていないデバイスツリー (つまり、前の手順で開始されていない devnodes) を示します。 各デバイスが起動すると、PnP マネージャーはデバイスの子を列挙します (存在する場合)。

    これらのデバイスを構成するときに、PnP マネージャーは、ドライバーの**starttype**値 ( **STARTTYPE**が SERVICE_DISABLED の場合を除く) に*関係なく*、デバイスのドライバーを読み込み、デバイスの起動に進みます。 これらのドライバーの多くは、SERVICE_DEMAND_START ドライバーです。

    PnP マネージャーは、INF**依存関係**エントリの結果として作成されたレジストリエントリと、この手順で読み込まれるドライバーの**loadordergroup**エントリを無視します。 負荷の順序は、物理デバイスの階層に基づいています。

    この手順の最後に、すべてのデバイスが構成されます。ただし、PnP で列挙できないデバイスと、それらのデバイスの子孫のデバイスは除きます。 (子孫は、PnP 列挙可能である場合とない場合があります)。

4.  PnP マネージャーは、まだ読み込まれていない**Starttype** SERVICE_SYSTEM_START のドライバーを読み込みます。

    これらのドライバーは、非 PnP デバイスを検出して報告します。 PnP マネージャーは、これらのドライバーの INF **Loadordergroup**エントリの結果であるレジストリエントリを処理します。 これらのドライバーの INF**依存関係**のエントリによって作成されたレジストリエントリは無視されます。

5.  サービスコントロールマネージャーは、まだ読み込まれていない**Starttype** SERVICE_AUTO_START のドライバーを読み込みます。

    サービスコントロールマネージャーは、サービスの**依存関係 Ongroup**と**依存**関係に関して、サービスデータベース情報を処理します。 この情報は、INF **Addservice**エントリの**依存関係**エントリに含まれています。 **依存関係**情報は、必要な pnp ドライバーがシステムスタートアップの前の手順で読み込まれていたため、非 PnP ドライバーに対してのみ処理されることに注意してください。 サービスコントロールマネージャーは、INF **Loadordergroup**情報を無視します。

    サービスコントロールマネージャーの詳細については、Microsoft Windows SDK のドキュメントを参照してください。

### <a name="using-bootflags-to-promote-a-drivers-starttype-at-boot-depending-on-boot-scenario"></a>ブート時にブート時にブートフラグを使用してドライバーの StartType を昇格する方法

オペレーティングシステムは、ドライバーの INF に指定されている**Bootflags**の値に応じて、ドライバーの**starttype**をブート開始ドライバーに昇格させることができます。 INF ファイルでは、16進数の値として表現された、次の数値の1つ以上 (論理和) を指定できます。

-   ネットワークブート時にドライバーをブート開始ドライバーに昇格させる必要がある場合は、 **0x1** (CM_SERVICE_NETWORK_BOOT_LOAD) を指定します。
-   VHD からブートするときにドライバーを昇格する必要がある場合は、 **0x2** (CM_SERVICE_VIRTUAL_DISK_BOOT_LOAD) を指定します。
-   USB ディスクから起動しているときにドライバーを昇格させる必要がある場合は、 **0x4** (CM_SERVICE_USB_DISK_BOOT_LOAD) を指定します。
-   SD ストレージから起動しているときにドライバーを昇格する必要がある場合は、 **0x8** (CM_SERVICE_SD_DISK_BOOT_LOAD) を指定します。
-   USB 3.0 コントローラーのディスクから起動しているときにドライバーを昇格させる必要がある場合は、 **0x10** (CM_SERVICE_USB3_DISK_BOOT_LOAD) を指定します。
-   測定ブートが有効になっている状態で起動しているときにドライバーを昇格させる必要がある場合は、 **0x20** (CM_SERVICE_MEASURED_BOOT_LOAD) を指定します。
-   検証ツールでブートしているときにドライバーを昇格させる必要がある場合は、 **0x40** (CM_SERVICE_VERIFIER_BOOT_LOAD) を指定します。
-   ドライバーを WinPE ブートで昇格させる必要がある場合は、 **0x80** (CM_SERVICE_WINPE_BOOT_LOAD) を指定します。

ブート時にドライバーの**Starttype**を昇格する方法の詳細については、「 [**INF addservice ディレクティブ**](inf-addservice-directive.md)」を参照してください。

 

 





