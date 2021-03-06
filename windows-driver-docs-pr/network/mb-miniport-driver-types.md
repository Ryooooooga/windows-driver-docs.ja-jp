---
title: MB ミニポート ドライバーの種類
description: MB ミニポート ドライバーの種類
ms.assetid: ec1743a1-4c5e-4960-b352-40fc5b9c016a
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d211d9601932917cd491dcb09c46416161997704
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63343286"
---
# <a name="mb-miniport-driver-types"></a>MB ミニポート ドライバーの種類


データ パケットの処理、DHCP サーバーおよび ARP エミュレーションに基づき、複数 MB ミニポート ドライバーの実装の種類はもあります。 次の表は、さまざまな考えられる実装の種類と実稼働品質のミニポート ドライバーに必要な実装を表します。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">説明</th>
<th align="left">MediaType</th>
<th align="left">EnableDhcp</th>
<th align="left">ARP エミュレーション</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>DHCP のエミュレーションでイーサネット エミュレーション</p></td>
<td align="left"><p>NdisMedium802_3</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>必須</p></td>
</tr>
<tr class="even">
<td align="left"><p>イーサネット エミュレーションと DHCP がありません。</p></td>
<td align="left"><p>NdisMedium802_3</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>必須</p></td>
</tr>
<tr class="odd">
<td align="left"><p>IP パケットを DHCP エミュレーションと処理</p></td>
<td align="left"><p>NdisMediumWirelessWan</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>不要</p></td>
</tr>
<tr class="even">
<td align="left"><p>IP パケットの処理機能</p></td>
<td align="left"><p>NdisMediumWirelessWan</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>必須ではない</p></td>
</tr>
</tbody>
</table>

 

開発や移行のフェーズ中にミニポート ドライバーが、最初の 3 つのエントリのいずれかを指定できます。 ただし、実稼働品質のミニポート ドライバーでは、テーブル (「IP パケット処理機能」) の最後のエントリで指定された設定のみを使用する必要があります。

運用環境品質 MB ミニポート ドライバーでは、INF ファイルで次の表に、設定を指定する必要があります。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">INF ファイル内のフィールド</th>
<th align="left">推奨値</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>* IfType</p></td>
<td align="left"><p>IF_TYPE_WWANPP/IF_TYPE_WWANPP2</p></td>
</tr>
<tr class="even">
<td align="left"><p>MediaType</p></td>
<td align="left"><p>NdisMediumWirelessWan</p></td>
</tr>
<tr class="odd">
<td align="left"><p>EnableDhcp</p></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="even">
<td align="left"><p>UpperRange</p></td>
<td align="left"><p>"flpp4"と"flpp6"(IPv6 がサポートされている) 場合</p></td>
</tr>
<tr class="odd">
<td align="left"><p>LowerRange</p></td>
<td align="left"><p>"ppip"</p></td>
</tr>
</tbody>
</table>

 

 

 





