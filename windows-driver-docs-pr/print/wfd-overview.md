---
title: Wi-Fi Direct 印刷の概要
description: Wi-Fi Direct 印刷には、サポートされているユーザーのエクスペリエンスとユース ケースでについてを説明します。
ms.assetid: 40ED3410-EC46-42C8-B09B-8010639F2268
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6e6949b11b989e091aa6ed932b711625b6059c07
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63345294"
---
# <a name="wi-fi-direct-printing-overview"></a>Wi-Fi Direct 印刷の概要


## <a name="supported-user-experiences"></a>サポートされているユーザーのエクスペリエンス


**Windows から Wi-Fi Direct プリンターとのペアリングします。**

海外のパートナーとの会議、一方では、役員は、リビジョン、コントラクトを受信し、これで、彼女のミーティングの前に更新されたコピーを印刷する必要があります。

彼女は、Wi-Fi Direct をサポートするパートナーのオフィスでの Windows 認定の印刷デバイスを検索します。 彼女は、デバイスと、Windows 画面とのペアリングを開始し、彼女迅速に、デバイスへの接続を確立および印刷する準備ができて。 彼女は、ドキュメントの複数のコピーを出力し、自分のパートナーに、新しい承認済みのコントラクトを提示することが。

空港; に彼女は数時間後コントラクトを手動で署名します。

このシナリオについて説明します。

暗証番号 (pin) を使用してペアリング

-   コントロール パネルの デバイスを選択すると、接続のピン留めするように求められます。 彼女にとって、受付によって提供される暗証番号 (PIN) を入力します。 接続が完了し、彼女が印刷可能

アドホック暗証番号 (pin) を使用してペアリング

-   コントロール パネルの デバイスを選択すると、デバイスのコントロール パネルが求められますいずれかに一致する PIN の入力を彼女は自分のデバイスだけ (Bluetooth のペアリング) などに入力します。 彼女は、デバイスのコントロール パネルで PIN を入力しのプロンプトに自分の PC で同じ番号を入力します。 接続が完了し、彼女は印刷する準備ができます。

**ペアになっている以前の Wi-Fi Direct プリンターで印刷するには**

別のユーザーは、彼が自宅にあるときに、自分の Windows PC でインターネット接続を取得するのに、モバイル ブロード バンド接続のみを使用します。 彼は、以前にペアリングし、彼の Windows PC にインストールされている彼が Wi-Fi Direct 印刷デバイスを所有しています。

彼は自宅での文書で作業がし、ハード コピーを印刷する必要があります。 自分のアプリケーションで"Print"を選択します。 彼の Wi-Fi Direct プリンターが、Wi-Fi Direct 経由でブロードキャストは常に、範囲内で現在彼は. 印刷ダイアログ ボックスが表示されたら、彼の Wi-Fi Direct プリンターが「オンライン」として表示されます。 彼は、デバイスを選択し、印刷をクリックします。 彼の Windows PC では、デバイスへの接続を確立し、印刷ジョブを送信します。 、彼には、彼の Wi-Fi Direct プリンターは、ネットワーク経由または直接を使用している他のプリンターを使用する接続が表示されます。 印刷ジョブに出力し、編集を続行しています。

## <a name="use-cases"></a>ユース ケース


**プリンターの初めてのペアリング**

最新のデバイスのコントロール パネルの前提条件を WI-FI DIRECT 印刷デバイスに手動で接続

-   ユーザーが Wi-Fi Direct 印刷デバイスの範囲内
-   ユーザーのデバイスが Wi-Fi Direct 印刷デバイス用のドライバー
-   Windows 認定要件を満たす Wi-Fi Direct 印刷デバイス

トリガー

ユーザーは、Windows のスタート画面で [プリンターの追加] を入力、「設定」を選択し、デバイスのコントロール パネルを起動します。

手順

1.  デバイスは、使用可能な印刷デバイスのパネルの検索を制御します。
2.  DAF は、Wi-Fi Direct (WFD) デバイスの L2 チャレンジを発行します。
3.  使用可能な WFD 印刷デバイスがデバイスの一覧内のユーザーのオプションとして表示されます。
4.  WFD 印刷デバイスのユーザーのクリック
5.  DAF で WFD デバイスおよびトリガーで L2 と L3 接続は、WSD プロバイダーとのペアリングを垂直方向。 デバイスのキューが組み込まれており、ドライバーが構成されます。
6.  WFD プロバイダーがデバイスから切断します。

