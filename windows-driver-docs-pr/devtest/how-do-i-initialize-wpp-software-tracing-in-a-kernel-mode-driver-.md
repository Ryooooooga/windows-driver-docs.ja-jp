---
title: カーネル モード ドライバーでは、WPP ソフトウェア トレースを初期化する方法
description: カーネル モード ドライバーでは、WPP ソフトウェア トレースを初期化する方法
ms.assetid: 739428e8-14ff-4435-80e6-35b5c3366c79
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 358775b6a920a2c870eadaf38b9a58d37a8f6320
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530972"
---
# <a name="how-do-i-initialize-wpp-software-tracing-in-a-kernel-mode-driver"></a>カーネル モード ドライバーでは、WPP ソフトウェア トレースの初期化方法


カーネル モード ドライバーでは、WPP トレースを初期化するには呼び出すことによって、 [WPP\_INIT\_トレース](https://msdn.microsoft.com/library/windows/hardware/ff556191)WPP ソフトウェア トレースを初期化するためにマクロ。

エラーを回避するために呼び出す必要がありますが、 [WPP\_INIT\_トレース](https://msdn.microsoft.com/library/windows/hardware/ff556191)マクロで、 [ **DriverEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff552644)ドライバーの機能です。

 

 




