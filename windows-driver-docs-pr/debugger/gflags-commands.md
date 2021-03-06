---
title: GFlags コマンド
description: GFlags を使用するには、コマンドラインで次のコマンドを入力します。 [GFlags コマンド] ダイアログボックスと [グローバルフラグ] ダイアログボックスは、同じように使用できます。
ms.assetid: 832b7269-623a-4f32-8bda-1059087bab09
keywords:
- GFlags コマンドウィンドウのデバッグ
ms.date: 06/12/2018
topic_type:
- apiref
api_name:
- GFlags Commands
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 5f0ee7c2b587a2f6c26c4983d9dea27a07558237
ms.sourcegitcommit: e6b3dd2a67618e84116ca91393336b34353d9e5a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/21/2019
ms.locfileid: "72680677"
---
# <a name="gflags-command-overview"></a>GFlags コマンドの概要

Msbuild.exe をインストールおよび検索する方法に関する一般的な情報については、「 [gflags](gflags.md)」を参照してください。

[GFlags コマンド[] ダイアログボックスと [グローバルフラグ] ダイアログボックス](global-flags-dialog-box.md)は、同じように使用できます。

## <a name="gflags-command-usage"></a>GFlags コマンドの使用法 

GFlags を使用するには、コマンドラインで次のコマンドを入力します。


[GFlags] ダイアログボックスを開くには、次のようにします。

```console
gflags
```

レジストリのグローバルフラグを設定またはクリアするには、次のようにします。

```console
gflags /r [{+ | -}Flag [{+ | -}Flag...]]
```

現在のセッションのグローバルフラグを設定またはクリアするには、次のようにします。

```console
gflags /k [{+ | -}Flag [{+ | -}Flag...]]
```

イメージファイルのグローバルフラグを設定またはクリアするには、次のようにします。

```console
gflags /i ImageFile [{+ | -}Flag [{+ | -}Flag...]]
gflags /i ImageFile /tracedb SizeInMB
```

特別なプール機能を設定またはクリアするには (Windows Vista 以降)

```console
gflags {/r | /k} {+ | -}spp {PoolTag | 0xSize}
```

オブジェクト参照のトレース機能を有効または無効にするには (Windows Vista 以降)

```console
gflags {/ro | /ko} [/p] [/i ImageFile | /t PoolTag;[PoolTag...]]
```

```console
gflags {/ro | /ko} /d
```

ページヒープの検証を有効にして構成するには

```console
gflags /p /enable ImageFile  [ /full [/backwards] | /random Probability | /size SizeStart SizeEnd | /address AddressStart AddressEnd | /dlls DLL [DLL...] ] 
[/debug ["DebuggerCommand"] | /kdebug] [/unaligned] [/notraces] [/fault Rate [TimeOut]] [/leaks] [/protect] [/no_sync] [/no_lock_checks] 
```

ページヒープの検証を無効にするには:

```console
gflags /p [/disable ImageFile] [/?]
```

ヘルプを表示するには:

```console
gflags /?
```

## <a name="span-idddk_gflags_commands_dtoolsspanspan-idddk_gflags_commands_dtoolsspanparameters"></a><span id="ddk_gflags_commands_dtools"></span><span id="DDK_GFLAGS_COMMANDS_DTOOLS"></span>パラメータ


<span id="_______Flag______"></span><span id="_______flag______"></span><span id="_______FLAG______"></span>*フラグ*   
デバッグ機能を表す3文字の省略形 (*FlagAbbr*) または16進値 (*flaghex*) を指定します。 省略形と16進値は、 [GFlags フラグテーブル](gflags-flag-table.md)に一覧表示されます。

