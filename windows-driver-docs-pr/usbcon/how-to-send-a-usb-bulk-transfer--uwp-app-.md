---
Description: USB 一括転送と USB デバイスと通信する UWP アプリからの転送要求を開始する方法について説明します。
title: USB バルク転送要求の送信方法 (UWP アプリ)
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 88c294772aa685d17a97cfdd09d2e43b290d001f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67363892"
---
# <a name="how-to-send-a-usb-bulk-transfer-request-uwp-app"></a>USB バルク転送要求の送信方法 (UWP アプリ)

このトピックでは、USB 一括転送と USB デバイスと通信する UWP アプリからの転送要求を開始する方法について学習します。

USB フル_スピード、高速および SuperSpeed デバイスは、一括のエンドポイントをサポートできます。 これらのエンドポイントは、大量転送する、または USB フラッシュ ドライブからデータを転送するなどのデータを転送するために使用されます。 一括転送では、エラーの検出を許可するので、信頼性の高いし、データが、ホストまたはデバイスで受信したかどうかを確認する再試行回数制限にはが含まれます。 時刻が重要なデータを一括転送が使用されます。 使用されていない帯域幅が使用可能なバスの場合にのみ、データが転送されます。 そのため、その他の転送でビジー状態に、バスは、データの一括が無期限に待機できます。

一括のエンドポイントが一方向であり、データ転送は 1 つで、IN または OUT の方向にも転送されます。 一括データの読み取りと書き込みをサポートするには、デバイスは、一括 IN および OUT エンドポイント一括をサポートする必要があります。 一括のエンドポイントは、ホストからデバイスへのデータを送信するデバイスからデータをホストと外部エンドポイントの一括が使用される読み取りに使用されます。

一括転送要求を開始するには、アプリはへの参照が必要、*パイプ*を表すエンドポイント。 パイプは、デバイスが構成されている場合、デバイス ドライバーによって開かれた通信チャネルです。 アプリでは、パイプは、エンドポイントの論理表現です。 エンドポイントからデータを読み取るには、アプリは、関連付けられている一括 IN パイプからデータを取得します。 エンドポイントにデータを書き込むには、アプリは、データをパイプを一括に送信します。 一括読み、パイプの書き込みは、使用[ **UsbBulkInPipe** ](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbBulkInPipe)と[ **UsbBulkOutPipe** ](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbBulkOutPipe)クラス。

アプリは、特定のポリシーのフラグを設定して、パイプの動作を変更することができますも。 たとえば、読み取り要求をパイプで停止状態を自動的にクリアするフラグを設定できます。 これらのフラグについては、次を参照してください。 [ **UsbReadOptions** ](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbReadOptions)と[ **UsbWriteOptions**](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbWriteOptions)します。

## <a name="before-you-start"></a>開始前の作業

* 必要がある場合、デバイスを開くし、取得、 [ **UsbDevice** ](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbDevice)オブジェクト。 読み取り[USB デバイス (UWP アプリ) に接続する方法](how-to-connect-to-a-usb-device--uwp-app-.md)します。
* このトピックで示すように完全なコードを確認できます、 [CustomUsbDeviceAccess サンプル](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/CustomUsbDeviceAccess)、Scenario4\_BulkPipes ファイル。

## <a name="step-1-get-the-bulk-pipe-object"></a>手順 1:一括パイプ オブジェクトを取得します。

譲渡要求を開始するには、一括パイプ オブジェクトへの参照を取得する必要があります ([**UsbBulkOutPipe** ](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbBulkOutPipe)または[ **UsbBulkInPipe**](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbBulkInPipe))。 パイプは、すべてのインターフェイスのすべての設定を列挙することによって取得できます。 ただし、データ転送、アクティブな設定のパイプのみ使用する必要があります。 パイプ オブジェクトがアクティブな設定に関連付けられているエンドポイントがない場合は null の場合は。

