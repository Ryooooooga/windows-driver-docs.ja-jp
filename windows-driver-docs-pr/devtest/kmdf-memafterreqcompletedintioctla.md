---
title: MemAfterReqCompletedIntIoctlA ルール (kmdf)
description: MemAfterReqCompletedIntIoctlA ルールは、EvtIoInternalDeviceControl コールバック関数内で、i/o 要求の完了後にフレームワークメモリオブジェクトにアクセスできないことを指定します。
ms.assetid: ff64d344-8b8e-4dec-adc3-d1e99f737e8a
ms.date: 05/21/2018
keywords:
- MemAfterReqCompletedIntIoctlA ルール (kmdf)
topic_type:
- apiref
api_name:
- MemAfterReqCompletedIntIoctlA
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 86e0d8cb6e87e9b5f9dd97427867fc1c336caf7c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839471"
---
# <a name="memafterreqcompletedintioctla-rule-kmdf"></a>MemAfterReqCompletedIntIoctlA ルール (kmdf)


**MemAfterReqCompletedIntIoctlA**ルールは、 [*Evtiointernaldevicecontrol*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_internal_device_control)コールバック関数内で、i/o 要求の完了後にフレームワークメモリオブジェクトにアクセスできないことを指定します。

ドライバーの*Evtiointernaldevicecontrol*コールバック関数内で、 [**WdfRequestRetrieveInputMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestretrieveinputmemory)メソッドまたは[**WdfRequestRetrieveOutputMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestretrieveoutputmemory)メソッドを呼び出すことによって取得されたフレームワークメモリオブジェクトにアクセスできません。[**Wdfrequestcomplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcomplete)を呼び出した後、 [**wdfrequestcompletewithinformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcompletewithinformation)または[**Wdfrequestcompletewith優先順位**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcompletewithpriorityboost)が i/o 要求によってブーストされます。

この規則は、次のメモリアクセス方法を考慮します。

[**WdfMemoryGetBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfmemory/nf-wdfmemory-wdfmemorygetbuffer)
[**WDF\_メモリ\_記述子\_INIT\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfmemory/nf-wdfmemory-wdf_memory_descriptor_init_handle)
[**Wdfmemory割り当てバッファー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfmemory/nf-wdfmemory-wdfmemoryassignbuffer)
[**wdfmemorycopytobuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfmemory/nf-wdfmemory-wdfmemorycopytobuffer)
[**WdfMemoryCopyFromBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfmemory/nf-wdfmemory-wdfmemorycopyfrombuffer)
[**Wdfobjectreference**](https://docs.microsoft.com/windows-hardware/drivers/wdf/wdfobjectreference)
[**wdfobject逆**](https://docs.microsoft.com/windows-hardware/drivers/wdf/wdfobjectdereference)参照
[**wdfobjectdelete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/nf-wdfobject-wdfobjectdelete)

|              |      |
|--------------|------|
| ドライバー モデル | KMDF |

<a name="how-to-test"></a>テスト方法
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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">静的ドライバー検証ツール</a>を実行し、 <strong>MemAfterReqCompletedIntIoctlA</strong>規則を指定します。</p>
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

[**WDF\_メモリ\_記述子\_初期化\_ハンドル**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfmemory/nf-wdfmemory-wdf_memory_descriptor_init_handle)
[**Wdfmemoryの割り当てバッファー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfmemory/nf-wdfmemory-wdfmemoryassignbuffer)
Wdfmemorycopyfrombuffer
[**Wdfmemorycopytobuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfmemory/nf-wdfmemory-wdfmemorycopytobuffer) [](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfmemory/nf-wdfmemory-wdfmemorycopyfrombuffer)
[**WdfMemoryGetBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfmemory/nf-wdfmemory-wdfmemorygetbuffer)
Wdfobjectdelete
[](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/nf-wdfobject-wdfobjectdelete) [**Wdfobjectreference**](https://docs.microsoft.com/windows-hardware/drivers/wdf/wdfobjectdereference)
wdfrequestcomplete
[](https://docs.microsoft.com/windows-hardware/drivers/wdf/wdfobjectreference) [**wdfrequestcompletewithinformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcomplete)
[](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcompletewithinformation)_t_33_ [**WdfrequestcompletewithWdfRequestRetrieveInputMemory ブースト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcompletewithpriorityboost)
[](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestretrieveinputmemory)
[**WdfRequestRetrieveOutputMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestretrieveoutputmemory)









