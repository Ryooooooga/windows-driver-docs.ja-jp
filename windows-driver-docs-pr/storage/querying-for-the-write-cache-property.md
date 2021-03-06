---
title: 書き込みキャッシュのプロパティのクエリ
description: 書き込みキャッシュのプロパティのクエリ
ms.assetid: 80b7c366-3b54-4dae-8ac7-63caaa1767f9
keywords:
- ストレージドライバー WDK、書き込みキャッシュ
- 書き込みキャッシュ WDK ストレージ
- WDK ストレージの書き戻し
- WDK ストレージを使用した書き込み
- 同期キャッシュサポート WDK ストレージ
- バッテリバックアップ WDK ストレージ
- WDK ストレージのキャッシュ
- 書き込みキャッシュのクエリ
- ライトスルー要求 WDK ストレージ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d83cd90fd9cb556e5f7cef45b62267ea40f5de5b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842722"
---
# <a name="querying-for-the-write-cache-property"></a>書き込みキャッシュのプロパティのクエリ


多くの場合、記憶装置は、データを不揮発性メディア (ディスクプラッタなど) に書き込む前に書き込みキャッシュにデータをバッファリングします。 この種類のバッファーにより、デバイスのパフォーマンスが向上しますが、データの整合性も低下します。 書き込みキャッシュにバッテリバックアップがない場合、電源障害により、キャッシュされたデータが失われる可能性があります。

データ損失の問題の解決策の1つは、(SCSI 同期キャッシュコマンドを使用して) 書き込みキャッシュをフラッシュすることです。 ただし、書き込みキャッシュのフラッシュは負荷の高い操作であるため、頻繁に実行するとパフォーマンスが大幅に低下する可能性があります。 書き込みキャッシュをフラッシュするのではなく、多くの記憶装置が*書き込み*要求を許可します。 書き込み要求は書き込みキャッシュをバイパスし、データを直接メディアに送信します。

たとえば、データベースアプリケーションでは、書き込み要求を使用して、トランザクションログがメディアに到達するようにすることができます。また、ファイルシステムドライバーは書き込み要求を使用して、ファイルシステムのメタデータがメディアに到達できるようにすることができます。

ただし、書き込みキャッシュを持つすべての記憶装置は、書き込み要求またはキャッシュの同期をサポートしているわけではありません。また、一部のデバイスでは、キャッシュされたデータを予防またはフラッシュする必要がありません。これは、電源障害時のデータの破損を防ぐバッテリバックアップシステムがあるためです。 アプリケーションとドライバーは、有効に使用する前に、デバイスの書き込みキャッシュのプロパティに関する情報を持っている必要があります。

Windows Vista では、 [**IOCTL の\_ストレージ\_クエリ\_プロパティ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/ni-ntddstor-ioctl_storage_query_property)の**要求を使用**して、ストレージクラスドライバーに対してクエリを実行することができます。書き込みキャッシュプロパティは、デバイスの書き込みキャッシュの特性。 "書き込みキャッシュ" プロパティには、デバイスのキャッシュ機能に関する次の情報が含まれています。

-   *書き込みキャッシュの存在*。 書き込みキャッシュプロパティは、デバイスに書き込みキャッシュがあるかどうかを指定します。

-   *書き込みキャッシュの種類*。 書き込みキャッシュには、*ライトバック*と書き込みの2つの主な種類*があります*。 ライトバックキャッシュを使用すると、デバイスは、必要なときまでキャッシュデータを不揮発性メディアにコピーしません。 この操作により、書き込み操作のパフォーマンスが向上します。 ライトスルーキャッシュを使用すると、デバイスはデータをキャッシュとメディアに並列で書き込みます。 これによって書き込みパフォーマンスが向上するわけではありませんが、後続の読み取り操作が高速になります。

    ライトスルー*キャッシュ*と書き込み*要求*を混同しないようにしてください。 ライトスルー要求は、デバイスが書き込み要求をサポートしている場合、ライトバックキャッシュを含む任意の種類のキャッシュと共に使用できます。 たとえば、ターゲットがライトバックキャッシュを持つ SCSI デバイスであるとします。 デバイスで書き込み要求がサポートされている場合、イニシエーターは write コマンドのコマンド記述子ブロック (CDB) で force unit access (FUTEX) ビットを設定することにより、書き込みキャッシュをバイパスできます。

-   *同期キャッシュのサポート*。 書き込みキャッシュプロパティは、デバイスが SCSI 同期キャッシュコマンドをサポートしているか、他のバスで同等のコマンドをサポートしているかを示します。

-   *バッテリバックアップ*。 書き込みキャッシュプロパティは、電源障害時にキャッシュデータの整合性を保護するバッテリバックアップがデバイスにあるかどうかを示します。

書き込みキャッシュプロパティによって報告される情報の詳細については、「 [**STORAGE\_write\_cache\_プロパティ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/ns-ntddstor-_storage_write_cache_property)」を参照してください。

書き込みキャッシュプロパティメカニズムを使用しない場合 (つまり、IOCTL\_ストレージ\_クエリ\_プロパティの要求と**StorageDeviceWriteCacheProperty**プロパティ識別子)、アプリケーションとドライバーはデバイスのすべてのバスに対して異なるコマンドシーケンスを使用して、キャッシュ特性を書き込みます。 たとえば、ターゲットデバイスが IEEE 1394 バスに接続され、縮小ブロックコマンド (RBC) プロトコルを使用している場合、イニシエーターはデバイスのモードデータのページ6を取得して、書き込みキャッシュが有効になっているかどうかを判断する必要があります。 ただし、ターゲットデバイスが SCSI に準拠している場合、イニシエーターはモードデータのページ8を取得する必要があります。 書き込みキャッシュのプロパティメカニズムは、イニシエーターからこれらの操作の詳細を非表示にし、異なるバス間で同じストレージデバイスの書き込みキャッシュの特性を照会する手法を提供します。

書き込みキャッシュプロパティのメカニズムは、RAID デバイスではサポートされていません (これらのデバイスに対してクエリを実行するための標準的な手法がないため)。または、フラッシュメモリデバイス用です。

書き込みキャッシュプロパティは、Windows の64ビットバージョンでサポートされています。

 

 




