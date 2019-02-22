---
title: DEVPKEY_Device_BusNumber
description: DEVPKEY_Device_BusNumber
ms.assetid: 17cbe49a-e10b-4483-b030-c061ced065c3
keywords:
- DEVPKEY_Device_BusNumber デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- DEVPKEY_Device_BusNumber
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 65a82ca0255a608dad6bbf2b032ea9a49ff1dce6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56527575"
---
# <a name="devpkeydevicebusnumber"></a>DEVPKEY_Device_BusNumber


DEVPKEY_Device_BusNumber デバイス プロパティは、バス インスタンスに関連付けられているデバイスのインスタンスを識別する番号を表します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>プロパティのキー</strong></p></td>
<td align="left"><p>DEVPKEY_Device_BusNumber</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>データ型のプロパティの識別子</strong></p></td>
<td align="left"><p><a href="devprop-type-int32.md" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_INT32&lt;/strong&gt;](devprop-type-int32.md)"><strong>DEVPROP_TYPE_INT32</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>プロパティへのアクセス</strong></p></td>
<td align="left"><p>アプリケーションをインストールし、インストーラーによって、読み取り専用アクセス</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>対応する SPDRP_</strong><em>Xxx</em> <strong>識別子</strong></p></td>
<td align="left"><p>SPDRP_BUSNUMBER</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>ローカライズか。</strong></p></td>
<td align="left"><p>X</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

Windows の BusNumber メンバーの値に DEVPKEY_Device_BusNumber の値の設定、 [ **PNP_BUS_INFORMATION** ](https://msdn.microsoft.com/library/windows/hardware/ff559608)バス ドライバーへの応答を返す構造、 [ **IRP_MN_QUERY_BUS_INFORMATION** ](https://msdn.microsoft.com/library/windows/hardware/ff551654)要求。

呼び出すことができます[ **SetupDiGetDeviceProperty** ](https://msdn.microsoft.com/library/windows/hardware/ff551963) DEVPKEY_Device_BusNumber の値を取得します。

Windows Server 2003、Windows XP、および Windows 2000 は、このプロパティをサポートは DEVPKEY_Device_BusNumber プロパティのキーをサポートしていません。 代わりに、Windows の以前のバージョンのプロパティの値へのアクセスに対応する SPDRP_BUSNUMBER 識別子を使用することができます。 Windows の以前のバージョンでこのプロパティの値にアクセスする方法については、次を参照してください。[デバイス インスタンス SPDRP_Xxx プロパティへのアクセス](https://msdn.microsoft.com/library/windows/hardware/ff537737)します。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>バージョン</p></td>
<td align="left"><p>Windows Vista および Windows の以降のバージョンで使用できます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Devpkey.h (Devpkey.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**IRP_MN_QUERY_BUS_INFORMATION**](https://msdn.microsoft.com/library/windows/hardware/ff551654)

[**PNP_BUS_INFORMATION**](https://msdn.microsoft.com/library/windows/hardware/ff559608)

[**SetupDiGetDeviceProperty**](https://msdn.microsoft.com/library/windows/hardware/ff551963)

 

 





