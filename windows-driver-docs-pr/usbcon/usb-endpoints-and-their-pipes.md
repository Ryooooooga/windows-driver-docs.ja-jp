---
Description: A USB device has endpoints that are used to for data transfers.
title: USB の端点と、パイプ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f6e04a27d03fe54fcd80370d8ae6e40b66b22566
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56561090"
---
# <a name="usb-endpoints-and-their-pipes"></a>USB の端点と、パイプ


**要約**

-   エンドポイントは、デバイス上のハードウェアパイプは、ホスト側のソフトウェアです。
-   エンドポイントが構成されていません。パイプが転送用に構成されました。
-   ホストを送信または受信データをパイプします。

USB デバイスには、データ転送に使用されるエンドポイントがあります。 ホスト側のエンドポイントは、パイプで表されます。 このトピックでは、これら 2 つの用語によって区別されます。

## <a name="usb-endpoint"></a>USB エンドポイント


*エンドポイント*USB デバイス上のバッファーします。 エンドポイントは、ハードウェア自体、別のホストのオペレーティング システムに関連する用語です。 ホストは、そのバッファーとの間のデータを送受信することができます。 エンドポイントは、エンドポイントの制御とデータに分類できます。

すべての USB デバイスには、既定のエンドポイントまたは Endpoint0 と呼ばれるアドレス 0 で、少なくとも 1 つのコントロール エンドポイントを提供する必要があります。 このエンドポイントは、双方向です。 ホストは、エンドポイントにデータを送信し、転送は 1 つ内からデータを受信できます。 コントロールの転送では、デバイス情報を取得するには、デバイスを構成するホストを有効にするか、デバイスに固有の管理操作を実行します。

データのエンドポイントとは省略可能で、データを転送するために使用されます。 これらは一方向で、(コントロール、割り込み、一括でアイソクロナス) の型とその他のプロパティがあります。 エンドポイント記述子ではこれらのプロパティをすべて説明 (標準の USB ディスクリプターを参照してください)。

USB の用語では、エンドポイント (および転送したり、そこから) の方向をホストに基づきます。 したがってで常には、参照のデバイスから、ホストに転送するを常に参照を転送する、ホストからデバイスへ。 USB デバイスでは、コントロールのデータの双方向の送信もサポートできます。

デバイス上のエンドポイントは、機能のインターフェイスにグループ化し、一連のインターフェイスは、デバイスの構成をします。 詳細については、USB デバイスのレイアウトを参照してください。

エンドポイントは、前に、デバイスが構成されているまたは代替の設定の選択中に、ホスト ソフトウェアを検索できます。 すべてのインターフェイスを使用し、設定の各インターフェイスの一覧を反復処理し、または各エンドポイントのプロパティの設定でエンドポイントのセット全体を確認します。 エンドポイント情報を見ても、デバイスの構成済みの状態は影響しません。

## <a name="usb-pipes"></a>USB パイプ


USB デバイスとという抽象化を通じて USB ホスト間でデータを転送する*パイプ*します。 パイプは、純粋なソフトウェア用語です。 パイプがエンドポイントに、デバイス上で説明して、そのエンドポイント アドレスがあります。 パイプのもう一方の端は、ホスト コント ローラーでは常にします。

構成を選択するか、デバイスが構成されており、インターフェイスの代替エンドポイント用のパイプが開かれる設定。 このため I/O 操作の対象となります。 パイプには、エンドポイントのすべてのプロパティがアクティブであり、ホストと通信するために使用されます。

未構成のエンドポイントは構成済みのエンドポイントは、パイプの呼び出し中に、エンドポイントと呼ばれます。

![usb パイプとエンドポイント](images/endpoints.png)

## <a name="related-topics"></a>関連トピック
[すべての USB 開発者の概念](usb-concepts-for-all-developers.md)  


