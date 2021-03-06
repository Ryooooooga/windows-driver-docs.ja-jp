---
title: OID_WDI_GET_ADAPTER_CAPABILITIES
description: OID_WDI_GET_ADAPTER_CAPABILITIES は、初期化中に、アダプターをホストから発行され、アダプターの機能を要求する読み取り専用プロパティです。
ms.assetid: e79deb29-bc0b-472e-b549-86bf71fe66ff
ms.date: 07/18/2017
keywords:
- OID_WDI_GET_ADAPTER_CAPABILITIES ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 4d7477f741c34bcc4250a28f2017c7b7defd083d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67353677"
---
# <a name="oidwdigetadaptercapabilities"></a>OID\_WDI\_取得\_アダプター\_機能


OID\_WDI\_取得\_アダプター\_機能は、アダプターをホストからの初期化中に発行され、アダプターの機能を要求する読み取り専用プロパティ。

| Scope   | タスクでシリアル化された設定します。 | 通常の実行時間 (秒) |
|---------|--------------------------|---------------------------------|
| [アダプター] | Set はサポートされません。        | 1                               |

 

## <a name="get-property-parameters"></a>プロパティのパラメーターを取得します。


追加のパラメーターはありません。 ヘッダー内のデータで十分です。
## <a name="get-property-results"></a>プロパティの結果を得る


