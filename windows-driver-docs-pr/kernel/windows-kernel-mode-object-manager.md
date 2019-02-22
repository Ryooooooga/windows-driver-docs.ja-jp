---
title: Windows カーネル モードのオブジェクト マネージャー
description: Windows カーネル モードのオブジェクト マネージャー
ms.assetid: f10561a3-d831-4c13-9edf-be40fb1db403
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: e511270bb63eb3865e1bd6b1109e197372a374c5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56556791"
---
# <a name="windows-kernel-mode-object-manager"></a>Windows カーネル モードのオブジェクト マネージャー


Windows カーネル モードのオブジェクトの manager コンポーネントを管理して*オブジェクト*します。 ファイル、デバイス、同期メカニズム、レジストリ キー、およびはすべてカーネル モードでのオブジェクトとして表現します。 各オブジェクトには、*ヘッダー* (名前、種類、場所などのオブジェクトに関する情報を含む)、および*本文*(各オブジェクトの種類によって決められた形式のデータを含む)。

Windows では、25 を超える種類のオブジェクトがあります。 いくつかの種類は次のとおりです。

-   ファイル

-   デバイス

-   スレッド数

-   Processes (プロセス)

-   イベント

-   ミュー テックス

-   セマフォ

-   レジストリ キー

-   Jobs

-   セクション

-   アクセス トークン

-   シンボリック リンク

オブジェクト マネージャーは、次の主要なタスクを実行することによって、Windows 内のオブジェクトを管理します。

-   作成とオブジェクトの破棄を管理します。

-   オブジェクトの情報を追跡するためのオブジェクトの名前空間データベースを保持します。

-   維持する方法の各プロセスに割り当てられているリソースを追跡します。

-   セキュリティを提供する特定のオブジェクトのアクセス権を追跡します。

-   オブジェクトの有効期間を管理し、ときに、オブジェクトが自動的に破棄されるリソース容量をリサイクルするかを決定します。

Windows でのオブジェクトの詳細については、次を参照してください。[デバイス オブジェクトとデバイス スタック](device-objects-and-device-stacks.md)します。

オブジェクト マネージャーに直接インターフェイスを提供するルーチンには文字で、通常、プレフィックス"**Ob**"。 たとえば、 **ObGetObjectSecurity**します。 オブジェクト マネージャーのルーチンの一覧は、次を参照してください。[オブジェクト マネージャー ルーチン](https://msdn.microsoft.com/library/windows/hardware/ff557759)します。

Windows が、リソースの抽象化としてオブジェクトを使用することに注意してください。 ただし、Windows でないオブジェクト指向の用語の従来の C++ 意味します。 Windows は*オブジェクトに基づく*します。 Windows のオブジェクト ベースの意味の詳細については、次を参照してください。[オブジェクトに基づく](object-based.md)します。

 

 



