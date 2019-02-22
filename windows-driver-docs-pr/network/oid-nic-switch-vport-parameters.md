---
title: OID_NIC_SWITCH_VPORT_PARAMETERS
description: 上にある、ドライバーは、シングル ルート I/O 仮想化 (SR-IOV) をサポートするネットワーク アダプターで作成された NIC スイッチ上の仮想ポート (VPort) のパラメーターを取得できます。
ms.assetid: B22C760E-F2B0-4774-A532-4044C679CD64
ms.date: 08/08/2017
keywords: -OID_NIC_SWITCH_VPORT_PARAMETERS ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 0f8cfe00f7a921662c4d0de32e245a01ccf5c2d1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56528799"
---
# <a name="oidnicswitchvportparameters"></a>OID\_NIC\_スイッチ\_VPORT\_パラメーター


上にある、ドライバーは、シングル ルート I/O 仮想化 (SR-IOV) をサポートするネットワーク アダプターで作成された NIC スイッチ上の仮想ポート (VPort) のパラメーターを取得できます。 OID のオブジェクト識別子 (OID) メソッド要求を発行\_NIC\_スイッチ\_VPORT\_パラメーターをこれらのパラメーターを取得します。

ドライバーの問題を後続 OID の要求の設定、OID\_NIC\_スイッチ\_VPORT\_ネットワーク アダプターの NIC のスイッチに接続されている指定された VPort の構成パラメーターを設定するパラメーター。 これらの OID セット要求は、ミニポート ドライバーのネットワーク アダプターの PCI Express (PCIe) 物理機能 (PF) に発行されます。 これらの OID セット要求は、PF ミニポート ドライバー シングル ルート I/O 仮想化 (SR-IOV) インターフェイスをサポートする必要があります。

**InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)構造体にはへのポインターが含まれています、 [ **NDIS\_NIC\_スイッチ\_VPORT\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh451597)構造体。

上にあるドライバーが、OID メソッド VPort を指定しますまたは、セットの要求を設定して、 **VPortId**のメンバー、 [ **NDIS\_NIC\_スイッチ\_VPORT\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh451597) VPort に関連付けられている識別子に構造体。 上にあるドライバーは、次の方法のいずれかで VPort 識別子を取得します。

-   前の OID メソッド要求から[OID\_NIC\_スイッチ\_作成\_VPORT](oid-nic-switch-create-vport.md)します。

-   前の OID メソッド要求から[OID\_NIC\_スイッチ\_ENUM\_拡張](oid-nic-switch-enum-vports.md)します。

<a name="remarks"></a>注釈
-------

