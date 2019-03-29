---
title: バグ チェック 0 xc MAXIMUM_WAIT_OBJECTS_EXCEEDED
description: MAXIMUM_WAIT_OBJECTS_EXCEEDED のバグ チェックでは、0x0000000C の値を持ちます。 これは、現在のスレッドが待機オブジェクトの許可されている数を超えていることを示します。
ms.assetid: 99d2eb8f-f331-45b8-a96b-68696802c269
keywords:
- バグ チェック 0 xc MAXIMUM_WAIT_OBJECTS_EXCEEDED
- MAXIMUM_WAIT_OBJECTS_EXCEEDED
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- MAXIMUM_WAIT_OBJECTS_EXCEEDED
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: c24698abce2a62fa26584eb9eae04423ce92a199
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56573972"
---
# <a name="bug-check-0xc-maximumwaitobjectsexceeded"></a>バグ チェック 0xC:最大\_待機\_オブジェクト\_超過


最大\_待機\_オブジェクト\_超過のバグ チェックが 0x0000000C の値を持ちます。 これは、現在のスレッドが待機オブジェクトの許可されている数を超えていることを示します。

**重要な**プログラマ向けのトピックです。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)します。

## <a name="maximumwaitobjectsexceeded-parameters"></a>最大\_待機\_オブジェクト\_超過パラメーター


なし

<a name="cause"></a>原因
-----

このバグ チェックの結果の不適切な使用の**KeWaitForMultipleObjects**または**FsRtlCancellableWaitForMultipleObjects**します。

呼び出し元がこのルーチンのバッファーへのポインターを渡すことがあります*WaitBlockArray*パラメーター。 待機オブジェクトの追跡にこのバッファーが使用されます。

バッファーは、指定した場合、*カウント*パラメーターが最大値を超える可能性がありますいない\_待機\_オブジェクト。 バッファーが指定されていない場合、*カウント*パラメーターには、スレッドが超えない\_待機\_オブジェクト。

場合の値*カウント*許容される値を超える場合、このバグ チェックが発行されます。

 

 



