---
title: PagedCode ルール (storport)
description: このルールの検証時に、ページング\_コードのマクロが呼び出されると、ドライバーは IRQL ディスパッチ\_レベル。 IRQL のディスパッチを実行してコード\_レベルはページ フォールトを回避するために、非ページ メモリである必要があります。
ms.assetid: 7FED3FEF-E6E5-4C26-8777-0A4BCCE0E1EE
ms.date: 05/21/2018
keywords:
- PagedCode ルール (storport)
topic_type:
- apiref
api_name:
- PagedCode
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 9ee5d3dfc4840513d75d9dafa77593e8f270fb92
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529839"
---
# <a name="pagedcode-rule-storport"></a>PagedCode ルール (storport)


このルールの検証時に、 [**ページ\_コード**](https://msdn.microsoft.com/library/windows/hardware/ff558773)マクロが呼び出されると、ドライバーが、 **IRQL&lt;ディスパッチ\_レベル**します。 任意のコード実行**IRQL &gt;= ディスパッチ\_レベル**ページ フォールトを回避するために、非ページ メモリである必要があります。

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>PagedCode</strong>ルール。</p>
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

[**ページングされた\_コード**](https://msdn.microsoft.com/library/windows/hardware/ff558773)
 

 




