---
title: キャッシュの一貫性の維持
description: キャッシュの一貫性の維持
ms.assetid: 70b4b313-ce33-4562-aa0d-127a91706409
keywords:
- I/O WDK カーネルでは、キャッシュの一貫性
- キャッシュ コヒレンシー WDK カーネル
- WDK の I/O の整合性
- データ転送の WDK カーネル、キャッシュの一貫性
- WDK カーネルでは、キャッシュ コヒレンシーのデータを転送します。
- メモリ管理の WDK カーネル、キャッシュの一貫性
- プロセッサ キャッシュ WDK I/O
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 20495fec25a2aa119fe634e5ecb4852af180223d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63378752"
---
# <a name="maintaining-cache-coherency"></a>キャッシュの一貫性の維持


ドライバーがシステム メモリ、およびそのデバイスの間でデータを転送する際、システムの DMA コント ローラーのキャッシュまたは 1 つまたは複数のプロセッサのキャッシュ内のデータをキャッシュできます。 DMA または PIO サービスを使用してドライバー読み取り/書き込み Irp または DMA または PIO データ転送操作する必要があります整合性を確認する可能性があるキャッシュされたデータの転送中に操作が必要です。 デバイス I/O 制御要求。 このセクションでは、操作を行う方法について説明します。

このセクションでは、次のトピックについて説明します。

[DMA 操作中にキャッシュされたデータのフラッシュ](flushing-cached-data-during-dma-operations.md)

[PIO 操作中にキャッシュされたデータのフラッシュ](flushing-cached-data-during-pio-operations.md)

 

 