OID\_NIC\_スイッチ\_VPORT\_パラメーターは、どちらかで使用できる[OID メソッド要求](#oid-method-requests)または[OID 設定要求](#oid-set-requests)します。

### <a href="" id="oid-method-requests"></a>OID の OID メソッド要求を処理して\_NIC\_スイッチ\_VPORT\_パラメーター

上にあるドライバーは、OID の OID メソッド要求を発行\_NIC\_切り替える\_VPORT\_パラメーターをネットワーク アダプターの NIC のスイッチに接続されている VPort の現在の構成パラメーターをクエリします。 上にあるドライバーを設定して照会する VPort の指定、 **VPortId**のメンバー、 [ **NDIS\_NIC\_スイッチ\_VPORT\_パラメーター**](https://msdn.microsoft.com/library/windows/hardware/hh451597) VPort 識別子に構造体。

OID の OID メソッド要求を処理する NDIS\_NIC\_スイッチ\_VPORT\_ミニポート ドライバーのパラメーター。 NDIS はの以前の OID 要求から取得した情報を返します[OID\_NIC\_スイッチ\_作成\_VPORT](oid-nic-switch-create-vport.md)と[OID\_NIC\_スイッチ\_ENUM\_拡張](oid-nic-switch-enum-vports.md)します。

OID メソッドの要求から正常に戻った後、 **InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)構造体ポインターが含まれています、 [ **NDIS\_NIC\_スイッチ\_VPORT\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh451597)構造体。 この構造体には、指定されたスイッチの構成パラメーターが含まれています。

詳細については、次を参照してください。[仮想ポートのパラメーターのクエリを実行する](https://msdn.microsoft.com/library/windows/hardware/hh440181)します。

### <a href="" id="oid-set-requests"></a>OID の要求を設定する処理 OID\_NIC\_スイッチ\_VPORT\_パラメーター

OID の要求の OID 設定ドライバーの問題を後続\_NIC\_スイッチ\_VPORT\_のネットワーク アダプターの NIC のスイッチに接続されている VPort の現在の構成パラメーターを変更するパラメーター。 この OID 要求は、既定以外の拡張と同様に既定のパラメーターを更新できます。

VPort の構成パラメーターの一部のサブセットのみを変更することができます。 上にあるドライバーの次のメンバーを設定して変更するパラメーターを指定します、 [ **NDIS\_NIC\_スイッチ\_VPORT\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh451597)構造体。

1.  **VPortId**メンバーはパラメーターを持つ変更 VPort の識別子に設定されます。

2.  適切な NDIS\_NIC\_スイッチ\_VPORT\_パラメーター\_*Xxx*\_変更されたフラグが設定されて、**フラグ**メンバー。 メンバー、 [ **NDIS\_NIC\_スイッチ\_VPORT\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh451597)構造体は、対応する NDIS 場合にのみ変更できます\_NIC\_スイッチ\_パラメーター\_*Xxx*\_Ntddndis.h で変更されたフラグが定義されています。

3.  対応するメンバー、 [ **NDIS\_NIC\_スイッチ\_VPORT\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh451597) VPort 構成構造を設定変更するパラメーターです。

OID の OID セット要求を受信するミニポート ドライバー、PF 後\_NIC\_スイッチ\_VPORT\_パラメーター、ドライバーで、構成パラメーターを使用してハードウェアが構成されます。 ドライバーでは、NDIS で識別されるこれらの構成パラメーターを変更できるだけ\_NIC\_スイッチ\_VPORT\_パラメーター\_*Xxx*\_CHANGEDフラグ、**フラグ**のメンバー、 [ **NDIS\_NIC\_スイッチ\_VPORT\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh451597)構造体。

詳細については、次を参照してください。[仮想ポートのパラメーターを設定する](https://msdn.microsoft.com/library/windows/hardware/hh440228)します。

### <a name="return-status-codes"></a>リターン状態コード

NDIS または PF ミニポート ドライバーにより、設定、またはメソッドの次のステータス コードが OID の OID 要求返します\_NIC\_スイッチ\_VPORT\_パラメーター。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>状態コード</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>NDIS_STATUS_SUCCESS</p></td>
<td><p>要求は正常に完了しました。 <strong>InformationBuffer</strong>を指す、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff566583" data-raw-source="[&lt;strong&gt;NDIS_NIC_SWITCH_CAPABILITIES&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566583)"> <strong>NDIS_NIC_SWITCH_CAPABILITIES</strong> </a>構造体。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_NOT_SUPPORTED</p></td>
<td><p>PF のミニポート ドライバーでは、シングル ルート I/O 仮想化 (SR-IOV) インターフェイスをサポートしていませんか、またはインターフェイスを使用して有効になっていません。</p></td>
</tr>
<tr class="odd">
<td><p>NDIS_STATUS_INVALID_PARAMETER</p></td>
<td><p>1 つ以上のメンバーの<a href="https://msdn.microsoft.com/library/windows/hardware/hh451597" data-raw-source="[&lt;strong&gt;NDIS_NIC_SWITCH_VPORT_PARAMETERS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh451597)"> <strong>NDIS_NIC_SWITCH_VPORT_PARAMETERS</strong> </a>構造が無効な値を指定します。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_INVALID_LENGTH</p></td>
<td><p>情報バッファーが小さすぎます。 NDIS または PF ミニポート ドライバーの設定、<strong>データ。METHOD_INFORMATION します。BytesNeeded</strong> (OID メソッド要求) のメンバーまたは<strong>データ。SET_INFORMATION します。BytesNeeded</strong>で (OID セット要求) のメンバー、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff566710" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566710)"> <strong>NDIS_OID_REQUEST</strong> </a>構造体に必要な最小バッファー サイズ。</p></td>
</tr>
<tr class="odd">
<td><p>NDIS_STATUS_FAILURE</p></td>
<td><p>他の理由から、要求が失敗しました。</p></td>
</tr>
</tbody>
</table>

 

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>バージョン</p></td>
<td><p>NDIS 6.30 以降をサポートします。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis.h (include Ndis.h)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


****
[**NDIS\_NIC\_スイッチ\_VPORT\_パラメーター**](https://msdn.microsoft.com/library/windows/hardware/hh451597)

[**NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)

[OID\_NIC\_スイッチ\_作成\_VPORT](oid-nic-switch-create-vport.md)

[OID\_NIC\_SWITCH\_ENUM\_VPORTS](oid-nic-switch-enum-vports.md)

 

 



