---
title: ESRT テーブルの定義
description: ESRT テーブルへのポインターは、EFI_CONFIGURATION_TABLE で対応する GUID を使用して識別されます。
ms.assetid: F332CCF3-AE6D-4B02-A63E-DB05910C8E6E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 17b7f46d926c20be7b920c31848401b782d3c24c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63337593"
---
# <a name="esrt-table-definition"></a>ESRT テーブルの定義


ESRT テーブルへのポインターは、efi 対応する GUID を使用して識別\_構成\_テーブル。

```cpp
#define EFI_SYSTEM_RESOURCE_TABLE_GUID   \
{ 0xb122a263, 0x3661, 0x4f68,  0x99, 0x29, 0x78, 0xf8, 0xb0, 0xd6, 0x21, 0x80  }
```

次の表では、ESRT テーブルとテーブルに含まれているリソースのファームウェア エントリの形式について説明します。

<table>
<colgroup>
<col width="20%" />
<col width="10%" />
<col width="10%" />
<col width="10%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>フィールド</th>
<th>配列の値</th>
<th>バイトの長さ</th>
<th>バイト オフセット</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>ファームウェアのリソースの数</td>
<td></td>
<td>4</td>
<td>0</td>
<td>ESRT ファームウェア リソース エントリの数。 0 があります。</td>
</tr>
<tr class="even">
<td>ファームウェアのリソースの最大数</td>
<td></td>
<td>4</td>
<td>4</td>
<td>テーブルを再割り当てせずに追加できるリソース配列エントリの最大数。 大きいまたはファームウェア リソース数に等しい必要があります。</td>
</tr>
<tr class="odd">
<td>リソースのファームウェア バージョン</td>
<td></td>
<td>8</td>
<td>8</td>
<td>ファームウェア リソース エントリのバージョン。 この値は 1 に設定する必要があります。</td>
</tr>
<tr class="even">
<td>ファームウェア リソース エントリの配列</td>
<td></td>
<td></td>
<td></td>
<td>ファームウェア リソース エントリ 0</td>
</tr>
<tr class="odd">
<td></td>
<td>ファームウェア クラス</td>
<td>16</td>
<td>16</td>
<td>更新カプセルを使用して更新できるファームウェア コンポーネントを識別する GUID。 この GUID は更新中に、更新カプセル: ヘッダーの CapsuleGuid パラメーターとして、UEFI 更新カプセル: 実行時サービスに渡されます。</td>
</tr>
<tr class="even">
<td></td>
<td>ファームウェアの種類</td>
<td>4</td>
<td>32</td>
<td>ファームウェアのリソースの種類を識別する値は次のいずれか:
<ul>
<li>0:Unknown</li>
<li>1:システム ファームウェア</li>
<li>2:デバイスのファームウェア</li>
<li>3:UEFI ドライバー</li>
</ul></td>
</tr>
<tr class="odd">
<td></td>
<td>ファームウェア バージョン</td>
<td>4</td>
<td>36</td>
<td>現在のファームウェアのバージョンより多くが、新しいリリースを表します。 この値の形式が定義されていませんが、メジャーおよびマイナーのバージョン番号を組み込む必要があります。 推奨される形式は、まず word が主要な 2 番目の word はマイナー バージョン番号です。</td>
</tr>
<tr class="even">
<td></td>
<td>サポートされているファームウェアの最小バージョン</td>
<td>4</td>
<td>40</td>
<td>ファームウェア リソース ロールバックできます。 指定されたシステム/デバイス、最も低いファームウェア リソース バージョン。 セキュリティ関連の修正プログラムをこのファームウェア バージョンで使用できる場合は、少なくとも互換性のあるバージョンが現在のファームウェアのバージョンと等しくなければなりません。</td>
</tr>
<tr class="odd">
<td></td>
<td>Capsule フラグ</td>
<td>4</td>
<td>44</td>
<td>UEFI に渡されるフラグは、ビット 0 ~ 15 (OS が担当 UEFI 仕様のセクション 7.5.3 で定義されているフラグのビット 16 ~ 31 日を構成する)、更新カプセル: ヘッダーの Flags フィールドの capsule の実行時サービスを更新します。</td>
</tr>
<tr class="even">
<td></td>
<td>前回の試行</td>
<td>4</td>
<td>48</td>
<td>更新が試行された最後のファームウェアのバージョン。 この値は、ファームウェアのバージョンと同じ形式を使用します。</td>
</tr>
<tr class="odd">
<td></td>
<td>前回の試行の状態</td>
<td>4</td>
<td>52</td>
<td>最後にファームウェア更新のステータスを記述する値は次のいずれかを試行します。
<ul>
<li>0:成功</li>
<li>1:失敗しました。</li>
<li>2:リソース不足</li>
<li>3:バージョンが正しくありません。</li>
<li>4:無効なイメージ形式</li>
<li>5:認証エラー</li>
<li>6:接続されていない AC の電源イベント</li>
<li>7:不足しているバッテリの電源イベント</li>
</ul></td>
</tr>
<tr class="even">
<td> ...</td>
<td></td>
<td></td>
<td></td>
<td>ファームウェア リソース エントリ 1</td>
</tr>
</tbody>
</table>

 

