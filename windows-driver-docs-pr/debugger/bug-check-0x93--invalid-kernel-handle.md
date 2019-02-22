---
title: バグ チェック 0x93 INVALID_KERNEL_HANDLE
description: INVALID_KERNEL_HANDLE のバグ チェックでは、0x00000093 の値を持ちます。 このバグ チェックでは、そのファイルに対してクローズに、無効であるか、保護されているハンドルが渡されたことを示します。
ms.assetid: c8564da7-cdbf-40f5-94f4-b1fac23b8b42
keywords:
- バグ チェック 0x93 INVALID_KERNEL_HANDLE
- INVALID_KERNEL_HANDLE
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- INVALID_KERNEL_HANDLE
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: e7bfb6a2d05a70d1f7c0f335a2e35070df745510
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56528626"
---
# <a name="bug-check-0x93-invalidkernelhandle"></a>バグ チェック 0x93 の。無効な\_カーネル\_処理


無効な\_カーネル\_ハンドルのバグ チェックが 0x00000093 の値を持ちます。 このバグ チェックに、無効であるか、保護されているハンドルが渡されたことを示します**そのファイルに対してクローズ**します。

**重要な**プログラマ向けのトピックです。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)します。

## <a name="invalidkernelhandle-parameters"></a>無効な\_カーネル\_ハンドル パラメーター


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
<td align="left"><p>渡されるハンドル<strong>そのファイルに対してクローズ</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p><strong>0:</strong>呼び出し元が、保護されたハンドルを終了しようとしています。</p>
<p><strong>1:</strong>呼び出し元が、無効なハンドルを閉じるしようとしています。</p></td>
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

無効な\_カーネル\_ハンドルのバグ チェックでは、カーネル コード (サーバー、リダイレクター、または別のドライバーなど) が無効なハンドルまたは保護されたハンドルを終了しようとしたことを示します。

 

 



