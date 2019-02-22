---
title: StartDeviceWait ルール (wdm)
description: StartDeviceWait ルールでは、ドライバーが IRP のデバイスの起動のコンテキストで kewaitforsingleobject の 1 を呼び出す必要がありますいないことを指定します。
ms.assetid: 99DFB919-916C-4D08-B00D-400C02E20388
ms.date: 05/21/2018
keywords:
- StartDeviceWait ルール (wdm)
topic_type:
- apiref
api_name:
- StartDeviceWait
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: b5acfc03a14af33049fbed1818631e7ff6431f83
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56559317"
---
# <a name="startdevicewait-rule-wdm"></a>StartDeviceWait ルール (wdm)


**StartDeviceWait**ルールでは、ドライバーを呼び出さないことを指定します[ **kewaitforsingleobject の 1** ](https://msdn.microsoft.com/library/windows/hardware/ff553350)スタート デバイス IRP のコンテキストでします。

|              |     |
|--------------|-----|
| ドライバー モデル | WDM |

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>StartDeviceWait</strong>ルール。</p>
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

[**IoSetCompletionRoutine**](https://msdn.microsoft.com/library/windows/hardware/ff549679)
[**KeInitializeEvent**](https://msdn.microsoft.com/library/windows/hardware/ff552137)
[**kewaitforsingleobject の 1**](https://msdn.microsoft.com/library/windows/hardware/ff553350)
 

 




