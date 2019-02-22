---
title: 自動アイテム
description: 自動アイテム
ms.assetid: 59f9b71b-e4bd-44a3-a4f2-dfea9f1045e2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 289f90f3a34325df8a1d6f2942189639be609bf2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56537148"
---
# <a name="auto-item"></a>自動アイテム


実装する[スキャンの自動構成](auto-configured-scanning.md)Windows 7 以降では、WIA ミニドライバーを含める必要があります、*自動項目*で、 [WIA 項目ツリー](wia-item-trees.md)スキャナー デバイス。 自動項目が属する、WIA\_カテゴリ\_自動カテゴリ。 このカテゴリの詳細については、次を参照してください。 [WIA 項目カテゴリ](wia-item-categories.md)します。

次の図は、自動の項目を含むサンプル WIA 項目のツリーを示します。 自動アイテムは、ツリーのルート項目の子です。

![自動アイテムを含む項目ツリーを示す図](images/wia-feeder-tree5.png)

自動アイテムだけでなく、WIA ツリー上の図には、フラット ベッド項目およびフィーダー アイテムのルート項目の子プロパティがどちらもが含まれます。 WIA アーキテクチャでは、自動の項目が唯一の子ではないことが必要です - ルート項目の自動アイテム常に、1 つまたは複数の兄弟です。 これらの兄弟の少なくとも 1 つは、フラット ベッド項目、フィーダー項目、またはフィルム項目である必要があります。 これらの項目に関する詳細については、次を参照してください。 [WIA 項目カテゴリ](wia-item-categories.md)します。

WIA スキャナーのデバイスでは、スキャンの自動構成をサポートする場合、WIA アプリケーションは自動項目からのデータ転送を要求することによって、デバイスで現在選択されている入力ソースからのイメージを取得できます。 この要求に応答して、デバイスは、イメージを取得する前に自動的にスキャンの設定のほとんどを構成します。 アプリケーションは、転送を使用するファイル形式を確認する場合だけです。 このため、自動項目は完全にプログラミング可能な入力ソース (つまり、フラット ベッド アイテム、取引先フィーダー項目、またはフィルム項目) の WIA 項目によって実装される WIA プロパティの比較的小さなサブセットを実装します。 詳細については、次を参照してください。 [WIA して自動アイテムのプロパティがサポートされている](wia-properties-supported-by-an-auto-item.md)します。

WIA アーキテクチャは、自動的に入力ソースから取得したイメージ データを転送するために使用するファイル形式を選択するスキャン モードを自動構成で動作しているスキャナーのデバイスを許可されていません。 代わりに、形式を明示的に選択するか、単に既定の形式をそのまま使用して、アプリケーションは、ファイルのフォーマットを決定します。 この制限は、デバイスが、アプリケーションが使用できない形式にスキャンした画像データを転送することを防ぎます。

スキャンの自動構成をサポートするスキャナー デバイス WIA ミニドライバーが自動に設定する必要があります\_ソース フラグ ビット、 [ **WIA\_DPS\_ドキュメント\_処理\_機能**](https://msdn.microsoft.com/library/windows/hardware/ff551379) WIA ツリーで、ルート項目によって実装されるプロパティの値。 WIA アプリケーションでは、デバイスの WIA 項目のツリーに自動の項目が含まれるかどうかを確認するには、このプロパティを照会できます。

 

 



