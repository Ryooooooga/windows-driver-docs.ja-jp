---
title: C28638
description: C28638 関数遅延読み込みスタブを警告には、対応する宣言がありません。
ms.assetid: 25999552-6316-414b-972d-25797f477b15
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28638
ms.openlocfilehash: 1b52c49978388a95ed4daa2ad14aa3881f96229c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56551927"
---
# <a name="c28638"></a>C28638


警告 C28638: 関数遅延読み込みスタブに対応する宣言がありません

関数が宣言されているヘッダー ファイルを含めずに、多くの遅延読み込みスタブを実装できます。 時間の経過と共に、関数のシグネチャは、対応するすべての遅延読み込みスタブを更新することがなく変更可能性があります。 遅延読み込みスタブに正しくないシグネチャがある場合は、アクセス違反につながります。

通常、 **\#含める&lt;header.h&gt;** に実装されている、遅延読み込みスタブが不足している関数のプロトタイプを含みます。 よくある間違いでは、(そのため、プライベートの省略すると)、パブリックとプライベートの両方の序数の遅延読み込みスタブを実装するときにパブリック ヘッダー ファイルをインクルードします。 修正プログラムは、実装されている、遅延読み込みスタブ用の適切なヘッダー ファイルが含まれます。

 

 





