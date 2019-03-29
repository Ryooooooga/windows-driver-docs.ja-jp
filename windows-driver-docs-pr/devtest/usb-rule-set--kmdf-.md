---
title: Usb ルール セット (KMDF)
description: これらの規則を使用するには、ドライバーが USB デバイスの一部の特殊な KMDF メソッドを正しく処理することを確認します。
ms.assetid: E07F4E18-CE93-43A8-AAB4-C3CF8CC790CC
ms.date: 05/21/2018
ms.localizationpriority: medium
ms.openlocfilehash: 7fea3eafe6dfe5e6c9a87683cd7440b83af6142e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56548938"
---
# <a name="usb-rule-set-kmdf"></a>Usb ルール セット (KMDF)


これらの規則を使用するには、ドライバーが USB デバイスの一部の特殊な KMDF メソッドを正しく処理することを確認します。

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
<td align="left"><p><a href="kmdf-faild0entryiotargetstate.md" data-raw-source="[&lt;strong&gt;FailD0EntryIoTargetState&lt;/strong&gt;](kmdf-faild0entryiotargetstate.md)"><strong>FailD0EntryIoTargetState</strong></a></p></td>
<td align="left"><p><a href="kmdf-faild0entryiotargetstate.md" data-raw-source="[&lt;strong&gt;FailD0EntryIoTargetState&lt;/strong&gt;](kmdf-faild0entryiotargetstate.md)"> <strong>FailD0EntryIoTargetState</strong> </a>ルール内で USB の継続的なリーダー対象が I/O が開始されたことを指定します、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff540848" data-raw-source="[&lt;em&gt;EvtDeviceD0Entry&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540848)"> <em>EvtDeviceD0Entry</em> </a>は取得停止適切に、同じコールバックの場合、 <em>EvtDeviceD0Entry</em>は失敗します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-usbcontreader.md" data-raw-source="[&lt;strong&gt;UsbContReader&lt;/strong&gt;](kmdf-usbcontreader.md)"><strong>UsbContReader</strong></a></p></td>
<td align="left"><p><a href="kmdf-usbcontreader.md" data-raw-source="[&lt;strong&gt;UsbContReader&lt;/strong&gt;](kmdf-usbcontreader.md)"> <strong>UsbContReader</strong> </a>ルールでは、ドライバー内で、継続的なリーダーが正しく構成されているを指定します&#39;s <a href="https://msdn.microsoft.com/library/windows/hardware/ff540880" data-raw-source="[&lt;em&gt;EvtDevicePrepareHardware&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540880)"> <em>EvtDevicePrepareHardware</em></a>ドライバーへの呼び出しは、場所、イベントのコールバック関数、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff551130" data-raw-source="[&lt;strong&gt;WdfUsbTargetPipeConfigContinuousReader&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551130)"> <strong>WdfUsbTargetPipeConfigContinuousReader</strong> </a>メソッド。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-usbdevicecreate.md" data-raw-source="[&lt;strong&gt;UsbDeviceCreate&lt;/strong&gt;](kmdf-usbdevicecreate.md)"><strong>UsbDeviceCreate</strong></a></p></td>
<td align="left"><p><a href="kmdf-usbdevicecreate.md" data-raw-source="[&lt;strong&gt;UsbDeviceCreate&lt;/strong&gt;](kmdf-usbdevicecreate.md)"> <strong>UsbDeviceCreate</strong> </a>ルールでは、ことを指定します、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff550077" data-raw-source="[&lt;strong&gt;WdfUsbTargetDeviceCreate&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550077)"> <strong>WdfUsbTargetDeviceCreate</strong> </a>と<a href="https://msdn.microsoft.com/library/windows/hardware/hh439428" data-raw-source="[&lt;strong&gt;WdfUsbTargetDeviceCreateWithParameters&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh439428)"> <strong>WdfUsbTargetDeviceCreateWithParameters</strong> </a>の外側のメソッドを呼び出さない、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff540880" data-raw-source="[&lt;em&gt;EvtDevicePrepareHardware&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540880)"> <em>EvtDevicePrepareHardware</em> </a>イベント コールバック関数。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-usbdevicecreatefail.md" data-raw-source="[&lt;strong&gt;UsbDeviceCreateFail&lt;/strong&gt;](kmdf-usbdevicecreatefail.md)"><strong>UsbDeviceCreateFail</strong></a></p></td>
<td align="left"><p><a href="kmdf-usbdevicecreatefail.md" data-raw-source="[&lt;strong&gt;UsbDeviceCreateFail&lt;/strong&gt;](kmdf-usbdevicecreatefail.md)"> <strong>UsbDeviceCreateFail</strong> </a>ルールでは、ドライバーがから返すことを指定します、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff540880" data-raw-source="[&lt;em&gt;EvtDevicePrepareHardware&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540880)"> <em>EvtDevicePrepareHardware</em> </a>イベント コールバックWDFUSBDEVICE オブジェクトの作成が失敗した場合はエラー状態の関数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-usbdevicecreatetarget.md" data-raw-source="[&lt;strong&gt;UsbDeviceCreateTarget&lt;/strong&gt;](kmdf-usbdevicecreatetarget.md)"><strong>UsbDeviceCreateTarget</strong></a></p></td>
<td align="left"><p><a href="kmdf-usbdevicecreatetarget.md" data-raw-source="[&lt;strong&gt;UsbDeviceCreateTarget&lt;/strong&gt;](kmdf-usbdevicecreatetarget.md)"> <strong>UsbDeviceCreateTarget</strong> </a>ルールでは、デバイス コンテキストでは現在 WDFUSBDEVICE オブジェクトがリーク中に複数 WDFUSBDEVICE オブジェクトが作成しないことを指定します。</p></td>
</tr>
</tbody>
</table>

 

**Usb のルールを選択するには、次のように設定します。**

1.  Microsoft Visual Studio で、ドライバーのプロジェクト (.vcxProj) を選択します。 **ドライバー**  メニューのをクリックして**Static Driver Verifier を起動しています**.

2.  をクリックして、**ルール**タブ。**規則セット**、 **Usb**します。

    Visual Studio の開発者コマンド プロンプト ウィンドウから既定のルールを選択するには、次のように指定します。 **Usb.sdv**で、 **/check**オプション。 次に、例を示します。

    ```
    msbuild /t:sdv /p:Inputs="/check:Usb.sdv" mydriver.VcxProj /p:Configuration="Win8 Release" /p:Platform=Win32
    ```

    詳細については、次を参照してください。[ドライバーで障害を検出する Static Driver Verifier を使用して](https://msdn.microsoft.com/library/windows/hardware/hh454281)と[Static Driver Verifier のコマンド (MSBuild)](https://msdn.microsoft.com/library/windows/hardware/hh466459)します。

 

 