事後条件

-   Wi-Fi Direct プリンターの印刷キューが確立されています。
-   WFD L2 ビーコン チャレンジが成功すると常に、印刷キューが「使用可能な」が表示します。

代替フロー

なし

考慮事項

なし

 

追加プリンター ウィザードの前提条件を WI-FI DIRECT 印刷デバイスに手動で接続

-   ユーザーが Wi-Fi Direct 印刷デバイスの範囲内
-   ユーザーのデバイスが Wi-Fi Direct 印刷デバイス用のドライバー
-   Windows 認定要件を満たす Wi-Fi Direct 印刷デバイス

トリガー

ユーザーは、従来のコントロール パネルを開き、デバイスとプリンターのコントロール パネルが起動します。

手順

1.  ユーザーがデバイスとプリンターのコントロール パネル を起動します。
2.  ユーザーは、"デバイスの追加 をクリックします。
3.  DAF は、Wi-Fi Direct (WFD) デバイスの L2 チャレンジを発行します。
4.  使用可能な WFD 印刷デバイスがデバイスの一覧内のユーザーのオプションとして表示されます。
5.  WFD 印刷デバイスのユーザーのクリック
6.  DAF で WFD デバイスおよびトリガーで L2 と L3 接続は、WSD プロバイダーとのペアリングを垂直方向。 デバイスのキューが組み込まれており、ドライバーが構成されます。
7.  WFD プロバイダーがデバイスから切断します。

事後条件

-   Wi-Fi Direct プリンターの印刷キューが確立されています。
-   WFD L2 ビーコン チャレンジが成功すると常に、印刷キューが「使用可能な」が表示します。

代替フロー

なし

考慮事項

なし

 

印刷デバイスの事前条件への接続のエラー

ユーザーを使用してペアリングを開始します。

-   手動接続に、WI-FI DIRECT 印刷デバイスを通じて最新デバイス [コントロール パネル] 上記で説明されているとおりに、最新のデバイス コントロール パネル
-   上で「手動接続を WI-FI DIRECT 印刷デバイスからプリンターの追加ウィザード」に示したなど、デバイスとプリンターのコントロール パネル

トリガー

ペアリング/キューのセットアップ中にエラー イベントが発生します。

手順

1.  任意部分的にセットアップの印刷キューが削除されます。
2.  エラーのユーザーに通知されます。

事後条件

-   ユーザーの印刷システムが返されます、試行をペアリングする前に、状態

代替フロー

-   エラーの原因は、不足しているドライバーが、ドライバーをダウンロードまたは (x86 または amd64 従量制以外の接続) を追加できる場合、ペアリングを再試行する入力が求められます。

考慮事項

なし

 

WI-FI を PIN に必要な作業の直接印刷デバイスの前提条件への接続

ユーザーを使用してペアリングを開始します。

-   手動接続に、WI-FI DIRECT 印刷デバイスを通じて最新デバイス [コントロール パネル] 上記で説明されているとおりに、最新のデバイス コントロール パネル
-   上で「手動接続を WI-FI DIRECT 印刷デバイスからプリンターの追加ウィザード」に示したなど、デバイスとプリンターのコントロール パネル

トリガー

デバイスでは、ペアリングの PIN が必要です。

手順

1.  1. ユーザーは、印刷デバイスに必要な PIN を受け取りました。
2.  2. WSD のセットアップ中に、ユーザーは PIN の要求します。
3.  3. ユーザーが PIN を入力し、ペアリングが完了します。

事後条件

-   印刷キューが適切にセットアップ

代替フロー

-   エラーの原因は、不足しているドライバーが、ドライバーをダウンロードまたは (x86 または amd64 従量制以外の接続) を追加できる場合、ペアリングを再試行する入力が求められます。

考慮事項

-   Ad hoc 暗証番号 (pin)
    1.  ユーザーがプリンターの両方で、PIN を入力するために必要とデバイスの Bluetooth のペアリングに似ています。
    2.  WSD のセットアップ中にユーザーがデバイスに適切な PIN を入力および入力を求められたら、PC クライアント。
    3.  ユーザーが PIN を入力し、ペアリングが完了するとします。

