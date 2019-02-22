---
title: SIO_WSK_REGISTER_EXTENSION
description: SIO_WSK_REGISTER_EXTENSION
ms.assetid: e7fd6d68-85e8-4c5f-b67f-2193d200130d
ms.date: 07/18/2017
keywords:
- SIO_WSK_REGISTER_EXTENSION ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 2565e9cd247807123a8185c3241ecda24bf5b75d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532666"
---
# <a name="siowskregisterextension"></a>SIO\_WSK\_登録\_拡張機能


SIO\_WSK\_登録\_ソケット I/O 制御操作の拡張機能を使用すると、WSK サブシステムによってサポートされている拡張機能インターフェイスを登録する WSK アプリケーション。 このソケット I/O 制御操作は、すべての種類のソケットに適用されます。

拡張機能インターフェイスを登録する WSK アプリケーションを呼び出す、 [ **WskControlSocket** ](https://msdn.microsoft.com/library/windows/hardware/ff571127)関数は次のパラメーター。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>パラメーター</th>
<th>Value</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>RequestType</em></p></td>
<td><p><strong>WskIoctl</strong></p></td>
</tr>
<tr class="even">
<td><p><em>ControlCode</em></p></td>
<td><p>SIO_WSK_REGISTER_EXTENSION</p></td>
</tr>
<tr class="odd">
<td><p><em>レベル</em></p></td>
<td><p>0</p></td>
</tr>
<tr class="even">
<td><p><em>InputSize</em></p></td>
<td><p>sizeof(WSK_EXTENSION_CONTROL_IN)</p></td>
</tr>
<tr class="odd">
<td><p><em>InputBuffer</em></p></td>
<td><p>ポインターを<a href="https://msdn.microsoft.com/library/windows/hardware/ff571167" data-raw-source="[&lt;strong&gt;WSK_EXTENSION_CONTROL_IN&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff571167)"> <strong>WSK_EXTENSION_CONTROL_IN</strong> </a>構造体。 この構造体にはへのポインターが含まれています、<a href="https://msdn.microsoft.com/library/windows/hardware/ff568373" data-raw-source="[Network Programming Interface (NPI)](https://msdn.microsoft.com/library/windows/hardware/ff568373)">ネットワーク プログラミング インターフェイス (NPI)</a>識別子の拡張機能インターフェイスとディスパッチ テーブルおよび WSK アプリケーションのコンテキストにポインター&#39;の実装、拡張機能インターフェイスです。</p></td>
</tr>
<tr class="even">
<td><p><em>OutputSize</em></p></td>
<td><p>sizeof(WSK_EXTENSION_CONTROL_OUT)</p></td>
</tr>
<tr class="odd">
<td><p><em>OutputBuffer</em></p></td>
<td><p>ポインターを<a href="https://msdn.microsoft.com/library/windows/hardware/ff571168" data-raw-source="[&lt;strong&gt;WSK_EXTENSION_CONTROL_OUT&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff571168)"> <strong>WSK_EXTENSION_CONTROL_OUT</strong> </a>構造体。 この構造体は、ディスパッチ テーブルへのポインターと WSK サブシステムのコンテキストへのポインターを受け取る&#39;、拡張機能インターフェイスの実装。</p></td>
</tr>
<tr class="even">
<td><p><em>OutputSizeReturned</em></p></td>
<td><p>NULL</p></td>
</tr>
</tbody>
</table>


呼び出すときに、WSK アプリケーションが IRP へのポインターを指定しない、 **WskControlSocket**拡張機能インターフェイスを登録する関数。

ディスパッチ テーブル構造体の内容は、拡張機能インターフェイスに固有です。

拡張機能インターフェイスを登録の詳細については、次を参照してください。[拡張機能インターフェイスを登録する](https://msdn.microsoft.com/library/windows/hardware/ff570461)します。

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
<td><p>Windows Vista および Windows オペレーティング システムの以降のバージョンで使用できます。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Wsk.h (Wsk.h を含む)</td>
</tr>
</tbody>
</table>

 

 



