---
title: デバイス フィルター ドライバーの順序
description: Microsoft は、スタックの位置ではなく、フィルターの意図を表現することによって宣言的にフィルターを追加する方法として「デバイス フィルター ドライバーの順序」を開発しました。
ms.date: 04/16/2019
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: c146762cf55ceb51c081c0852fa966424e6df221
ms.sourcegitcommit: 459c7928a7917609afb68bafb65c2fcc1d9040ff
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/21/2019
ms.locfileid: "69887197"
---
# <a name="device-filter-driver-ordering"></a>デバイス フィルター ドライバーの順序

Microsoft は、スタックの位置ではなく、フィルターの意図を表現することによって宣言的にフィルターを追加する方法として「デバイス フィルター ドライバーの順序」を開発しました。

## <a name="the-need-for-device-filter-driver-ordering"></a>デバイス フィルター ドライバーの順序の必要性

Windows 10 バージョン 1903 以前にデバイス フィルター ドライバーを登録する方法としてサポートされていたのは、([AddReg ディレクティブ](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addreg-directive)を使った) レジストリ エントリの追加のみでした。 しかし、レジストリを操作するこの方法には、特定のフィルターを登録する**正確な位置**を指定する柔軟性はありません。

AddReg ディレクティブを使ったフィルターの登録では、単純にフィルターの一覧の最後にフィルターが付加されます。 このアプローチでは、順序付けられた値の一覧を使い、スタック内でフィルターを読み込む場所を決定します。

順序付けられた値の単一の一覧を使う方法は、特に [AddReg](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addreg-directive) によって "*末尾に* *付加*される*だけ*" の場合は、理想的とは言えません。複数のドライバーによって同じデバイスにフィルターが追加された場合に、悪影響が生じるためです。

