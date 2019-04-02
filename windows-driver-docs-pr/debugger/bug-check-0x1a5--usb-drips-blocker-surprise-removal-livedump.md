---
title: バグ チェック 0x1A5 USB_DRIPS_BLOCKER_SURPRISE_REMOVAL_LIVEDUMP
description: USB_DRIPS_BLOCKER_SURPRISE_REMOVAL_LIVEDUMP のバグ チェックでは、0x000001A5 の値を持ちます。 これは、USB デバイスが突然 DRIPS ファイアウォールによってブロックされているため、削除になることを示します。
keywords:
- バグ チェック 0x1A5 USB_DRIPS_BLOCKER_SURPRISE_REMOVAL_LIVEDUMP
- USB_DRIPS_BLOCKER_SURPRISE_REMOVAL_LIVEDUMP
ms.date: 01/10/2019
topic_type:
- apiref
api_name:
- USB_DRIPS_BLOCKER_SURPRISE_REMOVAL_LIVEDUMP
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 3979c2d637f6f979d937ff486030c043e744485e
ms.sourcegitcommit: ece0a2affa08f1b6446368ede06040b3153aaae2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/23/2019
ms.locfileid: "56743556"
---
# <a name="bug-check-0x1a5-usbdripsblockersurpriseremovallivedump"></a>バグ チェック 0x1A5 の。USB\_DRIPS\_BLOCKER\_突然\_削除\_LIVEDUMP

USB\_DRIPS\_BLOCKER\_突然\_削除\_LIVEDUMP バグ チェックが 0x000001A5 の値を持ちます。 これは、USB デバイスが突然 DRIPS ファイアウォールによってブロックされているため、削除になることを示します。

**重要な**プログラマ向けのトピックです。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)します。

## <a name="usbdripsblockersurpriseremovallivedump-parameters"></a>USB\_DRIPS\_BLOCKER\_突然\_削除\_LIVEDUMP パラメーター

|パラメーター|説明|
|--- |--- |
|1| ブロックしているデバイスの PDO します。|
|2| 予約済み。 |
|3| 予約済み。 |
|4| 予約済み。 |

## <a name="cause"></a>原因
-----

USB デバイスが最新のスタンバイ中に電源をオフから最上位レベルのコント ローラーをブロックしていると驚きを結果として、削除予定します。

(このコードは、実際のバグチェックには使用されません。 ライブ ダンプの識別に使用されます)。


## <a name="see-also"></a>関連項目
----------

[バグチェック コード リファレンス](bug-check-code-reference2.md)
