---
title: SPB フレームワーク拡張機能 (SpbCx)
description: Windows 8 以降、SPB フレームワーク拡張機能 (SpbCx) は、システムが指定した拡張機能をカーネル モード ドライバー フレームワーク (KMDF) です。
ms.assetid: 84015f3c-ff55-4c1a-bb52-63b6f29b99d7
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d9459c687995c2d78598c72a7d0bf48022693472
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67376910"
---
# <a name="spb-framework-extension-spbcx"></a>SPB フレームワーク拡張機能 (SpbCx)


Windows 8 以降、SPB フレームワーク拡張機能 (SpbCx) がするシステム提供の拡張機能、[カーネル モード ドライバー フレームワーク](https://docs.microsoft.com/windows-hardware/drivers/wdf/what-s-new-for-wdf-drivers)(KMDF)。 SpbCx がで使用できます、 [SPB コント ローラー ドライバー](https://docs.microsoft.com/previous-versions/hh698221(v=vs.85))に接続されている周辺機器のデバイスでの I/O 操作を実行する、[シンプルな周辺機器のバス](https://docs.microsoft.com/previous-versions/hh450903(v=vs.85))(SPB) I²C または SPI など。

SPB コント ローラーのドライバーは、ハードウェア固有のすべての操作を実行します。 これらの操作には、sp B に接続されている周辺機器とバスの転送を開始して、コント ローラーを構成する SPB コント ローラーのハードウェア レジスタへのアクセスが含まれます。

SpbCx は、SPB コント ローラーのデバイスに共通するタスクの処理を実行します。 具体的には、SpbCx SPB コント ローラーの I/O 要求のキューを管理します。 これらのキューには、バスに接続されている周辺機器のデバイスの I/O 要求が含まれます。 ハードウェア ベンダー SPB コント ローラーには、これらの要求を処理するために必要なすべてのハードウェアに固有の操作を実行する SPB コント ローラーのドライバーを提供します。

SpbCx と SPB コント ローラー ドライバーの責任の分担は次のとおりです。

-   SpbCx は、SPB のコント ローラー デバイス クラスのすべてのメンバーに共通する汎用的な機能を管理します。 SpbCx では、コント ローラーのドライバーの既定の要求の処理とフロー制御の多くを提供します。 Windows 8 以降、SpbCx は、Windows オペレーティング システムの受信トレイ コンポーネントです。

-   SPB コント ローラーのドライバーでは、SPB コント ローラー デバイスのハードウェアに固有の機能を管理します。 ハードウェア ベンダーは、SPB コント ローラー デバイスのコント ローラーのドライバーを指定します。

SpbCx と SPB コント ローラーのドライバーは、カーネル モードで実行します。 SpbCx はフレームワークの拡張機能、および SPB コント ローラーのドライバーは、KMDF ドライバー。 SPB コント ローラーのドライバーでは、SpbCx デバイス ドライバー インターフェイス (DDI) で SPB 固有の操作を実行するメソッドを呼び出し、他の一般的なドライバーの機能を実行する KMDF メソッドを呼び出します。 KMDF ドライバーを構築する方法の詳細については、次を参照してください。 [Framework ベースのドライバーの読み込みのビルドと](https://docs.microsoft.com/windows-hardware/drivers/wdf/building-and-loading-a-kmdf-driver)します。

SpbCx スタブ ライブラリ、Spbcx.lib DDI エントリ ポイントに SPB コント ローラー ドライバーが静的にリンクします。 実行時に、このライブラリは、フレームワークの拡張機能モジュールに、Spbcx.sys DDI を実装する動的にリンクするために必要なドライバーのバージョンのネゴシエーションを実行します。 Spbcx.sys の特定のバージョンを必要とする SPB コント ローラー ドライバーより高いバージョン番号を持つ Spbcx.sys のバージョンに安全にリンクできます。 ただし、このドライバーは、バージョン番号が低い Spbcx.sys のバージョンにリンクできません。 SpbCx I/O 要求インターフェイスは、同様に旧バージョンと互換性があります。

ハードウェア ベンダーが、SpbCx を使用しないモノリシック SPB コント ローラーのドライバーを作成するオプションがありますが、そのためには多大な労力が必要です。 比較すると、SpbCx を使用するコント ローラー ドライバーは簡単に開発であり、通常より信頼性の高い。

 

 




