---
title: 複数の行列による頂点のブレンド
description: 複数の行列による頂点のブレンド
ms.assetid: d7348609-324d-4852-b217-4c298b8aaab7
keywords:
- 貸出 WDK Direct3D
- 頂点の WDK Direct3D のブレンド
- Direct3D WDK Windows 2000 の表示、頂点のブレンド
- 複数の行列による頂点の WDK Direct3D のブレンド
- 複数の行列による頂点の複数の行列による頂点の描画ついて WDK の Direct3D のブレンド
- WDK Direct3D を変換します。
- WDK の Direct3D をブレンド スキンを適用します。
- WDK の Direct3D をブレンド geometry
- ジョイント WDK Direct3D のブレンド
- WDK の Direct3D をブレンド マトリックス頂点
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ef426d08b1e3e987abbf4763805faa93a7602eb3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530275"
---
# <a name="multimatrix-vertex-blending"></a>複数の行列による頂点のブレンド


## <span id="ddk_multimatrix_vertex_blending_gg"></span><span id="DDK_MULTIMATRIX_VERTEX_BLENDING_GG"></span>


複数の行列による頂点のブレンドは、スムーズにブレンド スキン ジョイントを持つオブジェクトをレンダリングするための手法です。 この特定の手法は最新のソフトウェアでは一般的ではありませんが、何らかの滑らかなスキニングがアニメーション化された文字に関連するほとんどのゲームで使用されています。

これは、さまざまな手法をブレンドするジオメトリです。 ここで説明した手法は、ジオメトリが描画の形式です。 この手法は、関節削減多角形の数の増加のリアリティを提供する、関節セグメント化されたモデルの間での頂点をブレンドします。 各フレームで共同が変更された場合は、ジオメトリのパイプラインは、その共同でセグメントの間でスムーズに blend を隣接する頂点の位置を更新します。 この機能は、回転、翻訳、スケール、はさみ、または 4 X 4 変換マトリックスで表すことができる任意の組み合わせなど以外の結合の種類によって関連付けられたセグメントの間で操作できます。

一般原則では、ジョイントにメッシュの頂点を融合して一般的なセグメント化された文字を拡張します。

セグメント化されたモデルは、セグメント、または座標系から構築されると見なされます、各変換行列を使用して定義します。 これまでは、メッシュの各頂点は、1 つのセグメントのみに属していると見なされます。 このパラダイムは他のセグメントの部分的なメンバーシップに頂点を許可する拡張されています。 2 つ以上のセグメントの間の共同の近くには、各頂点は、スキンの重みを持つことができます*ベータ値*を実際に属している他のセグメントの比率を表します。

クラシックの階層的なモデリングで使用されているときにルート セグメントを取得しないブレンドします。 Blend に使用するには、他の変換がないため、剛体は常にします。 スキン重みベータ版は、使用するのには、親の座標システムの割合として定義されます。 0.0 はまったく剛体 - 場合全体のオブジェクトの上になります。

ベータ版は、親セグメントに厳格にアタッチされているような部分を 1.0 になります。 これは、blend 削除に対する親セグメントの貢献度の比率をドロップします。 それら (0.0) におけるいくつかのセグメントのジオメトリの継続性を維持するために 1.0 と点のいくつかのセットがあります。

複数の行列による頂点の描画には、各頂点を指定する別々 の 4 X 4 変換を必要とせずに、各頂点の位置を更新することで実行するブレンド滑らかなスキンが使用できます。 継続的な滑らかなサーフェイスの一般的なケースに対処し、まだ 1 つだけ追加値--スキン重みが必要ですが*Beta* --頂点、あたり追加の帯域幅要件を最小限に抑えます。

すべてのアクティブなワールド行列を使用して指定された頂点の位置データを変換し、結果は、対応する頂点の重みを使用してブレンドされました。

頂点内で通常すべて存在するのと同じ手順が実行されます。 これには、1 つの頂点 (位置、または通常) し、従来の照明とクリッピングのパイプラインの残りの部分にフィードバックするが生成されます。 詳細については、次を参照してください。 [Multimatrix 頂点ブレンディング アルゴリズム](multimatrix-vertex-blending-algorithm.md)します。

多くの場合、文字は、シーンの多角形の大部分を含めることができます、主要なパフォーマンスの問題になります。 Smooth スキニングも処理しないジオメトリのパイプラインは、大部分のコンテンツで、問題になります。

さらに、表示されている文字数では、シーンのほとんどの変動のコンポーネントの 1 つです。 フレーム レートの平準化動作に深刻な影響があります。 対話型アプリケーションの場合は、レベルのフレーム レートが高の平均フレーム レート、効率的な文字が非常に重要な機能のレンダリングを行うよりもより重要です。

頂点のブレンドは、変換後に実行する必要があります。 レンダリング パイプラインにブレンドが統合されていない場合、変換を 2 回実行する必要があります: スキニングとに 1 回とレンダリングに 1 回です。

合成されず頂点のだけの速度制限された帯域幅の場合、頂点データの 1 つのトラバーサルで対処するには、この場合は、頂点のブレンド ジオメトリのパイプラインに統合できます。

次のセクションでは、複数の行列による頂点のブレンドの実装の詳細を説明します。

[複数の行列による頂点ブレンディング アルゴリズム](multimatrix-vertex-blending-algorithm.md)

[FVF コードの変更](fvf-code-changes.md)

[D3DTRANSFORMSTATE 変更](d3dtransformstate-changes.md)

[D3DRENDERSTATETYPE 変更](d3drenderstatetype-changes.md)

 

 




