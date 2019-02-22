---
title: バグ チェック 0x5 INVALID_PROCESS_ATTACH_ATTEMPT
description: INVALID_PROCESS_ATTACH_ATTEMPT のバグ チェックでは、0x00000005 の値を持ちます。
ms.assetid: 72efb88f-1bf7-4552-b44e-4ecb04754b7d
keywords:
- バグ チェック 0x5 INVALID_PROCESS_ATTACH_ATTEMPT
- INVALID_PROCESS_ATTACH_ATTEMPT
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- INVALID_PROCESS_ATTACH_ATTEMPT
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: dbaf5dbf1a6e23b3cd30b9d21153111c5819b683
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553843"
---
# <a name="bug-check-0x5-invalidprocessattachattempt"></a>0x5 チェックをバグします。無効な\_プロセス\_アタッチ\_試行


無効な\_プロセス\_アタッチ\_試行のバグ チェックが 0x00000005 の値を持ちます。 これは、通常、スレッドは許可されていませんかのような状況でのプロセスにアタッチされたことを示します。 たとえば、このバグ チェックが場合に発生する**KeAttachProcess** (これは有効ではありません)、接続されている状態で特定の関数を呼び出すスレッドから返された場合、スレッドが既に (これは、法律ではありません)、プロセスにアタッチされている、またはときに呼び出されました

このバグ チェックが非常に少ない回数が表示されます。

**重要な**プログラマ向けのトピックです。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)します。

## <a name="invalidprocessattachattempt-parameters"></a>無効な\_プロセス\_アタッチ\_試行パラメーター


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
<td align="left"><p>ターゲット プロセスでは、ディスパッチャー オブジェクトへのポインターのかどうか、スレッドは既にまたは接続された、元のプロセスのオブジェクトへのポインター。</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>現在のスレッドに現在アタッチされているプロセスのディスパッチャー オブジェクトへのポインター。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>スレッドの値&#39;s APC 状態のインデックス。</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>0 以外の値は、現在のプロセッサの DPC が実行されていることを示します。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

このバグ チェックは、ドライバーを呼び出す場合に発生することができます、 **KeAttachProcess**関数と、スレッドは既に別のプロセスにアタッチされています。 使用することをお勧め、 **KeStackAttachProcess**関数。 現在のスレッドが既に別のプロセスにアタッチされている場合、 **KeStackAttachProcess**新しいプロセスに現在のスレッドをアタッチする前に、関数が現在の APC 状態を保存します。

 

 