アダプターが Wi-Fi Direct をサポートする場合両方[ **WDI\_TLV\_AP\_属性**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-ap-attributes)と[ **WDI\_TLV\_P2P\_属性**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-p2p-attributes)指定する必要があります。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th>TLV</th>
<th>許可されている複数の TLV インスタンス</th>
<th>省略可能</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><a href="https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-communication-configuration-attributes" data-raw-source="[&lt;strong&gt;WDI_TLV_COMMUNICATION_CONFIGURATION_ATTRIBUTES&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-communication-configuration-attributes)"><strong>WDI_TLV_COMMUNICATION_CONFIGURATION_ATTRIBUTES</strong></a></td>
<td></td>
<td>x</td>
<td>ホスト アダプターの通信プロトコルの構成の属性。</td>
</tr>
<tr class="even">
<td><a href="https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-interface-attributes" data-raw-source="[&lt;strong&gt;WDI_TLV_INTERFACE_ATTRIBUTES&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-interface-attributes)"><strong>WDI_TLV_INTERFACE_ATTRIBUTES</strong></a></td>
<td></td>
<td></td>
<td>インターフェイス属性。</td>
</tr>
<tr class="odd">
<td><a href="https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-station-attributes" data-raw-source="[&lt;strong&gt;WDI_TLV_STATION_ATTRIBUTES&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-station-attributes)"><strong>WDI_TLV_STATION_ATTRIBUTES</strong></a></td>
<td></td>
<td></td>
<td>ステーションの属性。</td>
</tr>
<tr class="even">
<td><a href="https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-ap-attributes" data-raw-source="[&lt;strong&gt;WDI_TLV_AP_ATTRIBUTES&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-ap-attributes)"><strong>WDI_TLV_AP_ATTRIBUTES</strong></a></td>
<td></td>
<td>x</td>
<td>アクセス ポイントの属性。</td>
</tr>
<tr class="odd">
<td><a href="https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-virtualization-attributes" data-raw-source="[&lt;strong&gt;WDI_TLV_VIRTUALIZATION_ATTRIBUTES&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-virtualization-attributes)"><strong>WDI_TLV_VIRTUALIZATION_ATTRIBUTES</strong></a></td>
<td></td>
<td>x</td>
<td>仮想化の属性。</td>
</tr>
<tr class="even">
<td><a href="https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-p2p-attributes" data-raw-source="[&lt;strong&gt;WDI_TLV_P2P_ATTRIBUTES&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-p2p-attributes)"><strong>WDI_TLV_P2P_ATTRIBUTES</strong></a></td>
<td></td>
<td>x</td>
<td>Wi-Fi Direct 属性。</td>
</tr>
<tr class="odd">
<td><a href="https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-datapath-attributes" data-raw-source="[&lt;strong&gt;WDI_TLV_DATAPATH_ATTRIBUTES&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-datapath-attributes)"><strong>WDI_TLV_DATAPATH_ATTRIBUTES</strong></a></td>
<td></td>
<td>x</td>
<td>データパス属性。</td>
</tr>
<tr class="even">
<td><a href="https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-band-info" data-raw-source="[&lt;strong&gt;WDI_TLV_BAND_INFO&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-band-info)"><strong>WDI_TLV_BAND_INFO</strong></a></td>
<td>x</td>
<td>x</td>
<td>バンド情報。</td>
</tr>
<tr class="odd">
<td><a href="https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-phy-info" data-raw-source="[&lt;strong&gt;WDI_TLV_PHY_INFO&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-phy-info)"><strong>WDI_TLV_PHY_INFO</strong></a></td>
<td>x</td>
<td>x</td>
<td>PHY 情報。</td>
</tr>
<tr class="even">
<td><a href="https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-pm-capabilities" data-raw-source="[&lt;strong&gt;WDI_TLV_PM_CAPABILITIES&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-pm-capabilities)"><strong>WDI_TLV_PM_CAPABILITIES</strong></a></td>
<td></td>
<td>x</td>
<td>電源管理機能。</td>
</tr>
<tr class="odd">
<td><a href="https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-country-region-list" data-raw-source="[&lt;strong&gt;WDI_TLV_COUNTRY_REGION_LIST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-country-region-list)"><strong>WDI_TLV_COUNTRY_REGION_LIST</strong></a></td>
<td></td>
<td>x</td>
<td>国または地域コードです。</td>
</tr>
<tr class="even">
<td><a href="https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-receive-coalescing-capabilities" data-raw-source="[&lt;strong&gt;WDI_TLV_RECEIVE_COALESCING_CAPABILITIES&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-receive-coalescing-capabilities)"><strong>WDI_TLV_RECEIVE_COALESCING_CAPABILITIES</strong></a></td>
<td></td>
<td>x</td>
<td>ハードウェア支援によるフィルターの機能が表示されます。</td>
</tr>
<tr class="odd">
<td><a href="https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-tcp-offload-capabilities" data-raw-source="[&lt;strong&gt;WDI_TLV_TCP_OFFLOAD_CAPABILITIES&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-tcp-offload-capabilities)"><strong>WDI_TLV_TCP_OFFLOAD_CAPABILITIES</strong></a></td>
<td></td>
<td>x</td>
<td>TCP/IP はオフロード機能です。</td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-supported-guids" data-raw-source="[&lt;strong&gt;WDI_TLV_SUPPORTED_GUIDS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-supported-guids)"><strong>WDI_TLV_SUPPORTED_GUIDS</strong></a></p></td>
<td><p>x</p></td>
<td><p>x</p></td>
<td><p>Windows 10 version 1607 では、バージョン 1.0.21 WDI に追加されます。</p>
<p>渡される NDIS WDI がクエリされるときに Guid のリスト<a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-supported-guids" data-raw-source="[OID_GEN_SUPPORTED_GUIDS](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-supported-guids)">OID_GEN_SUPPORTED_GUIDS</a>します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="wdi-tlv-os-power-management-features.md" data-raw-source="[&lt;strong&gt;WDI_TLV_OS_POWER_MANAGEMENT_FEATURES&lt;/strong&gt;](wdi-tlv-os-power-management-features.md)"><strong>WDI_TLV_OS_POWER_MANAGEMENT_FEATURES</strong></a></p></td>
<td></td>
<td></td>
<td><p>Windows 10、バージョン 1803、WDI 1.1.6 のバージョンで追加します。</p>
<p>高度な OS の電源管理機能を有効にするために使用します。</p>
</td>
</tr>
</tbody>
</table>

 

<a name="requirements"></a>必要条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>サポートされている最小のクライアント</p></td>
<td><p>Windows 10</p></td>
</tr>
<tr class="even">
<td><p>サポートされている最小のサーバー</p></td>
<td><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td><p>Header</p></td>
<td>Dot11wdi.h</td>
</tr>
</tbody>
</table>

 

 




