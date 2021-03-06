---
title: INF ファイルの一般的な構文規則
description: INF ファイルの一般的な構文規則
ms.assetid: ba11a229-d0d3-4217-bcf8-9aada2f159aa
keywords:
- INF ファイル WDK デバイス インストールでは、一般的な構文規則
- INF ファイルのセクションでは、WDK のデバイス インストール
- WDK の INF ファイルのセクションでは
- INF ファイル WDK デバイス インストールでは、ディレクティブ
- WDK の INF ファイルのディレクティブ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ec48e4c4d81caf081ce27a846b970062fe0d29fb
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67387329"
---
# <a name="general-syntax-rules-for-inf-files"></a>INF ファイルの一般的な構文規則





INF ファイルでは、テキスト ファイルが名前付きセクション別に分類です。 いくつかのセクションがあるシステム定義の名前と、いくつかのセクションがある名前の INF ファイルの作成者によって決定されます。

各セクションで解釈されるセクションに固有のエントリが含まれています。[デバイス インストール コンポーネント](https://docs.microsoft.com/previous-versions/ff541277(v=vs.85))(インストーラー、共同インストーラーは、SetupAPI クラス)。 いくつかのエントリは、定義済みのキーワードで始まります。 これらのエントリが呼び出される*ディレクティブ*します。

いくつかの INF ファイル エントリは、特定の目的で 1 つのセクションから、別のポインターでは基本的にします。 たとえば、 [ **INF AddReg ディレクティブ**](inf-addreg-directive.md) Windows レジストリを変更するよう指示するエントリを含むセクションを識別します。 これらのエントリには、追加の引数 (必須または省略可能) の Windows のインストール中に解釈することもありますが含まれます。

他の INF ファイルのエントリを他のセクションでは、ポイントします、を指定しないでフラグのファイル名、レジストリ値、ハードウェアの構成情報などのインストール中に Windows が使用する情報と具合です。 たとえば、 [ **INF DriverVer ディレクティブ**](inf-driverver-directive.md)ドライバーのバージョン情報を提供します。

最初に Windows インストールの開始時に、 [ **INF バージョン セクション**](inf-version-section.md) INF ファイルの有効性を確認し、インストール ファイルの場所を決定します。 検索してインストールを開始し、 [ **INF 製造元セクション**](inf-manufacturer-section.md)します。 このセクションで説明するためのディレクティブ[ **INF*モデル*セクション**](inf-models-section.md)、さらに、さまざまな先行するディレクティブを提供する[ **INF *DDInstall*セクション**](inf-ddinstall-section.md)インストールされているデバイスのハードウェア ID に基づきます。

次の構文規則では、INF ファイル、文字列トークン、および行の形式、継続、およびコメントを使用して、セクション名の形式の必須およびオプションの内容を制御します。

### <a href="" id="case-sensitivity"></a> 大文字小文字の区別

-   セクション名、エントリ、およびディレクティブが区別されます。 たとえば、**バージョン**、**バージョン**と**バージョン**名の指定、INF ファイル内で均等に有効なセクション。

### <a href="" id="required-and-optional-contents"></a> 必須およびオプションの内容

- 必須およびオプションのセクションでは、エントリ、および特定の INF ファイルでディレクティブのセットは、インストールするデバイスとドライバーまたはアプリケーションまたはデバイス クラス インストーラー DLL) などのコンポーネントの種類に依存します。

- セクションでは、セクションに固有のエントリ、および特定のデバイスとドライバーのインストールに必要なディレクティブのセットでは、対応するクラスのインストーラーをいくらかによっても異なります。 方法の詳細についてシステムが提供するクラスのインストーラーはデバイスの種類に固有の INF ファイルの処理、WDK でデバイスの種類の特定のドキュメントを参照してください。

- 構文の定義内では、省略可能なエントリはで区切られます*太字でない*角かっこ (\[、\])。 その一方で、*太字*角かっこ ( **\[** 、 **\]** ) が含まれるエントリの必要な構成要素。 次の例は、かっこで**バージョン**、かっこの中に、必要な**クラス**=*クラス名*このエントリを示す省略可能。

  <pre>
  <b>[</b>Version<b>]</b>

  Signature="signature-name"
  [Class=class-name]
  ...
  </pre>