次のいずれかのフラグ形式を使用します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">表記</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>{<strong> +</strong> | <strong> -</strong>}<em>FlagAbbr</em></p></td>
<td align="left"><p>フラグの省略形で表されるフラグを設定 (+) またはクリア (-) します。 正符号 (+) またはマイナス記号 (-) が指定されていない場合、コマンドは無効です。</p></td>
</tr>
<tr class="even">
<td align="left"><p>[<strong> +</strong> | <strong> -</strong>]<em>Flaghex</em></p></td>
<td align="left"><p>フラグの16進数値を加算 (+) または減算 (-) します。 値が合計に含まれる場合は、フラグが設定されます。 Add (+) が既定値です。 1つのフラグを表す16進値 (0x なし) を入力するか、複数のフラグの16進値の合計を入力します。</p></td>
</tr>
</tbody>
</table>

 

<span id="_______ImageFile______"></span><span id="_______imagefile______"></span><span id="_______IMAGEFILE______"></span>*イメージ*の   
ファイル名拡張子 (notepad.exe、mydll.dll など) を含む実行可能ファイルの名前を指定します。

<span id="________r______"></span><span id="________R______"></span> **/r**   
登録. レジストリに格納されているシステム全体のデバッグフラグを表示または変更します。 これらの設定は、Windows を再起動すると有効になり、変更するまで有効のままになります。

追加のパラメーターを使用しない場合、 **gflags/r**はレジストリに設定されているシステム全体のフラグを表示します。

<span id="________k______"></span><span id="________K______"></span> **/k**   
カーネルフラグの設定。 このセッションのシステム全体のデバッグフラグを表示または変更します。 これらの設定は直ちに有効になりますが、Windows がシャットダウンすると失われます。 設定は、このコマンドの完了後に開始されたプロセスに影響します。

追加のパラメーターを使用しない場合、 **gflags/k**は、現在のセッションに対して設定されたシステム全体のフラグを表示します。

<span id="________i______"></span><span id="________I______"></span> **/i**   
イメージファイルの設定。 特定のプロセスのデバッグフラグを表示または変更します。 これらの設定はレジストリに格納されます。 これらは、このプロセスのすべての新しいインスタンスに対して有効であり、変更するまで有効なままです。

追加のパラメーターを指定しない場合、 **gflags/i**の*イメージ*は、指定されたプロセスに設定されているフラグを表示します。

<span id="________tracedb_______SizeInMB______"></span><span id="________tracedb_______sizeinmb______"></span><span id="________TRACEDB_______SIZEINMB______"></span> **/tracedb** *sizeinmb*   
プロセスのユーザーモードスタックトレースデータベースの最大サイズを設定します。 このパラメーターを使用するには、プロセスに対して[Create user mode stack trace database](create-user-mode-stack-trace-database.md) (ust) フラグを設定する必要があります。

*Sizeinmb*は、10進数単位のメガバイト数を表す整数です。 既定値は、最小サイズである 8 MB です。最大サイズはありません。 既定のサイズに戻すには、 *Sizeinmb*を0に設定します。

<span id="_______spp______"></span><span id="_______SPP______"></span>**spp**   
(Windows Vista 以降)。[特別なプール](special-pool.md)機能を設定または解除します。 例については、「[例 14: 特別なプールの構成](example-14---configuring-special-pool.md)」を参照してください。

<span id="_______PoolTag______"></span><span id="_______pooltag______"></span><span id="_______POOLTAG______"></span>*Pooltag*   
(Windows Vista 以降)。[特別なプール](special-pool.md)機能のプールタグを指定します。 **Spp**フラグを使用する場合にのみ使用します。

*Pooltag*に4文字のパターン (Tag1 など) を入力します。 これ**には**、 (任意の1文字の代替) と **\*** (複数の文字の代わり) ワイルドカード文字。 たとえば、Fat\* または Av? 4 のようになります。 プールタグでは、常に大文字と小文字が区別されます。

<span id="0xSize______"></span><span id="0xsize______"></span><span id="0XSIZE______"></span>**0x ** * * サイズ   
(Windows Vista 以降)。特別なプール機能のサイズの範囲を指定します。 **Spp**フラグを使用する場合にのみ使用します。 サイズ値の選択に関するガイダンスについては、「[特殊なプール](special-pool.md)での割り当てサイズの選択」を参照してください。

