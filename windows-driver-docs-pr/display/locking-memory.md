---
title: メモリのロック
description: メモリのロック
ms.assetid: bf14e0f7-13cc-4e55-bbb1-a6b6f6b6271f
keywords:
- ロックのメモリ WDK の表示
- GPU 失速防止 WDK の表示
- メモリ ロック WDK の表示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1f9b08fbf0dcbf6c914bd0f2518f1a5d66daa467
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63347547"
---
# <a name="locking-memory"></a>メモリのロック


## <span id="ddk_locking_memory_gg"></span><span id="DDK_LOCKING_MEMORY_GG"></span>


失速、グラフィックス処理装置 (GPU) を保持するには、準備のワーカー スレッドは、GPU が他の操作でビジー状態中にメモリをロックします。 ただし場合は、完全な大規模に割り当てられたディスクにページングにドライバーが、割り当てのページに GPU スケジューラの待機中に、GPU は遅延があります。

 

 