<table>
  <thead>
    <tr>
      <th>目的の処理</th>
      <th>このプロパティの値を使用して、</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <tr>
      <td rowspan="5">一括パイプにデータを送信するへの参照を取得<a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbBulkOutPipe"> <strong>UsbBulkOutPipe</strong></a>します。</td>
      </tr>
      <tr>
      <td><a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbInterface#Windows_Devices_Usb_UsbInterface_BulkOutPipes"><strong>UsbDevice.DefaultInterface.BulkOutPipes[n]</strong> </a>デバイスの構成が 1 つの USB インターフェイスを公開している場合。</td>
      </tr>
      <tr>
      <td><a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbInterface#Windows_Devices_Usb_UsbInterface_BulkOutPipes"><strong>UsbDevice.Configuration.UsbInterfaces[m]。[N] BulkOutPipes</strong></a>) デバイスでサポートされている複数のインターフェイスでパイプ一括を列挙するためです。</td>
      </tr>
       <td><a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbInterruptOutEndpointDescriptor#Windows_Devices_Usb_UsbInterruptOutEndpointDescriptor_Pipe"><strong>UsbInterface.InterfaceSettings\[m\]します。BulkOutEndpoints [n]。パイプ</strong></a>インターフェイスの設定によって定義されているパイプ一括を列挙するためです。</td>
      </tr>
      <tr>
      <td><a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbInterruptOutEndpointDescriptor#Windows_Devices_Usb_UsbInterruptOutEndpointDescriptor_Pipe"><strong>UsbEndpointDescriptor.AsBulkOutEndpointDescriptor.Pipe</strong> </a>の大部分は外部エンドポイントのエンドポイント記述子からパイプ オブジェクトを取得します。
      </td>
      </tr>
    </tr>
    <tr>
      <tr>
        <td rowspan="5">一括パイプからデータを受信、取得することができます、 <a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbBulkInPipe"> <strong>UsbBulkInPipe</strong> </a>オブジェクト</td>
      </tr>
       <tr>
        <td><a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbInterface#Windows_Devices_Usb_UsbInterface_BulkInPipes"><strong>UsbDevice.DefaultInterface.BulkInPipes[n]</strong> </a>デバイスの構成が 1 つの USB インターフェイスを公開している場合。</td>
       </tr>
       <tr>
       <td><a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbInterface#Windows_Devices_Usb_UsbInterface_BulkInPipes"><strong>UsbDevice.Configuration.UsbInterfaces[m]。[N] BulkInPipes</strong> </a>デバイスでサポートされている複数のインターフェイスに一括でパイプを列挙するためです。</td>
       </tr>
       <tr>
       <td><a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbBulkInEndpointDescriptor#Windows_Devices_Usb_UsbBulkInEndpointDescriptor_Pipe"><strong>UsbInterface.InterfaceSettings[m]。BulkInEndpoints [n]。パイプ</strong></a>インターフェイスの設定によって定義されている一括のパイプを列挙するためです。</td>
       </tr>
       <tr>
        <td><a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbBulkInEndpointDescriptor#Windows_Devices_Usb_UsbBulkInEndpointDescriptor_Pipe"><strong>UsbEndpointDescriptor.AsBulkInEndpointDescriptor.Pipe</strong> </a>一括のエンドポイントのエンドポイント記述子からパイプ オブジェクトを取得するためです。</td>
      </tr>
    </tr>
  </tbody>
</table>

注: アクティブな設定にするか、または null チェックが必要です。

## <a name="step-2-configure-the-bulk-pipe-optional"></a>手順 2:一括パイプ (省略可能) を構成します。

読み取りの動作を変更したり、取得した一括パイプで特定のフラグを設定して操作を記述できます。