<span id="________ro______"></span><span id="________RO______"></span> **/ro**   
[オブジェクト参照のトレース](object-reference-tracing.md)設定をレジストリに有効または無効にし、表示します。 この設定を有効に変更するには、Windows を再起動する必要があります。

追加のパラメーターを指定しない場合、 **/ro**ではオブジェクト参照のトレース設定がレジストリに表示されます。

オブジェクト参照のトレースを有効にするには、コマンドに少なくとも1つのプールタグ ( **/T** *pooltag*) または1つのイメージファイル ( **/i**イメージファイル) を含める必要があります。 詳細については、「[例 15: オブジェクト参照トレースの使用](example-15--using-object-reference-tracing.md)」を参照してください。

次の表に、 **/ro**で有効なサブパラメーターの一覧を示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>/T</strong> <em>pooltags</em></p></td>
<td align="left"><p>指定されたプールタグを持つオブジェクトにトレースを制限します。 タグ名を区切るには、セミコロン (<strong>;</strong>) を使用します。 最大16個のプールタグを入力します。</p>
<p><em>Pooltags</em>の4文字のパターン (Tag1 など) を入力します。</p>
<p>複数のプールタグを指定した場合、Windows は指定されたプールタグのいずれかを使用してオブジェクトをトレースします。</p>
<p>プールタグを指定しない場合、Windows では、イメージによって作成されたすべてのオブジェクトがトレースされます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>/i</strong> <em>ImageFile</em></p></td>
<td align="left"><p>指定されたイメージファイルを持つプロセスによって作成されたオブジェクトにトレースを制限します。 指定できるイメージファイルは、 <strong>/i</strong>パラメーターで1つだけです。</p>
<p>メモ帳などのイメージファイル名を64文字以内で入力します。 "System" と "Idle" は有効なイメージ名ではありません。</p>
<p>イメージファイルを指定しない場合、Windows は指定されたプールタグを持つすべてのオブジェクトをトレースします。 イメージファイル (<strong>/i</strong>) と1つ以上のプールタグ (<strong>/t</strong>) の両方を指定した場合、Windows は、指定されたイメージによって作成される指定されたプールタグのいずれかを使用してオブジェクトをトレースします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>d</strong></p></td>
<td align="left"><p>オブジェクト参照トレース機能の設定を消去します。 <strong>/Ro</strong>と共に使用すると、レジストリの設定がクリアされます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>/p</strong></p></td>
<td align="left"><p>無期限. トレースデータは、オブジェクト参照のトレースが無効になるか、コンピューターがシャットダウンまたは再起動されるまで保持されます。 既定では、オブジェクトのトレースデータは、オブジェクトが破棄されると破棄されます。</p></td>
</tr>
</tbody>
</table>

 

<span id="________ko______"></span><span id="________KO______"></span> **/ko**   
カーネルフラグ (実行時)[オブジェクト参照のトレース](object-reference-tracing.md)設定を有効にし、無効にして、表示します。 この設定に対する変更はすぐに有効になりますが、システムをシャットダウンまたは再起動すると失われます。 詳細については、「[例 15: オブジェクト参照トレースの使用](example-15--using-object-reference-tracing.md)」を参照してください。

追加のパラメーターを指定しない場合、 **/ko**では、カーネルフラグ (実行時) のオブジェクト参照のトレース設定が表示されます。

オブジェクト参照のトレースを有効にするには、コマンドに少なくとも1つのプールタグ ( **/T** *pooltag*) または1つのイメージファイル ( **/i** *イメージファイル) を*含める必要があります。