### <a href="" id="section-names"></a> セクション名

- セクションでは、任意の順序で指定できます。 ほとんどの INF ファイル セクションでは、特定の順序で規則により、ボックスの一覧が、INF ファイル内の位置ではなく、名前で、Windows がセクションを検索します。

- セクション名を角かっこで囲まれた、INF ファイル内の各セクションから始まります ( **\[ \]** )。 セクション名には、システム定義または INF ライター定義を指定できます。

  たとえば、 **\[製造元\]** システムという名前の先頭を指定します**製造元** セクションで、中に<strong>\[</strong>Std.Mfg<strong>\]</strong>特定を表す INF ライター定義*モデル*セクション名。

  セクション名では、Windows 2000 で 255 文字の最大長と以降のバージョンの Windows があります。

  各セクションは、新しいの先頭に終了 **\[** <em>セクション名</em> **\]** またはファイルの終端マークの位置。

- INF ファイルでは、複数のセクションには、同じ名前が付いている場合に、システムは、1 つのセクションに、エントリとディレクティブをマージします。

- 二重引用符文字で囲まれている場合を除き、( **"** )、INF ライター定義セクション名は INF に固有の特定の文字を除く、明示的に表示される文字の一意にする-、-INF 引用符なし文字列である必要があります意味があります。 具体的には、セクション エントリによって参照されている、引用符なしのセクション名またはディレクティブは、先頭または末尾のスペース、改行文字、戻り値の文字、または任意のコントロールを非表示文字を持つことはできませんし、タブを含めることはできません。 さらに、角かっこのいずれかに含めることはできません ( **\[ \]** ) 文字を 1 つのパーセント ( **%** ) 文字、セミコロン ( **;** )、または内部の二重引用符 ( **"** ) 文字、およびそれには、円記号を含めることはできません ( **\\** ) の最後の文字として。

  たとえば、Std.Mfg と Std_Mfg は、INF ファイル エントリまたはディレクティブが Std; によって参照されるときに、一意かつ有効なセクション名製造 (とその内部セミコロン) が二重引用符で囲まれている場合を除き、無効です ( **"** )。

  として INF ライター定義セクション名を指定する、 **"** <em>文字列を引用符で囲まれた</em> **"** ほとんどの文字で以前に説明した制限の上書きセクション名を参照します。 このような区切り記号付きのセクション名は、右中かっこ以外のほぼすべての明示的または暗黙的に表示されている文字を含めることができます ( **\]** ) INF ファイルに対応するセクションでは、これと一致する限り **"** <em>文字列を引用符で囲まれた</em> **"** 正確にします。

  たとえば、 **"** ; です。Std 製造 **"** INF ファイルに対応するセクションの宣言に関しては、その領域とセミコロン文字として二重引用符の内部名を完全に一致する場合は、セクション名の有効な参照を **\[** ;;Std 製造 **\]** します。

### <a href="" id="using-string-tokens"></a> 文字列トークンを使用します。

- INF ライター定義のセクションの名前も含め、INF ファイルの多くの値は、フォームのキーのトークンを文字列として表現できる **%** <em>strkey</em> **%** . INF**文字列**INF ファイル、各文字列のキーのセクションは、明示的に表示されている文字のシーケンスで構成される文字列値を関連付ける必要があります。 必要に応じて、セットアップ コードを Unicode 文字列の値に変換します。

  定義する方法についての詳細は **%** <em>strkey</em> **%** トークンと、その値、の説明を参照してください[。 **INF 文字列セクション**](inf-strings-section.md)します。

### <a href="" id="line-format--continuation--and-comments"></a> 行の形式、継続、およびコメント

- 各エントリ ディレクティブのセクションでは、リターンや改行文字で終了します。 そのため、INF ファイルを作成するために使用するテキスト エディターは、任意のエディターにより決定されたいくつかの文字の後にリターンや改行文字を挿入する必要があります。

