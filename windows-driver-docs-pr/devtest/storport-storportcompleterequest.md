---
title: StorPortCompleteRequest ルール (storport)
description: このルールは、ミニポートによって StorPortCompleteRequest への呼び出しが行われていないことを確認します。 StorPortCompleteRequest の使用は推奨されません。ミニポートは、notificationType RequestComplete で StorPortNotification を代わりに呼び出す必要があります。
ms.assetid: 6DDAC83F-C4D5-4600-B5F3-AA7F216BB797
ms.date: 05/21/2018
keywords:
- StorPortCompleteRequest ルール (storport)
topic_type:
- apiref
api_name:
- StorPortCompleteRequest
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: de042c9d9af5f7ab608b2f1e97a5ac765161b2b2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56549802"
---
# <a name="storportcompleterequest-rule-storport"></a>StorPortCompleteRequest ルール (storport)


このルールを確認するを呼び出せなく**StorPortCompleteRequest**ミニポートによって行われます。 使用状況、 **StorPortCompleteRequest**は推奨されません。 ミニポートが代わりに呼び出す必要があります**StorPortNotification**で**notificationType = RequestComplete**します。

|              |          |
|--------------|----------|
| ドライバー モデル | Storport |

<a name="how-to-test"></a>テスト方法
-----------

<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">コンパイル時</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>StorPortCompleteRequest</strong>ルール。</p>
コードの分析を実行するには、次の手順に従います。
<ol>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh454281#preparing-your-source-code" data-raw-source="[Prepare your code (use role type declarations).](https://msdn.microsoft.com/library/windows/hardware/hh454281#preparing-your-source-code)">(ロールの型宣言の使用)、コードを準備します。</a></li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh454281#running-static-driver-verifier" data-raw-source="[Run Static Driver Verifier.](https://msdn.microsoft.com/library/windows/hardware/hh454281#running-static-driver-verifier)">Static Driver Verifier を実行します。</a></li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh454281#viewing-and-analyzing-the-results" data-raw-source="[View and analyze the results.](https://msdn.microsoft.com/library/windows/hardware/hh454281#viewing-and-analyzing-the-results)">表示し、結果を分析します。</a></li>
</ol>
<p>詳細については、次を参照してください。<a href="https://msdn.microsoft.com/library/windows/hardware/hh454281" data-raw-source="[Using Static Driver Verifier to Find Defects in Drivers](https://msdn.microsoft.com/library/windows/hardware/hh454281)">ドライバーで障害を検出する Static Driver Verifier を使用して</a>します。</p></td>
</tr>
</tbody>
</table>

<a name="applies-to"></a>適用対象
----------

[**StorPortCompleteRequest**](https://msdn.microsoft.com/library/windows/hardware/ff567042)
 

 