次の表に、 **/ko**で有効なサブパラメーターの一覧を示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>/T</strong> <em>pooltags</em></p></td>
<td align="left"><p>指定されたプールタグを持つオブジェクトにトレースを制限します。 タグ名を区切るには、セミコロン (<strong>;</strong>) を使用します。 最大16個のプールタグを入力します。</p>
<p><em>Pooltags</em>の4文字のパターン (Tag1 など) を入力します。</p>
<p>複数のプールタグを指定した場合、Windows は指定されたプールタグのいずれかを使用してオブジェクトをトレースします。</p>
<p>プールタグを指定しない場合、Windows では、イメージによって作成されたすべてのオブジェクトがトレースされます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>/i</strong> <em>ImageFile</em></p></td>
<td align="left"><p>指定されたイメージファイルを持つプロセスによって作成されたオブジェクトにトレースを制限します。 指定できるイメージファイルは、 <strong>/i</strong>パラメーターで1つだけです。</p>
<p>イメージファイルを指定しない場合、Windows は指定されたプールタグを持つすべてのオブジェクトをトレースします。</p>
<p>イメージファイル (<strong>/i</strong>) と1つ以上のプールタグ (<strong>/t</strong>) の両方を指定した場合、Windows は、指定されたイメージによって作成される指定されたプールタグのいずれかを使用してオブジェクトをトレースします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>d</strong></p></td>
<td align="left"><p>オブジェクト参照トレース機能の設定を消去します。 <strong>/Ro</strong>と共に使用すると、レジストリの設定がクリアされます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>/p</strong></p></td>
<td align="left"><p>無期限. トレースデータは、オブジェクト参照のトレースが無効になるか、コンピューターがシャットダウンまたは再起動されるまで保持されます。 既定では、オブジェクトのトレースデータは、オブジェクトが破棄されると破棄されます。</p></td>
</tr>
</tbody>
</table>

 

<span id="________p______"></span><span id="________P______"></span> **/p**   
プロセスのページヒープ検証オプションを設定します。

追加のパラメーターを指定しない場合、 **gflags/p**はページヒープ検証が有効になっているイメージファイルの一覧を表示します。

ページヒープ検証では、操作の割り当てや操作の解放など、動的なヒープメモリ操作が監視され、ヒープエラーが検出されるとデバッガーが中断します。

<span id="________disable_______ImageFile______"></span><span id="________disable_______imagefile______"></span><span id="________DISABLE_______IMAGEFILE______"></span> **/disable** *ImageFile*   
指定されたイメージファイルのページヒープの確認 (標準または完全) をオフにします。

このコマンドは、プロセスの [ページヒープ (hpa)[を有効に](enable-page-heap.md)する] フラグをオフにすることに相当します (**gflags/i** *イメージ*は**hpa**)。 コマンドは、同じように使用できます。

<span id="________enable_______ImageFile______"></span><span id="________enable_______imagefile______"></span><span id="________ENABLE_______IMAGEFILE______"></span> **/Enable** *イメージ*   
指定されたイメージファイルのページヒープ検証をオンにします。

既定では、 **/enable**パラメーターは、イメージファイルの*標準*ページヒープ検証をオンにします。 イメージファイルのページヒープの*完全な*検証を有効にするには、コマンド**に [ファイル] パラメーターを**追加するか、または **/i**パラメーターを **+ hpa**フラグと共に使用します。

<span id="________full______"></span><span id="________FULL______"></span>/ **/ **  
プロセスのページヒープの完全な検証をオンにします。 ページヒープの完全な検証では、各割り当ての最後に予約済みの仮想メモリのゾーンが配置されます。

このパラメーターを使用することは、プロセスの[ページヒープ](enable-page-heap.md)(hpa) フラグを有効にすることに相当します (**Gflags/i** *イメージ*化 **+ hpa**)。 コマンドは、同じように使用できます。

<span id="________backwards______"></span><span id="________BACKWARDS______"></span> **/後方**   
予約された仮想メモリのゾーンを、末尾ではなく、割り当ての先頭に配置します。 その結果、デバッガーはバッファーの末尾ではなく、バッファーの先頭にあるオーバーランをトラップします。 **の場合**にのみ有効です。

<span id="________random_______Probability______"></span><span id="________random_______probability______"></span><span id="________RANDOM_______PROBABILITY______"></span> **/ランダム***確率*   
指定された確率に基づいて、割り当てごとに完全または標準のページヒープ検証を選択します。

*確率*は、完全なページヒープ検証の確率を表す 0 ~ 100 の10進整数です。 100の確率**は、の**使用と同じです。 0の確率は、標準のページヒープ検証を使用する場合と同じです。

