---
title: PagedCodeAtD0 ルール (kmdf)
description: PagedCodeAtD0 ルールでは、ドライバーがパワーアップ コード パスに含まれるコールバック関数内でページング可能としてコードをマークする必要がありますを指定します。
ms.assetid: e3e0ee8f-eebe-4855-be35-3d8b153dd09e
ms.date: 05/21/2018
keywords:
- PagedCodeAtD0 ルール (kmdf)
topic_type:
- apiref
api_name:
- PagedCodeAtD0
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 52981b20ecefd5de443c0da8680cad1a77738082
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67392978"
---
# <a name="pagedcodeatd0-rule-kmdf"></a>PagedCodeAtD0 ルール (kmdf)


**PagedCodeAtD0**ルールでは、ドライバーがパワーアップ コード パスに含まれるコールバック関数内でページング可能としてコードをマークする必要がありますを指定します。

関数は、ページングがマークされ、コード セクションがページ アウト後、関数では、コンピューターの高速な再開動作に影響を与えるページ フォールトが生成されます。 これは、クライアント ドライバーは、システム ドライバーは、このページ フォールトにサービスを提供するまで待機する必要があるために発生します。

|              |      |
|--------------|------|
| ドライバー モデル | KMDF |

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
<td align="left"><p>実行<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">Static Driver Verifier</a>を指定し、 <strong>PagedCodeAtD0</strong>ルール。</p>
コードの分析を実行するには、次の手順に従います。
<ol>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code" data-raw-source="[Prepare your code (use role type declarations).](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code)">(ロールの型宣言の使用)、コードを準備します。</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier" data-raw-source="[Run Static Driver Verifier.](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier)">Static Driver Verifier を実行します。</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results" data-raw-source="[View and analyze the results.](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results)">表示し、結果を分析します。</a></li>
</ol>
<p>詳細については、次を参照してください。<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers" data-raw-source="[Using Static Driver Verifier to Find Defects in Drivers](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers)">ドライバーで障害を検出する Static Driver Verifier を使用して</a>します。</p></td>
</tr>
</tbody>
</table>

<a name="applies-to"></a>適用対象
----------

[**ページングされた\_コード**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)
 

 





