---
title: PnP のコンポーネント
description: PnP のコンポーネント
ms.assetid: 33612da4-1ddb-40cf-a8a2-838f85b52cd6
keywords:
- PnP WDK カーネルでは、コンポーネント
- プラグ アンド プレイの WDK カーネル、コンポーネント
- PnP WDK のソフトウェア コンポーネント
- PnP ドライバー WDK カーネル
- ユーザー モード PnP マネージャー WDK
- カーネル モード PnP マネージャー WDK
- PnP マネージャー WDK
- PnP コンポーネント WDK ユーザー モード
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3a366b3d7da6c4eedb2ecc0aa32ed3f5dc3a4d5c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67380932"
---
# <a name="pnp-components"></a>PnP のコンポーネント





次の図は、PnP をサポートするために連携して動作するコンポーネントを示しています。

![プラグ アンド プレイ ソフトウェア コンポーネントを示す図します。](images/pnpcomp.png)

PnP マネージャーが 2 つの部分。 カーネル モードの PnP マネージャーとユーザー モードの PnP マネージャー。 カーネル モードの PnP マネージャーは、オペレーティング システムのコンポーネントと構成、管理、およびデバイスを管理するドライバーと対話します。 ユーザー モードの PnP マネージャー クラスのインストーラー、構成して、デバイスをインストールするなど、ユーザー モードのセットアップ コンポーネントとやり取りします。 ユーザー モードの PnP マネージャーは、アプリケーションなどのデバイス変更の通知用のアプリケーションを登録し、デバイスのイベントが発生したとき、アプリケーションに通知するともやり取りします。

PnP ドライバーは、コンピューターで物理ディスク、論理、および仮想デバイスをサポートします。 「PnP ドライバー」という用語は、このセクションで説明されているインターフェイスをサポートする任意の Windows ドライバーを指します。 ほとんどの PnP ドライバーが WDM ドライバーではもあり、したがってソースと互換性のある Windows プラットフォーム間で、いくつかのドライバー サポート WDM を完全に実装することがなく PnP します。

すべてのドライバーには、PnP、電源管理をサポートする必要があります。 1 つのドライバーが PnP や電源管理をサポートしていない場合、全体として、システムの PnP、電源管理のサポートが制限されます。

参照してください[デバイス インストールの概要](https://docs.microsoft.com/windows-hardware/drivers/install/overview-of-device-and-driver-installation)デバイスとドライバーのセットアップについては、(INF) ファイル、CAT ファイル、およびレジストリを含むです。

 

 




