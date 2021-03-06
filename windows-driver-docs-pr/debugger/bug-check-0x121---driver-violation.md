---
title: バグ チェック 0x121 DRIVER_VIOLATION
description: DRIVER_VIOLATION のバグ チェックでは、0x00000121 の値を持ちます。 このバグ チェックでは、ドライバーの違反が原因となったことを示します。
ms.assetid: 4a5d1d84-a958-45a6-9511-b5b4ecd4c067
keywords:
- バグ チェック 0x121 DRIVER_VIOLATION
- DRIVER_VIOLATION
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- DRIVER_VIOLATION
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 8e80b189a39ae5b36bd7ee713e47886cff963904
ms.sourcegitcommit: d03b44343cd32b3653d0471afcdd3d35cb800c0d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2019
ms.locfileid: "67520837"
---
# <a name="bug-check-0x121-driverviolation"></a>バグ チェック 0x121:ドライバー\_違反


ドライバー\_違反のバグ チェックが 0x00000121 の値を持ちます。 このバグ チェックでは、ドライバーの違反が原因となったことを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://www.windows.com/stopcode)します。


## <a name="driverviolation-parameters"></a>ドライバー\_違反パラメーター


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
<td align="left"><p>種類の違反について説明します</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>予約済み</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>予約済み</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

カーネル デバッガーを使用し、違反の原因となったドライバーの名前を確認する呼び出し履歴を表示: [ **! 分析**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-analyze)バグ チェックに関する情報を表示拡張機能をデバッグおよびに役に立ついずれかを入力し、根本原因を突き止める、 [ **k (Display Stack Backtrace)** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-)呼び出し履歴を表示するコマンド。

 

 




