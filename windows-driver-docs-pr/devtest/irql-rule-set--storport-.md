---
title: Irql の規則セット (Storport)
description: これらの規則を使用すると、ドライバーが必要な IRQL で DDI 呼び出しを行うことを確認します。IRQL の規則に従っていないドライバーは、デッドロック状態またはコンピューターがクラッシュする可能性のある操作中に重大な問題を発生することができます。
ms.assetid: 3322200A-2073-4568-B1FC-481B216D8F61
ms.date: 05/21/2018
ms.localizationpriority: medium
ms.openlocfilehash: 17d6c8f838e8662ed7963477468cad197072e0ee
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373670"
---
# <a name="irql-rule-set-storport"></a>Irql の規則セット (Storport)


これらの規則を使用すると、ドライバーが必要な IRQL で DDI 呼び出しを行うことを確認します。

IRQL の規則に従っていないドライバーは、デッドロック状態またはコンピューターがクラッシュする可能性のある操作中に重大な問題を発生することができます。

## <a name="in-this-section"></a>このセクションの内容


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">トピック</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="storport-irqldispatch.md" data-raw-source="[&lt;strong&gt;IrqlDispatch&lt;/strong&gt;](storport-irqldispatch.md)"><strong>IrqlDispatch</strong></a></p></td>
<td align="left"><p>このルールは、次のルーチンがでのみ呼び出されることを確認します。 <strong>IRQL = DISPATCH_LEVEL</strong>します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="storport-irqlkereleasespinlock.md" data-raw-source="[&lt;strong&gt;IrqlKeReleaseSpinLock&lt;/strong&gt;](storport-irqlkereleasespinlock.md)"><strong>IrqlKeReleaseSpinLock</strong></a></p></td>
<td align="left"><p>このルールはことを確認します<strong>KeReleaseSpinLock</strong>で呼び出される<strong>IRQL = DISPATCH_LEVEL</strong>のみです。 前の IRQL レベルに、IRQL も設定があります。 通常この呼び出しの呼び出し前は<strong>KeAcquireSpinLock</strong>します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="storport-spchangeirql.md" data-raw-source="[&lt;strong&gt;SpChangeIrql&lt;/strong&gt;](storport-spchangeirql.md)"><strong>SpChangeIrql</strong></a></p></td>
<td align="left"><p>このルールは、呼び出される位置のレベルと同じ IRQL レベル、StorPort コールバック ルーチンを返すことを確認します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="storport-spirql.md" data-raw-source="[&lt;strong&gt;SpIrql&lt;/strong&gt;](storport-spirql.md)"><strong>SpIrql</strong></a></p></td>
<td align="left"><p>このルールを検証するルーチン<strong>TdiRegisterPnPHandlers</strong>と<strong>TdiDeregisterPnPHandlers</strong>のみ呼び出される IRQL でよりも低い<strong>DISPATCH_LEVEL</strong>。 ただし場合、 <strong>ExFreeToNPagedLookasideList</strong>を呼び出すと、ルール パス。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="storport-storportirql.md" data-raw-source="[&lt;strong&gt;StorPortIrql&lt;/strong&gt;](storport-storportirql.md)"><strong>StorPortIrql</strong></a></p></td>
<td align="left"><p><a href="storport-storportirql.md" data-raw-source="[&lt;strong&gt;StorPortIrql&lt;/strong&gt;](storport-storportirql.md)"> <strong>StorPortIrql</strong> </a>ルールが StorPort ルーチンが、適切な IRQL レベルと呼ばれることを確認します。</p></td>
</tr>
</tbody>
</table>

 

**Irql ルールを選択するには、次のように設定します。**

1.  Microsoft Visual Studio で、ドライバーのプロジェクト (.vcxProj) を選択します。 **ドライバー**  メニューのをクリックして**Static Driver Verifier を起動しています**.

2.  をクリックして、**ルール**タブ。**規則セット**、 **Irql**します。

    Visual Studio の開発者コマンド プロンプト ウィンドウから既定のルールを選択するには、次のように指定します。 **Irql.sdv**で、 **/check**オプション。 以下に例を示します。

    ```
    msbuild /t:sdv /p:Inputs="/check:Irql.sdv" mydriver.VcxProj /p:Configuration="Win8 Release" /p:Platform=Win32
    ```

    詳細については、次を参照してください。[ドライバーで障害を検出する Static Driver Verifier を使用して](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers)と[Static Driver Verifier のコマンド (MSBuild)](https://docs.microsoft.com/windows-hardware/drivers/devtest/-static-driver-verifier-commands--msbuild-)します。

 

 





