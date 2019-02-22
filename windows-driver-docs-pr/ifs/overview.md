---
title: 概要
description: 概要
ms.assetid: 3b2895a2-9a2e-46eb-b8fb-47d6db4a1de0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ee729166924cf60c7af642c2891c6e6e7745135d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56531944"
---
# <a name="overview"></a>概要


## <span id="ddk_network_redirector_design_and_performance_if"></span><span id="DDK_NETWORK_REDIRECTOR_DESIGN_AND_PERFORMANCE_IF"></span>


便宜的ロック、または oplock の場合、ファイル サーバー クライアント (など、SMB および SMB2 プロトコルを利用するもの) を許可するメカニズムを提供しますパフォーマンスが向上し、軽減する一貫した方法で動的に指定されたファイルまたはストリームのバッファリングの戦略を変更するには。ネットワークで使用します。 リモートのファイル操作のためのネットワーク パフォーマンスを向上させるクライアントはローカル ネットワーク パケットを送受信する手間を縮小またはファイル データを入れることができます。 たとえば、クライアントをクライアントが他のプロセスが、データにアクセスしないことを知っている情報をリモート サーバー上のファイルに書き込む必要がありますされません。 同様に、クライアントは、クライアントが、他のプロセスがなしデータ ファイルへの書き込みリモートを知っている場合、リモート ファイルからデータを先行読み取りをバッファー可能性があります。 アプリケーションおよびドライバーでは、それらのファイルを使用するのに必要がある他のアプリケーションに影響を与えずにファイルに透過的にアクセスするのにの各 oplock を使用しても。

NTFS のようなファイル システムでは、ファイルごとに複数のデータ ストリームをサポートします。 つまり、操作は、ファイルの場合は、指定した開いているストリームに適用して、一般に、1 つのストリームでの操作には影響しません別のストリームの各 oplock のストリームのハンドルは、上の各 Oplock が付与されます。 この明示的に以下に示す例外があります。 FAT などの代替データ ストリームをサポートしていないファイル システムの場合は、"file"考えるとき、このドキュメントで「ストリーム」を参照。

現在、8 つのさまざまな種類の各 oplock は。

-   A**レベル 2** (または共有) oplock がストリームの複数のリーダーとライターを示します。 これは、読み取りキャッシュ クライアントをサポートします。

-   A**レベル 1** (または排他) oplock がにより、クライアントは排他アクセスのためのストリームを開くし、クライアントは、任意のバッファリングを行うことができます。 これにより、読み取りキャッシュ クライアントをサポートし、書き込みキャッシュします。

-   A**バッチ**oplock (も排他) により、クライアントはクライアント コンピューターでローカルのアクセサーには、ストリームが閉じられている場合でも、ストリームをサーバーで開いたままにします。 これは、クライアントの繰り返しを開くし、バッチ スクリプトの実行中など、同じファイルを閉じる必要がありますのシナリオをサポートします。 このクライアントの読み取りがサポートするキャッシュ、書き込みキャッシュ、およびキャッシュを処理します。

-   A**フィルター** oplock (排他も)、アプリケーションおよびファイル システム フィルター (ミニフィルターを含む) を開き、読み取り、ストリーム データをバックアップする方法""その他のアプリケーション、クライアント、またはその両方が同じストリームにアクセスしようとします。 これにより、読み取りキャッシュ クライアントをサポートし、書き込みキャッシュします。

-   A**読み取り**がストリームの複数のリーダーとライター (共有) (R) oplock を示します。 これは、読み取りキャッシュ クライアントをサポートします。

-   A**読み取りハンドル**(共有) (RH) oplock は、ライターのストリームの複数のリーダーがあり、ストリームが閉じられたことクライアントできますストリームを開いたまま、サーバーの場合でもクライアント コンピューターでローカルのアクセサーことを示します。 これにより、読み取りキャッシュ クライアントをサポートし、キャッシュを処理します。

-   A**読み取り/書き込み**(RW) oplock (排他) により、クライアントは排他アクセスのためのストリームを開くし、クライアントは、任意のバッファリングを行うことができます。 これにより、読み取りキャッシュ クライアントをサポートし、書き込みキャッシュします。

