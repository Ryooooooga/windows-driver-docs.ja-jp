---
title: RemoveLockMnRemove ルール (wdm)
description: RemoveLockMnRemove ルールは、IoAcquireRemoveLock および IoReleaseRemoveLockAndWait への呼び出しが、MinorFunction\_IRP を使用して\_PNP を\_処理するときに正しく使用されることを確認し、\_デバイス\_削除します。
ms.assetid: 3BB367F0-AAF7-4A9E-B642-BA839DDCAA4E
ms.date: 05/21/2018
keywords:
- RemoveLockMnRemove ルール (wdm)
topic_type:
- apiref
api_name:
- RemoveLockMnRemove
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 398840e480b4dded1d6775f28eefa3f974690664
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839869"
---
# <a name="removelockmnremove-rule-wdm"></a>RemoveLockMnRemove ルール (wdm)


**RemoveLockMnRemove**ルールは、 [**IoAcquireRemoveLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioacquireremovelock)および[**IoReleaseRemoveLockAndWait**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreleaseremovelockandwait)への呼び出しが、minorfunction\_irp で\_PNP を\_処理するときに正しく使用されるかどうかを検証\_削除\_デバイス。

このルールは、FDO および FIDO ドライバーにのみ適用されます。

たとえば、フィルタードライバー、FDO、および PDO で構成される PnP ドライバースタックを考えてみます。

PnP マネージャーは、スタックを通じて削除クエリを送信します。 システムの実行中は、FDO がアイドル状態になります。 FDO は、クエリの削除された状態の電源を切り、d0 IRP を要求します。 D0 IRP が到着する前に、PnP マネージャーは PnP の削除 IRP を送信し、その IRP はフィルタードライバーによって処理されます。 フィルタードライバーはスタックからデタッチし、その状態をクリーンアップします。 D0 はスタックの一番上に到達しますが、フィルタードライバーは、それを送信する場所を認識するためのコンテキストまたはデータがないため、スタックには送信しません。 FDO が、d0 IRP が到着するのを待機している間にハングしていますが、その IRP は停止しません。

**このエラーを回避するには**

1.  デバイスがデバイススタックからデタッチされる前に、 [**IoAcquireRemoveLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioacquireremovelock)は irp が次の種類の irp に対してスタックに転送される前に成功する必要があります。

    -   IRP\_\_クエリ\_削除
    -   IRP\_\_SUPRISE 削除\_
    -   IRP\_\_\_デバイスの削除

2.  [**IoDetachDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iodetachdevice)または[**iodeletedevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iodeletedevice)を呼び出す前に、 [**IoReleaseRemoveLockAndWait**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreleaseremovelockandwait)を呼び出す必要があります。 (これにより、すべての削除ロックがデバイスドライバーで確実に解放されます)。

|              |     |
|--------------|-----|
| ドライバーモデル | WDM |

<a name="how-to-test"></a>テストする方法
-----------

<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">コンパイル時</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">静的ドライバー検証ツール</a>を実行し、 <strong>RemoveLockMnRemove</strong>規則を指定します。</p>
コードの分析を実行するには、次の手順に従います。
<ol>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code" data-raw-source="[Prepare your code (use role type declarations).](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code)">コードを準備します (ロールの種類の宣言を使用します)。</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier" data-raw-source="[Run Static Driver Verifier.](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier)">静的ドライバー検証ツールを実行します。</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results" data-raw-source="[View and analyze the results.](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results)">結果を表示して分析します。</a></li>
</ol>
<p>詳細については、「 <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers" data-raw-source="[Using Static Driver Verifier to Find Defects in Drivers](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers)">Static Driver Verifier を使用したドライバーの欠陥の検出</a>」を参照してください。</p></td>
</tr>
</tbody>
</table>

<a name="applies-to"></a>適用対象
----------

[**IoAcquireRemoveLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioacquireremovelock)
[**IoReleaseRemoveLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreleaseremovelock)
[**IoReleaseRemoveLockAndWait**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreleaseremovelockandwait)
[**removeヘッドの一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-removeheadlist)
 

 





