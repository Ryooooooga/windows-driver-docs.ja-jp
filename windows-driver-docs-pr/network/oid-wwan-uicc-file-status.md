---
title: OID_WWAN_UICC_FILE_STATUS
description: OID_WWAN_UICC_FILE_STATUS は、指定された UICC ファイルに関する情報を取得します。
ms.assetid: 1FD3E140-1CE3-416C-8CB4-27012363B60B
ms.date: 04/09/2019
keywords: -Windows Vista 以降のネットワークドライバーの OID_WWAN_UICC_FILE_STATUS
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: d0d247384205d1d439e77bf86224ece343ce9c17
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843769"
---
# <a name="oid_wwan_uicc_file_status"></a>OID_WWAN_UICC_FILE_STATUS

OID_WWAN_UICC_FILE_STATUS は、指定された UICC ファイルに関する情報を取得します。 

クエリペイロードには、ターゲットファイルに関する情報を含む[**NDIS_WWAN_UICC_FILE_PATH**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_uicc_file_path)構造が含まれます。 ミニポートドライバーは、クエリ要求を非同期的に処理し、最初に元の要求に NDIS_STATUS_INDICATION_REQUIRED を返してから、指定されたファイルを記述する[**NDIS_WWAN_UICC_FILE_STATUS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_uicc_file_status)構造を含む[NDIS_STATUS_WWAN_UICC_FILE_STATUS](ndis-status-wwan-uicc-file-status.md)状態通知を送信する必要があります。 

Set 要求は適用できません。

## <a name="remarks"></a>注釈

この OID の使用方法の詳細については、「 [MB UICC アプリケーションとファイルシステムアクセス](mb-uicc-application-and-file-system-access.md)」を参照してください。

## <a name="requirements"></a>要件

|   |   |
| --- | --- |
| バージョン | Windows 10 バージョン 1903 |
| Header | Ntddndis (Ndis .h を含む) |

## <a name="see-also"></a>関連項目

[MB UICC アプリケーションとファイルシステムアクセス](mb-uicc-application-and-file-system-access.md)

[NDIS_STATUS_WWAN_UICC_UICC_FILE_STATUS](ndis-status-wwan-uicc-file-status.md)

[**NDIS_WWAN_UICC_FILE_PATH**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_uicc_file_path) 

[**NDIS_WWAN_UICC_FILE_STATUS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_uicc_file_status)
