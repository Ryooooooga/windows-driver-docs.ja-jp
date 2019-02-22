---
title: HDAUDIO_BUS_INTERFACE_V2 DDI オブジェクトを取得します。
description: HDAUDIO_BUS_INTERFACE_V2 DDI オブジェクトを取得します。
ms.assetid: 3aad8c7a-8c89-499a-bfe8-e3facdffcd15
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8702bbf1c60f4d57e6d3991d3e56c5d0755cae7e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558831"
---
# <a name="obtaining-an-hdaudiobusinterfacev2-ddi-object"></a>取得、HDAUDIO\_BUS\_インターフェイス\_V2 DDI オブジェクト


次の表は入力パラメーターの値に、関数のドライバーを書き込みます、 [ **IRP\_MN\_クエリ\_インターフェイス**](https://msdn.microsoft.com/library/windows/hardware/ff551687) IOCTL、を取得するには[**HDAUDIO\_BUS\_インターフェイス\_V2** ](https://msdn.microsoft.com/library/windows/hardware/ff536418)構造と、この構造体を定義する HD オーディオ DDI のバージョンのコンテキスト オブジェクト。

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
<td align="left"><p><strong>GUID_HDAUDIO_BUS_INTERFACE_V2</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p>USHORT<em>サイズ</em></p></td>
<td align="left"><p><strong>sizeof</strong>(<a href="https://msdn.microsoft.com/library/windows/hardware/ff536418" data-raw-source="[&lt;strong&gt;HDAUDIO_BUS_INTERFACE_V2&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff536418)"><strong>HDAUDIO_BUS_INTERFACE_V2</strong></a>)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>USHORT<em>バージョン</em></p></td>
<td align="left"><p>0x0100</p></td>
</tr>
<tr class="even">
<td align="left"><p>PINTERFACE<em>インターフェイス</em></p></td>
<td align="left"><p>ポインター <a href="https://msdn.microsoft.com/library/windows/hardware/ff536418" data-raw-source="[&lt;strong&gt;HDAUDIO_BUS_INTERFACE_V2&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff536418)"> <strong>HDAUDIO_BUS_INTERFACE_V2</strong> </a>構造体</p></td>
</tr>
<tr class="odd">
<td align="left"><p>PVOID <em>InterfaceSpecificData</em></p></td>
<td align="left"><p><strong>NULL</strong></p></td>
</tr>
</tbody>
</table>

 

Function ドライバーの記憶域の割り当て、 [ **HDAUDIO\_BUS\_インターフェイス\_V2** ](https://msdn.microsoft.com/library/windows/hardware/ff536418)構造し、IOCTL でこの構造体へのポインターが含まれています。 前の表へのポインター、 **HDAUDIO\_BUS\_インターフェイス\_V2**構造が型にキャスト**PINTERFACE**型の構造体へのポインターであります。[**インターフェイス**](https://msdn.microsoft.com/library/windows/hardware/ff547825)します。 名前と型の最初の 5 つのメンバーの**HDAUDIO\_BUS\_インターフェイス\_V2**の 5 つのメンバーに合わせて**インターフェイス**します。 **HDAUDIO\_BUS\_インターフェイス\_V2** DDI ルーチンへの関数ポインターであるその他のメンバーが含まれています。 HD オーディオ バス ドライバーの設定関数ドライバーからの IOCTL の受信に対する応答として、 **HDAUDIO\_BUS\_インターフェイス\_V2**構造体。

次の表は、値の最初の 5 つのメンバーに、HD オーディオ バス ドライバーを記述、 [ **HDAUDIO\_BUS\_インターフェイス\_V2** ](https://msdn.microsoft.com/library/windows/hardware/ff536418)構造体。

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
<td align="left"><p><strong>sizeof</strong>(<a href="https://msdn.microsoft.com/library/windows/hardware/ff536418" data-raw-source="[&lt;strong&gt;HDAUDIO_BUS_INTERFACE_V2&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff536418)"><strong>HDAUDIO_BUS_INTERFACE_V2</strong></a>)</p></td>
</tr>
<tr class="even">
<td align="left"><p>USHORT<strong>バージョン</strong></p></td>
<td align="left"><p>0x0100</p></td>
</tr>
<tr class="odd">
<td align="left"><p>PVOID<strong>コンテキスト</strong></p></td>
<td align="left"><p>すべて DDI ルーチンへの呼び出しの最初のパラメーターとして渡す必要があるコンテキスト情報。</p></td>
</tr>
<tr class="even">
<td align="left"><p>PINTERFACE_REFERENCE <strong>InterfaceReference</strong></p></td>
<td align="left"><p>コンテキスト オブジェクトをインクリメントするルーチンへのポインター&#39;s 参照カウントします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>PINTERFACE_DEREFERENCE <strong>InterfaceDereference</strong></p></td>
<td align="left"><p>ルーチンへのポインター値をデクリメントするコンテキスト オブジェクト&#39;s 参照カウントします。</p></td>
</tr>
</tbody>
</table>

 

前の表に、**コンテキスト**HD オーディオ DDI 基準計画の特定のインスタンスに固有の情報が含まれるコンテキスト オブジェクトへのポインターします。 クライアントは、IOCTL から HD オーディオ DDI この基準を取得します。 常に指定する必要があります、クライアント機能のドライバーでは、DDI でルーチンのいずれかを呼び出し、ときに、**コンテキスト**最初の呼び出しのパラメーターとしてメンバーの値。 コンテキスト情報は、クライアントに対して非透過的です。 HD オーディオ バス ドライバーでは、各クライアントのさまざまなコンテキスト オブジェクトを作成します。 クライアントが呼び出すことによって、コンテキスト オブジェクトを解放するコンテキスト オブジェクトが必要でなくなったときに、 **InterfaceDereference**ルーチンは、前の表に示すようにします。 クライアントが呼び出すことによってオブジェクトへの他の参照を作成できますが必要な場合、 **InterfaceDereference**ルーチンが、クライアントが不要になった要求して、これらの参照を解放します。

 

 



