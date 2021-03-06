---
title: エラー情報の取得
description: エラー情報の取得
ms.assetid: 4af06727-9660-4bbc-8c9e-a50c8f2d566d
keywords:
- Windows ハードウェアエラーアーキテクチャ WDK、エラー情報の取得
- WHEA WDK、エラー情報の取得
- ハードウェアエラー WDK WHEA、エラー情報の取得
- エラー WDK WHEA、エラー情報の取得
- プラットフォーム固有のハードウェアエラードライバープラグイン WDK WHEA、エラー情報の取得
- PSHED プラグイン WDK WHEA、エラー情報の取得
- エラー情報の取得 (WDK WHEA)
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a7db8bf1551c2e771dbd1f126b4921beed3e2045
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844789"
---
# <a name="error-information-retrieval"></a>エラー情報の取得


ハードウェアエラー状態の処理中に、エラー処理プロセス内の3つの独立したポイントで PSHED が呼び出されます。

-   低レベルのハードウェアエラーハンドラー (LLHEH) は、エラー状態に関する補足情報をハードウェアエラーパケットに追加して、LLHEH がオペレーティングシステムにエラーを報告できるようにするために、このように呼び出します。

-   Windows カーネルは、エラー状態を説明するエラーレコードに補足エラーレコードセクションを追加できるように、を呼び出します。

-   修正されたエラーについては、Windows カーネルはエラーの処理が完了した後にエラーソースのエラー状態レジスタをクリアできるように、を呼び出します。

Pshed 検出された標準エラーソースによって報告されたエラー状態に対して、エラー情報の取得操作をサポートします。 [エラーソースの検出](error-source-discovery.md)に参加し、pshed サポートされていないオペレーティングシステムに追加のエラーソースを報告する、pshed プラグインが実装されている場合は、これらのエラーソースのエラー情報の取得操作をサポートするために、エラー情報の取得にも参加する必要があります。 また、必要に応じて、標準のエラーソースによって報告されたエラー状態に関する追加のエラー情報を提供するために、必要に応じて、エラー情報の取得に参加することもできます。

  **注**: エラー情報の取得に参加するプラグインは、次のいずれかに該当する場合は、[エラーソースの検出](error-source-discovery.md)にも参加する必要があります。
-   このプラグインは、特定のエラーソースによって報告されたハードウェアエラーパケットに追加のエラー情報を提供します。 このような状況では、エラーソースの検出時にそのエラーソースについて、 [ **\_\_\_WHEA**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_whea_error_source_descriptor)の**maxrawdatalength**メンバーに含まれている値を変更して、追加のエラー情報を考慮する必要があります。

-   このプラグインは、特定のエラーソースによって報告されたハードウェアエラーのエラーレコードに追加のエラーレコードセクションを提供します。 このような状況では、エラーソースの検出時にそのエラーソースの、WHEA\_エラー\_ソース\_記述子構造の**Maxsectionsperrecord**メンバーに含まれている値を変更して、追加のエラーレコードセクションを考慮する必要があります。

 

エラー情報の取得に参加する PSHED プラグインを実装する方法の詳細については、「[エラー情報の取得に参加](participating-in-error-information-retrieval.md)する」を参照してください。

 

 