- 円記号 ( **\\** ) エントリまたはディレクティブで、明示的な行 continuator として使用できます。 ただし、円記号の文字は、パスの指定にも使用されます。 パスの指定に表示される円記号が行 continuator として解釈されないことを確認するには、次の戦略を使用します。

  -   2 つの行にまたがるうちの 1 つ円記号を含むエントリは、ディレクティブ、円記号を格納するエントリを区切るために引用符を使用します。

      ```cpp
      CopyFiles = "SomeDirectory\"\
      ,SomeFile
      ```

  -   次の例に示すように、円記号を使用しないでください。 Windows では、最初の円記号を無視し、行 continuator として 2 つ目の円記号を解釈します。

      ```cpp
      CopyFiles = SomeDirectory\\
      ,SomeFile
      ```

  -   次の構文が有効なと等価`CopyFiles = "SomeDirectory\",SomeFile ; comment`します。

      ```cpp
      CopyFiles = "SomeDirectory\"\ ; comment 
      ,SomeFile
      ```
      セミコロンを無視すると後のテキストは`CopyFiles = "SomeDirectory\" ; comment ,SomeFile`は機能しません。

- コメントはセミコロンで始まります ( **;** ) 文字。 解析と、INF ファイルを解釈する、システムは次であるとみなしますなし、インストール プロセスに関連性。
  - 任意の文字内に表示する、セミコロンがない限り、同じ行にセミコロンの後、 **"** <em>文字列を引用符で囲まれた</em> **"** または **%** <em>strkey</em> **%** トークン
  - ライン フィードまたは戻り値の文字以外何も含まれている空の行

- セクションのエントリとディレクティブで指定された値はコンマで区切ります。

  INF ファイル エントリまたはディレクティブは、値のリストの途中で、省略可能な値を省略できますが、コンマである必要があります。 INF ファイルでは、末尾のコンマを省略できます。

  たとえば、構文、 **SourceDisksFiles**セクション エントリ。

  <em>ファイル名</em> **=** <em>diskid</em>\[ **、** \[*subdir* \] \[ **、** <em>サイズ</em>\]\]

  エントリを省略した、 *subdir*装置が、値、*サイズ*値は次の例に示すように、両方の値のコンマ区切り記号を指定する必要があります。

  <em>ファイル名</em> **=** <em>diskid</em> **、および**<em>サイズ</em>

  2 つの省略可能な値の指定を省略する INF ファイル内のエントリには、この形式を持つことができます。

  <em>filename</em> **=** <em>diskid</em>
- パーセント (%) を含めるためにセクションのエントリとディレクティブで指定された値内の文字、もう 1 つのパーセント記号、パーセント文字をエスケープします。

  たとえば、このステートメントで、 *[追加-レジストリ-セクション]* セクション。

  *HKR,,EventMessageFile,0x00020000,"%%SystemRoot%%\System32\IoLogMsg.dll"*

  レジストリ値は、次の値に設定されます。

  *%SystemRoot%\System32\IoLogMsg.dll*
- セクションのエントリとディレクティブで指定された値で二重引用符 (") 文字を含めるために、もう 1 つの二重引用符と二重引用符をエスケープします。  文字列は内である必要がありますに注意してください、 **"** <em>文字列を引用符で囲まれた</em> **"** します。  

  たとえば、このステートメントで、 *[追加-レジストリ-セクション]* セクション。

  *HKR、およびの例「、""example""の文字列を表示」*

  レジストリ値は、次の値に設定されます。

  *"Example"の文字列を表示します。*

### <a href="" id="inf-size-limits"></a> INF サイズの制限

-   文字列の置換と終端の NULL 文字を含む前に、INF ファイルのフィールドの文字の最大長は、4096 です。

-   文字列の置換後の INF ファイルの文字列の文字の最大長は 4096、終端の NULL 文字を含むです。

-   ただし、注意するプラグ アンド プレイ (PnP) が認識またはデバイスの説明、ドライバーのプロバイダー、デバイスの製造元など、使用される特定の INF ファイルのフィールドのより制限の厳しい制限をかける場合があります。