コアの UEFI ファームウェアは、割り当て、自体 (システム ファームウェア) のシステム リソースの 1 つのエントリを含む ESRT 構成テーブルを設定する必要があります。 例示を目的として、このガイドのコアでファームウェアは作成もファームウェアの更新プログラム パッケージのメカニズムを使用してデバイス ファームウェアの更新をサポートするデバイスを表す 1 つの追加エントリ。

システム ファームウェアを記述する 1 つのエントリが常にする必要があります。 このエントリは、ターゲットのシステム ファームウェアの更新に使用されます。 実装は、システムを実行し、更新プログラムを対象に、1 つのモノリシックな操作で、システムのファームウェア エントリとしてデバイス ファームウェアの更新プログラムを使用する必要があります。 その他のすべての場合は、デバイス ファームウェアの更新プログラムの対象となって ESRT エントリの記述するデバイスのファームウェア。

つまり、これら 2 つのファームウェアのリソースを表す Guid を生成する最初の手順は、{SYSTEM\_ファームウェア} と {デバイス\_ファームウェア}。 表 2 は、テーブルの定義の例を示します。 この例では、両方のファームウェア バージョンがバージョン 1 では現在 (ファームウェアのバージョン 1 を = =)。

| フィールド                         | 配列の値                       | 値                     | Comment                                                                                                            |
|-------------------------------|-----------------------------------|---------------------------|--------------------------------------------------------------------------------------------------------------------|
| ファームウェアのリソースの数       |                                   | 2                         | このテーブルには、2 つのファームウェア リソース エントリが含まれています。                                                                 |
| ファームウェアのリソースの最大数     |                                   | 2                         | このテーブルの割り当てには、2 つのリソースの最大値を記述するのに十分な領域が含まれています。                                |
| リソースのファームウェア バージョン     |                                   | 1                         | このテーブルを使用してファームウェア リソース エントリの形式バージョンには 1 です。                                                   |
| ファームウェア リソース エントリの配列 |                                   | ファームウェア リソース エントリ 0 |                                                                                                                    |
|                               | ファームウェア クラス                    | (システム\_ファームウェア)        | この GUID は、システム ファームウェア PnP を使用して更新プログラムを識別します。                                                       |
|                               | ファームウェアの種類                     | 1                         | システム ファームウェアの種類には 1 です。                                                                                         |
|                               | ファームウェア バージョン                  | 1                         | 現在システム ファームウェアのバージョンには 1 です。                                                                          |
|                               | サポートされているファームウェアの最小バージョン | 1                         | サポートされているファームウェアの最小バージョンは、ファームウェアはロールバックできませんバージョンより前のバージョン 1 のように 1 です。 |
|                               | Capsule フラグ                     | 0                         | システム ファームウェア プライベート capsule 更新フラグのいずれかが定義されません。                                                   |
|                               | 前回の試行              | 1                         | 更新が試行された最後のシステム ファームウェアのバージョンでは、バージョン 1 をしました。                                  |
|                               | 前回の試行の状態               | 0                         | 最後のシステム ファームウェアの更新の試行は成功しました。                                                            |
|                               |                                   | ファームウェア リソース エントリ 1 |                                                                                                                    |
|                               | ファームウェア クラス                    | (デバイス\_ファームウェア)        | この GUID は、デバイスのファームウェア PnP を使用して更新プログラムを識別します。                                                       |
|                               | ファームウェアの種類                     | 2                         | デバイス ファームウェアの種類には 2 です。                                                                                         |
|                               | ファームウェア バージョン                  | 1                         | 現在のデバイス ファームウェアのバージョンには 1 です。                                                                          |
|                               | サポートされているファームウェアの最小バージョン | 1                         | サポートされているファームウェアの最小バージョンは、ファームウェアは、バージョンにロールバックをより前のバージョン 1 することはできませんので、1 です。 |
|                               | Capsule フラグ                     | 0x8010                    | デバイスのファームウェアは、プライベートの capsule 更新フラグ (0x8010) を定義します。                                                     |
|                               | 前回の試行              | 1                         | 更新が試行された最後のデバイス ファームウェアのバージョンはバージョン 1 です。                                    |
|                               | 前回の試行の状態               | 0                         | 最後のデバイス ファームウェアの更新の試行は成功しました。                                                            |

 

上記の例で ESRT が、ファームウェアの更新プロセスを紹介し、ファームウェアのサポート実装と同様に、更新プロセスの Windows のサポートについて説明にこのドキュメントで他の場所で使用されます。

## <a name="related-topics"></a>関連トピック
[プラグ アンド プレイ デバイス](plug-and-play-device.md)  
[更新プログラムのドライバー パッケージの作成](authoring-an-update-driver-package.md)  
[更新プログラムの処理](processing-updates.md)  
[UEFI 環境からデバイス I/O](device-i-o-from-the-uefi-environment.md)  
[シームレスな危機防止と回復](seamless-crisis-prevention-and-recovery.md)  
[ファームウェアの更新状態](firmware-update-status.md)  



