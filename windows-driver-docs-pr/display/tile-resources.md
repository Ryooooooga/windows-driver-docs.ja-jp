---
title: タイルのリソース
description: タイルのリソースに対して十分でないデバイスのページングのキューで実行されている非同期ビデオ メモリ マネージャーのサービス。
ms.assetid: D48D2046-64A6-4B0E-9235-84DD2A83DB39
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b8a663c211d154411e5191072aaf1464ca93f3b1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56559894"
---
# <a name="tile-resources"></a>タイルのリソース


タイルのリソースに対して十分でないデバイスのページングのキューで実行されている非同期ビデオ メモリ マネージャーのサービス。 具体的には、タイル リソースのレンダリングとキューのページ テーブルの更新を描画操作の間で同期的に、更新プログラムが適用されていることを確認します。

たとえば、アプリケーションによって次の API 呼び出しのシーケンスを考えてみます。

1.  描画\#42
2.  タイルのマッピングを更新します。
3.  描画\#43

いることを確認したい*描画\#42*中に古い状態でページのテーブルで実行される*描画\#43*ページ テーブルの新しい状態で実行します。 *タイルのマッピングを更新*no-overwrite フラグを指定する操作の場合は、この同期は、少し緩和されることができますが、高パフォーマンスの同期更新をサポートする必要があります。
高パフォーマンスをサポートするためには、キュー更新、機能を事前にページング操作を生成およびコンテキストをキューに登録して、依存のレンダリング コンテキストが特定の時点に達すると、実行するまで待機する必要があります (例: 描画後\#42 上)。

これは、ページング操作が処理ユニット (GPU) 待機特定のレンダリング コンテキストによって通知されるグラフィックスの背後にあるキューに配置する必要があることを意味します。 このためがキューに入れられません共有システム コンテキストに直接とおりこれは 1 つのアプリケーションがシステムの他の人がページング操作の実行をブロックする可能性があります。

理論上は、今日のパケットに基づくスケジューリング デバイス ページングのキューで待機部分の操作を実装、待機を監視して待機条件が満たされた後に、共有システム コンテキストにページング操作を送信できます。 ただし、を超えて移動パケットはベースのスケジュール設定し、ハードウェアが GPU に GPU を使用できるようにする必要をスケジュール設定に最適なパフォーマンスを確実にインタロックされた操作のプリミティブを同期します。

この問題を解決するには、コンテキストごとのページングのコンパニオン コンテキストの概念を導入しました。 最初の呼び出しでページング コンパニオン コンテキストの遅延作成[ *UpdateGpuVirtualAddress* ](https://msdn.microsoft.com/library/windows/hardware/dn906365)インタロックされた同期が必要なすべてのページ テーブルの更新に使用されます。 *UpdateGpuVirtualAddress*監視 GPU フェンスのオブジェクトと特定のフェンス値をパラメーターとして受け取ります。 この監視対象のフェンスのコンパニオン コンテキスト待機はページのテーブルの更新とし、フェンスの監視対象オブジェクトをインクリメントしを通知します。 これにより、コンパニオン コンテキストと密接に同期するレンダリングのコンテキスト。

コンパニオン コンテキストを使用してページ テーブルの更新は、次に示します。

![インタロックされたページ テーブルの更新](images/tile-resources.1.png)

コンパニオン コンテキストがコンテキストの作成時に、カーネル モード ドライバーによって選択されたエンジンに対して、ビデオ メモリ マネージャーによって作成された遅延 (**DXGKARG\_CREATECONTEXT します。PagingCompanionNodeId**)。

プロセスごとの特権を持つアドレス領域で付属のコンテキストを実行します。 カーネルによって制御される両方と内で実行する、カーネルで生成されたダイレクト メモリ アクセス (DMA) バッファーのみが許可されているために、アドレス空間が特権します。 外部で、これは通常 GPU 仮想アドレス空間であり、特殊なハードウェア仮想アドレス領域の権限のサポートを必要としません。

仮想 GPU アドレスわかりやすくするためのスペースをシステムのページングのプロセスを再利用するのではなく、プロセスごとの特権のある GPU 仮想アドレス空間を選択しました。 割り当てや割り当てのリソースは、一般的なタイルのマップまたはマップ解除するために頻繁にしないようにするアドレス空間で完全にマップされているアプリケーションのページ テーブルを保持する必要があります。 また、ここすぐについて説明しますとすべてのタイル プール自体も永続的な方法でマップする必要があります。 システムのアドレス空間内でこれらの永続的なマッピングを実行が発生し不要な複雑さを増加します。

プロセスごとの特権のある GPU 仮想アドレス空間は、プロセスの GPU のページ テーブルが GPU を使用してさまざまなページ テーブル エントリを更新するコマンドを更新できるので、アドレス空間を表示するように初期化されます。 さらに、すべてのタイルがプロセスによって作成されたプールがアドレス空間にもマップされます。

コンパニオン コンテキストによってページ テーブル エントリを更新する方法は、少し特殊ないくつかを説明する必要があります。 ときに、*マップ*共有システム コンテキストで実行するための操作がキューに置かれた、ビデオ メモリ マネージャーにマップされる物理アドレスを知っているし、これらの物理アドレスが関連付けられているページング バッファーに直接表示されることができます。 [*UpdatePageTable* ](https://msdn.microsoft.com/library/windows/hardware/ff560815)ページング操作がここで使用して、ビデオ メモリ マネージャーは、いくつかの特定のページにページング操作が完了した後、他のいくつかの目的でこれらのページが再利用されることが保証されます。

ただし、コンパニオン コンテキストのページ テーブルの同期更新の処理はより困難です。 更新操作は、構築時に参照されているタイルのプールの物理ページただし、特定のこれらの操作がキューに配置任意の long GPU の背後にあるビデオ メモリ マネージャーが知っている待機 (アプリでしたデッドロックも通知しない)、ビデオ メモリマネージャーは、ページング操作は実行時に、タイルのプールの物理ページがありますが知らないし、ビデオ メモリ マネージャーは任意の時間をその場所でタイルのプールを保持することはできません。

基本的に、ページング操作をキューまたは物理アドレスの変更や遅延更新に使用する実際のアドレスをバインドする必要があります。 後で更新プログラムのいずれかに必要があります、この問題を解決するには、ビデオ メモリ マネージャーは、後者の場合は。

この問題を解決するためには、ビデオ メモリ マネージャーは、次の 2 つが。 最初に、GPU の仮想アドレスは、すべての特権のプロセスのアドレス空間内のプロセスに属するタイル プール要素にマップされます。 タイルのプールがメモリ内で移動すると、ビデオ メモリ マネージャーは自動的には他の割り当ての種類の場合、同じ単純なメカニズムを使用して、タイルのプールの適切な場所を指しているこれらの GPU 仮想アドレスを保持します。

ビデオ メモリ マネージャーを新しい紹介タイル リソースのページ テーブル エントリを更新する**CopyPageTableEntry**タイル リソースの仮想アドレスにタイルのプールの仮想アドレスからのページ テーブル エントリをコピーする操作をページングします。 保持しているため、ビデオ メモリ マネージャー タイル プールの仮想アドレス最新の状態タイルのプールがメモリに移動すると、コピー操作の間の経過時間に関係なく、タイルのプールの有効な現在の物理的な場所で実行することが保証されます。生成されたコマンドとコマンドを実際に実行します。

キューに置かれたページ テーブルの更新が特定のタイルのプールを参照している限り、ビデオ メモリ マネージャーがそのタイルの保持プール ユーザー モード ドライバーまたはアプリケーションの動向を確実に関係なく、アプリケーションの保存場所の要件に注意してください、タイルのプールの仮想アドレスは、更新操作を実行するときに有効です。

このメカニズムは、次に示します。

![ページのテーブル操作をコピーします。](images/tile-resources.2.png)**

## <a name="span-idupdategpuvirtualaddressongpuswithcpuvirtualpagetableupdatemodespanspan-idupdategpuvirtualaddressongpuswithcpuvirtualpagetableupdatemodespanspan-idupdategpuvirtualaddressongpuswithcpuvirtualpagetableupdatemodespan-update-gpu-virtual-address-on-gpus-with-cpuvirtual-page-table-update-mode"></a><span id="_Update_GPU_virtual_address_on_GPUs_with_CPU_VIRTUAL_page_table_update_mode"></span><span id="_update_gpu_virtual_address_on_gpus_with_cpu_virtual_page_table_update_mode"></span><span id="_UPDATE_GPU_VIRTUAL_ADDRESS_ON_GPUS_WITH_CPU_VIRTUAL_PAGE_TABLE_UPDATE_MODE"></span> CPU と Gpu で GPU の仮想アドレスを更新\_仮想ページ テーブルの更新モード


サポートする Gpu、 **DXGK\_PAGETABLEUPDATE\_CPU\_仮想**ページ テーブルの更新モード、 **CopyPageTableEntries**操作は使用されません。 これらの統合は GPU で、ページング バッファーを使用しないでください。 ビデオ メモリ マネージャーは、適切なタイミングと使用まで、更新操作を遅延、 [ *UpdatePageTable* ](https://msdn.microsoft.com/library/windows/hardware/ff560815)セットアップ操作ページのテーブル。

この方法の欠点は、 [ *UpdatePageTable* ](https://msdn.microsoft.com/library/windows/hardware/ff560815)レンダリング操作で並列操作ではありません。 利点は、ドライバーがページング バッファーのサポートを実装および実装する必要がないこと*UpdatePageTable*操作即時として。

 

 




