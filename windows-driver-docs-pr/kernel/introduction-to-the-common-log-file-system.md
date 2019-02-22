---
title: Common Log File System の概要
description: Common Log File System の概要
ms.assetid: 2185d834-81f3-4bf9-afa6-897c1515f8b5
keywords:
- Common Log File System についての一般的なログ ファイル システムの WDK カーネル
- Common Log File System の詳細については、CLFS WDK カーネル
- ログ サービス WDK CLFS
- 一般的なログ ファイル システムの WDK ユーザー モード
- CLFS WDK ユーザー モード
- WDK CLFS ログに記録します。
- WDK CLFS ログを多重化
- 専用ログ WDK CLFS
- WDK CLFS のログ シーケンス番号
- Lsn の WDK CLFS
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: b2f61ec177cdab10e1d0219f450ed0860fc70aac
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532267"
---
# <a name="introduction-to-the-common-log-file-system"></a>Common Log File System の概要





Common Log File System (CLFS) がソフトウェアで使用できる汎用的なログ記録サービス[*クライアント*](clfs-terminology.md#kernel-clfs-term-client)ユーザー モードまたはカーネル モードで実行されています。 このドキュメントでは、カーネル モードのクライアントに対して、CLFS インターフェイスについて説明します。 ユーザー モード インターフェイスについては、Microsoft Windows SDK に共通のログ ファイル システムを参照してください。

CLFS は、復旧と分離を悪用するセマンティクス (ARIES) アルゴリズムのすべての機能をカプセル化します。 ただし、CLFS デバイス ドライバー インターフェイス (DDI) は ARIES; サポートに制限はありません。さまざまなログ記録シナリオに適しています。

任意の高パフォーマンス トランザクション ログの主な仕事は、ログ クライアントの履歴を正確に繰り返してに許可するのには。 CLFS は、クライアントのログ レコードをメモリ バッファーにマーシャ リングによって、安定したストレージに強制することと、レコードの読み取り要求でバックアップを作成します。 レコードは、安定したストレージにすると、ストレージ メディアはそのまま、CLFS されるシステム障害が発生したレコードを読み込むことに注意してください。 重要です。

CLFS をサポートでは、専用のログとログを多重化します。 1 つの専用ログ[*ストリーム*](clfs-terminology.md#kernel-clfs-term-stream)のすべてのログのクライアントによって使用されるログ レコード。 多重化されたログ (一般的なログとも呼ばれます) にある複数のストリーム。 各ストリームには、独自のクライアントおよびマーシャ リングする際は、ログ レコードの独自のメモリ バッファーが、これらすべてのバッファーからレコードが 1 つのキューに多重化し、1 つのログを安定したストレージにフラッシュします。 多重化を統合する複数のストリームの I/O 操作ができます。

クライアントでは、レコードを書き込むストリームを今後の参照用のログ レコードを識別するログ シーケンス番号 (LSN) で取得バックアップします。 増加するシーケンスが、一種の特定のストリームに書き込まれるレコードに割り当てられている Lsn。 つまり、ストリームに書き込まれたレコードに割り当てられている LSN では、その同じストリームに書き込まれる前のレコードに割り当てられている LSN よりも大きいは常にします。

CLFS は、マーシャ リングと、フラッシュは、ログ レコードを取得するだけでなく、いくつかのサービスを提供します。 次の一覧では、これらの追加サービスの一部について説明します。

-   事前には、一連の関連するログ レコードの領域を確保することができます。 つまり、クライアントはトランザクションが把握 CLFS がログに追加できることを進んですべてのトランザクションを記述するレコード。

-   CLFS は、各ログ レコードのヘッダーを保持します。 クライアントは、逆の順序で後で走査できるリンクのレコードのチェーンを作成するヘッダーで特定のフィールドを設定できます。

-   CLFS を安定した、そのポリシーに従ってストレージのログ レコードが、クライアントが安定ストレージにログ レコードのセットを強制することができます。

-   CLFS は、ログと多重化されたログの各ストリームのメタデータを保持します。 クライアントは、メタデータを表示し、メタデータの一部を設定できます。

-   各ストリームでは、CLFS ベースの LSN と、クライアントは、ストリームのアクティブな部分を区切るために使用できる最後の LSN を保持します。

-   専用のログは、CLFS は、アーカイブされたログの部分を追跡する、クライアントが使用できるアーカイブ末尾を (クライアントの要求) で保持します。

CLFS (以前の LSN とレコード ヘッダーの元に戻す次 LSN フィールドなど) の特定の機能は、ARIES を調べることで、最も理解できます。 ARIES の詳細については、次のホワイト ペーパーを参照してください。

-   C. Mohan、Don Haderle、Bruce Lindsay、Hamid Pirahesh、Peter の Schwarz *ARIES:粒度の細かいロックをサポートしているトランザクションの回復方法および先行書き込みログ記録を使用して、部分ロールバック*します。

-   C. Mohan、 *ARIES を超える履歴を繰り返し*します。

 

 



