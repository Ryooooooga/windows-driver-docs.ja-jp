---
title: ECPs を使用して、ファイル システム フィルター ドライバーで irp_mj_create 用を処理するには
description: ECPs irp_mj_create 用の操作を処理を使用して、ファイル システム フィルター ドライバー
ms.assetid: 969709a9-cdca-4a1a-95a0-0bb89cd17693
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a05d82d4e6ba4e5fe1be8c36973ca95bb7fe034c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532421"
---
# <a name="using-ecps-to-process-irpmjcreate-operations-in-a-file-system-filter-driver"></a>ECPs を使用して、IRP を処理する\_MJ\_作成操作、ファイル システム フィルター ドライバー


処理には、ファイル システム フィルター ドライバー ECPs を使用する[ **IRP\_MJ\_作成**](https://msdn.microsoft.com/library/windows/hardware/ff548630)操作。 ファイル システム フィルター ドライバーは、取得、確認、追加、およびの ECPs を削除するには、次のセクションで、ルーチンを呼び出すことができます、 **IRP\_MJ\_作成**操作。 ECPs が元のオペレーティング システムの領域を指定することもできます。

### <a name="span-idretrievingecpsspanspan-idretrievingecpsspanspan-idretrievingecpsspanretrieving-ecps"></a><span id="Retrieving_ECPs"></span><span id="retrieving_ecps"></span><span id="RETRIEVING_ECPS"></span>ECPs を取得します。

ファイル システム フィルター ドライバー次の手順の ECPs を取得する、 [ **IRP\_MJ\_作成**](https://msdn.microsoft.com/library/windows/hardware/ff548630)操作。

1.  呼び出す、 [ **FltGetEcpListFromCallbackData** ](https://msdn.microsoft.com/library/windows/hardware/ff543016)または[ **FsRtlGetEcpListFromIrp** ](https://msdn.microsoft.com/library/windows/hardware/ff546015)ルーチン、ECP コンテキストへのポインターを取得するには構造体のリスト (ECP\_リスト) を作成する操作に関連付けられています。

2.  次の操作のいずれかを実行します。
    -   呼び出す、 [ **FltGetNextExtraCreateParameter** ](https://msdn.microsoft.com/library/windows/hardware/ff543104)または[ **FsRtlGetNextExtraCreateParameter** ](https://msdn.microsoft.com/library/windows/hardware/ff546028)ルーチンへのポインターを取得します[次へ] (または最初) ECP コンテキスト構造 ECP 一覧。
    -   呼び出す、 [ **FltFindExtraCreateParameter** ](https://msdn.microsoft.com/library/windows/hardware/ff542094)または[ **FsRtlFindExtraCreateParameter** ](https://msdn.microsoft.com/library/windows/hardware/ff545968) ECP ECP 一覧を検索するルーチン指定された型のコンテキストの構造体。 いずれかのルーチンでは、構造が見つかった場合に、ECP context 構造体にポインターを返します。

### <a name="span-idsettingecpsspanspan-idsettingecpsspanspan-idsettingecpsspansetting-ecps"></a><span id="Setting_ECPs"></span><span id="setting_ecps"></span><span id="SETTING_ECPS"></span>ECPs の設定

ECPs を設定する、 [ **IRP\_MJ\_作成**](https://msdn.microsoft.com/library/windows/hardware/ff548630)操作、ファイル システム フィルター ドライバーはまず既存の ECP コンテキスト構造の一覧を取得しますか (ECP\_一覧表示する) は、作成操作に関連付けられている、または ECP を割り当てる\_一覧と、ECP コンテキスト構造体し、ECP ECP context 構造体に挿入\_一覧。

ファイル システム フィルター ドライバー次の手順で既存の ECP ECPs を設定する\_一覧作成操作に関連付けられています。

1.  呼び出す、 [ **FltGetEcpListFromCallbackData** ](https://msdn.microsoft.com/library/windows/hardware/ff543016)または[ **FsRtlGetEcpListFromIrp** ](https://msdn.microsoft.com/library/windows/hardware/ff546015)ルーチン、ECP コンテキストへのポインターを取得するには構造体のリスト (ECP\_リスト) を作成する操作に関連付けられています。

2.  呼び出す、 [ **FltAllocateExtraCreateParameter** ](https://msdn.microsoft.com/library/windows/hardware/ff541728)または[ **FsRtlAllocateExtraCreateParameter** ](https://msdn.microsoft.com/library/windows/hardware/ff545609)ページングされたメモリ割り当てルーチンプール ECP コンテキストの構造体と構造体へのポインターを生成します。

3.  呼び出す、 [ **FltInsertExtraCreateParameter** ](https://msdn.microsoft.com/library/windows/hardware/ff543305)または[ **FsRtlInsertExtraCreateParameter** ](https://msdn.microsoft.com/library/windows/hardware/ff546179) ECP context 構造体を挿入するルーチン[ECP\_一覧](https://msdn.microsoft.com/library/windows/hardware/ff540148)構造体。

ファイル システム フィルター ドライバー次の手順では、新しく作成された ECP ECPs を設定する\_一覧作成操作に関連付けられています。

1.  呼び出す、 [ **FltAllocateExtraCreateParameterList** ](https://msdn.microsoft.com/library/windows/hardware/ff541741)または[ **FsRtlAllocateExtraCreateParameterList** ](https://msdn.microsoft.com/library/windows/hardware/ff545632)メモリ割り当てルーチン[ECP\_一覧](https://msdn.microsoft.com/library/windows/hardware/ff540148)構造体。

2.  呼び出す、 [ **FltAllocateExtraCreateParameter** ](https://msdn.microsoft.com/library/windows/hardware/ff541728)または[ **FsRtlAllocateExtraCreateParameter** ](https://msdn.microsoft.com/library/windows/hardware/ff545609)ページングされたメモリ割り当てルーチンプール ECP コンテキストの構造体と構造体へのポインターを生成します。

3.  呼び出す、 [ **FltInsertExtraCreateParameter** ](https://msdn.microsoft.com/library/windows/hardware/ff543305)または[ **FsRtlInsertExtraCreateParameter** ](https://msdn.microsoft.com/library/windows/hardware/ff546179) ECP context 構造体を挿入するルーチン[ECP\_一覧](https://msdn.microsoft.com/library/windows/hardware/ff540148)構造体。

4.  呼び出す、 [ **FltSetEcpListIntoCallbackData** ](https://msdn.microsoft.com/library/windows/hardware/ff544510)または[ **FsRtlSetEcpListIntoIrp** ](https://msdn.microsoft.com/library/windows/hardware/ff547250)ルーチンを作成する操作に、ECP リストをアタッチするには.

### <a name="span-idremovingecpsspanspan-idremovingecpsspanspan-idremovingecpsspanremoving-ecps"></a><span id="Removing_ECPs"></span><span id="removing_ecps"></span><span id="REMOVING_ECPS"></span>ECPs を削除します。

ファイル システム フィルター ドライバー次の手順の ECPs を削除する、 [ **IRP\_MJ\_作成**](https://msdn.microsoft.com/library/windows/hardware/ff548630)操作。

1.  呼び出す、 [ **FltRemoveExtraCreateParameter** ](https://msdn.microsoft.com/library/windows/hardware/ff544339)または[ **FsRtlRemoveExtraCreateParameter** ](https://msdn.microsoft.com/library/windows/hardware/ff547203) ECP ECP リストを検索するルーチンコンテキストの構造体。 ECP context 構造体が見つかった場合、ルーチンは、ECP リストから ECP context 構造体をデタッチします。

2.  デタッチの ECP 構造体のメモリを解放する呼び出し、 [ **FltFreeExtraCreateParameter** ](https://msdn.microsoft.com/library/windows/hardware/ff542957)または[ **FsRtlFreeExtraCreateParameter** ](https://msdn.microsoft.com/library/windows/hardware/ff545989)ルーチン。 次の方法のいずれかでメモリを割り当てている場合に、ECP の構造体のメモリを解放するこれらのルーチンを呼び出すことができます。
    -   呼び出す、 [ **FltAllocateExtraCreateParameter** ](https://msdn.microsoft.com/library/windows/hardware/ff541728)または[ **FsRtlAllocateExtraCreateParameter** ](https://msdn.microsoft.com/library/windows/hardware/ff545609)割り当てルーチンのページングメモリ プール
    -   呼び出す、 [ **FltAllocateExtraCreateParameterFromLookasideList** ](https://msdn.microsoft.com/library/windows/hardware/ff541734)または[ **FsRtlAllocateExtraCreateParameterFromLookasideList** ](https://msdn.microsoft.com/library/windows/hardware/ff545616)ルック アサイド リストからメモリ プールの割り当てルーチン

### <a name="span-idmarkingecpsasacknowledgedordeterminingacknowledgestatusspanspan-idmarkingecpsasacknowledgedordeterminingacknowledgestatusspanspan-idmarkingecpsasacknowledgedordeterminingacknowledgestatusspanmarking-ecps-as-acknowledged-or-determining-acknowledge-status"></a><span id="Marking_ECPs_as_Acknowledged__or_Determining_Acknowledge_Status"></span><span id="marking_ecps_as_acknowledged__or_determining_acknowledge_status"></span><span id="MARKING_ECPS_AS_ACKNOWLEDGED__OR_DETERMINING_ACKNOWLEDGE_STATUS"></span>ECPs のマークを受信確認または決定する状態を確認します。

ファイル システム フィルター ドライバーには、確認として、ECPs をマークまたは受信確認として、ECPs がマークされているかどうか判断には、次のルーチンを呼び出すことができます。

-   呼び出す、 [ **FltAcknowledgeEcp** ](https://msdn.microsoft.com/library/windows/hardware/ff541661)または[ **FsRtlAcknowledgeEcp** ](https://msdn.microsoft.com/library/windows/hardware/ff545574)ルーチンを ECP コンテキストの構造体のマーク付けを確認します。 ECP に使用される、処理、またはその他の条件で説明したように、ECP をマークできます。

-   呼び出す、 [ **FltIsEcpAcknowledged** ](https://msdn.microsoft.com/library/windows/hardware/ff543321)または[ **FsRtlIsEcpAcknowledged** ](https://msdn.microsoft.com/library/windows/hardware/ff546808) ECP コンテキストの構造体がかどうかを判断するルーチン確認済みとしてマークされます。

### <a name="span-iddeterminingoriginationmodespanspan-iddeterminingoriginationmodespanspan-iddeterminingoriginationmodespandetermining-origination-mode"></a><span id="Determining_Origination_Mode"></span><span id="determining_origination_mode"></span><span id="DETERMINING_ORIGINATION_MODE"></span>発信元のモードの決定

ファイル システム フィルター ドライバーを呼び出すことができます、 [ **FltIsEcpFromUserMode** ](https://msdn.microsoft.com/library/windows/hardware/ff543325)または[ **FsRtlIsEcpFromUserMode** ](https://msdn.microsoft.com/library/windows/hardware/ff546813)ルーチンを決定するにはかどうか、ECP context 構造は、ユーザー モードから開始されます。 ファイル システム フィルター ドライバーは、ユーザー モードで発生した ECP context 構造に同意を拒否できます。

### <a name="span-idusinglookasideliststoallocateecpsspanspan-idusinglookasideliststoallocateecpsspanspan-idusinglookasideliststoallocateecpsspanusing-lookaside-lists-to-allocate-ecps"></a><span id="Using_Lookaside_Lists_to_Allocate_ECPs"></span><span id="using_lookaside_lists_to_allocate_ecps"></span><span id="USING_LOOKASIDE_LISTS_TO_ALLOCATE_ECPS"></span>リストを割り当てる ECPs ルック アサイドを使用しました。

ファイル システム フィルター ドライバーは、ルック アサイド リストから ECPs を割り当てると、ルック アサイド リストおよび ECPs 管理には、次のルーチンを呼び出すことができます。

-   呼び出す、 [ **FltInitExtraCreateParameterLookasideList** ](https://msdn.microsoft.com/library/windows/hardware/ff543261)または[ **FsRtlInitExtraCreateParameterLookasideList** ](https://msdn.microsoft.com/library/windows/hardware/ff546102)ルーチンを固定サイズの 1 つまたは複数の ECP コンテキスト構造の割り当てに使用されるページまたは非ページ プール ルック アサイド リストを初期化します。

-   呼び出す、 [ **FltDeleteExtraCreateParameterLookasideList** ](https://msdn.microsoft.com/library/windows/hardware/ff541973)または[ **FsRtlDeleteExtraCreateParameterLookasideList** ](https://msdn.microsoft.com/library/windows/hardware/ff545849)ルーチンをルック アサイド リストを解放します。

-   呼び出す、 [ **FltAllocateExtraCreateParameterFromLookasideList** ](https://msdn.microsoft.com/library/windows/hardware/ff541734)または[ **FsRtlAllocateExtraCreateParameterFromLookasideList** ](https://msdn.microsoft.com/library/windows/hardware/ff545616)ルーチン ECP の構造体のルック アサイド リストからメモリ プールの割り当てと構造体へのポインターを生成します。

-   呼び出す、 [ **FltFreeExtraCreateParameter** ](https://msdn.microsoft.com/library/windows/hardware/ff542957)または[ **FsRtlFreeExtraCreateParameter** ](https://msdn.microsoft.com/library/windows/hardware/ff545989) ECP コンテキストのメモリを解放するルーチン構造体。

 

 



