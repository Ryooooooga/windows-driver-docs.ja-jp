---
title: デバイスとドライバー パッケージのアンインストール方法
description: デバイスとドライバー パッケージのアンインストール方法
ms.assetid: 0f4f0bbf-ca8f-47ef-b70b-d023bba9b842
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d5b38ca5dac8bd56d5b0b2eea096aa9d2475d664
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386406"
---
# <a name="how-devices-and-driver-packages-are-uninstalled"></a>デバイスとドライバー パッケージのアンインストール方法


このセクションは、デバイスの削除を行う必要があるものの概要を説明し、[ドライバー パッケージ](driver-packages.md)します。 次のいずれかを実行して、これらのアクションを実行します。

-   [デバイス マネージャー](using-device-manager.md)します。

-   デバイスのインストール アプリケーションを呼び出す、 [SetupAPI](setupapi.md)と[デバイスのインストール](https://docs.microsoft.com/previous-versions/ff541299(v=vs.85))関数。

必要となる操作には、次のようなものがあります。

-   [デバイスのアンインストール](#uninstalling-the-device)

-   [ドライバー ストアからドライバー パッケージを削除します。](#deleting-a-driver-package-from-the-driver-store)

-   [インストールされているドライバーのバイナリ ファイルを削除します。](#deleting-the-binary-files-of-the-installed-driver)

**注**  これらのアクションは順番に実行する必要はありません。

 

### <a href="" id="uninstalling-the-device"></a> デバイスのアンインストール

[デバイス] ノードをアクションを削除しますこのアンインストール (*devnode*) システムで、デバイスの物理インスタンスを表します。 次のメソッドのいずれかを使用して Devnode は削除されます。

-   デバイス マネージャー。 詳細については、次を参照してください。[デバイス マネージャーを使用して](using-device-manager.md)します。

-   デバイスのインストール アプリケーションを呼び出す、 [SetupAPI](setupapi.md) [**SetupDiCallClassInstaller** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdicallclassinstaller)関数の要求で[ **DIF_削除**](https://docs.microsoft.com/windows-hardware/drivers/install/dif-remove)します。 詳細については、次を参照してください。[セットアップ関数の一般的な使用](using-general-setup-functions.md)します。

-   デバイスのインストール アプリケーションを呼び出す、SetupAPI [ **DiUninstallDevice** ](https://docs.microsoft.com/windows/desktop/api/newdev/nf-newdev-diuninstalldevice)関数 (Windows 7 および Windows の以降のバージョン)。 詳細については、次を参照してください。[デバイス インストールの機能を使用して](using-device-installation-functions.md)します。

これらのメソッドのいずれかを使用して、デバイスがアンインストールされると、プラグ アンド プレイ (PnP) マネージャーは、デバイスのインストール中に作成されたシステム状態のサブセットを削除します。 たとえば、ドライバーのバイナリ ファイルとデバイス間の関連付けを削除します。 この関連付けは、サービス コントロール マネージャー (SCM) によってをデバイスの適切なドライバーの読み込みに使用されます。

これをアンインストール、インストール プロセス中に実行されたすべてのアクションを取り消すことはできません。 たとえば、ドライバー パッケージまたは*共同インストーラー* (とその他のいくつかのレジストリ操作) は変更されません。

**注**  これをアンインストールした後が完了したら、devnode、デバイスが存在しなくただしの[ドライバー パッケージ](driver-packages.md)は引き続き存在、[ドライバー ストア](driver-store.md)します。 PnP マネージャーは、再 (ときに、デバイスが電源が入っていないし、接続し、もう一度) などのデバイスを列挙する場合、PnP マネージャーがデバイスの新しいインスタンスとして扱われ、ドライバー ストアからドライバー パッケージをインストールします。

 

### <a href="" id="deleting-a-driver-package-from-the-driver-store"></a> ドライバー ストアからドライバー パッケージを削除します。

アクションの削除をファイルに関連付けられているこのアンインストール、[ドライバー パッケージ](driver-packages.md)から、[ドライバー ストア](driver-store.md)PnP マネージャーの内部データベースから、関連するメタデータを削除します。 この操作も削除されます、 [INF ファイル](overview-of-inf-files.md)INF のシステム ディレクトリから、ドライバー パッケージに関連付けられています。

ドライバー パッケージがドライバー ストアから削除された後、デバイスにインストールできますが不要になったです。 ドライバー パッケージを restaged し、にインストールする必要があります、[ドライバー ストア](driver-store.md)光学式メディア、ネットワーク共有では、Windows Update など、元のソースからです。

ドライバー ストアからドライバー パッケージを削除する前に必ずそれを使用しているすべてのデバイスをアンインストールしてください。

**重要な**  手動で削除する必要があります、[ドライバー パッケージ](driver-packages.md)から、[ドライバー ストア](driver-store.md)します。 生じることが、INF の間に不整合ファイル、ドライバー ストア カタログ、およびドライバー ストアにドライバー。 ドライバー ストアに同じドライバー パッケージを段階的にできることもあります。

 

### <a href="" id="deleting-the-binary-files-of-the-installed-driver"></a> インストールされているドライバーのバイナリ ファイルを削除します。

[デバイス マネージャー](using-device-manager.md) PnP マネージャーではインストールされているターゲットの場所からの削除のドライバー バイナリがサポートされていません。 

ドライバー パッケージをアンインストールすると、関連するドライバーのバイナリはデバイスまたはアプリケーションで引き続き使用可能性があります。 バイナリを削除すると、システム障害につながります。 すべてのドライバー バイナリを削除する前にことをバイナリがないことを確認して、他のコンポーネント、システム上でまだ使用されていると、安全に削除できます。



 

 





