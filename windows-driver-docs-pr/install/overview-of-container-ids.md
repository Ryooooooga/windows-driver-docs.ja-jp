---
title: コンテナー ID の概要
description: コンテナー ID の概要
ms.assetid: fb7a4a31-01f9-4f7e-a35c-9076c7d73a29
keywords:
- コンテナー Id WDK, 概要
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e408ccdd1af64187fe284a141be33ebe8be705e3
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67366652"
---
# <a name="overview-of-container-ids"></a>コンテナー ID の概要


Windows ファミリのオペレーティング システムでは、使用するデバイスとは、基本的に何らかの形式のデバイスとの通信ができるようにする機能のエンドポイントを表すデバイスの機能のインスタンスのコレクションです。

用語*デバイス ノード*(*devnode*) を指す、*ドライバー スタック*このような機能エンドポイントの場合、エンドポイントを記述するプロパティだけでなく、その関連付けられた状態。 たとえば、プリンターをサポートする多機能デバイス スキャナー、および fax 機能にデバイスで各機能のエンドポイントに 1 つずつ、複数の devnode ことができます。

Windows 7 では、前に、各機能のエンドポイントには、それに関連付けられている devnode が必要があります。 Windows プラットフォームのコンポーネントとサード パーティ製のアプリケーションのデバイスの状態および情報、devnode にクエリを実行でき、ただし機能エンドポイントを公開するインターフェイスのデバイスのハードウェアと通信できます。

単一関数デバイスの場合は、単一 devnode には、デバイスの機能のエンドポイントに関連するすべての情報が含まれています。 同様に、多機能のデバイスでは、各デバイスの機能のエンドポイントに関連付けられている複数の devnode があります。 ただし、Windows が devnode のグループが同じ物理デバイスから発生したことを認識することはできません。 同じ多機能デバイスに属している各 devnode では、1 つのデバイスとしていくつかの devnode をグループ化するプラグ アンド プレイ (PnP) マネージャーを使用する任意の識別情報は含まれません。 そのため、デバイスと 1 つの物理デバイスを提供する関数の包括的な表示ことはできません。

Windows 7 以降のオペレーティング システムで新しい ID を使用 (*コンテナー ID*) で発生した 1 つまたは複数の devnode をグループ化し、特定の物理デバイスの各インスタンスに属しています。 コンテナー ID はすべての devnode のプロパティで、グローバルに一意の識別子によって指定されます (*GUID*) 値。

コンピューターにインストールされている物理デバイスの各インスタンスは、コンテナーの一意の ID を持つ 物理デバイスのインスタンス上の関数を表すすべての devnode 同じコンテナー ID を共有します。 次の図は、そのリレーションシップの例を示します。

![多機能デバイスの devnode 用のコンテナー id を示す図します。](images/containerid-1.png)

バス ドライバーの特別な意味を持つ 1 つのコンテナー ID があります。として定義されている NULL_GUID:{00000000-0000-0000-0000-000000000000}します。

一般に、返さない NULL_GUID として既定では、コンテナー ID を報告するときに 代わりに、しない BusQueryContainerIDs ケース IRP_MN_QUERY_ID を処理するようにし、PnP できるように、既定のロジックを適用します。

コンテナー ID として NULL_GUID を返すときに、バス ドライバーを宣言します PnP をデバイスには、したがって NULL_GUID は非常に特殊なケースだけで適切なを返す任意のコンテナーの一部にする必要があります。 たとえば、 *devnode*ボリューム デバイスは、複数のコンテナー内の複数のディスクにまたがる可能性がありますが、任意のコンテナーに属していないなど。 このようなデバイスには、 [ **DEVPKEY_Device_BaseContainerId** ](https://docs.microsoft.com/windows-hardware/drivers/install/devpkey-device-basecontainerid) NULL_GUID、等しいし、はありません、 [ **DEVPKEY_Device_ContainerId** ](https://docs.microsoft.com/windows-hardware/drivers/install/devpkey-device-containerid)まったくです。

別に、非常に特殊なケースは、そのバスから NULL_GUID 値を報告するハードウェアの障害を防ぐ必要がありますハードウェア デバイスとバス ドライバーのレポートと、バス ドライバーする必要があります NULL_GUID を返さない。 このような場合は、バス ドライバーはする必要があります、としてデバイス エラーの場合は、この脅威またはいずれか、デバイスは、値を報告しなかったかのように扱うことです。

 

 





