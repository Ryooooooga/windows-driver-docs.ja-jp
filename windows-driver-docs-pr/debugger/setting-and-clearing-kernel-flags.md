---
title: カーネル フラグの設定とクリア
description: カーネル フラグの設定とクリア
ms.assetid: 6bca8007-2d9f-4b93-b5fb-300c262604c8
keywords:
- GFlags、カーネル フラグ
- GFlags、実行時の設定
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6fe55fef0fd81b02ca7b5a976e3bbc2e81d5a160
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63381968"
---
# <a name="setting-and-clearing-kernel-flags"></a>カーネル フラグの設定とクリア


## <span id="ddk_setting_and_clearing_kernel_mode_flags_dtools"></span><span id="DDK_SETTING_AND_CLEARING_KERNEL_MODE_FLAGS_DTOOLS"></span>


カーネルのフラグ設定、「実行時設定」とも呼ばれるでは、システム全体に影響します。 直ちに有効になり、再起動しますが、シャット ダウン、システムを再起動するか失われます。

カーネルの設定よりも優先レジストリ設定、実行時ですがシャット ダウン、システムを再起動すると、カーネルのフラグ設定が失われ、レジストリ設定は、もう一度有効。

**設定し、カーネルのフラグをクリア**

1.  をクリックして、**カーネル フラグ**タブ。

    次のスクリーン ショットは、**カーネル フラグ**Windows Vista タブ。

    ![windows vista のカーネル フラグ タブのスクリーン ショット ](images/gflags-kernel.png)

2.  設定またはフラグをオンまたはオフ、フラグに関連付けられているチェック ボックスをオフにします。

3.  選択またはすべてのフラグをオフになっている、クリックして**適用**します。

 

 