<span id="________size________SizeStart_SizeEnd______"></span><span id="________size________sizestart_sizeend______"></span><span id="________SIZE________SIZESTART_SIZEEND______"></span> **/Size** *Sizestart sizestart*   
指定されたサイズ範囲内の割り当てに対してページヒープの完全な検証を有効にし、プロセスによる他のすべての割り当てに対して標準のページヒープ検証を有効にします。

*Sizestart*と*sizestart*は10進数の整数です。 既定では、すべての割り当てに対して標準のページヒープ検証が使用されます。

<span id="________address________AddressStart_AddressEnd______"></span><span id="________address________addressstart_addressend______"></span><span id="________ADDRESS________ADDRESSSTART_ADDRESSEND______"></span> **/Address** *Addressstart addressend*   
指定されたアドレス範囲のリターンアドレスがランタイムコールスタック上にあるときに、割り当てられたメモリのページヒープの完全な検証を有効にします。 これにより、プロセスによる他のすべての割り当てに対して、標準のページヒープ検証が有効になります。

この機能を使用するには、問題があると思われる割り当てを使用して関数を呼び出すすべての関数のアドレスを含む範囲を指定します。 呼び出し元関数のアドレスは、問題のある割り当てが発生したときに呼び出し履歴に表示されます。

*Addressstart*と*addressend*は、割り当て履歴トレースで検索されるアドレス範囲を指定します。 アドレスは16進形式で指定します (例、0xAABBCCDD)。

Windows Server 2003 以前のシステムでは、 **/address**パラメーターは*x*86 ベースのコンピューターでのみ有効です。 Windows Vista の場合: サポートされているすべてのアーキテクチャで有効です。

<span id="________dlls_DLL___DLL...__"></span><span id="________dlls_dll___dll...__"></span><span id="________DLLS_DLL___DLL...__"></span> **/** dll *dll*\[ **、** *dll*...\]   
指定された Dll によって要求された割り当てのページヒープの完全な検証と、プロセスによる他のすべての割り当ての標準ページヒープ検証を有効にします。

*DLL*ファイル名拡張子を含むバイナリファイルの名前を指定します。 指定されたファイルは、実行中にプロセスが読み込まれる関数ライブラリである必要があります。

<span id="________debug______"></span><span id="________DEBUG______"></span> **/debug**   
は、デバッガーで、 **/enable**パラメーターによって指定されたプロセスを自動的に起動します。

既定では、このパラメーターは、コマンドラインの ntsd-g- **x**とページヒープが有効になっている ntsd デバッガーを使用しますが、debugger*コマンド*変数を使用して、別のデバッガーとコマンドラインを指定することもできます。

NTSD の詳細については、「 [CDB と Ntsd を使用](debugging-using-cdb-and-ntsd.md)したデバッグ」を参照してください。

このオプションは、コマンドプロンプトから起動するのが困難なプログラムや、他のプロセスによって起動されるプログラムに役立ちます。

<span id="_DebuggerCommand_______"></span><span id="_debuggercommand_______"></span><span id="_DEBUGGERCOMMAND_______"></span> **"** <em>デバッガーコマンド</em> **"**    
デバッガーと、デバッガーに送信されるコマンドを指定します。 この引用符で囲まれた文字列には、デバッガーへの完全修飾パス、デバッガー名、およびデバッガーによって解釈されるコマンドパラメーターを含めることができます。 引用符が必要です。

コマンドにデバッガーへのパスが含まれている場合、パスに他の引用符を含めることはできません。 他の引用符が表示される場合は、コマンドシェル (*cmd.exe*) によってコマンドが誤って解釈されます。

<span id="________kdebug______"></span><span id="________KDEBUG______"></span> **/kdebug**   
は、ntsd デバッガー**で、コマンド**ラインを使用して指定されたプロセスを自動的に起動します。**また、ページ**ヒープが有効になっており、カーネルデバッガーに対する ntsd の制御が有効になっています。

NTSD の詳細については、「 [CDB と Ntsd を使用](debugging-using-cdb-and-ntsd.md)したデバッグ」を参照してください。