-   A**読み取り-書き込みハンドル**(RWH) oplock (排他) により、クライアントはクライアント コンピューターでローカルのアクセサーには、ストリームが閉じられている場合でも、ストリームをサーバーで開いたままにします。 このクライアントの読み取りがサポートするキャッシュ、書き込みキャッシュ、およびキャッシュを処理します。

Windows NT 3.1 では、レベル 1、レベル 2、およびバッチの各 oplock が実装されました。 Windows 2000 では、フィルター oplock が追加されました。 Windows 7 では、R、RH、RW、および RWH oplock が追加されました。

いくつかの各 oplock 見えるとよく似ています。 具体的には、R がレベル 2 のような RW ようレベル 1 のようなおよび RWH ようバッチに似ています。 キャッシュの意図を表現して、oplock の区切りとアップグレードできるようにするには、呼び出し元の柔軟性を提供する Windows 7 に R、RH、RW、および RWH oplock が (以下総称として"Windows 7 の各 oplock") が追加されました (の変更は、大きいキャッシュのレベルに 1 つのレベルから oplock の状態たとえば、読み取り oplock にアップグレードする読み取り/書き込み oplock) (以下総称として"レガシ oplock")、レベル 2、レベル 1、バッチ、およびフィルターの各 oplock でこのような柔軟性を実現することはありません。 Windows 7 の各 oplock と従来の oplock の違いは、このドキュメントの後半で説明します。

カーネルの oplock のパッケージのコア機能が実装されている (主にを通じて*FsRtlXxx*ルーチン)。 ファイル システムは、自身のファイル システムに oplock 機能を実装するには、このパッケージを呼び出します。 このドキュメントでは、NTFS ファイル システムがカーネル oplock のパッケージと相互運用する方法について説明します。 他のファイル システムは、若干の違いがある可能性がありますが、同様の方法で機能します。

各 Oplock がストリームのハンドルに付与されます。 つまり、ストリームの特定のオープンの oplock が与えられています。 Windows 7 以降では、ストリームのハンドルを関連付ける、 *oplock キー*、つまりに属している複数のハンドルを識別するために使用される GUID 値と同じクライアントのキャッシュを表示 (このトピックの注を参照してください)。 Oplock のキーを明示的に指定することができます (に[ **IoCreateFileEx**](https://msdn.microsoft.com/library/windows/hardware/ff548283)) ハンドルが作成されたとき。 Oplock のキーを指定しない場合は明示的にハンドルが作成されたときに、システムはその他のいずれかのハンドルの他の任意のキーとそのキーは異なるように、それに関連付けられている一意の oplock のキーを持つものとしてハンドルを扱います。 Oplock が許可されたもの以外のハンドルでファイルの操作を受信したと操作のハンドルに関連付けられているキーから oplock のハンドルに関連付けられている oplock キーとは異なる、その操作と互換性がない場合、現在 oplock を与え、し、その oplock は解除されます。 プロセスまたは互換性のない操作を実行するスレッドが同じである場合でも、oplock が解除されます。 プロセスは排他 oplock が付与されますストリームを開き、同じプロセスで同じストリームをもう一度表示し、別の (またはなし) の使用など、oplock キー排他 oplock が壊れているすぐにします。

Oplock のキーが、ハンドルの上に存在「れたりする」、ハンドル、ハンドルが作成されることに注意してください。 各 oplock が付与されていない場合でも、oplock のキーを持つハンドルを関連付けることができます。

**注**  がより正確に言えば、oplock のキーに関連付けられていること、 [**ファイル\_オブジェクト**](https://msdn.microsoft.com/library/windows/hardware/ff545834)ストリームのハンドルを表す構造体。 など、ハンドルが重複している場合は、この区別が重要で[DuplicateHandle](https://go.microsoft.com/fwlink/p/?linkid=124237)します。 それぞれの重複するハンドルを同じ基になる指す**ファイル\_オブジェクト**構造体。

 

 

 



