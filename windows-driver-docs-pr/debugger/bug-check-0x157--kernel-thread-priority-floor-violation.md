---
title: バグ チェック 0x157 KERNEL_THREAD_PRIORITY_FLOOR_VIOLATION
description: ATTEMPTED_SWITCH_FROM_DPC のバグ チェックでは、0x00000157 の値を持ちます。 これは、特定のスレッドの優先度のフロアに無効な操作が試行されたことを示します。
ms.assetid: 93D15A0A-1413-47DB-91E8-DB61A3604BB1
keywords:
- バグ チェック 0x157 KERNEL_THREAD_PRIORITY_FLOOR_VIOLATION
- KERNEL_THREAD_PRIORITY_FLOOR_VIOLATION
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- KERNEL_THREAD_PRIORITY_FLOOR_VIOLATION
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 3e59062ab6ba025b9fe3d2b531017c89aad6af7c
ms.sourcegitcommit: d03b44343cd32b3653d0471afcdd3d35cb800c0d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2019
ms.locfileid: "67520039"
---
# <a name="bug-check-0x157-kernelthreadpriorityfloorviolation"></a>バグ チェック 0x157:カーネル\_スレッド\_優先度\_FLOOR\_違反


試行\_スイッチ\_FROM\_DPC バグ チェックが 0x00000157 の値を持ちます。 これは、特定のスレッドの優先度のフロアに無効な操作が試行されたことを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://www.windows.com/stopcode)します。


## <a name="kernelthreadpriorityfloorviolation-parameters"></a>カーネル\_スレッド\_優先度\_FLOOR\_違反パラメーター


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
<td align="left">1</td>
<td align="left">スレッドのアドレス</td>
</tr>
<tr class="even">
<td align="left">2</td>
<td align="left">ターゲットの優先度の値</td>
</tr>
<tr class="odd">
<td align="left">3</td>
<td align="left"><p>違反の性質を示す状態コード</p>
0x1:ターゲットの優先度の優先度のカウンターでは、0x2 過剰フロー。ターゲットの優先度の優先度カウンター 0x3 の下でフローします。ターゲットの優先度の値は無効です。</td>
</tr>
<tr class="even">
<td align="left">4</td>
<td align="left">予約済み</td>
</tr>
</tbody>
</table>

 

 

 




