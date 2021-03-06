---
title: UE-V の検出手順1-14
description: 次に、UE-V の検出の手順 1 ~ 14 を説明します。 手順は、「UE-V の検出と復旧のフロー」に示されている図に対応しています。
ms.assetid: 0F6F9B31-27FB-44B1-8C0E-A270E8BAF295
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 63524cfacbb0f651a5ac56cccf7727ab5bfe22d8
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841708"
---
# <a name="ue-hang-detection-steps-1-14"></a>UE-V の検出: 手順1-14


次に、UE-V の検出の手順 1 ~ 14 を説明します。 手順は、「 [ue-v の検出と復旧のフロー](wdi-ue-hang-detection-and-recovery-flow.md)」に示されている図に対応しています。

この例では、\_POWER\_設定する OID を使用します。

1.  NDIS がシステム電源 IRP を受け取るか、NIC のアクティブな参照が0に設定されます。
2.  NDIS は、WDI ドライバーに対して POWER D3\_設定された OID\_設定します。
3.  WDI は、WDI コマンド (M1) のタイマーを設定します。これには、WDI OID を LE に送信する前のタスクも含まれます。 コマンドがタスクの場合は、タスクに追加のタイマーも設定されます。 どちらのタイマーもタイムアウトすることができますが、リセットの復旧をトリガーできるのは最大で1つだけです。
4.  WDI は、WDI コマンドを LE に送信します。 LE の推奨事項は、OID を完成させるためにファームウェアコマンドが必要な場合に、アダプター構造内の WDI OID を記憶することです。 WDI OID のジョブがファームウェアによって完了すると、LE は OID を完了し、アダプター構造から削除します。 WDI が Oid を LE にシリアル化するため、LE は、保留中の WDI OID を記憶するために必要なスロットを1つだけ必要とします。 ファームウェアコマンドがハングしている場合、LE はいつでも OID を返すことができますが、ファームウェアが無効になっている場合は、手順 17. で、驚かずに削除することができます。 それ以外の場合は、WDI OID が診断コールバックの前後にあるかどうかに関係なく、ファームウェアが対応するジョブを完了したときに、LE によって単純に完了します。 WDI OID を診断後に覚えておく必要がある場合は、他のスロットで記憶する必要があります。 ただし、診断後に受信した Oid の場合、LE は、カスケードのハングを避けるためにファームウェアに触れるべきではありません。
5.  LE は、ファームウェアにコマンドを送信します。
6.  ファームウェアコマンドがタイムアウトした場合は、ファームウェアがハングしているか、時間がかかっていることが原因である可能性があります。
    -   タイムアウト後にファームウェアがコマンドを完了するのに時間がかかりすぎる場合、LE は WDI コマンドを完了できます。 UE-V は適切に処理します。
    -   ファームウェアがハングした場合、WDI コマンドは間もなく完了しません。 ハードウェアがリセットされた場合、LE は手順16で驚くの削除で完了する必要があるため、競合状態が発生した場合に特別な処理を行わなくても安全に完了できます。

7.  WDI timer は、WDI 診断コマンドを生成するために発生します。 この WDI コマンドは、WDI OID ではなく、LE ドライバー [*MiniportWdiAdapterHangDiagnose*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/nc-dot11wdi-miniport_wdi_adapter_hang_diagnose)の呼び出しです。
8.  LE は、ハードウェア制御の登録状態を収集し、必要に応じて完全なファームウェアの状態を収集します。
    -   IHV ドライバーは、1 KB に制限されているハードウェアレジスタコンテンツを収集して、関数の戻り値として返すことが想定されています。 さらに、運用前環境では、LE がファームウェアコンテキストをファイルにダンプして、IHV が事後分析のデバッグを十分に行えるようにする必要もあります。 スイッチは、ハードウェアレジスタとファームウェアイメージの収集を制御するレジストリキーとして実装できます。
    -   また、LE は、現在のコマンドに取り消しをマークします。 コマンド完了の競合によって診断が行われた場合、LE がこのコマンドに何も実行しないと、許容されます。
    -   このコマンドが保留中の場合、UE-V はリセットの結果として、さらに WDI コマンドを送信することがあります。 これらは、インフライトコマンドまたはクリーンアップコマンドです。 診断呼び出しの後、LE はファームウェアに触れずにそれらを処理する必要があります。

9.  WDI は、コントロールの登録状態を受け取ります。
10. WDI は hang WDI コマンドをマークして、後で LE で示されるようにします。
11. WDI は、WDI を完了せずに NDIS コマンドを返します (完了します)。 WDI は、NDIS コマンドをダブルバッファーするため、これは安全です。
12. WDI は、ndis を呼び出して、NdisWriteErrorLogEntry をリセットし、*エラー* **\_\_コード\_ハードウェア\_障害**(0xc000138a) を使用して、 [](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiswriteerrorlogentry)を呼び出します。 これにより、モジュール名が LE のシステムイベントログに記録されたイベントが生成されます。 エラーイベント ID は、(0xc000138a | 0xffff) –0n5002 として自動的にポップアップ表示されます。 LE でも同じエラーコードを使用してエラーログを書き込む場合、LE によって簡単にイベントを分離するために、データの最初の DWORD に high ビットセット (0x80000000) が含まれている必要があります。 WDI は、最初の DWORD データに対して0x00000000 を使用します。
13. この呼び出しはを返します。
14. NDIS が IRP を完了します。

この時点で、NDIS はバスを呼び出して、突然削除し、再列挙します。 WDI は、ndis コマンドを完了するために WDI コマンドが返されるまで待機する必要がないように、NDIS コマンドをダブルバッファーすることに注意してください。 これにより、LE がキャンセル logics を実行する必要がなくなります。これは、非常に複雑です。

PnP 操作のデッドロックを回避するには、NDIS OID\_SET\_の完了が必要です。 すべての PnP と電源状態の変化イベントがシリアル化されます。 これは、セットの power OID が返されない場合、NDIS は Set power IRP を返すことができないことを意味します。これは、リセット復旧が、突然削除される IRP によってロックアップされることを意味します。

## <a name="related-topics"></a>関連トピック


[*MiniportWdiAdapterHangDiagnose*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/nc-dot11wdi-miniport_wdi_adapter_hang_diagnose)

[リセット (驚くべき削除): 手順15-20](wdi-reset--surprise-remove---steps-15-20.md)

[UE-V の検出と復旧のフロー](wdi-ue-hang-detection-and-recovery-flow.md)

 

 






