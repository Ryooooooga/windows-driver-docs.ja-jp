---
title: コンテナー ID の生成方法
description: コンテナー ID の生成方法
ms.assetid: baa3c045-05ee-4012-97a3-c6e575c897be
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f58a9839611130670b1b6c9bf0236530ba8e3b51
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386407"
---
# <a name="how-container-ids-are-generated"></a>コンテナー ID の生成方法


Windows 7 以降、プラグ アンド プレイ (PnP) マネージャーはデバイス ノードのコンテナー ID が生成されます (*devnode*) 3 つのメカニズムのいずれかで。

-   バス ドライバーは、コンテナー ID を提供します。

    コンテナー ID を devnode に割り当てるときに、PnP マネージャーはまず devnode のバス ドライバーがコンテナー ID を指定できるかどうか バス ドライバーを通じてコンテナー ID を提供する、 [ **IRP_MN_QUERY_ID** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-id)の要求、 **Parameters.QueryId.IdType**フィールドに設定**BusQueryContainerID**.

    バス ドライバーは物理デバイスのハードウェアに埋め込まれた正規コンテナー ID を取得または bus 固有一意の ID、デバイスのハードウェアからを使用して、コンテナー ID を生成するには バスに固有の一意の Id の例では、デバイスのシリアル番号またはデバイスのファームウェアでのメディア アクセス制御 (MAC) アドレスを示します。

    **注**独立系ハードウェア ベンダー (IHV) は、バス ドライバーによって報告されたコンテナー ID の一意性を確認します。




詳細については、次を参照してください。[コンテナー Id は、バスに固有の一意の ID から生成された](container-ids-generated-from-a-bus-specific-unique-id.md)します。


-   PnP マネージャーでは、リムーバブル デバイスの機能を通じてコンテナー ID を生成します。

    バス ドライバーは、列挙 devnode のコンテナーの ID を提供することはできません、PnP マネージャーは、デバイスの列挙されたすべての devnode のコンテナー ID を生成するのにリムーバブル デバイスの機能を使用します。 バス ドライバーへの応答でこのデバイスの機能の報告、 [ **IRP_MN_QUERY_CAPABILITIES** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-capabilities)要求。

    詳細については、次を参照してください。[コンテナー Id は、リムーバブル デバイスの機能から生成された](container-ids-generated-from-the-removable-device-capability.md)します。

-   PnP マネージャーでは、リムーバブル デバイスの機能の上書きすることによって、コンテナー ID を生成します。

    **注**で Windows 10、DPWS デバイスは常に生成をこのメソッドを使用してデバイスのコンテナーの ID。




優先機構はリムーバブル デバイスの機能の値を変更していない、デバイス用のコンテナーの Id を生成するときに、上書きの設定とリムーバブル デバイスの機能の値ではなくを使用する PnP マネージャーを強制します。

たとえば、リムーバブル デバイスの機能のオーバーライドでは、デバイスがリムーバブルを指定します、PnP マネージャーは、デバイスの列挙されたすべての devnode のコンテナー ID を生成します。 この操作は、かどうか、デバイス自体として報告リムーバブルかどうかに関係なく実行されます。

IHV は、デバイスによって報告されたリムーバブル デバイスの機能をオーバーライドするキーを持つレジストリを設定できます。 このオーバーライド メカニズムは、リムーバブル デバイスの機能をサポートまたはしない正しく報告して従来のデバイスに役立ちます。

詳細については、次を参照してください。[コンテナー Id は、リムーバブル デバイス機能オーバーライドから生成された](container-ids-generated-from-a-removable-device-capability-override.md)します。


これらのメソッドだけでなくデバイス コンテナー グループを指定するのにオブジェクトの ACPI BIOS 設定が使用されます。 詳細については、次を参照してください。[デバイス コンテナーのグループ化を使用して ACPI](using-acpi-for-device-container-grouping.md)します。









