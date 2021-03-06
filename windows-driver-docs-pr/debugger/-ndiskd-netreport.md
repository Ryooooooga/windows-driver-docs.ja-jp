---
title: ndiskd netreport
description: Ndiskd netreport 拡張機能によって、ネットワークスタック全体のビジュアルレポートが生成されます。
ms.assetid: 0FC134A8-8D91-4299-8D15-4E8EDD9ED855
keywords:
- ndiskd netreport Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ndiskd.netreport
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 11498301e69860be71183593494b7eba4c0b52e4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72826561"
---
# <a name="ndiskdnetreport"></a>!ndiskd.netreport


**! Ndiskd netreport**拡張機能によって、ネットワークスタック全体のビジュアルレポートが生成されます。 レポート **! ndiskd netreport**は HTML ファイルを生成し、その場所へのリンクを提供します。 HTML ファイルにはネットワークスタックに関する詳細情報が含まれているため、分析のために共有する必要がある場合は、大きなクラッシュダンプファイルを送信するのではなく、電子メールで送信することができます。

```console
!ndiskd.netreport [-outputpath <str>] [-jsononly] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメータ


<span id="_______-outputpath______"></span><span id="_______-OUTPUTPATH______"></span> *-outputpath*   
レポートファイルの書き込み先を指定します。

<span id="_______-jsononly______"></span><span id="_______-JSONONLY______"></span> *-jsononly*   
では、HTML ではなく生データのみが書き込まれます。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Ndiskd .dll

<a name="examples"></a>例
--------

**! Ndiskd netreport**拡張機能を実行して、ネットワークスタックのボックス図を描画します。

```console
1: kd> !ndiskd.netreport


NETWORK STACK REPORT


    Want more stuff?  Rerun with the -verbose flag
                                                                                            

    Report was saved to C:\Users\******\AppData\Local\Temp\NKDFE9F.html
    View the report                        Send in email
```

下部にある [レポートの表示] リンクをクリックして、レポートが生成されたことを確認します。 次の図は、クラッシュダンプファイルから生成された net レポートを示しています。 各垂直スタックはネットワークアダプターであり、スタックのコンポーネントを示す層に分割されます。 各ボックスの色は、コンポーネントの名前をハッシュすることによって生成されます。これは、レポートを実行するたびに同じ色で同じコンポーネントがレンダリングされることを意味します。 これは、問題をデバッグしている場合に、特定のドライバーまたはアダプターを簡単に選択できることを意味します。

![クラッシュダンプからのネットワークデバッグレポート](images/!ndiskd-netreport-crashdump.png)

次の図は、クラッシュダンプファイルではなくアクティブシステムから生成された net レポートを示しています。 HTML ページの下部に [データフローの表示] と [パケットのシミュレート] の2つのオプションがあります。レポートの上部には、"データフロー" の4番目のタブがあります。 デバッグ対象マシンで NBL tracking が有効になっているため、これらのオプションが表示されました。これにより、 **! ndiskd netreport**で NBL 追跡ログを解析し、情報を視覚的に表示できます。 NBL tracking が有効になっていない場合、これらのオプションは表示されません。 NBL tracking と NBL ログの詳細については、「 [ **! ndiskd ndiskd**](-ndiskd-nbllog.md)」を参照してください。

[データフローの表示] ボックスをオンにすると、データが流れるパスを確認できます。 [パケットをシミュレートする] ボックスをオンにすると、アニメーション化された円がデータフローパスを上下に移動します。 各円はネットワークパケットを表します。

![アクティブシステムからのネットワークデバッグレポート](images/!ndiskd-netreport-activesystem.png)

アクティブシステムからのこの2番目の例では、クラッシュダンプファイルを使用した最初の例とは別の違いも示しています。 2番目の例のターゲットデバッグ対象マシンは、ネットワーク上でのカーネルデバッグ用にプロビジョニングされています。そのため、データフローが Microsoft カーネルデバッグネットワークアダプターのスタック上のネットワークアダプターを確認できます。 このアダプターは、デバッグ対象マシンでカーネルデバッグが有効になっていない限り、通常は非表示になります。 実際には、カーネルデバッグネットワークアダプターはデバッグセッション用にコンピューターのイーサネットアダプターを予約しているため、トラフィックはイーサネット経由で送信されます。

ネットワークスタックを視覚化し、トラフィックが流れている場所を確認することで、問題が発生している場所をすばやく特定できます。 これは、前の例よりも複雑なネットワーク図を持つ仮想スイッチまたはサーバーに特に便利です。 たとえば、NIC チーミングを使用する Windows Server では、複数のネットワークスタックが相互に分散してトラフィックの負荷を分散し、1つのスタックの一番下に別のスタックに影響を与える問題があるかどうかを確認できます。 これを示すネットワークデバッグレポートの例については、「[ネットワークスタックのデバッグ](https://go.microsoft.com/fwlink/p/?linkid=845311)」を参照してください。 NIC チーミングの詳細については、「 [Nic チーミングを使用したネットワークサブシステムのパフォーマンス](https://docs.microsoft.com/previous-versions/dn567652(v=vs.85))」を参照してください。

**! ndiskd netreport**には、システム、集計、およびデータフローのページの上部にある他のタブもあります (該当する場合)。 これらのタブには、ネットワークスタックの状態に関する有用な情報が含まれています。 次の図は、[概要] タブの下にある [ネットワークインターフェイス] タブを示しています。このタブの表では、システム内のネットワークインターフェイスの名前と識別子に関する詳細情報を確認できます。

![ネットワークデバッグレポートのネットワークインターフェイス](images/!ndiskd-netreport-activesystem-networkinterfaces.png)

ターゲットシステムで NBL tracking が有効になっている場合に表示される [データフロー] タブには、トラフィックイベントのテーブルと各イベントの詳細が表示されます。 次の図は、前に説明した2番目のサンプルデバッグレポートのアクティブシステムの [データフロー] タブを示しています。

![ネットワークデバッグレポートのデータフロー](images/!ndiskd-netreport-activesystem-dataflows.png)

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[ネットワークドライバーの設計ガイド](https://docs.microsoft.com/windows-hardware/drivers/network/index)

[Windows Vista 以降のネットワークリファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)

[ネットワークスタックのデバッグ](https://go.microsoft.com/fwlink/p/?linkid=845311)

[**NDIS 拡張機能 (Ndiskd .dll)** ](ndis-extensions--ndiskd-dll-.md)

[ **!ndiskd.help**](-ndiskd-help.md)

[ **!ndiskd.nbllog**](-ndiskd-nbllog.md)

[NIC チーミングを使用したネットワークサブシステムのパフォーマンス](https://docs.microsoft.com/previous-versions/dn567652(v=vs.85))

 

 






