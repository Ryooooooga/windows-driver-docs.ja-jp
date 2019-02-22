---
title: コンポーネントとネットワーク コンポーネントのインストールに使用されるファイル
description: コンポーネントとネットワーク コンポーネントのインストールに使用されるファイル
ms.assetid: be056ff1-0b92-4e81-a506-7750012aad4e
keywords:
- ネットワーク コンポーネント コンポーネントおよびファイルの使用、WDK をインストールします。
- ネットワーク コンポーネントのインストール コンポーネントと使用するファイルの WDK
- WDK のネットワーク インストールのコンポーネント
- クラスのインストーラーの WDK ネットワーク
- WDK ネットワークの共同インストーラー
- DLL の WDK のネットワーク移行
- テキスト モードのセットアップの WDK ネットワーク
- ドライバーのイメージ ファイルの WDK ネットワーク
- ドライバー ライブラリ ファイルの WDK ネットワーク
- DLL の WDK ネットワークの移行
- ベンダーから提供されたインストール ファイルの WDK ネットワーク
- ファイルの WDK ネットワーク コンポーネントがインストールされます。
ms.date: 01/16/2019
ms.localizationpriority: medium
ms.openlocfilehash: 2b3c4163ad8b7bb88193f737b08bd499225b1a37
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56557611"
---
# <a name="components-and-files-used-for-network-component-installation"></a>コンポーネントとネットワーク コンポーネントのインストールに使用されるファイル

次のコンポーネントとファイルは、ネットワーク ドライバーをインストールするに使用されます。

-   1 つ以上の情報 (INF) ファイル

-   必要なクラスのインストーラーと、ミニポート ドライバーの省略可能な共同インストーラー

-   INetCfg のプロトコルとフィルター ドライバー

-   省略可能な通知オブジェクト

1 つ以上の前のコンポーネント、だけでなく仕入先はまた、必要に応じて、次のファイルを提供します。

-   1 つまたは複数のデバイス ドライバー (.sys) のイメージ ファイルおよびドライバー ライブラリ (.dll) ファイル

-   ドライバー カタログのファイル

-   テキスト モードのセットアップ情報ファイル (txtsetup.oem)

## <a name="inf-files"></a>INF ファイル

各ネットワーク コンポーネント、コンポーネントをインストールするネットワーク クラスのインストーラーを使用する情報 (INF) ファイルが必要です。 ネットワークの INF ファイルは、共通の INF ファイル形式に基づいています。 INF ファイルの形式に関する詳細については、次を参照してください。 [INF ファイルのセクションとディレクティブ](https://msdn.microsoft.com/library/windows/hardware/ff547433)します。

ネットワーク コンポーネントの INF ファイルの作成の詳細については、次を参照してください。[ネットワーク INF ファイルの作成](creating-network-inf-files.md)です。

## <a name="inetcfg"></a>INetCfg

呼び出すことによってこれらの NDIS プロトコルとフィルター ドライバーがインストールされている現在、`INetCfg`ファミリの[構成のネットワーク インターフェイス](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff559080(v%3dvs.85))します。 たとえば、ネットワークのコンポーネントをインストールまたは削除、ドライバー ライターを呼び出すには[INetCfgClassSetup](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff547709%28v%3dvs.85%29)インターフェイス。 

ドライバー作成者がこのインターフェイスのいずれかの呼び出しをプログラムでできますか、使用できる[netcfg.exe](https://docs.microsoft.com/windows-server/administration/windows-commands/netcfg)、呼び出す`INetCfg`代わりにします。

プロトコル ドライバーのインストールの詳細については、次を参照してください。 [NDIS ドライバーのインストールのプロトコル](ndis-protocol-driver-installation.md)します。

フィルター ドライバーのインストールの詳細については、次を参照してください。 [NDIS フィルター ドライバーのインストール](ndis-filter-driver-installation.md)します。

## <a name="notify-object"></a>オブジェクトへの通知します。

ネットワーク プロトコル、クライアント、またはサービスなどのソフトウェア コンポーネントを持つことができます、*通知オブジェクト*します。 通知オブジェクトは、ユーザー インターフェイスを表示、イベントをバインドできるように、コンポーネント、バインディング プロセスをいくつかの制御し条件付きでインストールまたは削除できるソフトウェア コンポーネントのコンポーネントに通知できます。 詳細については、オブジェクトに通知を参照してください[ネットワーク コンポーネントの通知オブジェクト](notify-objects-for-network-components.md)します。

ネットワーク アダプターには、通知オブジェクトを含めることはできません。 共同インストーラーことができます。 共同インストーラーの詳細については、次を参照してください。[共同インストーラーの作成](https://msdn.microsoft.com/library/windows/hardware/ff554011)です。

## <a name="vendor-supplied-files"></a>ベンダーから提供されたファイル

仕入先には、通常のドライバー (.sys) のイメージ ファイルとドライバー ライブラリ (.dll) ファイルで構成されると、デバイスの 1 つまたは複数のドライバーが用意されています。 仕入先がオプションのドライバーを指定しても*カタログ ファイル*します。 仕入先は、そのドライバー パッケージのテストと署名 Windows Hardware Quality Lab (WHQL) に送信することで、デジタル署名を取得します。 WHQL は、カタログ (.cat) ファイルを使用して、パッケージを返します。 仕入先は、デバイスの INF ファイルで、カタログ ファイルを一覧表示する必要があります。

省略可能なテキスト モードのセットアップ情報ファイル (txtsetup.oem) は、ベンダーによっても指定することがあります。 ネットワーク デバイスは、マシンを起動する必要は、か、オペレーティング システムのキットでは、ドライバーまたはデバイスのドライバーを含める必要があるようなデバイスのベンダーに txtsetup.oem ファイルを提供する必要があります。 Txtsetup.oem ファイルには、テキスト モードのセットアップ中にデバイスをインストールするセットアップのシステム コンポーネントによって使用される情報が含まれています。

 

 




