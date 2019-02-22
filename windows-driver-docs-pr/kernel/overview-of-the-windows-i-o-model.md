---
title: Windows I/O モデルの概要
description: Windows I/O モデルの概要
ms.assetid: 17a012b7-946e-4f42-8d80-e270bc26de06
keywords:
- Irp WDK カーネルでは、Windows I/O モデルについて
- Windows I/O model WDK
- I/O WDK カーネル、モデル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3b86daddcaf0016aa417d5cf54ce6db32f57f79d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529450"
---
# <a name="overview-of-the-windows-io-model"></a>Windows I/O モデルの概要





すべてのオペレーティング システムが、暗黙的または明示的な I/O のモデルと周辺機器の間のデータのフローを処理するためです。 Microsoft Windows I/O モデルの機能の 1 つは、非同期 I/O のサポートです。 さらに、I/O のモデルでは、次の一般的な機能があります。

-   I/O マネージャーが最下位レベルを含むすべてのカーネル モード ドライバーに一貫性のあるインターフェイスを表示、中間、およびファイル システム ドライバー。 すべての I/O 要求のドライバーには、I/O 要求パケット (Irp) として送信されます。

-   I/O 操作が重ねられています。 I/O マネージャーは、ユーザー モードには、そのアプリケーションまたはエンドユーザーの代わりの I/O 操作を実行するサブシステムの呼び出しが保護されている、I/O システム サービスをエクスポートします。 I/O マネージャーは、これらの呼び出しをインターセプト、1 つまたは複数の Irp を設定し、物理デバイスに可能性がある階層型のドライバーを介してルーティングします。

-   I/O マネージャーは、標準のルーチン、省略可能なドライバーがサポートしている他のユーザーおよび必要ないくつかのセットを定義します。 すべてのドライバーでは、周辺機器とバス、関数、フィルター、およびファイル システム ドライバーの必要なさまざまな機能の間での違いがある、比較的一貫性のある実装モデルに従います。

-   オペレーティング システム自体のようなドライバーは、オブジェクト ベースです。 ドライバー、そのデバイス、およびシステムのハードウェアは、オブジェクトとして表されます。 I/O マネージャーや他のオペレーティング システム コンポーネント、ドライバーは、適切なオブジェクトを操作することによって作業を呼び出すことができる、カーネル モードのサポート ルーチンをエクスポートします。

Irp を使用して、従来の I/O 要求を伝達するだけでなく、I/O マネージャーは PnP と電力の要求を含む Irp を送信する PnP と電力のマネージャーとは動作します。

 

 



