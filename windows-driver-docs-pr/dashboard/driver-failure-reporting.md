---
title: ドライバー エラー レポート
description: パートナー センターのドライバー エラー レポートでは、クラッシュやその他のイベントなど、ドライバーに関するパフォーマンスのデータを取得できます。
ms.assetid: F98F61EF-6C4A-400A-BA01-B79C72A7993A
ms.topic: article
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a47bc7db736a65498ad0db8e1203634c97c8f1b8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56518745"
---
# <a name="driver-failure-reporting"></a>ドライバー エラー レポート

パートナー センターのドライバー エラー レポートによって、クラッシュや応答停止イベントなど、ドライバーのパフォーマンスと品質に関連するデータを取得できます。 該当する場合、さらにデバッグのスタック トレースを表示できます。

## <a name="apply-filters"></a>フィルターの適用

次の項目でレポート内のすべてのデータを整理しフィルター処理することができます。

- 申請
- OS バージョン
- 市場
- Architecture
- フライト リング
- OEM 名
- OEM モデル
- デバイスの種類
- ［ドライバ名］

以下のグラフに示される情報は、**[フィルターの適用]** で選んだ期間を反映しています。 既定では、**[フィルターの適用]** を使ってパッケージ バージョンを 1 つに絞り込んでいない限り、その情報にはすべてのパッケージ バージョンのデータが含まれます。

## <a name="failure-hits"></a>Failure hits (エラーのヒット数)

**[Failure hits]** (エラーのヒット数) のグラフには、過去 30 日以内にユーザーが経験した 1 日のクラッシュとイベントの数が表示されます。 各アプリで発生した各種のイベントは、個別に追跡され、**ライブ カーネル イベント**と**システム クラッシュ**で分類されます。

## <a name="failure-breakdown"></a>エラーの詳細

次に示すさまざまな属性でエラーの回数をピボットで表示できます。

- ドライバーのバージョン
- OS バージョン
- フライト リング
- OEM モデル
- デバイスの種類
- Architecture

## <a name="failures"></a>障害

**[Failures]** (エラー) のグラフには、選んだフィルターに対応するエラーの合計数が表示されます。 既定では、レポートには **[hits]** (ヒット数) の降順でエラーが表示されます。 このグラフの **[Hits]** (ヒット数) 列の矢印をクリックすることで、この順序を逆にすることができます。 また、各エラーはエラーの合計数に占める割合と共に表示されます。 特定のエラーに関するエラーの詳細レポートを表示するには、エラー名を選びます。 エラーの詳細レポートには、先月のエラーのヒット数、CAB ダウンロードへのリンクを示すエラー ログ、次に示すエラーの発生に関するいくつかの詳細が含まれます。

- date
- パッケージ バージョン
- デバイスの種類
- デバイスのモデル
- OS ビルド