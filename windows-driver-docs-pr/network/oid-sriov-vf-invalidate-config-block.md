---
title: OID_SRIOV_VF_INVALIDATE_CONFIG_BLOCK
description: NDIS は、ミニポート ドライバーの PCI Express (PCIe) 仮想機能 (VF) 1 つまたは複数の構成ブロック内のデータが変更されたことを通知する OID_SRIOV_VF_INVALIDATE_CONFIG_BLOCK のオブジェクト識別子 (OID) メソッド要求を発行します。
ms.assetid: CF73E0DA-20DA-49A0-80B0-0F5A56DCEF5D
ms.date: 08/08/2017
keywords: -OID_SRIOV_VF_INVALIDATE_CONFIG_BLOCK ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 9b6437cd91a0dca9486ab1ee6053db96a832fe6b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530165"
---
# <a name="oidsriovvfinvalidateconfigblock"></a>OID\_SRIOV\_VF\_INVALIDATE\_CONFIG\_ブロック


OID のオブジェクト識別子 (OID) メソッド要求を発行する NDIS\_SRIOV\_VF\_INVALIDATE\_CONFIG\_ミニポート ドライバーの PCI Express (PCIe) 仮想機能 (VF) そのデータへの通知をブロック1 つまたは複数の構成ブロック内でが変更されました。 NDIS ミニポート ドライバー PCIe 物理機能 (PF) を呼び出すときにこの OID の問題[ **NdisMInvalidateConfigBlock**](https://msdn.microsoft.com/library/windows/hardware/hh451517)します。

**InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)構造体にはへのポインターが含まれています、 [ **NDIS\_SRIOV\_VF\_INVALIDATE\_CONFIG\_ブロック\_情報**](https://msdn.microsoft.com/library/windows/hardware/hh451684)構造体。 この構造体を持つデータが変更されている 1 つ以上の仮想機能 (VF) の構成ブロックを指定します (*無効*) によって PF のミニポート ドライバー。

<a name="remarks"></a>注釈
-------

VF 構成ブロックは、PF と VF のミニポート ドライバーの間のバック チャネル通信に使用されます。 IHV は、デバイスの 1 つ以上の VF 構成ブロックを定義できます。 各 VF 構成ブロックは、IHV で定義された形式、長さ、およびブロック id。

**注**  各 VF 構成ブロックからのデータは、PF と VF のミニポート ドライバーでのみ使用します。

 

VF 構成データは、次のドライバーの間で交換されます。

-   VF ドライバー、ゲスト オペレーティング システムで実行されます。 このオペレーティング システムは、HYPER-V 子パーティション内で実行されます。

-   PF ドライバーは、管理オペレーティング システムで実行されます。 このオペレーティング システムは、HYPER-V 親パーティション内で実行されます。

NDIS ミニポート ドライバーおよび無効な VF 構成データの通知を処理するために次の手順に従います。

1.  NDIS、ゲスト オペレーティング システムの I/O 制御要求を発行[ **IOCTL\_VPCI\_INVALIDATE\_ブロック**](https://msdn.microsoft.com/library/windows/hardware/hh439301)要求。 この IOCTL が完了したら、NDIS は VF 構成データが変更されたことが通知されます。

2.  管理オペレーティング システムでは、次の手順が発生します。

    1.  PF のミニポート ドライバー呼び出し、 [ **NdisMInvalidateConfigBlock** ](https://msdn.microsoft.com/library/windows/hardware/hh451517) VF 構成データが変更され、無効になっている NDIS に通知します。 ドライバーのセット、 *BlockMask* VF 構成ブロックを指定する ULONGLONG ビットマスクにパラメーターが変更されました。 ビットマスクの各ビットは、VF 構成ブロックに対応します。 ビットが 1 つに設定されている場合、対応する VF 構成ブロック内のデータが変更されました。
    2.  NDIS は、VF 構成ブロックのデータへの変更について、管理オペレーティング システムで実行される仮想化スタックを通知します。 仮想化スタックは、キャッシュ、 *BlockMask*パラメーターのデータ。

        **注**  PF ミニポート ドライバーを呼び出すたびに[ **NdisMInvalidateConfigBlock**](https://msdn.microsoft.com/library/windows/hardware/hh451517)、仮想化スタックの Or、 *BlockMask*キャッシュに現在の値を持つパラメーターのデータ。

         

    3.  仮想化スタックでは、VF 構成データの無効化について、ゲスト オペレーティング システムで実行される仮想の PCI (VPCI) ドライバーに通知します。 仮想化スタックは、キャッシュされた送信*BlockMask* VPCI ドライバーにパラメーターのデータ。

3.  ゲスト オペレーティング システムでは、次の手順が発生します。

    1.  VPCI ドライバーは、キャッシュされた保存*BlockMask*でパラメーターのデータ、 **BlockMask**のメンバー、 [ **VPCI\_INVALIDATE\_ブロック\_出力**](https://msdn.microsoft.com/library/windows/hardware/hh451586)構造に関連付けられている、 [ **IOCTL\_VPCI\_INVALIDATE\_ブロック**](https://msdn.microsoft.com/library/windows/hardware/hh439301)要求。

    2.  VPCI ドライバーが正常に完了、 [ **IOCTL\_VPCI\_INVALIDATE\_ブロック**](https://msdn.microsoft.com/library/windows/hardware/hh439301)要求。 NDIS が OID の OID メソッド要求を発行してこのような場合は、\_SRIOV\_VF\_INVALIDATE\_CONFIG\_VF のミニポート ドライバーをブロックします。 [ **NDIS\_SRIOV\_VF\_INVALIDATE\_CONFIG\_ブロック\_情報**](https://msdn.microsoft.com/library/windows/hardware/hh451684) OID 要求で渡されますが。 この構造体が含まれていますが、キャッシュされた*BlockMask*パラメーターのデータ。

        NDIS 別問題も[ **IOCTL\_VPCI\_INVALIDATE\_ブロック**](https://msdn.microsoft.com/library/windows/hardware/hh439301) VF 構成データの変更の連続する通知を処理するために要求します。

    3.  VF ドライバーが、OID を処理するときに\_SRIOV\_VF\_INVALIDATE\_CONFIG\_ブロックの要求、指定した VF 構成要素からデータを読み取ることです。

シングル ルート I/O 仮想化 (SR-IOV) インターフェイス内でのバック チャネル通信の詳細については、次を参照してください。 [SR-IOV PF/VF のバック チャネル通信](https://msdn.microsoft.com/library/windows/hardware/hh440251)します。

### <a name="return-status-codes"></a>リターン状態コード

ミニポート ドライバーでは、OID の OID メソッド要求の次のステータス コードのいずれかを返します\_SRIOV\_VF\_INVALIDATE\_CONFIG\_をブロックします。

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
<td><p>OID 要求は正常に完了しました。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_NOT_SUPPORTED</p></td>
<td><p>ミニポート ドライバーでは、シングル ルート I/O 仮想化 (SR-IOV) インターフェイスをサポートしていませんか、またはインターフェイスを使用して有効になっていません。</p></td>
</tr>
<tr class="odd">
<td><p>NDIS_STATUS_INVALID_PARAMETER</p></td>
<td><p>1 つ以上のメンバーの<a href="https://msdn.microsoft.com/library/windows/hardware/hh451684" data-raw-source="[&lt;strong&gt;NDIS_SRIOV_VF_INVALIDATE_CONFIG_BLOCK_INFO&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh451684)"> <strong>NDIS_SRIOV_VF_INVALIDATE_CONFIG_BLOCK_INFO</strong> </a>構造が無効な値を指定します。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_INVALID_LENGTH</p></td>
<td><p>情報バッファーが小さすぎます。 NDIS セット、<strong>データ。SET_INFORMATION します。BytesNeeded</strong>内のメンバー、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff566710" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566710)"> <strong>NDIS_OID_REQUEST</strong> </a>構造体のサイズを<a href="https://msdn.microsoft.com/library/windows/hardware/hh451684" data-raw-source="[&lt;strong&gt;NDIS_SRIOV_VF_INVALIDATE_CONFIG_BLOCK_INFO&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh451684)"> <strong>NDIS_SRIOV_VF_INVALIDATE_CONFIG_BLOCK_INFO</strong></a>構造体。</p></td>
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
[**IOCTL\_VPCI\_INVALIDATE\_BLOCK**](https://msdn.microsoft.com/library/windows/hardware/hh439301)

[**NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)

[**NDIS\_SRIOV\_VF\_INVALIDATE\_CONFIG\_ブロック\_情報**](https://msdn.microsoft.com/library/windows/hardware/hh451684)

[**NdisMInvalidateConfigBlock**](https://msdn.microsoft.com/library/windows/hardware/hh451517)

[OID\_SRIOV\_読み取り\_VF\_CONFIG\_領域](oid-sriov-read-vf-config-space.md)

[**VPCI\_INVALIDATE\_ブロック\_出力**](https://msdn.microsoft.com/library/windows/hardware/hh451586)

 

 



