---
title: Bug Check 0xB8 ATTEMPTED_SWITCH_FROM_DPC
description: ATTEMPTED_SWITCH_FROM_DPC のバグ チェックでは、0x000000B8 の値を持ちます。 これは、無効な操作が遅延プロシージャ呼び出し (DPC) のルーチンによって試行されたことを示します。
ms.assetid: 614b7be8-cec9-4dd9-b183-66db1790c31f
keywords:
- Bug Check 0xB8 ATTEMPTED_SWITCH_FROM_DPC
- ATTEMPTED_SWITCH_FROM_DPC
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ATTEMPTED_SWITCH_FROM_DPC
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 1d09a235a5f9b3290418280efe445e4d0439ef52
ms.sourcegitcommit: d03b44343cd32b3653d0471afcdd3d35cb800c0d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2019
ms.locfileid: "67519011"
---
# <a name="bug-check-0xb8-attemptedswitchfromdpc"></a>バグ チェック 0xB8:試行\_スイッチ\_FROM\_DPC


試行\_スイッチ\_FROM\_DPC バグ チェックが 0x000000B8 の値を持ちます。 これは、無効な操作が遅延プロシージャ呼び出し (DPC) のルーチンによって試行されたことを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://www.windows.com/stopcode)します。


## <a name="attemptedswitchfromdpc-parameters"></a>試行\_スイッチ\_FROM\_DPC パラメーター


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">パラメーター</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>1</p></td>
<td align="left"><p>元のスレッドが、エラーの原因</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>新しいスレッド</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>元のスレッドのスタック アドレス</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>予約済み</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

A 待機操作では、アタッチ (プロセス)、または yield が DPC ルーチンから実行しようとしました。 これは、無効な操作です。

<a name="resolution"></a>解決方法
----------

スタック トレースは、エラーの原因となった元の DPC ルーチン内のコードになります。

 

 