少なくとも 1 つの[拡張 INF](https://docs.microsoft.com/windows-hardware/drivers/install/using-an-extension-inf-file) が使われているシナリオで、INF による **AddReg** の使用法が不適切な場合 (つまり append フラグが使われていない場合)、異なる INF によって追加されたフィルターが消去される可能性があります。

さらに、複数の拡張 INF によってフィルターが追加されていて、それらのフィルターの相対順序が重要であったとしても、プラグ アンド プレイ (PnP) プラットフォームではそれらの拡張のインストール順が保証されません。 その結果、"付加" の順序は保証されません。

## <a name="implementing-device-filter-driver-ordering"></a>デバイス フィルター ドライバーの順序の実装

Microsoft は、デバイス フィルターを柔軟かつ宣言的に登録する方法を提供するために、スタックの位置ではなく、フィルターの意図を表現することによって宣言的にフィルターを追加する方法を開発しました。 このソリューションにより、ファンクション ドライバーの作成者は INF 内で**順序付けした一連の位置 (レベル)** を表現し、フィルターはそのレベルに対して自身を登録することができます。

フィルターは、特定のレベルだけでなく、単に "*上位*" または "*下位*" レベルのフィルターとして宣言的に登録することができます。

このインフラストラクチャは、デバイス スタック内でのドライバーの順序を指定する新しいフィルター登録方法に基づいています。 この新しい方法によって、従来のフィルター追加方法の互換性が失われることはありません。 その代わりに、より堅牢で柔軟性の高い方法で新しいフィルターを登録できるようになります。

この方法を有効にするには、基本 INF で、1 つ以上の "レベル" を含む順序指定済みの一覧を定義します。 基本 INF と拡張 INF の両方で、サービス名とフィルターのレベルを指定する新しい INF ディレクティブを通じて、宣言型のフィルターを登録できます。 上位と下位のフィルターは、それぞれに対応する順序指定済みのレベルの一覧で表されます。

これらの上位と下位のフィルターの一覧は、すべてのフィルター ドライバーを各自のレベルで並べ替えることで作成します。 各レベル内のフィルターの順序は "*ランダム*" であると見なされ、特定レベル内のフィルターの順序に、依存関係は考慮されません。 2 つのフィルターの相対順序が "**保証**" されなければならないシナリオでは、これらを別々のレベルに登録する必要があります。

次のようなデバイス ドライバーの例を考えてみましょう。

![デバイス ドライバーのインストールを、目的の位置と順序を維持しながらフィルター ドライバーの一覧をマージするデバイス スタックの順序として表す図。](images/device_filter_ordering_1.png)

デバイス ドライバーの基本 INF によって、2 つの上位フィルター レベル A と B が (この順序で) 宣言されます。 基本 INF に関連付けられた拡張 INF で、2 つのレベルのそれぞれに 2 つのフィルターが追加されます。

デバイス ドライバーのインストールの結果は、目的の位置と順序を維持しながらフィルター ドライバーの一覧をマージするデバイス スタックの順序になります。 結果のデバイス スタックの順序により、"A" レベルのフィルターはすべて、"B" レベルのどのフィルターよりも前に配置されるようになります。 ただし、各レベル内での順序はランダムです。

例に示すように、Filter3 は Filter5 の前に配置される可能性も、Filter5 の後ろに配置される可能性もあります。 どちらの場合でも、Filter3 と Filter5 は、次のレベルである "B" のフィルターよりも前に配置されます。

フィルターを登録する一連のレベルを設計するときは、順序付けのために一連のレベルを作成するのではなく、フィルターの目的に対応するようにレベルの名前付けと順序付けを行う必要があります。 たとえば I/O デバイスでは、*Encryption* レベルを定義し、そこに暗号化フィルターをすべて登録できます。 これにより、フィルターの目的を簡単に理解および管理できるようになり、スタックはファンクション ドライバーの重大な変更に対してより堅牢になります。

> [!NOTE]
> 宣言型のフィルターは、基本 INF によってレベルが定義されていなくても、単に上位や下位として登録できます。 レベルが定義されていないということは、UpperFilters/LowerFilters レジストリ値の末尾にフィルターを付加することと論理的に同じです。 レベルが定義されている場合、レベルの 1 つを基本ドライバーの既定のレベルとしてマークする必要があり、この例では、そのレベルにフィルターが登録されます。

## <a name="scenarios"></a>シナリオ

スタックを通過するデータを暗号化する I/O デバイス ドライバーについて考えてみましょう。 一般的な実装では、ファンクション ドライバーの直後の下位フィルター ドライバーを使ってこれを実現します。 ドライバーの作成者は、意図した正確な位置に暗号化フィルターを配置するために、次に示すような宣言型のフィルターを使用できます。

!["Encrypt" フィルター ドライバーを明示的に "Encryption" レベルに配置することで、その結果のデバイス スタックの順序で、"Encrypt" フィルター ドライバーがそれよりも下位のどのフィルターよりも前かつファンクション ドライバーの直後に配置されている図。](images/device_filter_ordering_2.png)

基本 INF では、下位フィルターの 2 つのレベル \"Encryption\" および "Monitoring"(既定値) が確立されます。 この例の "Monitoring" (既定) は、この特定のデバイスに存在する可能性のある残りの下位フィルターです。 "Encrypt" フィルター ドライバーを明示的に "Encryption" レベルに配置することで、その結果のデバイス スタックの順序では、"Encrypt" フィルター ドライバーがそれよりも下位のどのフィルターよりも前かつファンクション ドライバーの直後に配置されます。

さらに一歩踏み込んでみましょう。 ドライバーの新しいバージョンがリリースされ、作成者はファンクション ドライバーに組み込みの暗号化を用意しているとします。 これにより、"Encrypt" フィルター ドライバーを分ける必要がなくなります。 作成者は単に "Encrypt" フィルターを含むレベルを基本 INF から削除するだけで、ドライバーが更新されると、スタックが動的に再構築されます。

フィルターが自身を存在しない明示的なレベルに宣言した場合、そのフィルターはデバイス スタックに配置されません。 この例では、基本 INF が更新され、拡張 INF は変更されていないにもかかわらず、結果のデバイス スタックからは "Encrypt" フィルターが除外されます (基本 INF のレベルの宣言に含まれないため)。

![基本 INF から "Encrypt" フィルターを含むレベルが削除されている図](images/device_filter_ordering_3.png)

## <a name="default-filter-level"></a>既定のフィルター レベル

最後のフィルター スタックを生成するには、フィルター情報のすべてのソースを単一の一覧にマージします。 **デバイス スタックを作成するとき**に統合ロジックが実行されることに注意することが重要です。 新しい/更新された基本または拡張ドライバーをインストールすることで新しいフィルターを追加する場合、デバイスはインストール中に再起動され、新しいフィルターの一覧を取得します。

フィルターのソースの中には、位置情報を持たないものもあります。具体的には、従来の UpperFilters/LowerFilters レジストリ値、または位置のみの宣言型構文 (後述) を使って追加されたフィルターです。

位置情報がない場合に効果的にマージを行うには、基本 INF で追加の情報 (既定のフィルター レベル) を定義する必要があります。 既定のフィルター レベルは、レベルまたは位置情報を持たないフィルターが挿入される位置です。

たとえば、フィルター レベルは基本 INF で次のように定義できます。

```INF
Level Order: A, B, C
DefaultFilterLevel: C
```

既定のレベルを最終レベルとして指定することは、位置情報を持たないすべてのフィルターがフィルターの一覧の最後に**付加**されることを意味します。 または、ドライバーの作成者が、レベル C に明示的に登録されているフィルターを、常にスタックの最後に配置したい場合があります。

```INF
Level Order: A, B, C
DefaultFilterLevel: B
```

既定のフィルター レベルが B に設定されていることから、位置情報を持たないその他のフィルターはすべて、A のフィルターと C のフィルターの間に挿入されます。

## <a name="syntax"></a>構文

### <a name="registering-filters"></a>フィルターを登録する

```INF
[DDInstall.Filters]
AddFilter = <FilterName>, [Flags], FilterSection
```

FilterLevel または FilterPosition は 2 つの方法のいずれかで指定できます。

**選択肢 1:**

```INF
[FilterSection]
FilterLevel=<LevelName>
```

**選択肢 2:**

```INF
FilterPosition=Upper/Lower
```

これは、基本 INF と拡張 INF の**両方**で行えます。

\[DDInstall.Filters\]

**FilterName** は、システム上のサービスの名前です。

**Flags** は、現在使用されておらず、空または 0 に設定する必要があります。

**FilterSection** は、フィルターを記述するセクションです。

\[Filter Section\]

フィルター セクションには、2 つのディレクティブ   **FilterLevel** または **FilterPosition** のいずれか 1 つのみを含める必要があります。

**FilterLevel** は、基本 INF によって定義された、デバイス フィルターを挿入するスタック上の特定の場所です。  各レベル内でのフィルターの順序はランダムです。

**FilterPosition** は、サード パーティのフィルターを挿入する決まった場所を持つクラスで使用されます。

### <a name="defining-filter-levels"></a>フィルターのレベルを定義する

```INF
[DDInstall.HW]
AddReg = FilterLevel_Definition

[FilterLevel_Definition]
HKR,,UpperFilterLevels,%REG_MULTI_SZ%,"LevelA","LevelB","LevelC"
HKR,,UpperFilterDefaultLevel,,"LevelC"

HKR,,LowerFilterLevels,%REG_MULTI_SZ%,"LevelD","LevelE","LevelF"
HKR,,LowerFilterDefaultLevel,,"LevelE"
```

これを行えるのは、**基本**ドライバーのみです。

特定デバイスの宣言型フィルターの全一覧を取得するには、次のプロパティのクエリを実行します。

```INF
DEVPKEY_Device_CompoundUpperFilters
DEVPKEY_Device_CompoundLowerFilters
```

### <a name="legacy-equivalent-filter-registration"></a>従来と同じ方法でフィルターを登録する

INF を使って上位フィルターを追加する従来のアプローチを実現する方法を調べてみましょう。

```INF
[DDInstall.HW]
AddReg = Filters

[Filters]
HKR,,"UpperFilters", 0x00010008, "MyFilter"
```

この構文は、上位フィルターの一覧の末尾に "MyFilter" を追加します。

導入された新しい構文では、上のセクションは論理的に次と同じです。

```INF
[DDInstall.Filters]
AddFilter = MyFilter,,MyUpperFilterInstall

[MyUpperFilterInstall]
FilterPosition = Upper
```

これは、上位フィルターの一覧に "MyFilter" フィルターを追加するよう指定します。 基本 INF に指定のフィルター レベルがある場合、*FilterPosition* を使うと、その位置の既定のレベルにフィルターが登録されます。

フィルター レベルが指定されていない場合、このフィルターは上位フィルターとして順不同で登録されます。
