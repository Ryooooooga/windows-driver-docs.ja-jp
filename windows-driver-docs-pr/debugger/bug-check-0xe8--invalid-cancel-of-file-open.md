---
title: バグ チェック 0xE8 INVALID_CANCEL_OF_FILE_OPEN
description: INVALID_CANCEL_OF_FILE_OPEN のバグ チェックでは、0x000000E8 の値を持ちます。 これは、IoCancelFileOpen に無効なファイル オブジェクトが渡されたことを示します。
ms.assetid: 168d8b3a-62a0-4436-9e97-812ddfb8b7f7
keywords:
- バグ チェック 0xE8 INVALID_CANCEL_OF_FILE_OPEN
- INVALID_CANCEL_OF_FILE_OPEN
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- INVALID_CANCEL_OF_FILE_OPEN
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 3c584759aea989de4b58d5e13f8e6620f01139a3
ms.sourcegitcommit: d03b44343cd32b3653d0471afcdd3d35cb800c0d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2019
ms.locfileid: "67518801"
---
# <a name="bug-check-0xe8-invalidcanceloffileopen"></a>バグ チェック 0xE8:無効な\_キャンセル\_の\_ファイル\_開く


無効な\_キャンセル\_の\_ファイル\_バグを開くチェックが 0x000000E8 の値を持ちます。 これは、無効なファイル オブジェクトに渡されたことを示します。 **IoCancelFileOpen**します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://www.windows.com/stopcode)します。


## <a name="invalidcanceloffileopen-parameters"></a>無効な\_キャンセル\_の\_ファイル\_パラメーターを開く


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
<td align="left"><p>ファイル オブジェクトに渡される<strong>IoCancelFileOpen</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>デバイス オブジェクトに渡される<strong>IoCancelFileOpen</strong></p></td>
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

ファイル オブジェクトに渡される**IoCancelFileOpen**が無効です。 1 つの参照が必要です。 呼ばれるドライバー **IoCancelFileOpen**障害があります。

 

 




