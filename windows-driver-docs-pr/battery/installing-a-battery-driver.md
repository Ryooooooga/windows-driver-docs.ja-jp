---
title: バッテリ ドライバーのインストール
description: バッテリ ドライバーのインストール
ms.assetid: 09db4d88-0cac-4171-8d05-d15a2cf4dab4
keywords:
- バッテリ miniclass ドライバー WDK をインストールします。
- バッテリ クラス ドライバー WDK をインストールします。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: db85b577dee4fd28db8750063c8e90243a01d99e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67364750"
---
# <a name="installing-a-battery-driver"></a>バッテリ ドライバーのインストール


## <span id="ddk_installing_a_battery_driver_dg"></span><span id="DDK_INSTALLING_A_BATTERY_DRIVER_DG"></span>


バッテリ ドライバーの INF ファイルでは、ドライバーとデバイスの制御に関する情報を指定します。 バッテリ クラスのメンバーであるすべてのデバイスのバッテリおよびバッテリ クラスのインストーラーには、ドライバーがインストールされます。

このセクションでは、INF ファイルでバッテリに固有のエントリについて説明します。 作成と INF ファイルを配布するドライバーのインストールの詳細については、次を参照してください。 [INF ファイルを作成する](https://docs.microsoft.com/windows-hardware/drivers/install/overview-of-inf-files)と[INF ファイルのセクションとディレクティブ](https://docs.microsoft.com/windows-hardware/drivers/install/inf-file-sections-and-directives)します。

バッテリ ドライバーの INF ファイルには、以下に示すセクションが含まれます。

### <a name="span-idversionspanspan-idversionspanspan-idversionspanversion"></a><span id="Version"></span><span id="version"></span><span id="VERSION"></span>バージョン

バッテリ ドライバーの INF ファイルは、バッテリ クラスと、その GUID を指定します。 を使用して、 [ **INF バージョン セクション**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-version-section)次の例のように。

``` syntax
[Version]
Signature="$WINDOWS NT$"
Class=Battery
ClassGuid={72631e54-78a4-11d0-bcf7-00aa00b7b32a}
Provider=%MyCo%
```

その %myco% を定義する必要がありますに注意してください、 [ **INF 文字列セクション**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-strings-section) (示されていません)。

### <a name="span-iddestinationdirsspanspan-iddestinationdirsspanspan-iddestinationdirsspandestinationdirs"></a><span id="DestinationDirs"></span><span id="destinationdirs"></span><span id="DESTINATIONDIRS"></span>DestinationDirs

[ **INF DestinationDirs セクション**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-destinationdirs-section)、バッテリ ドライバーの INF ファイルをすべての既定値としてドライバー ディレクトリ (12) を指定します。

``` syntax
[DestinationDirs]
DefaultDestDir = 12
```

### <a name="span-idmanufacturerspanspan-idmanufacturerspanspan-idmanufacturerspanmanufacturer"></a><span id="Manufacturer"></span><span id="manufacturer"></span><span id="MANUFACTURER"></span>製造元

[ **INF 製造元セクション**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-manufacturer-section)デバイスの製造元を定義します。

``` syntax
[Manufacturer]
%MyCo%=MyCompany
```

### <a name="span-idmodelsspanspan-idmodelsspanspan-idmodelsspanmodels"></a><span id="Models"></span><span id="models"></span><span id="MODELS"></span>*モデル*

[ **INF*モデル*セクション**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-models-section) 、バッテリのプラグ アンド プレイ ハードウェア ID を指定します (として示す*pnpid*の例)。 このセクションが EISA スタイル ID を指定する必要がありますも ACPI を通じて、デバイスが列挙されている場合 (として示す*acpidevnum*)。 これらの Id を作成する方法の詳細については、次を参照してください。、 *Advanced Configuration and Power Interface Specification*、を通じて、 [ACPI/電源管理](https://uefi.org/acpi/specs)web サイト。

``` syntax
[MyCompany]
%pnpid.DeviceDesc% = NewBatt_Inst,pnpid
%ACPI\acpidevnum.DeviceDesc% = NewBatt_Inst,ACPI\acpidevnum
```

### <a name="span-idddinstallspanspan-idddinstallspanspan-idddinstallspanddinstall"></a><span id="DDInstall"></span><span id="ddinstall"></span><span id="DDINSTALL"></span>*DDInstall*

[ **INF *DDInstall*セクション**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-ddinstall-section) (という名前の NewBatt\_命令の例では)、 [ **INF CopyFiles ディレクティブ**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-copyfiles-directive)バッテリ クラス ドライバーがコピー (*ため、Battc.sys*) と新しい miniclass ドライバー (*NewBatt.sys*) で指定される宛先に、 **DestinationDirs**ディレクティブ。

``` syntax
[NewBatt_Inst]
CopyFiles = @NewBatt.sys
CopyFiles = @battc.sys
```

### <a name="span-idddinstallservicesspanspan-idddinstallservicesspanspan-idddinstallservicesspanddinstallservices"></a><span id="DDInstall.Services"></span><span id="ddinstall.services"></span><span id="DDINSTALL.SERVICES"></span>*DDInstall*します。サービス

[ **INF *DDInstall*します。サービス セクション**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-ddinstall-services-section)が含まれています、 [ **INF AddService ディレクティブ**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addservice-directive)バッテリ ドライバーに関する追加情報を指定します。 バッテリ ドライバーの INF ファイルは、ドライバーは、通常のエラー処理を使用して、オペレーティング システムの初期化中に開始するカーネル ドライバーであることを示す必要があります。 バッテリのドライバーでは、ロード順序グループ ベースの拡張を指定します。

``` syntax
[NewBatt_Inst.Services]
AddService = NewBatt,2,NewBatt_Service_Inst    ; function driver for the device
 
[NewBatt_Service_Inst]
DisplayName    = %NewBatt.SvcDesc%
ServiceType    = 1 ;    SERVICE_KERNEL_DRIVER
StartType      = 3 ;    SERVICE_DEMAND_START
ErrorControl   = 1 ;    SERVICE_ERROR_NORMAL%
ServiceBinary  = %12%\NewBatt.sys
```

 

 




