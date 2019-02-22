---
title: カーネル モードのパフォーマンス カウンターについて
description: カーネル モードのパフォーマンス カウンターについて
ms.assetid: 57655e65-6db4-487d-8831-282e8d30d84e
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8b134a6a302d30a5b7ea1912aae52cd44d20018f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56538774"
---
# <a name="about-kernel-mode-performance-counters"></a>カーネル モードのパフォーマンス カウンターについて


パフォーマンス カウンターの Windows (PCW) は、システムのさまざまなコンポーネントとやり取りし、カーネル モード コンポーネントによって提供されるカウンター セット (およびそれらのインスタンス) が記録されます。 さらに、PCW は、カウンター セットを確認し、要求されたデータを返すことでコンシューマーからサービス要求を追跡します。

カーネル モード PCW プロバイダーとしてパフォーマンス カウンター ライブラリ (PERFLIB) (バージョン 2 プロバイダー) を参照するには、そのカウンターでは、システムにインストールされてとデータのコレクションとインスタンスの列挙可能になります。 コンシューマーは、PDH と PERFLIB バージョン 1 を使用して、コンシューマー コードに変更を加えることがなく、KM PCW プロバイダーを照会できます。 詳細については、次を参照してください。[パフォーマンス カウンターを使用した開発](https://go.microsoft.com/fwlink/p/?linkid=144623)します。

カーネル モードで実行されているプロバイダーは、カーネル モード PCW プロバイダー API を使用して、カウンター セットを登録します。 プロバイダーでは、登録済みのカウンター セットのインスタンスを管理でき、(たとえば、ときにコンシューマーを追加するには、削除、またはカウンターを収集する) パフォーマンス カウンターに関連するさまざまなイベントが発生したときに通知する通知を使用することができます。

**注**  カーネル モード PCW プロバイダー、Windows 7 で導入された API (PERFLIB バージョン 2) は現在セッション領域ドライバーをサポートしていません。

 

 

 




