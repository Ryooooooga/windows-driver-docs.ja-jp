---
title: HDAUDIO_BUS_INTERFACE DDI オブジェクトを取得します。
description: HDAUDIO_BUS_INTERFACE DDI オブジェクトを取得します。
ms.assetid: 78667254-62a6-41fe-af36-43dbdea63aa8
keywords:
- HDAUDIO_BUS_INTERFACE 構造体
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3c31a65e20ef0e9c12a0be5d4b993447d1b5e26f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56535983"
---
# <a name="obtaining-an-hdaudiobusinterface-ddi-object"></a>取得、HDAUDIO\_BUS\_インターフェイス DDI オブジェクト


次の表は入力パラメーターの値に、関数のドライバーを書き込みます、 [ **IRP\_MN\_クエリ\_インターフェイス**](https://msdn.microsoft.com/library/windows/hardware/ff551687) IOCTL、を取得するには[**HDAUDIO\_BUS\_インターフェイス**](https://msdn.microsoft.com/library/windows/hardware/ff536413)構造と、この構造体を定義する HD オーディオ DDI のバージョンのコンテキスト オブジェクト。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">パラメーター</th>
<th align="left">Value</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>CONST GUID *<em>InterfaceType</em></p></td>
<td align="left"><p><strong>GUID_HDAUDIO_BUS_INTERFACE</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p>USHORT<em>サイズ</em></p></td>
<td align="left"><p><strong>sizeof</strong>(<a href="https://msdn.microsoft.com/library/windows/hardware/ff536413" data-raw-source="[&lt;strong&gt;HDAUDIO_BUS_INTERFACE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff536413)"><strong>HDAUDIO_BUS_INTERFACE</strong></a>)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>USHORT<em>バージョン</em></p></td>
<td align="left"><p>0x0100</p></td>
</tr>
<tr class="even">
<td align="left"><p>PINTERFACE<em>インターフェイス</em></p></td>
<td align="left"><p>ポインター <a href="https://msdn.microsoft.com/library/windows/hardware/ff536413" data-raw-source="[&lt;strong&gt;HDAUDIO_BUS_INTERFACE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff536413)"> <strong>HDAUDIO_BUS_INTERFACE</strong> </a>構造体</p></td>
</tr>
<tr class="odd">
<td align="left"><p>PVOID <em>InterfaceSpecificData</em></p></td>
<td align="left"><p><strong>NULL</strong></p></td>
</tr>
</tbody>
</table>

 

Function ドライバーの記憶域の割り当て、 [ **HDAUDIO\_BUS\_インターフェイス**](https://msdn.microsoft.com/library/windows/hardware/ff536413)構造し、IOCTL でこの構造体へのポインターが含まれています。 前の表へのポインター、 **HDAUDIO\_BUS\_インターフェイス**構造が型にキャスト**PINTERFACE**、型の構造体へのポインターである[**インターフェイス**](https://msdn.microsoft.com/library/windows/hardware/ff547825)します。 名前と型の最初の 5 つのメンバーの**HDAUDIO\_BUS\_インターフェイス**の 5 つのメンバーに合わせて**インターフェイス**します。 **HDAUDIO\_BUS\_インターフェイス**DDI ルーチンへの関数ポインターであるその他のメンバーが含まれています。 関数ドライバーからの IOCTL の受信に応答してでは、HD オーディオ バス ドライバー、全体で塗りつぶします**HDAUDIO\_BUS\_インターフェイス**構造体。

次の表は、値の最初の 5 つのメンバーに、HD オーディオ バス ドライバーを記述、 [ **HDAUDIO\_BUS\_インターフェイス**](https://msdn.microsoft.com/library/windows/hardware/ff536413)構造体。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">メンバー</th>
<th align="left">Value</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>USHORT<strong>サイズ</strong></p></td>
<td align="left"><p><strong>sizeof</strong>(<a href="https://msdn.microsoft.com/library/windows/hardware/ff536413" data-raw-source="[&lt;strong&gt;HDAUDIO_BUS_INTERFACE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff536413)"><strong>HDAUDIO_BUS_INTERFACE</strong></a>)</p></td>
</tr>
<tr class="even">
<td align="left"><p>USHORT<strong>バージョン</strong></p></td>
<td align="left"><p>0x0100</p></td>
</tr>
<tr class="odd">
<td align="left"><p>PVOID<strong>コンテキスト</strong></p></td>
<td align="left"><p>コンテキストについては、最初の呼び出しのパラメーターとして各 DDI ルーチンに渡す必要があります。</p></td>
</tr>
<tr class="even">
<td align="left"><p>PINTERFACE_REFERENCE <strong>InterfaceReference</strong></p></td>
<td align="left"><p>コンテキスト オブジェクトをインクリメントするルーチンへのポインター&#39;s 参照カウント</p></td>
</tr>
<tr class="odd">
<td align="left"><p>PINTERFACE_DEREFERENCE <strong>InterfaceDereference</strong></p></td>
<td align="left"><p>ルーチンへのポインター値をデクリメントするコンテキスト オブジェクト&#39;s 参照カウント</p></td>
</tr>
</tbody>
</table>

 

上記の表に、**コンテキスト**ベースライン HD オーディオ DDI IOCTL からクライアントを取得するは、特定のインスタンスに固有の情報が含まれるコンテキスト オブジェクトへのポインターします。 クライアント機能のドライバーが常に指定する必要があります DDI でこれらのルーチンを呼び出す場合、**コンテキスト**最初の呼び出しのパラメーターとしてのポインターの値。 コンテキスト情報は、クライアントに対して非透過的です。 HD オーディオ バス ドライバーでは、各クライアントのさまざまなコンテキスト オブジェクトを作成します。 クライアントが呼び出すことによって、コンテキスト オブジェクトを解放するコンテキスト オブジェクトが必要でなくなったときに、 **InterfaceDereference**ルーチンは、前の表に示すようにします。 クライアントが呼び出すことによってオブジェクトへの他の参照を作成できます、必要な場合、 **InterfaceReference**ルーチンが、クライアントが不要になった要求して、これらの参照を解放します。

 

 



