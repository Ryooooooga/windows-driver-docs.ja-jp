---
title: ndiskd netpacket
description: Ndiskd netpacket 拡張機能には、NET_PACKET 構造に関する情報が表示されます。
ms.assetid: 304BA2CF-B6BC-452C-8543-9B872054AA9E
keywords:
- ndiskd netpacket Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ndiskd.netpacket
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 71fc05678795a53d991d85a749ad4fc1d6dc7dff
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837575"
---
# <a name="ndiskdnetpacket"></a>!ndiskd.netpacket


**! Ndiskd netpacket**拡張機能には、 [NET\_パケット](https://docs.microsoft.com/windows-hardware/drivers/netcx/net-packet)構造に関する情報が表示されます。

ネットワークアダプターの WDF クラス拡張 (NetAdapterCx) の詳細については、「 [Network ADAPTER WDF Class extension (Cx)](https://docs.microsoft.com/windows-hardware/drivers/netcx)」を参照してください。

```console
!ndiskd.netpacket [-handle <x>] [-basic] [-layout] [-checksum] [-data] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメータ


<span id="_______-handle______"></span><span id="_______-HANDLE______"></span> *-  を処理*します  
必須。 NET\_パケットのアドレス。

<span id="_______-basic______"></span><span id="_______-BASIC______"></span> *-基本*   
基本情報を表示します。

<span id="_______-layout______"></span><span id="_______-LAYOUT______"></span> *-レイアウト*   
パケットプロトコルレイアウトを表示します。

<span id="_______-checksum______"></span><span id="_______-CHECKSUM______"></span> *-checksum*   
パケットチェックサム情報を表示します。

<span id="_______-data______"></span><span id="_______-DATA______"></span> *-データ*   
ペイロードメモリをダンプします。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Ndiskd .dll

<a name="examples"></a>例
--------

**  、** [オブジェクトの概要](https://docs.microsoft.com/windows-hardware/drivers/netcx/summary-of-objects)を参照して、NET\_PACKET オブジェクトと NetAdapterCx 内の他のオブジェクトとの関係を説明する図を参照してください。

 

NET\_パケットのハンドルを取得するには、次の手順を実行します。

1.  [ **! Ndiskd netadapter**](-ndiskd-netadapter.md)拡張機能を実行します。
2.  NetAdapterCx ドライバーがインストールされている NetAdapter のハンドルをクリックします。
3.  NetAdapter の NETADAPTER オブジェクトの右側にある [詳細情報] リンクをクリックして、 [ **! ndiskd cxadapter**](-ndiskd-cxadapter.md)拡張機能を実行します。
4.  *-データパス*パラメーターを指定して **! ndiskd cxadapter**コマンドを入力すると、netadapter のデータパスキューが表示されます。
5.  データパスキューのいずれかのハンドルをクリックします。
6.  データパスキューのリングバッファーのハンドルをクリックします。
7.  リングバッファーの詳細の下部にある [すべての要素の一覧表示] リンクをクリックして、含まれている要素を確認します。

この手順の手順1-4 の詳細については、 **! ndiskd cxadapter**トピックの例を参照してください。 この手順の手順5の詳細については、 [ **! ndiskd netqueue**](-ndiskd-netqueue.md)のトピックの例を参照してください。 この手順の手順6-7 の詳細については、 [ **「」の**](-ndiskd-netrb.md)例を参照してください。
次の例では、最初の NET\_パケットのハンドル ffffd1022d000040 を探します。

```console
0: kd> !ndiskd.netrb ffffd1022d000000 -dump

    [000] ffffd1022d000040 - NET_PACKET
    [001] ffffd1022d0000c0 - NET_PACKET
    [002] ffffd1022d000140 - NET_PACKET
    [003] ffffd1022d0001c0 - NET_PACKET
    [004] ffffd1022d000240 - NET_PACKET
    [005] ffffd1022d0002c0 - NET_PACKET
    
    ...

    [07b] ffffd1022d003dc0 - NET_PACKET
    [07c] ffffd1022d003e40 - NET_PACKET
    [07d] ffffd1022d003ec0 - NET_PACKET
    [07e] ffffd1022d003f40 - NET_PACKET
    [07f] ffffd1022d003fc0 - NET_PACKET
```

このネット\_パケットのハンドルをクリックするか、コマンドラインに「 **! ndiskd netpacket handle** 」と入力して、このネットワーク\_パケットの詳細を表示できます。これには、そのパケットを含むリングバッファー、そのリングを含むデータパスキューなどが含まれます。バッファー、および最初のフラグメントのハンドル。

```console
0: kd> !ndiskd.netpacket ffffd1022d000040


    NET_PACKET         ffffd1022d000040    Ring Buffer        ffffd1022d000000
    First fragment     ffffd1022d000040    NETTXQUEUE         ffffd1022f512700

    Client Context     ffffd1022d000090

    Show protocol layout
    Show checksum information
    Dump data payload
```

基本的な説明を他の任意の **! ndiskd netpacket**パラメーター (またはそのすべて) と組み合わせることで、このフラグメントに関する特定の情報を確認できるようになりました。 次の例では、すべてのパラメーターを使用します。

```console
0: kd> !ndiskd.netpacket ffffd1022d000040 -basic -layout -checksum -data

    NET_PACKET         ffffd1022d000040    Ring Buffer        ffffd1022d000000
    First fragment     ffffd1022d000040    NETTXQUEUE         ffffd1022f512700

    Client Context     ffffd1022d000090


    Protocol Layout                                                             

    Layer 2 Type       ETHERNET
    Header Length      0n14

    Layer 3 Type       IPV4_NO_OPTIONS
    Header Length      0n20

    Layer 4 Type       UDP
    Header Length      8


    Checksum Information                                                        

    Layer 2            TX_PASSTHROUGH
    Layer 3            TX_REQUIRED
    Layer 4            TX_PASSTHROUGH


    Payload data                                                                

    Fragment           ffffd1022d000040
    ffffd102303e8332  00 00 01 02 71 68 0a 89-be 39 e0 00 00 16 94 04  ····qh···9······
    ffffd102303e8342  00 00 22 00 fa 01 00 00-00 01 03 00 00 00 e0 00  ··"·············
    ffffd102303e8352  00 fc   
```

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[ネットワークドライバーの設計ガイド](https://docs.microsoft.com/windows-hardware/drivers/network/index)

[Windows Vista 以降のネットワークリファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)

[ネットワークスタックのデバッグ](https://go.microsoft.com/fwlink/p/?linkid=845311)

[**NDIS 拡張機能 (Ndiskd .dll)** ](ndis-extensions--ndiskd-dll-.md)

[ **!ndiskd.help**](-ndiskd-help.md)

[ネットワークアダプターの WDF クラス拡張 (Cx)](https://docs.microsoft.com/windows-hardware/drivers/netcx)

[オブジェクトの概要](https://docs.microsoft.com/windows-hardware/drivers/netcx/summary-of-objects)

[NET\_パケット](https://docs.microsoft.com/windows-hardware/drivers/netcx/net-packet)

[ **! ndiskd netadapter**](-ndiskd-netadapter.md)

[ **! ndiskd cxadapter**](-ndiskd-cxadapter.md)

[ **!ndiskd.netqueue**](-ndiskd-netqueue.md)

[ **!ndiskd.netrb**](-ndiskd-netrb.md)

 

 






