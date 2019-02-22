---
title: ネットワークのドライバーでの移植性
description: ネットワークのドライバーでの移植性
ms.assetid: 2cc74131-a80b-4d21-b969-56b61d1f7269
keywords:
- ネットワーク ドライバー WDK、ドライバーの移植
- 移植性の WDK ネットワーク
- ドライバー WDK ネットワー キングの移植
- NDIS 移植ドライバー WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 918a55747ae4a99eba93018c24f379a1fbe6963d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532201"
---
# <a name="portability-in-network-drivers"></a>ネットワークのドライバーでの移植性





Microsoft Windows オペレーティング システムをサポートするすべてのプラットフォーム間で簡単に移植可能なもの、NDIS ドライバーを記述する必要があります。 一般に、1 つのハードウェア プラットフォームから別の移植する必要がありますのみを必要とシステムと互換性のあるコンパイラで再コンパイルします。

NDIS ドライバーを記述するときに、次のガイドラインに従います。

-   オペレーティング システムに固有の関数の呼び出しを回避します。 代わりに、NDIS 同等の関数を使用します。 NDIS ドライバーを記述するためのサポート機能の豊富なセットをエクスポートする機能をサポートし、これらを呼び出すかどうか NDIS をサポートする Microsoft オペレーティング システムの間のコードを移植することができます。

-   C (具体的には、ANSI C 規格) では、ドライバーを記述します。 他のシステムと互換性のあるコンパイラをサポートしない言語の機能を使用しないでください。 ANSI C 規格を「実装で定義します」として指定する任意の機能を使用しません。

-   サイズとレイアウトは、プラットフォーム間で異なるデータ型への依存関係を回避します。 たとえば、NDIS で提供される関数ではなく C ランタイム ライブラリ関数を呼び出すドライバーのコードを書き込みません。

-   カーネル モードでは、浮動小数点演算を使用しません。 このような操作を試みると、致命的なエラーが発生します。

-   使用 **\#ifdef**と **\#endif**プラットフォームに固有の機能をサポートするために使用されるコードをカプセル化するステートメント。

 

 




