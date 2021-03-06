---
title: ネットワーク コンポーネントのインストール
description: ネットワーク コンポーネントのインストール
ms.assetid: b4e5d73a-4943-498d-bf59-a08e3732baa8
keywords:
- オブジェクトの WDK ネットワーク、ネットワーク コンポーネントのインストールを通知します。
- ネットワークがネットワーク コンポーネントのインストール、WDK をオブジェクトに通知します。
- ネットワーク コンポーネントの手順、WDK をインストールします。
- コンポーネントのインストール手順、WDK をネットワークします。
- 通知の WDK ネットワーク、ネットワーク コンポーネントのインストール
ms.date: 01/07/2019
ms.localizationpriority: medium
ms.openlocfilehash: f308279c7ed2deecc7fc8692b8832f8b7a19a069
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385846"
---
# <a name="installing-network-components"></a>ネットワーク コンポーネントのインストール

ネットワーク構成のサブシステムでは、ネットワーク コンポーネントがインストールされます。

**ネットワーク コンポーネントをインストールするには**

1.  ネットワーク構成のサブシステムは、特定のコンポーネントの種類のクラスのインストーラーを呼び出します。 クラスのインストーラーは、コンポーネントの INF ファイルから情報を取得し、コンポーネントをインストールするセットアップ API を呼び出します。

    コンポーネントに通知オブジェクトが所有している場合、クラスのインストーラーは、通知オブジェクトを格納する DLL の名前を取得します。 この DLL は、コンポーネントの INF ファイルで次のように表示されます。

    ```INF
    HKR, Ndi, ComponentDll,     0,     "notifyobject.dll"
    ```

    クラスのインストーラーは、通知オブジェクトを登録すると、DLL のエントリ ポイント関数を呼び出します。 ネットワーク構成のサブシステムが通知オブジェクトのインスタンスを作成し、オブジェクトを呼び出して[ **INetCfgComponentControl::Initialize** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff547729(v=vs.85))メソッド。 このメソッドは、オブジェクトを初期化し、コンポーネントとネットワークの構成のすべての側面へのアクセスを提供します。

2.  コンポーネントをインストールするために必要な操作を行うには、ネットワーク構成のサブシステムは通知オブジェクトを呼び出します。 [ **INetCfgComponentSetup::Install** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff547762(v=vs.85))メソッド。

    ネットワーク構成のサブシステムが通知オブジェクトを呼び出す場合は、コンポーネントのインストールは無人で実行、 [ **INetCfgComponentSetup::ReadAnswerFile** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff547765(v=vs.85))メソッド。 このメソッドが開き、コンポーネントのパラメーターと呼ばれる無人セットアップ ファイルから取得、*応答ファイル*します。

3.  サブシステムに通知オブジェクトの呼び出し後、ネットワーク構成のサブシステムでは、インスタンスを作成し、通知オブジェクトを初期化します、 [ **INetCfgComponentNotifyGlobal::GetSupportedNotifications** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff547734(v=vs.85))オブジェクトで必要な通知の種類を取得します。 サブシステムでは、この情報を使用して、オブジェクトに必要な通知を送信します。 オブジェクトは、これらの通知を使用して、ネットワークのセットアップと構成オブジェクトを所有するコンポーネントに影響を与える可能性がありますの側面を制御できます。 サブシステムを呼び出す場合など、 [ **INetCfgComponentNotifyGlobal::SysNotifyComponent** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff547736(v=vs.85))オブジェクトに通知するメソッド、サブシステムがインストールされているか、別のネットワーク コンポーネントを削除しますオブジェクトの変更に関連する操作を実行する機会があります。

    ネットワーク構成のサブシステムでは、インスタンスを作成し、通知オブジェクトを初期化します、サブシステムも呼び出して通知オブジェクトのメソッドのいずれかの[INetCfgComponentNotifyBinding](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff547730(v=vs.85))インターフェイス、オブジェクトに通知するには方法の変更の詳細については、サブシステムは、通知オブジェクトを所有するコンポーネントを他のネットワーク コンポーネントをバインドします。

4.  通知オブジェクトの呼び出し、ネットワーク構成のサブシステムのコンポーネントのプロパティをオペレーティング システムに適用する準備ができたら[ **INetCfgComponentControl::ApplyRegistryChanges** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff547727(v=vs.85))コンポーネントのレジストリ キーの下で、コンポーネントのパラメーターを割り当てる方法。 通知オブジェクトは、そのコンポーネントを呼び出して[ **INetCfgComponent::OpenParamKey** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff547890(v=vs.85))メソッドを開き、コンポーネントのレジストリ キーを取得します。

5.  コンポーネントのドライバーを構成するには、ネットワーク構成のサブシステムは、通知オブジェクトを呼び出します[ **INetCfgComponentControl::ApplyPnpChanges** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff547726(v=vs.85))メソッドを呼び出し、 [ **。INetCfgPnpReconfigCallback** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff547935(v=vs.85))インターフェイス。 通知オブジェクトの呼び出し、 [ **INetCfgPnpReconfigCallback::SendPnpReconfig** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff547943(v=vs.85))にそのコンポーネントのドライバーの構成情報を送信する方法。

無人セットアップ ファイルとセットアップ API についての詳細については、Microsoft Windows SDK を参照してください。