<!-- -->

-   暗証番号 (pin) エントリのエラー
    1.  ユーザーが受信したクライアント暗証番号 (pin) またはアドホックの PIN が必要です。
    2.  WFD のセットアップ中に、暗証番号 (pin) を求められます。
    3.  ユーザーは、正しくない PIN を入力します。
    4.  ユーザーが通知するは、PIN が正しく、ペアリングを完了できません。
    5.  探索が終了します。 キューには、セットアップはありません。

**事後条件**:印刷キューには、セットアップはありません。

 

**印刷**

アプリケーションの事前条件から WI-FI DIRECT 印刷デバイスの使用

-   ユーザーが Wi-Fi Direct 印刷デバイスの範囲内
-   ユーザーは、「プリンター-最初にペアリング」上記で説明されているように正常に完了した初回使用時の Wi-Fi Direct 印刷デバイスとのペアリングを持っています。

トリガー

ユーザーが、アプリケーションから印刷しようとしています。

手順

1.  DAF では、Wi-Fi Direct (WFD) デバイスの L2 チャレンジを発行します。
2.  L2 チャレンジに応答して既知の WFD 印刷デバイスがユーザーに「可能」と表示されます。
3.  ユーザーが WFD 印刷デバイスを選択し、"print"をクリックします。
4.  DAF では、ユーザー選択 WFD デバイスと L2 と L3 接続を確立して、L3 WSD 接続を確立しています。 デバイスへの参照カウントがインクリメントされます。
5.  印刷ジョブがスプールされ、レンダリング、およびデバイスに送信
6.  デバイスへの参照カウントは減少します。 場合はデクリメントが 0 の場合、接続した後は、参照カウントは閉じられます。

事後条件

-   印刷ジョブが正常に印刷デバイスに送信します。

代替フロー

なし

考慮事項

-   キューは、その他のすべての印刷キューと同じ方法で Windows PC に保存されます。 ユーザーの再接続し、ペアリングの間でどれ時間だけが過ぎるとに関係なく、デバイスに印刷することとそれ以降のことが必要ですを使用します。 情報が削除された場合は、接続情報と、ユーザーのペアリング、プリンターが排除されるは、ユーザーが印刷する間で再度ペアリングする必要があるときのみです。 Re ペアは、優れたユーザー エクスペリエンスを提供する最小限に抑える必要があります。 これは、こと、デバイスする必要がありますで維持メモリの使用目的を維持するが妥当の組み合わせの数を意味します。 たとえば、ホーム ユース用のプリンターは、10 ~ 25 の組み合わせを維持することが。 Office 用のプリンターをはるかに多く維持可能性があります。

 

## <a name="considerations-for-pairing"></a>ペアリングに関する考慮事項


**永続的なグループ**

Windows で、Wi-Fi Direct 印刷デバイスの印刷キューが作成されると、Windows クライアントできなくなる再ペアリングせず、そのデバイスに再接続する必要があります。 キューおよびデバイスの作成後に、Wi-Fi Direct の DAF プロバイダーは接続を閉じます。 ペアリングの情報は、印刷時に、デバイスに再接続するためのユーザーのためにそのため永続化する必要があります。

ペアリングの情報を接続した後たびに、デバイス側で削除する場合、ユーザーは、デバイスに印刷することことはありません。 ユーザーは、PC 設定で、デバイスを追加する、セットアップ後は、接続が閉じられたし、ペアリングが削除されるループ内で必要 PC 設定でデバイスをもう一度追加するユーザー。

**同時接続**

印刷デバイスが複数の PC の接続要求に応答できることが期待されます。 したがって、印刷デバイスでは、このシナリオを果たすためにグループが複数の同時接続を実装する必要があります。

**削除の組み合わせ**

Windows では、ユーザーが再プロビジョニングすることがなく、Wi-Fi Direct のキューに印刷を許可するペアに関する情報を維持するために Wi-Fi Direct デバイスが必要です。 ただし、デバイスに格納できる組み合わせの有限数があることを理解します。 デバイスに適切な数の使用を目的の接続のペアリングを維持するために十分なメモリがあることを強くお勧めします。 たとえば、30 の接続が自宅または小規模オフィスの使用は想定されて、デバイスに注意してください可能性があります。 ただし、広範囲にわたる使用およびパブリック環境で再利用が想定されているデバイスでは、多数のユーザーが接続があまりに頻繁に排除されないように注意してください必要があります。

