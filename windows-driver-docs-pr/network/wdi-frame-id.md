---
title: WDI_FRAME_ID
description: このトピックでは、WDI ミニポート ドライバー WDI_FRAME_ID データ型について説明します。
ms.assetid: 7D886BA2-EDD2-4770-948C-9C891D07EF58
keywords:
- WDI_FRAME_ID、WDK WDI_FRAME_ID ネットワーク ドライバー
ms.date: 11/27/2017
ms.localizationpriority: medium
ms.openlocfilehash: f3c88c7744c899f1f9ff3bb43d872757aad4b7b3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63367502"
---
# <a name="wdiframeid"></a>WDI_FRAME_ID

WDI_FRAME_ID のデータ型は、フレーム ID を定義する UINT16 値 これは、識別子のみです。 フレームの順序に関する情報が伝達されません。

```c++
typedef UINT16 WDI_FRAME_ID;
```

## <a name="requirements"></a>要件

|   |   |
| --- | --- |
| サポートされている最小のクライアント | Windows 10 |
| サポートされている最小のサーバー | Windows Server 2016 |
| Header | Dot11wdi.h |

