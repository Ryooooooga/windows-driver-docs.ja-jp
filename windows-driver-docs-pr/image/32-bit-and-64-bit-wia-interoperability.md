---
title: 32 ビットおよび 64 ビットの WIA 相互運用性
description: 32 ビットおよび 64 ビットの WIA 相互運用性
ms.assetid: f7f7a42a-590e-4f81-b325-ba9f9ffa9664
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 59a4112f2dee1d23457d4d1fa3480a7eac758740
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56577653"
---
# <a name="32-bit-and-64-bit-wia-interoperability"></a>32 ビットおよび 64 ビットの WIA 相互運用性


拡張プロセッサ用の Windows の 64 ビット エディションを実行しているシステムでは、すべての WIA コンポーネントは、これらの 64 ビット ドライバーと既存の 32 ビット アプリケーション間の相互運用を許可する、WIA インフラストラクチャが変更されたために 64 ビットが。

Windows オペレーティング システムの 64 ビット エディション、64 ビットの WIA ミニドライバーは、WIA サービスの 64 ビット プロセスに読み込まれたです。 ただし、WIA ミニドライバー UI 拡張機能は、アプリケーションのプロセス空間内で読み込まれます。 X64 ベースのマシンで実行されている Microsoft Win32 アプリケーションの変更されていない 32 ビット プロセスは、64 ビットの UI 拡張機能を読み込むことはできません。

32 ビットから 64 ビット問題を軽減するためには、マイクロソフトは、64 ビットの拡張機能のホストを提供しています*wiawow64.exe*します。 このホストは、32 ビット アプリケーションと 64 ビット WIA UI の間の透過的な相互運用性拡張機能をによりします。 *Wiawow64.exe*拡張機能ホストは拡張プロセッサの Windows Server 2003 の 64 ビット エディション、プロセッサの拡張、Windows Vista、およびそれ以降のオペレーティング システム バージョンの Windows XP 64-bit Edition で利用できます。

WIA サービスは読み込むかを決定、UI の拡張機能を取得物理的に、アプリケーションは、64 ビットまたは 32 ビットかどうかに応じて。

-   *64 ビット アプリケーション*します。 64 ビット WIA ミニドライバー UI 拡張機能は、アプリケーションのプロセス領域に直接読み込まれます。 32 ビット バージョンの Windows オペレーティング システムで 32 ビット アプリケーションを実行するときの動作に似ています。

-   *32 ビット アプリケーション*します。 WIA が起動、 *wiawow64.exe* UI 拡張機能が読み込まれる拡張機能ホスト。 インスタンスを個別*wiawow64.exe*が作成され、32 ビット アプリケーションからは、インターフェイス メソッドのいずれかへの呼び出しごとに起動します。 *Wiawow64.exe*ホスト アプリケーションと同じコンテキストで実行され、は、既存の COM インターフェイス経由でアプリケーションと通信します。

    **注**  にもかかわらず*wiawow64.exe* WIA アプリケーションの作成者と WIA ドライバー開発者向け、開発者は、デバッグする必要があるドライバーの両方に完全に透過的、 *wiawow64.exe*64 ビットの UI 拡張機能をデバッグする 32 ビット アプリケーションではなく処理します。

     

 

 