**削除されたペアリング シナリオ**:Windows は Wi-Fi Direct デバイスに完全な接続が、ユーザーが印刷ジョブを送信するまで再確立していません。 そのため場合は、デバイスが Windows PC のペアリング情報を削除すると、Windows が登録されていないこの印刷ジョブが既にキューに登録されるまでです。 **ユーザーがデバイスに接続および間で再度ペアリングを再プロビジョニングできる、ただし、印刷キューが削除され再構築が発生するが、プロセスのキューに登録された印刷ジョブは失われます。** 適切なメモリの組み合わせの数量を維持することによって、デバイスは、ユーザーの間で再度ペアリングし、印刷ジョブを再送信する必要があります、インスタンスの数を最小限にできます。

**PC の Wi-fi ドライバーに関する考慮事項**

Wi-fi のモジュールの Windows 8 ロゴの要件には、Wi-Fi Direct をサポートするモジュールが必要です。 ただし、この機能は、モジュールに提供されるドライバーでもサポートする必要があります。 Windows 8 からほとんどのインボックス ドライバーは、モジュールがその処理を実行できる場合でも、Wi-Fi Direct サポートされません。 これらのモジュールの製造元が、ドライバーのサイトから利用可能なドライバを更新します。 更新されたドライバーは、次の Windows リリース後に広く提供されます。

**Windows 8 ロゴ WI-FI モジュール**:次の表では、Windows 8 ロゴの提出 Wi-fi direct モジュールの一部のリストを指定します。 この情報は、nda のもとで共有され、どのような形式で再配布するのには。 パートナー企業の Wi-Fi Direct を使用すると予想される Wi-fi モジュールを識別する際、データが提供されます。 説明したとおり**6.2.4**付属のドライバーがこれらのデバイスを Wi-Fi Direct サポートしていませんが、更新されたドライバーがダウンロードされ、テストする前にインストールする必要があります。

Windows RT

Broadcom 802.11abgn SDIO ワイヤレス アダプターのもの AVASTAR ワイヤレス N ネットワーク コント ローラー (SDIO) Windows 8 (64 ビット)

Atheros ワイヤレス ネットワーク アダプター Broadcom 802.11 ac ワイヤレス ネットワーク アダプター Broadcom 802.11 ac ワイヤレスの USB アダプター Broadcom 802.11 n デュアル バンド ネットワーク ワイヤレス アダプター 802.11 n Broadcom ネットワーク アダプター Broadcom 802.11 n ワイヤレス ネットワーク アダプター intel (r)セントリーノ (r) 高度な N + WiMAX 6150 intel (r) Centrino(R) 高度な N + WiMAX 6250 intel (r) Centrino(R) 6200 の高度な-N intel (r) Centrino(R) 6205 の高度な-N intel (r) Centrino(R) 6235 の高度な-N intel (r) Centrino(R) Ultimate N 6300 intel (r) Centrino(R)Ultimate N 6300 AGN intel (r) Centrino(R) ワイヤレス N 105 intel (r) Centrino(R) ワイヤレス N 135 intel (r) Centrino(R) ワイヤレス N 2200 intel (r) Centrino(R) ワイヤレス N 2230 革新的なワイヤレス N もの AVASTAR 350N ワイヤレス ネットワーク コント ローラー N150MA N300MA QualcommAtheros ワイヤレス ネットワーク アダプター Realtek 8812AU ワイヤレス LAN 802.11 ac USB NIC Realtek RTL8188CE ワイヤレス LAN 802.11 n PCI-E NIC Realtek RTL8188CU RTL8191CU/RTL8192CU/RTL8188RU ワイヤレス LAN 802.11 n USB 2.0 ネットワーク アダプター Realtek RTL8188E ワイヤレス LAN802.11 n PCI-E NIC Realtek RTL8188EE ワイヤレス LAN 802.11 n PCI-E NIC Realtek RTL8723A ワイヤレス LAN 802.11 n USB 2.0 ネットワーク アダプター Realtek RTL8723AE ワイヤレス LAN 802.11 n PCI-E NIC Realtek ワイヤレス LAN 802.11 n USB 2.0 ネットワーク アダプター WNA3100M Windows 8 (32 ビット)

