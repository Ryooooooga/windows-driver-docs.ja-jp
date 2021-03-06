---
title: Enhanced Storage Certificate Management Tool の概要
description: Enhanced Storage Certificate Management Tool の概要
ms.assetid: 963e6510-d62f-421f-9c3d-781092f98969
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4d498a3be935663bfc1467b5ff5e167cb654ebf7
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67361266"
---
# <a name="overview-of-the-enhanced-storage-certificate-management-tool"></a>Enhanced Storage Certificate Management Tool の概要


Windows 7 以降のオペレーティング システムが提供、*拡張記憶域*USB ストレージ デバイスをコンピューターに接続されているインフラストラクチャ。 このインフラストラクチャは、デバイスの認証との通信に標準的な IEEE 1667 のバージョン 1.1 に基づきます。 IEEE 1667 standard の概要については、IEEE 1667 の標準的な用語と定義を参照してください。

記憶域証明書の管理の強化されたツールは、このツールは、次の機能を提供します。 標準的な IEEE 1667 に対応している USB 記憶装置に ASC ストア内で証明書を管理します。

-   ホストから ASC ストアに証明書をインポートします。

    証明書を追加または (ASCm 証明書) を除く標準的な IEEE 1667 に対応している任意の USB 記憶装置の ASC ストア内で置換できます。

    詳細については、次を参照してください。[拡張記憶域証明書の管理ツールを使って証明書をインポートする](importing-certificates-by-using-the-enhanced-storage-certificate-manag.md)します。

-   ASC ストアから証明書をファイルにエクスポートします。

    エクスポートするとすぐにこれらの証明書が IEEE 1667 標準に準拠している他の USB 記憶装置の ASC ストアにインポートすることができます。

-   ASC ストアから証明書を削除します。

    個々 の証明書は ASCm と PCp 証明書を除く、ASC ストアから削除できます。

-   ASCm と PCp 証明書を除く、ASC ストアから証明書をすべてクリアします。

-   その初期状態に戻し、ASC ストアを初期化します。

    これにより、ASCm 証明書を除く、ASC ストアから証明書をすべてクリアされます。

-   ASC ストア内の証明書を一覧表示します。

**注**  追加、削除、またはこのツールを使用して ASCm 証明書を削除することはできません。

 

記憶域証明書の管理の強化されたツールは、USB ストレージ デバイスで機能する IEEE 1667 コマンドを発行して、これらの関数を実行します。 各 USB ストレージ デバイスは、次の形式で一意のボリューム名を使用して指定されます。

```
\\?\USB_Hardware_ID{GUID}
```

各項目の意味は次のとおりです。

-   *USB\_ハードウェア\_ID*されているハードウェアや、USB ストレージ デバイスの互換性のある識別子 (ID)。 これらの Id の詳細については、次を参照してください。 [USB デバイスの識別子](https://docs.microsoft.com/windows-hardware/drivers/install/identifiers-for-usb-devices)します。

-   デバイス インスタンスを表す GUID。

たとえば、USB ストレージ デバイスのボリューム名の例は、次のように。

```
\\?\usbstor#ieee1667control&ven_&prod_&rev_#123456789&0&control#{4f40006f-b933-4550-b532-2b58cee614d3}
```

**注**  IEEE 1667 準拠 USB ストレージ デバイスをコンピューターに現在接続されているボリューム名の一覧を生成する入力**EhStorCertMgrCmd/List**コマンドライン。

 

USB ストレージ デバイスで機能する IEEE 1667 コマンドを発行するには、ユーザーは、デバイスを使用して認証する必要があります。 認証は、PCp の証明書とユーザーに提供される秘密キーに基づきます。 ユーザーに、PCp の適切な証明書と秘密キーを持たない場合、ユーザーには、記憶域証明書の管理の強化されたツールによるプロビジョニングについては、デバイスへのアクセスはありません。

 

 





