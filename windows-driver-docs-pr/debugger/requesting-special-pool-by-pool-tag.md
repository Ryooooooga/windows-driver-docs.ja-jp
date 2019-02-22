---
title: プールでプールの特殊なタグを要求します。
description: プールでプールの特殊なタグを要求します。
ms.assetid: 201eb8a5-b38b-4625-853d-448488214e52
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: dc71c56b19d726ab0d558f8fad0b413bd039e95a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56557622"
---
# <a name="requesting-special-pool-by-pool-tag"></a>プールでプールの特殊なタグを要求します。


## <span id="ddk_requesting_special_pool_for_allocations_with_a_specified_pool_tag_"></span><span id="DDK_REQUESTING_SPECIAL_POOL_FOR_ALLOCATIONS_WITH_A_SPECIFIED_POOL_TAG_"></span>


指定されたプール タグを使用してすべての割り当てのための特別なプールを要求することができます。 システム上の 1 つのみのプール タグは一度に 1 つカーネル特別なプールの要求を関連付けることができます。

Windows Vista および以降のバージョンの Windows では、プールでプールの特殊なタグを要求するのにコマンドラインを使用することもできます。 詳しくは、次を参照してください。 [ **GFlags コマンド**](gflags-commands.md)します。

**プールでプールの特殊なタグを要求するには**

1. 選択、**システム レジストリ**タブまたは**カーネル フラグ**タブ。

   Windows Vista と Windows の以降のバージョンでは、このオプションは両方のタブで使用します。 以前のバージョンの Windows では、上でのみ使用できますが、**システム レジストリ**タブ。

2. **カーネル特別なプール タグ**セクションで、**テキスト**、し、タグの 4 文字のパターンを入力します。

   タグを含めることができます、**でしょうか。** (単一の文字) と**\\*** (複数の文字) のワイルドカード文字です。 たとえば、Fat\*または Av? 4。

3. 次のスクリーン ショットは、システム レジストリ タブで、テキストとして入力タグを示しています。

   ![システム レジストリ タブで、テキストとして入力したタグのスクリーン ショット](images/gflags-specialpool-text.png)

4. **[適用]** をクリックします。

   クリックすると**適用**、GFlags から選択を変更する**テキスト**に**16 進**逆 (下のエンディアン) の順序で 16 進数の値として ASCII 文字を表示します。 たとえば、入力した**Tag1**、GFlags としてタグを表示します。 **0x31676154** (1gaT)。 この方法は、レジストリに格納されているし、デバッガーおよびその他のツールで表示されます。

   次の図は、クリックしての効果**適用**します。

   ![スクリーン ショット クリックしての効果を適用するは](images/gflags-specialpool-hex.png)

### <a name="span-idcommentsspanspan-idcommentsspanremarks"></a><span id="comments"></span><span id="COMMENTS"></span>「解説」

この機能を効果的に使用するには、ドライバーまたはその他のカーネル モードのプログラムが一意のプール タグを使用していることを確認します。 ドライバーを消費しているすべての特別なプールが疑われる場合、コードでの複数のプール タグの使用を検討してください。 テストできます、ドライバーを複数回テストごとに 1 つのプール タグへの特別なプールの割り当ています。

また、システムのページ サイズよりも大きい 16 進数の値を持つプール タグを選択します。 カーネル モード コードでは、プール タグを入力した場合のあるページより小さい値\_Gflags が特別なプールのサイズが、対応する範囲内にあるし、特別なプールのプールと同じタグを使用して割り当てを要求のすべての割り当てを要求するサイズ、します。 サイズを選択する場合など**30**、17 と 32 バイトとの間のすべての割り当てと、プール タグ 0x0030 割り当て特別のプールが使用されます。

 

 