Atheros ワイヤレス ネットワーク アダプターの Broadcom 11ac ネットワークのワイヤレス アダプター Broadcom 802.11abgn ワイヤレス LAN SDIO アダプター Broadcom 802.11abgn ワイヤレス SDIO アダプター Broadcom 802.11 ac ワイヤレス ネットワーク アダプターの Broadcom 802.11 ac ワイヤレス USB アダプター Broadcom802.11 n デュアル バンド ネットワーク ワイヤレス アダプター 802.11 n Broadcom ネットワーク アダプター Broadcom 802.11 n ワイヤレス ネットワーク アダプター (r) Centrino(R) 高度な N + WiMAX 6150 intel (r) Centrino(R) 高度な N + WiMAX 6250 intel (r) Centrino(R) 6200 の高度な-N intel (r)セントリーノ (r) 高度な-N 6205 intel (r) Centrino(R) 6235 の高度な-N intel (r) Centrino(R) Ultimate N 6300 intel (r) Centrino(R) Ultimate N 6300 AGN intel (r) Centrino(R) ワイヤレス N 105 intel (r) Centrino(R) ワイヤレス N 135 intel (r) Centrino(R) ワイヤレス N 2200Intel (r) Centrino(R) ワイヤレス N 2230 革新的なワイヤレス N もの AVASTAR 350N ワイヤレス ネットワーク コント ローラー N150MA N300MA Qualcomm Atheros ワイヤレス ネットワーク アダプター Realtek 8812AU ワイヤレス LAN 802.11 ac USB NIC Realtek RTL8188CE ワイヤレス LAN 802.11 n PCI-E NICRealtek RTL8188CU RTL8191CU/RTL8192CU/RTL8188RU ワイヤレス LAN 802.11 n USB 2.0 ネットワーク アダプター Realtek RTL8188E ワイヤレス LAN 802.11 n PCI-E NIC Realtek RTL8188EE ワイヤレス LAN 802.11 n PCI-E NIC Realtek RTL8723A ワイヤレス LAN 802.11 n USB 2.0 ネットワーク アダプターRealtek RTL8723AE LAN 802.11 n PCI-E NIC Realtek ワイヤレス LAN 802.11 n USB 2.0 のワイヤレス ネットワーク アダプター WNA3100M **Windows 内のデバイス名**

Windows では、Wi-fi P2P IE 形式のデバイス情報の P2P サブ要素のデバイス名の属性を使用して、デバイスがグループの所有者である場合は、Windows でデバイス名を設定します。 この属性は、すべての Windows UI 内のデバイス名として表示される、ユーザーにわかりやすい名前を含める必要があります。

![p2p oob デバイスをフォーマット ie 情報要素](images/wfd-p2pieformat.png)

*P2P IE 形式 OOB デバイス情報要素*

**グループの所有権**

印刷デバイスは、常にグループ所有者である必要があります。 Windows 印刷システムでは、Windows PC がグループの所有者であるシナリオはサポートしません。

既知の問題はグループの所有権と 5 GHz のネットワークに関連します。 Windows では、PC がグループの所有者、および 5 GHz の AP をまたは P2P グループ 5 GHz 以上に既に接続されている場合は、2.4 GHz のチャネルを使用してデバイスをペアリングすることはできません。

グループの所有者としての Windows では、Wi-Fi Direct デバイスとの接続をネゴシエートし、Windows は通信に優先されるチャネルを提供します。 推奨されるチャネルが 5 GHz の範囲内にある場合は、2.4 GHz のみをサポートしているデバイスはそのチャネルを使用することはできません。 Windows はデュアル帯域幅のグループを保持しないと、2.4 GHz に既存のグループまたは AP の接続を移動する機能はありません。 この場合は、印刷デバイスが検出されますが、チャネルを確立できませんのでペアリング常に失敗します。

ユーザーがこのシナリオが発生しないように、Windows 印刷にも印刷デバイス グループの所有者である必要があります。 P2P ネットワーク上のクライアントとしての Windows では、デュアル バンド シナリオを管理できます。 そのため、ユーザーがプリンターを検出できますが、ペアにより、既存の AP 接続することはできません、状況はありません。

 

 




