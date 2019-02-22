---
title: SPB の I/O 要求
description: これらの Ioctl は、コント ローラーのドライバーによって処理されるクライアント (周辺ドライバー) によって送信されます。
ms.assetid: 4b8ed75e-1f03-4b7a-ad9d-0dfa9b20274c
ms.date: 11/29/2017
ms.localizationpriority: medium
ms.openlocfilehash: 019da4445482ffffe61e6117e0d17eff1a478ce4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56550443"
---
# <a name="spb-io-requests"></a>SPB の I/O 要求
システム提供 CTL_CODE マクロを定義する I/O 制御コードに記載されてを使用して、Spb.h で IOCTL_SPB_ * 制御コードを定義します。

|トピック | 説明|
|------|:----------------|
|[IOCTL_SPB_EXECUTE_SEQUENCE](#ioctl-spb-execute-sequence) | IOCTL_SPB_EXECUTE_SEQUENCE I/O 制御コードでは、1 つの I/O 要求で 1 つのアトミック操作として転送 (読み取りと書き込み) のシーケンスを実行する SPB コント ローラーのドライバーのクライアント (周辺ドライバー) できるようにします。 バス上の指定されたデバイスは、シーケンス内のすべての転送の対象です。|
|[IOCTL_SPB_FULL_DUPLEX](#ioctl-spb-full-duplex) | IOCTL_SPB_FULL_DUPLEX 制御コードは、全二重の I/O 操作を要求するクライアント (周辺ドライバー) によって使用されます。 全二重 I/O 操作は、SPI を同時に読み書きできるデータなどのバスのコント ローラーでサポートされます。|
|[IOCTL_SPB_LOCK_CONNECTION](#ioctl-spb-lock-connection) | IOCTL_SPB_LOCK_CONNECTION 制御コードは、クライアント (周辺ドライバー) によって別のクライアントと共有されているターゲットの sp B に接続されているデバイスの接続のロックの取得に使用されます。 クライアントは、接続のロックを保持して、このクライアントでは、デバイスへの排他アクセスがあります。|
|[IOCTL_SPB_LOCK_CONTROLLER](#ioctl-spb-lock-controller) | IOCTL_SPB_LOCK_CONTROLLER 制御コードは、SPB コント ローラーをロックするクライアント (周辺ドライバー) によって使用されます。 コント ローラーがロックされているクライアントがロックを指定したターゲット デバイスにアクセスする bus を排他的に使用します。
|[IOCTL_SPB_UNLOCK_CONNECTION](#ioctl-spb-unlock-connection) | I/O 制御コードは、別のクライアントと共有されているターゲットの sp B に接続されているデバイスの接続のロックを解除するクライアント (周辺ドライバー) によって使用されます。 クライアントは、以前のデバイスへの排他アクセスを取得する IOCTL_SPB_LOCK_CONNECTION 要求を送信します。|
|[IOCTL_SPB_UNLOCK_CONTROLLER](#ioctl-spb-unlock-controller) |IOCTL_SPB_UNLOCK_CONTROLLER I/O 制御コードは、SPB コント ローラーのロックを解除するクライアント (周辺ドライバー) によって使用されます。 クライアントには、bus バス上のターゲット デバイスへのアクセスに排他的に使用できるコント ローラーが以前ロックされています。|

## <a href='#ioctl-spb-execute-sequence' id='ioctl-spb-execute-sequence'>IOCTL_SPB_EXECUTE_SEQUENCE</a>

IOCTL_SPB_EXECUTE_SEQUENCE I/O 制御コードでは、1 つの I/O 要求で 1 つのアトミック操作として転送 (読み取りと書き込み) のシーケンスを実行する SPB コント ローラーのドライバーのクライアント (周辺ドライバー) できるようにします。 バス上の指定されたデバイスは、シーケンス内のすべての転送の対象です。

固定長の転送のシーケンスを指定すると、1 つのアトミック操作として、IOCTL_SPB_EXECUTE_SEQUENCE I/O コントロール要求、I/O の転送を最適化し、パフォーマンスが向上するには、コント ローラー ドライバーを使用できます。

クライアントでは、対象デバイスのファイル オブジェクトをこの I/O 制御要求を送信します。

SPB コント ローラーのドライバーでは、I/O の転送シーケンスの場合、バスの転送を実行する、EvtSpbControllerIoSequence コールバック関数を登録します。 SPB フレームワーク拡張機能 (SpbCx) は、SPB コント ローラーのドライバーの処理に、IOCTL_SPB_EXECUTE_SEQUENCE 要求を渡すには、この関数を呼び出します。

### <a name="input-buffer"></a>入力バッファー
入力バッファーは、クライアントのデータ バッファーへのポインターのリストを含む、SPB_TRANSFER_LIST 構造です。 この一覧には、I/O の転送シーケンスの各転送 (読み取りまたは書き込み) のデータ バッファーが含まれています。
### <a name="input-buffer-length"></a>入力バッファーの長さ
SPB_TRANSFER_LIST 構造体のサイズ。

### <a name="status-block"></a>ステータス ブロック
操作が成功した場合、コント ローラー ドライバーが STATUS_SUCCESS、状態のメンバーに設定し、情報メンバーをシーケンス中に転送されたバイト数の合計数に設定します。

この操作が失敗するリソースの不足、無効なクライアントの入力、およびデバイスの誤動作に含めることができますが、さまざまな理由です。

I/O 要求を処理するコント ローラー ドライバーが起動かどうかは、シーケンス内の転送の 1 つの中にエラーが発生します (たとえば、ターゲット デバイスが転送を拒否する場合に NACK をシグナル、)、コント ローラー ドライバーが、シーケンス内の残りの転送を中止します。 ドライバーは STATUS_SUCCESS を完了状態を設定、情報メンバーをエラーが発生し、要求を完了する前に正常に転送されたバイト数に設定します。

## <a href='#ioctl-spb-full-duplex' id='ioctl-spb-full-duplex'>IOCTL_SPB_FULL_DUPLEX 制御コード</a>

IOCTL_SPB_FULL_DUPLEX 制御コードは、全二重の I/O 操作を要求するクライアント (周辺ドライバー) によって使用されます。 全二重 I/O 操作は、SPI を同時に読み書きできるデータなどのバスのコント ローラーでサポートされます。
システム提供 CTL_CODE マクロを定義する I/O 制御コードに記載されてを使用して、次のように IOCTL_SPB_FULL_DUPLEX を定義します。

ユーザー モード ドライバーまたはバス上のデバイス用のカーネル モード ドライバーは、対象デバイスのファイル オブジェクトをこの I/O 制御要求を送信します。

この IOCTL は、読み取りし、同時にデータを書き込むことができる SPI などのバスの SPB コント ローラーのドライバーでのみサポートされます。

SPB_TRANSFER_LIST 構造体では、全二重転送用の書き込みと読み取りバッファーがについて説明します。 この構造体には、次の形式を使用する必要があります。
- SPB_TRANSFER_LIST_ENTRY 構造体の配列には、2 つの要素が含まれています。 最初の要素は、書き込みバッファーを記述します。 (の方向 = SpbTransferDirectionToDevice)。 2 番目の要素は、読み取りバッファーをについて説明します (の方向 = SpbTransferDirectionFromDevice)。
- 2 つの SPB_TRANSFER_LIST_ENTRY 構造体の DelayInUs メンバーは、0 にする必要があります。
  バッファーの書き込みと読み取りバッファーのバッファーの形式は、次のいずれかになります。
  -    SpbTransferBufferFormatSimple
  -    SpbTransferBufferFormatList
  -    SpbTransferBufferFormatSimpleNonPaged
  -    上記の SpbTransferBufferFormatMdl 最後の 2 つの形式は、カーネル モードのクライアントでのみ使用できます。 書き込みと読み取りバッファーの形式が同じである必要はありません。 これらのバッファー形式の詳細については、SPB_TRANSFER_BUFFER_FORMAT を参照してください。

操作が成功すると場合があります情報メンバーの書き込みバッファーのサイズの合計よりも小さい値に設定し、操作がデバイスに完全な書き込みバッファーの内容を書き込むことはできませんか、要求が取り消された場合に発生することが、バッファーの読み取り、またはデバイスから読み取られるデータの読み取りバッファーを完全に入力します。

書き込みと読み取りバッファー サイズが同じである必要はありません。 書き込みバッファーが読み取りバッファーよりも大きい場合は、読み取りバッファーがいっぱいの後に、書き込みバッファーからデータを書き込む操作が続行されます。 読み取りバッファーが書き込みバッファーより大きい場合は、書き込みバッファーが空になった後に、読み取りバッファーを入力する操作が続行されます。

SPB コント ローラーのドライバーでは、EvtSpbControllerIoOther のコールバック関数を登録、SPB フレームワーク拡張機能 (SpbCx) は SPB コント ローラーのドライバーの処理に、IOCTL_SPB_FULL_DUPLEX 要求を渡すには、この関数を呼び出します。 SpbCx は、IOCTL_SPB_FULL_DUPLEX 要求に対して、パラメーターのチェック、転送リストの検証、またはその他の処理は実行されません。

SPB のコント ローラー ドライバーがこの IOCTL のサポートを実装する方法の詳細については、IOCTL_SPB_FULL_DUPLEX 要求の処理を参照してください。

### <a name="input-buffer"></a>入力バッファー
クライアントのデータ入力と出力データ バッファーへのポインターを含む SPB_TRANSFER_LIST 構造体へのポインター。 この構造体には、2 つの要素の転送の配列が含まれています。 最初の要素には、デバイスに書き込むデータを格納しているバッファーがについて説明します。 2 番目の要素には、デバイスから読み取られるデータを保持するために使用するバッファーがについて説明します。
SPB のコント ローラー ドライバーが SPB_TRANSFER_LIST 構造体を使用してバッファーを記述するカスタム I/O 制御 (IOCTL) 要求を実装する方法の詳細については、カスタム Ioctl の SPB_TRANSFER_LIST 構造体を使用して参照してください。

### <a name="input-buffer-length"></a>入力バッファーの長さ
SPB_TRANSFER_LIST 構造体のサイズ。

### <a name="status-block"></a>ステータス ブロック
操作が成功した場合、コント ローラーのドライバーに STATUS_SUCCESS、状態のメンバーを設定し、全二重操作中に (バイトの読み取りと書き込みバイト数) に転送されたバイトの合計数にはメンバーを設定します。

この操作が失敗するリソースの不足、無効なクライアントの入力、およびデバイスの誤動作に含めることができますが、さまざまな理由です。


## <a href='#ioctl-spb-lock-connection' id='ioctl-spb-lock-connection'>IOCTL_SPB_LOCK_CONNECTION 制御コード</a>

IOCTL_SPB_LOCK_CONNECTION 制御コードは、クライアント (周辺ドライバー) によって別のクライアントと共有されているターゲットの sp B に接続されているデバイスの接続のロックの取得に使用されます。 クライアントは、接続のロックを保持して、このクライアントでは、デバイスへの排他アクセスがあります。
システム提供 CTL_CODE マクロを定義する I/O 制御コードに記載されてを使用して、次のように IOCTL_SPB_LOCK_CONNECTION を定義します。

IOCTL_SPB_LOCK_CONNECTION と IOCTL_SPB_UNLOCK_CONNECTION 要求を取得し、シンプルな周辺機器のバスに接続されているターゲット デバイスの接続のロックを解除します。 ほとんどのクライアントは、これらの I/O 制御要求には使用しません。 これらの要求は、2 つのクライアントが同じターゲット デバイスへのアクセスを共有する場合にのみ使用されます。 詳細については、SPB 接続のロックを参照してください。

2 つのクライアントは、同じターゲット デバイスに個別の論理接続を開き、いずれかのクライアントは、デバイスへの排他アクセスを必要とする場合、接続のロックを使用できます。 1 つのクライアントは、ロックを保持しているときに、最初のクライアントは、ロックを解放するまで、デバイスに 2 つ目のクライアントからの I/O 要求が自動的に保留します。

クライアントは、ターゲット デバイスに接続ロックと SPB コント ローラー上のコント ローラーのロックを同時に保持できます。 IOCTL_SPB_LOCK_CONTROLLER と IOCTL_SPB_UNLOCK_CONTROLLER 要求を取得およびコント ローラーのロックを解放します。 クライアントは、コント ローラーのロックを取得する前に、接続のロックを取得する必要があり、接続のロックを解放する前に、コント ローラーのロックを解放する必要があります。 クライアントは、バスの単一のアトミック操作として bus 転送 (読み取りし、書き込み操作) の順序付けされたセットを実行するのにコント ローラーのロックを使用します。 詳細については、I/O 転送シーケンスを参照してください。

接続のデバイスのロック中にターゲット デバイスに、IRP_MJ_CLEANUP 要求が送信される場合、接続のロックが自動的に終了します。 クリーンアップ要求は、クライアントがデバイスにそのファイル ハンドルを閉じるときに、ターゲット デバイスに送信されます。

### <a name="status-block"></a>ステータス ブロック
操作が成功した場合は、状態のメンバーが STATUS_SUCCESS に設定されます。

操作に失敗した場合、状態のメンバーは、適切なエラー状態コードに設定されます。

クライアントは既にターゲット デバイスに接続ロックを保持またはステータスでコント ローラーのロック SPB コント ローラーで、この操作が失敗した場合は、STATUS_INVALID_DEVICE_REQUEST を = です。 この操作が失敗するその他の理由からは、リソース不足、無効なクライアントの入力、およびデバイスの誤動作に含めることができます。

## <a href='#ioctl-spb-lock-controller' id='ioctl-spb-lock-controller'>IOCTL_SPB_LOCK_CONTROLLER 制御コード</a>

IOCTL_SPB_LOCK_CONTROLLER 制御コードは、SPB コント ローラーをロックするクライアント (周辺ドライバー) によって使用されます。 コント ローラーがロックされているクライアントがロックを指定したターゲット デバイスにアクセスする bus を排他的に使用します。
システム提供 CTL_CODE マクロを定義する I/O 制御コードに記載されてを使用して、次のように IOCTL_SPB_LOCK_CONTROLLER を定義します。

ターゲット デバイスにアクセスする bus を排他的に使用を取得するには、クライアント (周辺ドライバー) は、対象のファイル オブジェクトへのこの IOCTL を送信します。 この IOCTL が完了すると、コント ローラーがロックされているし、すべての I/O ・転送 (読み取りまたは書き込み) バスに指定されたターゲットにアクセスします。 間転送では、コント ローラーで選択されたターゲット デバイスを保持するが、クロックが停止します。

コント ローラーは、クライアントは、コント ローラーのロックを解除する IOCTL_SPB_UNLOCK_CONTROLLER 要求を送信までロックされたままです。 転送するか、ターゲット デバイスからのクライアントのシーケンスが完了したら、クライアントはコント ローラーは、バス上の他のターゲットの I/O 要求を処理できるようにコント ローラーを解除する必要があります。

コント ローラーのターゲットのロック中にターゲット デバイスに、IRP_MJ_CLEANUP 要求が送信される場合、ロックが自動的に終了します。 クリーンアップ要求は、クライアントが、ターゲットへのハンドルを閉じるときに、ターゲットに送信されます。

SPB コント ローラーが IOCTL_SPB_LOCK_CONTROLLER と IOCTL_SPB_UNLOCK_CONTROLLER の要求をサポートする必要はありませんし、周辺機器のデバイス ドライバーがサポートされている想定しないでください。

SPB コント ローラーのドライバーでは、EvtSpbControllerLock のコールバック関数を登録、SPB フレームワーク拡張機能 (SpbCx) は SPB コント ローラーのドライバーの処理に、IOCTL_SPB_LOCK_CONTROLLER 要求を渡すには、この関数を呼び出します。


### <a name="status-block"></a>ステータス ブロック
操作が成功した場合は、状態のメンバーが STATUS_SUCCESS に設定されます。
この IOCTL では、さまざまな理由から、排他アクセス モードで動作するコント ローラーを構成する障害などのエラー状態を返すことができます。 このモードでは、コント ローラーは、ターゲット デバイスが選択されているため、これは、バス上のすべての I/O 転送の排他的なターゲットを保持します。 コント ローラーは、ロックが解除されるまで、このモードのままです。

## <a href='#ioctl-spb-unlock-connection' id='#ioctl-spb-unlock-connection'>IOCTL_SPB_UNLOCK_CONNECTION 制御コード</a>

IOCTL_SPB_UNLOCK_CONNECTION I/O 制御コードは、別のクライアントと共有されているターゲットの sp B に接続されているデバイスの接続のロックを解除するクライアント (周辺ドライバー) によって使用されます。 クライアントは、以前のデバイスへの排他アクセスを取得する IOCTL_SPB_LOCK_CONNECTION 要求を送信します。

IOCTL_SPB_LOCK_CONNECTION と IOCTL_SPB_UNLOCK_CONNECTION 要求を取得し、シンプルな周辺機器のバスに接続されているターゲット デバイスの接続のロックを解除します。 ほとんどのクライアントは、これらの I/O 制御要求には使用しません。 これらの要求は、2 つのクライアントが同じターゲット デバイスへのアクセスを共有する場合にのみ使用されます。 詳細については、SPB 接続のロックを参照してください。

クライアント (周辺ドライバー) は、バス上のターゲット デバイスに IOCTL_SPB_LOCK_CONNECTION 要求を送信する要求が正常に完了すると、接続がロックされたまま、クライアントは、ロックを解除する IOCTL_SPB_UNLOCK_CONNECTION 要求を送信するまで、接続します。

クライアントは、クライアントが不要になったデバイスへの排他アクセスを必要とする場合は、ターゲット デバイスに接続のロックを解放する IOCTL_SPB_UNLOCK_CONNECTION 要求を送信します。 接続は、その他のクライアントがデバイスにアクセスできるようににロック解除する必要があります。

### <a name="status-block"></a>ステータス ブロック
操作が成功した場合は、状態のメンバーが STATUS_SUCCESS に設定されます。

操作に失敗した場合、状態のメンバーは、適切なエラー状態コードに設定されます。 クライアントが、ターゲット デバイスに接続ロックを保持しないかの状態でこの操作は失敗、クライアントには、SPB コント ローラーの接続のロックも保持している場合は、STATUS_INVALID_DEVICE_REQUEST を = します。 この操作が失敗するその他の理由からは、リソース不足、無効なクライアントの入力、およびデバイスの誤動作に含めることができます。

## <a href='#ioctl-spb-unlock-controller' id='#ioctl-spb-unlock-controller'>IOCTL_SPB_UNLOCK_CONTROLLER 制御コード</a>

IOCTL_SPB_UNLOCK_CONTROLLER I/O 制御コードは、SPB コント ローラーのロックを解除するクライアント (周辺ドライバー) によって使用されます。 クライアントには、bus バス上のターゲット デバイスへのアクセスに排他的に使用できるコント ローラーが以前ロックされています。

クライアント (周辺ドライバー) は、バス上のターゲット デバイスに IOCTL_SPB_LOCK_CONTROLLER I/O 制御要求を送信、後に、コント ローラー、クライアントは、コント ローラーのロックを解除する IOCTL_SPB_UNLOCK_CONTROLLER I/O 制御要求を送信するまでロックは残ります。 クライアントは、対象デバイスのファイル オブジェクトにこれらの I/O 制御要求を送信します。

バス上の転送のシーケンスが完了し、ターゲット デバイスを解放しようとすると、クライアントは、IOCTL_SPB_UNLOCK_CONTROLLER 要求を送信します。 バス上の他のターゲットの I/O 要求を処理できるように、コント ローラーがロックする必要があります。

SPB コント ローラーが IOCTL_SPB_LOCK_CONTROLLER と IOCTL_SPB_UNLOCK_CONTROLLER の要求をサポートする必要はありませんし、周辺機器のデバイス ドライバーがサポートされている想定しないでください。

SPB フレームワーク拡張機能 (SpbCx) は、SPB コント ローラーのドライバーの省略可能な EvtSpbControllerUnlock のコールバック関数を SPB コント ローラーのドライバーを処理する、IOCTL_SPB_LOCK_CONTROLLER 要求を渡すを呼び出します。

## <a name="status-block"></a>ステータス ブロック
操作が成功した場合は、状態のメンバーが STATUS_SUCCESS に設定されます。
指定されたターゲットへの排他アクセスのロックされているコント ローラーがないクライアントによって送信された場合にのみ、この IOCTL が失敗します。
