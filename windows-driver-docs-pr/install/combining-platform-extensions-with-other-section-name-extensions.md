---
title: プラットフォーム拡張機能とその他のセクション名の拡張機能を組み合わせる
description: プラットフォーム拡張機能とその他のセクション名の拡張機能を組み合わせる
ms.assetid: ca82ba0f-0d65-47ca-826a-4f78435b1442
keywords:
- INF ファイル WDK デバイス インストールでは、プラットフォーム拡張機能
- 'プラットフォーム拡張機能: WDK INF ファイル'
- WDK INF プラットフォームの拡張機能
- 'プラットフォーム拡張機能: WDK INF ファイルの結合'
- WDK の INF ファイルのインストール セクション名
- 装飾の INF WDK
- WDK のオペレーティング システム
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b4234541fcb785fe0112bc8e0386682d3dfe1879
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56578167"
---
# <a name="combining-platform-extensions-with-other-section-name-extensions"></a>プラットフォーム拡張機能とその他のセクション名の拡張機能を組み合わせる


INF を含む INF ファイル*DDInstall*プラットフォーム拡張機能のセクションでは、必要ななどのデバイスごとの追加セクションを含めることも<em>DDInstall</em>**します。サービス**と省略可能な<em>DDInstall</em>**します。HW**、 <em>DDInstall</em>**します。CoInstallers**、 <em>DDInstall</em>**します。LogConfigOverride**、および<em>DDInstall</em>**します。インターフェイス**セクション。 クロス オペレーティング システムおよびクロス プラットフォーム INF ファイルでは、INF ライター定義セクション名の直後に、適切なプラットフォーム拡張機能を指定する必要があります (たとえば、<em>インストール セクション名</em>**.ntx86 します。HW**)。

クロス オペレーティング システムの INF ファイルが含まれている場合は、装飾<em>インストール セクション名</em>**.nt**、<em>インストール セクション名</em>**.ntx86**、 <em>インストール セクション名</em>**.ntia64**、または<em>インストール セクション名</em>**.ntamd64**セクションでは、その他必要があります並列装飾し、装飾されていないデバイスごとのセクションでします。 つまり、INF ファイルでは、両方を持つ場合*インストール セクション名*と<em>インストール セクション名</em>**.nt**のセクションでは、これが、 *DDInstall*.**HW**  セクションで、並列にも必要<em>インストール セクション名</em>**.nt します。HW**セクション (デバイスまたはドライバーが必要な場合、**します。HW** Windows 2000 と Windows の以降のバージョンについてのセクション)。

トピックでは、 [INF ファイルのセクションとディレクティブ](inf-file-sections-and-directives.md)セクションの表示、 **nt**<em>xxx</em>**します。HW**正式な構文のステートメント内の適切なセクションの一部として拡張機能参照、次の例のようにします。

**\[**<em>インストール セクション名</em>**します。HW\]** |
**\[**<em>インストール セクション名</em>**.nt します。HW\]** |
**\[**<em>インストール セクション名</em>**.ntx86 します。HW\]** |
**\[**<em>インストール セクション名</em>**.ntia64 します。HW\]** |
**\[**<em>インストール セクション名</em>**.ntamd64 します。HW\] **正式な構文のステートメントでは、これらの拡張機能の基本的なセクションに有効な代替手段であることを示します。 このステートメントの種類は*いない*がする INF ファイルを指定、<em>インストール セクション名</em>**.nt します。HW**セクションではすべて他のプラットフォームに固有を含める必要がありますも<em>インストール セクション名</em>**.nt**<em>xxx</em>**します。HW**セクション。 これらの拡張機能のサブセットを使用すると、特定のクロス プラットフォームのインストールを必要とされる装飾セクションを指定します。

INF ファイルが含まれている*インストール セクション名*プラットフォーム拡張機能とプラットフォームの拡張機能を含めることも、 [ **INF SourceDisksNames セクション**](inf-sourcedisksnames-section.md)と[ **INF SourceDisksFiles セクション**](inf-sourcedisksfiles-section.md)エントリ、プラットフォーム固有の方法でインストール ファイルの場所を指定します。

 

 




