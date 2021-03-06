---
title: SO_EXCLUSIVEADDRUSE
description: SO_EXCLUSIVEADDRUSE
ms.assetid: d281086f-4d8b-4e1e-b2bd-7b0a20338222
ms.date: 08/08/2017
keywords: -Windows Vista 以降の SO_EXCLUSIVEADDRUSE ネットワークドライバー
ms.localizationpriority: medium
ms.openlocfilehash: cf54ae5ff50218e6809e6d20b79275423c63639c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841886"
---
# <a name="so_exclusiveaddruse"></a>EXCLUSIVEADDRUSE\_


SO\_EXCLUSIVEADDRUSE socket オプションの状態によって、ソケットのバインド先のローカルトランスポートアドレスがそのソケット専用に予約されているかどうかが決まります。 このソケットオプションは、リッスンしているソケット、データグラムソケット、および接続指向のソケットにのみ適用されます。

WSK アプリケーションがこのソケットオプションを設定する場合は、ソケットがローカルトランスポートアドレスにバインドされる前に、そのアプリケーションを実行する必要があります。

このソケットオプションの状態を設定するために、WSK アプリケーションは次のパラメーターを使用して[**Wskcontrolsocket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_control_socket)関数を呼び出します。

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
<td><p><strong>WskSetOption</strong></p></td>
</tr>
<tr class="even">
<td><p><em>ControlCode</em></p></td>
<td><p>SO_EXCLUSIVEADDRUSE</p></td>
</tr>
<tr class="odd">
<td><p><em>平準</em></p></td>
<td><p>SOL_SOCKET</p></td>
</tr>
<tr class="even">
<td><p><em>InputSize</em></p></td>
<td><p>sizeof (ULONG)</p></td>
</tr>
<tr class="odd">
<td><p><em>InputBuffer</em></p></td>
<td><p>Socket オプションの新しい状態の値を格納する、ULONG 型の変数へのポインター。</p>
<p>0: ローカルトランスポートアドレスの排他的使用を無効にします。</p>
<p>1: ローカルトランスポートアドレスの排他的な使用を有効にします。</p></td>
</tr>
<tr class="even">
<td><p><em>OutputSize</em></p></td>
<td><p>0</p></td>
</tr>
<tr class="odd">
<td><p><em>OutputBuffer</em></p></td>
<td><p>NULL</p></td>
</tr>
<tr class="even">
<td><p><em>OutputSizeReturned</em></p></td>
<td><p>NULL</p></td>
</tr>
</tbody>
</table>


WSK アプリケーションは、このソケットオプションの状態を取得するために、次のパラメーターを使用して**Wskcontrolsocket**関数を呼び出します。

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
<td><p><strong>WskGetOption</strong></p></td>
</tr>
<tr class="even">
<td><p><em>ControlCode</em></p></td>
<td><p>SO_EXCLUSIVEADDRUSE</p></td>
</tr>
<tr class="odd">
<td><p><em>平準</em></p></td>
<td><p>SOL_SOCKET</p></td>
</tr>
<tr class="even">
<td><p><em>InputSize</em></p></td>
<td><p>0</p></td>
</tr>
<tr class="odd">
<td><p><em>InputBuffer</em></p></td>
<td><p>NULL</p></td>
</tr>
<tr class="even">
<td><p><em>OutputSize</em></p></td>
<td><p>sizeof (ULONG)</p></td>
</tr>
<tr class="odd">
<td><p><em>OutputBuffer</em></p></td>
<td><p>ソケットオプションの状態の値を受け取る、ULONG 型の変数へのポインター。</p>
<p>0: ローカルトランスポートアドレスを排他的に使用することはできません。</p>
<p>1: ローカルトランスポートアドレスの排他的な使用が有効になっています</p></td>
</tr>
<tr class="even">
<td><p><em>OutputSizeReturned</em></p></td>
<td><p>NULL</p></td>
</tr>
</tbody>
</table>


WSK アプリケーションは、 **Wskcontrolsocket**関数を呼び出して、SO\_EXCLUSIVEADDRUSE socket オプションの状態を設定または取得するときに、IRP へのポインターを指定する必要があります。

このソケットオプションの既定の状態は、ローカルトランスポートアドレスの排他的な使用が無効になっていることです。

SO\_EXCLUSIVEADDRUSE socket オプションの使用方法と、ソケット間のローカルトランスポートアドレスの共有に対する影響の詳細については、「[トランスポートアドレスの共有](https://docs.microsoft.com/windows-hardware/drivers/network/sharing-transport-addresses)」を参照してください。

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
<td><p>Windows Vista 以降のバージョンの Windows オペレーティングシステムで使用できます。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ws2def (Wsk .h を含む)</td>
</tr>
</tbody>
</table>

 

 