<span id="________unaligned______"></span><span id="________UNALIGNED______"></span> **/不整列**   
各割り当ての終了位置をページ境界の末尾に揃えます。これは、開始アドレスが8バイトブロックに配置されていないことを意味します。 既定では、ヒープマネージャーは、割り当ての開始アドレスが8バイトのブロックにアラインされることを保証します。

このオプションは、1バイトずつエラーを検出するために使用されます。 このパラメーター**をの場合**、このパラメーターを使用すると、占有仮想メモリのゾーンは、割り当ての最後のバイトの直後に開始され、プロセスが1バイトの割り当てを超えて1バイトでも読み取りまたは書き込みを試みると、即時エラーが発生します。

<span id="________decommit______"></span><span id="________DECOMMIT______"></span> **/decommit**   
このオプションは無効になっています。 これは受け入れられますが、無視されます。

Windows 2000 に含まれる PageHeap プログラム (PageHeap) は、割り当て後にアクセス不可能なページを配置することで、ページヒープの完全な検証を実装しています。 このツールでは、 **/デコミット**パラメーターを使用して、アクセスできないページに予約済みの仮想メモリのゾーンを置き換えます。 このバージョンの GFlags では、完全なページヒープ検証を実装するために、予約済みの仮想メモリのゾーンが常に使用されています。

<span id="________notraces______"></span><span id="________NOTRACES______"></span> **/notraces**   
実行時のスタックトレースが保存されないことを指定します。

このオプションを使用すると、パフォーマンスが若干向上しますが、デバッグがはるかに困難になります。 このパラメーターは有効ですが、使用することはお勧めしません。

<span id="________fault______"></span><span id="________FAULT______"></span> **/障害**   
プログラムのメモリ割り当てを指定した速度で、指定したタイムアウト後に強制的に失敗させます。

このパラメーターは、テスト対象のイメージファイル ("フォールト挿入" と呼ばれる) にヒープ割り当てエラーを挿入します。これにより、プログラムがメモリ不足の状態で実行されるときに発生する可能性があるメモリ割り当てが失敗することがあります。 このテストは、リソースの解放に失敗するなど、割り当てエラーを処理中のエラーを検出するのに役立ちます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><em>量</em></p></td>
<td align="left"><p>1 (. 01%) から10進数の整数を指定します。~ 1万 (100%)割り当てが失敗する確率を表します。 既定値は 100 (1%) です。</p></td>
</tr>
<tr class="even">
<td align="left"><p><em>タイムアウト</em></p></td>
<td align="left"><p>プログラムの開始からエラー挿入ルーチンの開始までの時間間隔を決定します。</p>
<p><em>タイムアウト</em>は秒単位で計測されます。 既定値は 5 (秒) です。</p></td>
</tr>
</tbody>
</table>

 

<span id="________leaks______"></span><span id="________LEAKS______"></span> **/リーク**   
プロセスの終了時にヒープリークをチェックします。

**/リーク**パラメーターを指定すると、ページヒープ全体が無効になります。 **/のリーク**が使用されている場合、 **/後方**のように **、の各**パラメーターを変更するパラメーターと**パラメーターは無視**され、GFlags はリークチェック付きで標準のページヒープの検証を実行します。

<span id="________protect______"></span><span id="________PROTECT______"></span> **/protect**   
ヒープの内部構造体を保護します。 このテストは、ランダムヒープの破損を検出するために使用されます。 実行速度が大幅に低下する可能性があります。

<span id="________no_sync______"></span><span id="________NO_SYNC______"></span> **/no\_sync**   
同期されていないアクセスを確認します。 このパラメーターは、ヒープで作成されたヒープ\_NO\_SERIALIZE フラグが異なるスレッドによってアクセスされたことを検出した場合に、中断を発生させます。

このフラグは、カスタマイズされたヒープマネージャーを含むプログラムのデバッグには使用しないでください。 ヒープアクセスを同期する関数を使用すると、ページヒープ検証ツールによって、存在しない同期エラーが報告されます。

