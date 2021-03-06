---
title: KsProcessingMutex ルール)
ms.assetid: AD73B241-7B08-4E48-94A1-B6BDE78590E6
ms.date: 05/21/2018
description: ''
keywords:
- KsProcessingMutex ルール)
topic_type:
- apiref
api_name:
- KsProcessingMutex
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: a5cfa89bc17693da1c412487c9d7019c33b6b856
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67392759"
---
# <a name="ksprocessingmutex-rule-"></a>KsProcessingMutex ルール)


KsProcessingMutex ルールでは、KS ミニポート ドライバーが、正しい順序で処理ミュー テックスを使用することを指定します。

-   再帰的に、処理のミュー テックスを取得できません。
-   スレッド処理のミュー テックスで取得した後でしようとしないでくださいフィルター コントロール ミュー テックスを取得します。
-   スレッドは、まずそれを取得しなくても、処理、ミュー テックスを解放する必要がありますされません。

|              |     |
|--------------|-----|
| ドライバー モデル | KS  |

|                                   |                                                                                                                                       |
|-----------------------------------|---------------------------------------------------------------------------------------------------------------------------------------|
| この規則で見つかったバグ チェック | [**バグ チェック 0xC4 の。ドライバー\_VERIFIER\_検出\_違反**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc4--driver-verifier-detected-violation) (0x0008100B) |

<a name="how-to-test"></a>テスト方法
-----------

<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">実行時に</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>このルールを確認するには、コマンド プロンプト ウィンドウを開きます。 Driver Verifier のコマンドを入力し、指定<strong>/domain ks</strong>します。</p>
<p>次に、例を示します。</p>
<p><strong>verifier /domain ks</strong> [<em>options</em>] <strong>/driver</strong> <em>&lt;yourdriver&gt;</em></p>
<p>詳細については、次を参照してください。 <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier" data-raw-source="[Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)">Driver Verifier</a>します。</p></td>
</tr>
</tbody>
</table>

 

<a name="see-also"></a>関連項目
--------

[AVStream でミュー テックスの処理](https://docs.microsoft.com/windows-hardware/drivers/stream/processing-mutex-in-avstream)
 

 