デバイスからの読み取り、設定、 [ **UsbBulkInPipe.ReadOptions** ](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbBulkInPipe#Windows_Devices_Usb_UsbBulkInPipe_ReadOptions)プロパティで定義されている値のいずれかを[ **UsbReadOptions**](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbReadOptions)します。 書き込みの場合は、設定、 [ **UsbBulkOutPipe.WriteOptions** ](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbBulkOutPipe#Windows_Devices_Usb_UsbBulkOutPipe_WriteOptions)プロパティで定義されている値のいずれかを**UsbWriteOptions**します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>目的の処理</th>
<th>このフラグを設定します。</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>データ フローを停止することがなく、エンドポイント上の任意のエラー条件を自動的にクリアします。</p></td>
<td><strong>AutoClearStall</strong>
<p>詳細については、次を参照してください。<a href="#clearing-stall-conditions">消去しています区画条件</a>します。 このフラグは、転送の読み書きの両方に適用されます。</p></td>
</tr>
<tr class="even">
<td><p>効率を最大限に複数の読み取り要求を送信します。 パフォーマンスを向上するには、エラー チェックをバイパスします。</p></td>
<td><strong>OverrideAutomaticBufferManagement</strong>
<p>データ要求は、各転送と呼ばれるバイト数が含まれている 1 つまたは複数の転送に分けることが、<em>最大転送サイズ</em>します。 複数の転送の遅延が発生可能性がある、ドライバーによって実行されるエラー チェックのためのキューの 2 つ転送。 このフラグは、そのエラーのチェックをバイパスします。 最大転送サイズを取得するには、使用、 <a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbBulkInPipe#Windows_Devices_Usb_UsbBulkInPipe_MaxTransferSizeBytes" data-raw-source="[&lt;strong&gt;UsbBulkInPipe.MaxTransferSizeBytes&lt;/strong&gt;](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbBulkInPipe#Windows_Devices_Usb_UsbBulkInPipe_MaxTransferSizeBytes)"> <strong>UsbBulkInPipe.MaxTransferSizeBytes</strong> </a>プロパティ。 要求のサイズが場合<strong>UsbBulkInPipe.MaxTransferSizeBytes</strong>、このフラグを設定する必要があります。 注:</p>
<p></p>
<div class="alert">
<strong>重要</strong><br/><p>このフラグを設定した場合は、パイプの最大パケット サイズの倍数でのデータを要求する必要があります。 その情報は、エンドポイントの記述子に格納されます。 サイズは、デバイスのバス速度に依存します。 フル_スピード、高速および SuperSpeed;最大パケット サイズは、それぞれ 64、512、1024 バイトです。 その値を取得する、 <a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbBulkInEndpointDescriptor#Windows_Devices_Usb_UsbBulkInEndpointDescriptor_MaxPacketSize" data-raw-source="[&lt;strong&gt;UsbBulkInPipe.EndpointDescriptor.MaxPacketSize&lt;/strong&gt;](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbBulkInEndpointDescriptor#Windows_Devices_Usb_UsbBulkInEndpointDescriptor_MaxPacketSize)"> <strong>UsbBulkInPipe.EndpointDescriptor.MaxPacketSize</strong> </a>プロパティ。</p>
</div>
<div>

</div>
このフラグは、読み取り転送にのみ適用されます。</td>
</tr>
<tr class="odd">
<td><p>長さ 0 のパケットの書き込み要求を終了します。</p></td>
<td><strong>ShortPacketTerminate</strong>
<p>長さゼロのパケットを転送の終了を示すを送信します。このフラグは、書き込み転送にのみ適用されます。</p></td>
</tr>
<tr class="even">
<td><p>短いパケット (より小さい最大パケット サイズが、エンドポイントでサポートされている) を無効にします。</p></td>
<td><strong>IgnoreShortPacket</strong>
<p>既定では、デバイスが、パケットの最大サイズ未満のバイトを送信する場合、アプリがそれらを受け取る。 短いパケットを受信しない場合は、このフラグを設定します。</p>
<p>このフラグは、読み取り転送にのみ適用されます。</p></td>
</tr>
</tbody>
</table>

## <a name="step-3-set-up-the-data-stream"></a>手順 3:データ ストリームを設定します。

デバイスで一括データを送信すると、一括パイプで入力ストリームのように、データを受信しました。 入力ストリームを取得するための手順を次に示します。

1. 取得することによって、入力ストリームへの参照を取得、 [ **UsbBulkInPipe.InputStream** ](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbBulkInPipe#Windows_Devices_Usb_UsbBulkInPipe_InputStream)プロパティ。
2. 作成、 [ **DataReader** ](https://docs.microsoft.com/uwp/api/Windows.Storage.Streams.DataReader)オブジェクト内の入力ストリームを指定することによって、 [ **DataReader コンス トラクター**](https://docs.microsoft.com/uwp/api/Windows.Storage.Streams.DataReader#Windows_Storage_Streams_DataReader__ctor_Windows_Storage_Streams_IInputStream_)します。

デバイスにデータの書き込みに、アプリは一括パイプで出力ストリームに書き込む必要があります。 出力ストリームを準備する手順を次に示します。

1. 出力ストリームへの参照を取得することによって取得、 [ **UsbBulkOutPipe.OutputStream** ](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbBulkOutPipe#Windows_Devices_Usb_UsbBulkOutPipe_OutputStream)プロパティ。
2. 作成、 [ **datawriter の各**](https://docs.microsoft.com/uwp/api/Windows.Storage.Streams.DataWriter)オブジェクト内の出力ストリームを指定することによって、 [ **datawriter の各**](https://docs.microsoft.com/uwp/api/Windows.Storage.Streams.DataWriter#Windows_Storage_Streams_DataWriter__ctor_Windows_Storage_Streams_IOutputStream_)コンス トラクター。
3. 出力ストリームに関連付けられているデータ バッファーを設定します。
4. によって、データ型のデータ転送、出力ストリームに書き込む呼び出して[ **datawriter の各メソッド**](https://docs.microsoft.com/uwp/api/Windows.Storage.Streams.DataWriter#Windows_Storage_Streams_DataWriter__ctor_Windows_Storage_Streams_IOutputStream_)など[ **WriteBytes**](https://docs.microsoft.com/uwp/api/Windows.Storage.Streams.DataWriter#Windows_Storage_Streams_DataWriter_WriteBytes_System_Byte___)します。

## <a name="step-4-start-an-asynchronous-transfer-operation"></a>手順 4:非同期転送操作を開始します。

非同期操作を一括転送が開始されます。

一括データの読み取りを呼び出して、非同期読み取り操作を開始します。 [ **DataReader.LoadAsync**](https://docs.microsoft.com/uwp/api/Windows.Storage.Streams.DataReader#Windows_Storage_Streams_DataReader_LoadAsync_System_UInt32_)します。

大量のデータを書き込む非同期書き込み操作を呼び出すことにより開始[ **DataWriter.StoreAsync**](https://docs.microsoft.com/uwp/api/Windows.Storage.Streams.DataWriter#Windows_Storage_Streams_DataWriter_StoreAsync)します。

## <a name="step-5-get-results-of-the-read-transfer-operation"></a>手順 5:読み取り転送操作の結果を取得します。

データの非同期操作が完了した後は、読み取りまたは書き込みタスク オブジェクトからバイトの数を取得できます。 読み取り操作では、呼び出す[ **DataReader メソッド**](https://docs.microsoft.com/uwp/api/Windows.Storage.Streams.DataReader)など[ **ReadBytes**](https://docs.microsoft.com/uwp/api/Windows.Storage.Streams.DataReader#Windows_Storage_Streams_DataReader_ReadBytes_System_Byte___)、入力ストリームからデータを読み取る。

## <a name="clearing-stall-conditions"></a>停止条件の消去

アプリには、失敗したデータ転送があります。 失敗した転送は、エンドポイントの停止条件が原因でことができます。 エンドポイントが停止している限り、データに書き込まれるまたはからの読み取りことはできません。 データ転送を続行するには、アプリは、関連するパイプの停止条件をクリアする必要があります。

アプリが発生したときに、停止条件を自動的にクリアするパイプを構成できます。 これを行うには、設定、 [ **UsbBulkInPipe.ReadOptions** ](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbBulkInPipe#Windows_Devices_Usb_UsbBulkInPipe_ReadOptions)プロパティを**UsbReadOptions.AutoClearStall**または[ **UsbBulkOutPipe.WriteOptions** ](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbBulkOutPipe#Windows_Devices_Usb_UsbBulkOutPipe_WriteOptions)プロパティを**UsbWriteOptions.AutoClearStall**します。 その自動構成では、アプリでは、失敗した転送は発生しませんし、データ転送のエクスペリエンスがシームレスにします。

停止状態を手動で消去するには、呼び出す[ **UsbBulkInPipe.ClearStallAsync** ](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbInterruptInPipe#Windows_Devices_Usb_UsbInterruptInPipe_ClearStallAsync)一括 IN パイプ; 呼び出す[ **UsbBulkOutPipe.ClearStallAsync** ](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbBulkOutPipe#Windows_Devices_Usb_UsbBulkOutPipe_ClearStallAsync)一括をパイプします。

**注**停止状態には、空のエンドポイントは示しません。 エンドポイントにデータがない場合は、転送が完了したが、長さがゼロ バイト。

読み取り操作の場合は、新しい転送要求を開始する前に保留中のパイプにデータをクリアする必要があります。 これを行うには、呼び出す[ **UsbBulkInPipe.FlushBuffer** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff551975(v=vs.85))メソッド。

## <a name="usb-bulk-transfer-code-example"></a>USB 一括転送のコード例

このコード例では、一括パイプに書き込む方法を示します。 例では、既定のインターフェイスのパイプを最初の一括データを送信します。 転送の最後に、長さ 0 のパケットを送信するパイプが構成されます。 転送が完了したら、バイト数が表示されます。

```CSharp
    private async void BulkWrite()
    {
        String dataBuffer = "Hello World!";
        UInt32 bytesWritten = 0;

        UsbBulkOutPipe writePipe = usbDevice.DefaultInterface.BulkOutPipes[0];
        writePipe.WriteOptions |= UsbWriteOptions.ShortPacketTerminate;

        var stream = writePipe.OutputStream;

        DataWriter writer = new DataWriter(stream);

        writer.WriteString(dataBuffer);

        try
        {
            bytesWritten = await writer.StoreAsync();
        }
        catch (Exception exception)
        {
            ShowStatus(exception.Message.ToString());
        }
        finally
        {
            ShowStatus("Data written: " + bytesWritten + " bytes.");
        }
    }
```

このコード例では、一括パイプから読み取る方法を示します。 この例では、既定のインターフェイスの最初の一括でパイプからデータを取得します。 効率を最大化するパイプを構成しますパケットの最大サイズのチャンク単位でデータを受信して。 転送が完了したら、バイト数が表示されます。

```CSharp
    private async void BulkRead()
    {
        UInt32 bytesRead = 0;

        UsbBulkInPipe readPipe = usbDevice.DefaultInterface.BulkInPipes[0];
        readPipe.ReadOptions |= UsbReadOptions.IgnoreShortPacket;

        var stream = readPipe.InputStream;
        DataReader reader = new DataReader(stream);

        try
        {
            bytesRead = await reader.LoadAsync(readPipe.EndpointDescriptor.MaxPacketSize);
        }
        catch (Exception exception)
        {
            ShowStatus(exception.Message.ToString());
        }
        finally
        {
            ShowStatus("Number of bytes: " + bytesRead);

            IBuffer buffer = reader.ReadBuffer(bytesRead);

            ShowData (buffer.ToString());

        }
    }
```