<span id="________no_lock_checks______"></span><span id="________NO_LOCK_CHECKS______"></span> **/no\_lock\_checks**   
クリティカルセクションの検証を無効にします。

<span id="_______________"></span> **/?**    
GFlags のヘルプを表示します。 **/P**、 **/?** GFlags のページヒープ検証オプションのヘルプを表示します。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>Comments

パラメーターを指定せずに「 **gflags** 」と入力すると、 **[グローバルフラグ]** ダイアログボックスが開きます。

追加のパラメーターを指定せずに「 **gflags/p** 」と入力すると、ページヒープ検証が有効になっているプログラムの一覧が表示されます。

すべてのフラグをクリアするには、*フラグ*を **-FFFFFFFF**に設定します。 (*フラグ*を0に設定すると、現在のフラグ値に0が加算されます。 すべてのフラグがクリアされるわけではありません)。

イメージファイルの*フラグ*を**FFFFFFFF**に設定すると、Windows はすべてのフラグをクリアし、イメージファイルのレジストリサブキーの GlobalFlag エントリを削除します。 サブキーはそのまま残ります。

ページ**ヒープを操作**するための/size、 **/random**、、 **/address**、および **/dll**パラメーターは、**ページヒープ検証**の対象となる割り当てと使用される検証方法を決定します。 各コマンドでは、これらのパラメーターのうち1つのみを使用できます。 既定では、プロセスのすべての割り当てについて、標準のページヒープ検証が実行されます。 残りのパラメーターは、ページヒープ検証のオプションを設定します。

GFlags のページヒープ機能は、標準の Windows ヒープマネージャー関数 (**HeapAlloc**、 **GlobalAlloc**、 **LocalAlloc**、 **malloc**、 **new**、 **new\[\]** 、またはそれに対応する割り当て解除関数) を使用するヒープメモリの割り当て、または標準のヒープマネージャー関数を呼び出すカスタム操作を使用するヒープメモリ割り当てのみを監視します。

プログラムに対してフルページヒープ検証または標準ページヒープ検証が有効になっているかどうかを確認するには、コマンドラインで「 **gflags/p**」と入力します。 結果の表示では、**トレース**は、プログラムに対して標準のページヒープ検証が有効になっていることを示し、**完全なトレース**は、そのプログラムに対して完全なページヒープ検証が有効になっていることを示します。

**/Enable**パラメーターは、レジストリ内のイメージファイルの[有効ページヒープ](enable-page-heap.md)(hpa) フラグを設定します。 ただし、既定では、 **/enable**パラメーターはイメージファイルの*標準*ヒープ検証をオンにします。これは、イメージファイルの*完全な*ヒープ検証を有効にする、 **+ hpa**フラグを指定した **/i**パラメーターとは異なります。

*標準*のページヒープ検証では、割り当ての最後にランダムなパターンが配置され、ヒープブロックが解放されるとパターンが検証されます。 ページヒープの*完全な*検証では、各割り当ての最後に予約済みの仮想メモリのゾーンが配置されます。

ページヒープの完全な検証では、システムメモリを迅速に使用できます。 メモリを集中的に使用するプロセスに対してページヒープの完全な検証を有効にするには、 **/size**または **/dll**パラメーターを使用します。

デバッグにグローバルフラグを使用した後、 **gflags/p/disable**コマンドを送信して、ページヒープの検証をオフにし、関連するレジストリエントリを削除します。 それ以外の場合、デバッガーが読み取るエントリはレジストリに残ります。 このタスクには、 **gflags/i hpa**コマンドを使用できません。ページヒープの検証は無効になりますが、レジストリエントリは削除されません。

既定では、Windows Vista 以降のバージョンの Windows では、プログラム固有の設定 (イメージファイルフラグとページヒープ検証の設定) が現在のユーザーアカウントに格納されます。

このバージョンの GFlags には、 **-v**オプションが含まれています。これにより、gflags 用に開発された機能が有効になります。 ただし、これらの機能はまだ完了していないため、ドキュメントには記載されていません。

 

 





