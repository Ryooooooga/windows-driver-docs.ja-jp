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
ms.openlocfilehash: cc3b8cc2724fc69ba4041b9da773f5cc0171740a
ms.sourcegitcommit: d03b44343cd32b3653d0471afcdd3d35cb800c0d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2019
ms.locfileid: "67518803"
---
# <a name="bug-check-0xe9-activeexworkerthreadtermination"></a>バグ チェック 0xE9:アクティブな\_EX\_ワーカー\_スレッド\_終了


アクティブな\_EX\_ワーカー\_スレッド\_終了バグ チェックが 0x000000E9 の値を持ちます。 これは、アクティブな実行ワーカー スレッドの終了を示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://www.windows.com/stopcode)します。


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

 

 




