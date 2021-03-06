---
title: デバイスのインストール アプリケーションの記述に関するガイドライン
description: デバイスのインストール アプリケーションの記述に関するガイドライン
ms.assetid: 7f364b95-98ca-479a-8cdb-5e5e77c70cfa
keywords:
- インストール アプリケーション WDK、ガイドライン
- デバイスのインストール アプリケーション WDK、ガイドライン
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dd25f55a13798c46185113374933264294c157b3
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383841"
---
# <a name="guidelines-for-writing-device-installation-applications"></a>デバイスのインストール アプリケーションの記述に関するガイドライン


*デバイスのインストール アプリケーション*   *する必要があります*次の操作を行います。

-   インストールするすべてのデバイス固有のアプリケーションの削除をサポートします。 アンインストール プロセスの一環としてデバイスのインストール アプリケーションかどうか、関連するデバイスがシステムにまだ存在して、そうである場合に、ユーザーに警告を確認する必要があります。

-   ガイドラインに従う[64 ビット システムでデバイスをインストールする](device-installations-on-64-bit-systems.md)します。

-   Microsoft Windows インストーラー (MSI) を使用してインストールしていたし、で提供されるすべてのアプリケーションを一覧表示、Windows Vista 以降**プログラムと機能**コントロール パネルの します。 必要に応じて、これらの項目をアンインストールできます。

-   Windows Vista より前のバージョンの Windows では、Microsoft Windows インストーラー (MSI) を使用してインストールしていたし、で提供されるすべてのアプリケーションを一覧表示**プログラムの追加または削除**コントロール パネルの します。 必要に応じて、これらの項目をアンインストールできます。

-   Microsoft Windows アプリケーションのガイドラインに従います。 参照してください、 [Microsoft Developer Network](https://go.microsoft.com/fwlink/p/?linkid=8714)詳細については、web サイト。

デバイスのインストール アプリケーション*できます*次の操作を行います。

-   [デバイス固有のアプリケーションをインストールします。](installing-device-specific-applications.md)

    **注**  を適切なデバイス固有のアプリケーションを送信することを強くお勧め[ハードウェア認定キット (HCK)](https://go.microsoft.com/fwlink/p/?linkid=227016)ソフトウェア。 参照してください、 [Microsoft Developer Network](https://go.microsoft.com/fwlink/p/?linkid=8714)詳細については、web サイト。

     

-   [ドライバー パッケージの事前読み込み](preloading-driver-packages.md)

-   [プレインストールのドライバー パッケージ](preinstalling-driver-packages.md)

デバイス インストール アプリケーション*は許可されません*次の操作を行います。

-   コピーまたは特にすべてのファイルを上書きするように指示します。*inf*および *。sys*ファイル。

-   ハードウェアが削除された場合でも、インストールされているドライバー ファイル、アンインストール操作中にシステムから削除します。

-   不要なシステムの再起動を強制します。 再起動は、通常の PnP デバイスまたはソフトウェア アプリケーションをインストールするために必要ありません。 *BRebootRequired*のパラメーター、 [ **UpdateDriverForPlugAndPlayDevices** ](https://docs.microsoft.com/windows/desktop/api/newdev/nf-newdev-updatedriverforplugandplaydevicesa)関数は、再起動の必要性を示します。

-   使用 RunOnce レジストリ キー、システムの再起動が要求されるためです。

-   ソフトウェア アプリケーションをインストールするために安全にデバイスのインストール中にシステムの状態を保証できないため、デバイスのインストール アプリケーションを開始するのにには、デバイスまたはクラスの共同インストーラー クラスのインストーラーを使用します。 具体的には、デバイスのインストール アプリケーションは、サーバー側のインストール時に実行する場合、システムによっては応答を停止します。

    使用してデバイスのインストール後にデバイスのインストールのアプリケーションを安全に起動できます[完了-インストール アクション](finish-install-actions--windows-vista-and-later-.md)クラスのインストーラーや共同インストーラーによって提供されます。

    共同インストーラーの詳細については、次を参照してください。[共同インストーラーの作成](writing-a-co-installer.md)です。

-   スタートアップ グループを使用して開始*デバイス インストール アプリケーション*します。

-   使用*win.ini*デバイス インストール アプリケーションを起動するエントリ。

-   ユーザーが任意のデバイス固有のアプリケーションをインストールするを強制しない限り、デバイスは、アプリケーションがなければ動作しません。 受信トレイ アプリケーションがこのような機能をサポートしていない場合の例には構成可能なキーボードのキーを設定するため、または、モデムの国/地域コードを設定するためのユーティリティが含まれます。

 

 





