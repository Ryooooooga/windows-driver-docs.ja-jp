---
title: バグ チェック 0xE9 ACTIVE_EX_WORKER_THREAD_TERMINATION
description: ACTIVE_EX_WORKER_THREAD_TERMINATION のバグ チェックでは、0x000000E9 の値を持ちます。 これは、アクティブな実行ワーカー スレッドの終了を示します。
ms.assetid: dd68f07f-fab1-402c-9a81-f43722f91b69
keywords:
- バグ チェック 0xE9 ACTIVE_EX_WORKER_THREAD_TERMINATION
- ACTIVE_EX_WORKER_THREAD_TERMINATION
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ACTIVE_EX_WORKER_THREAD_TERMINATION
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: f31bb9b0ede63709dfdcadd17a22f060fc00b505
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56578940"
---
# <a name="bug-check-0xe9-activeexworkerthreadtermination"></a>バグ チェック 0xE9:アクティブな\_EX\_ワーカー\_スレッド\_終了


アクティブな\_EX\_ワーカー\_スレッド\_終了バグ チェックが 0x000000E9 の値を持ちます。 これは、アクティブな実行ワーカー スレッドの終了を示します。

**重要な**プログラマ向けのトピックです。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)します。

## <a name="activeexworkerthreadtermination-parameters"></a>アクティブな\_EX\_ワーカー\_スレッド\_終了パラメーター


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
<td align="left"><p>既存の ETHREAD</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>予約済み</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>予約済み</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>予約済み</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

ワーカー スレッドのランダウン コードを経てことがなく実行ワーカー スレッドを終了しています。 これは禁止されています。作業項目のキューに登録、 **ExWorkerQueue**そのスレッドを終了する必要があります。

スタック トレースは、原因を示す必要があります。

 

 



