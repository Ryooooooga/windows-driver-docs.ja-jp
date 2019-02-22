---
title: ポート設定の認証パラメーター
description: ポート設定の認証パラメーター
ms.assetid: 88ac8229-d1d5-4287-8b5d-3a7b9b1f2e89
keywords:
- WDK の NDIS OID 要求をポートします。
- NDIS ポート WDK、OID 要求
- OID 要求 WDK NDIS ポート
- WDK NDIS ポートの認証パラメーター
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 09cb15313092b834341bbe840f576ade3b36a781
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56557111"
---
# <a name="setting-port-authentication-parameters"></a>ポート設定の認証パラメーター





NDIS および上にあるドライバーを使用して、 [OID\_GEN\_ポート\_認証\_パラメーター](https://msdn.microsoft.com/library/windows/hardware/ff569623) OID は、NDIS ポートの現在の状態を設定する要求を設定します。 NDIS ポートをサポートするミニポート ドライバーでは、この OID をサポートする必要があります。

ミニポート ドライバーが、受信ポートの方向、ポートのコントロールの状態を使用して状態からの認証とセットの要求が成功した場合、 [ **NDIS\_ポート\_認証\_パラメーター**](https://msdn.microsoft.com/library/windows/hardware/ff566788)構造体。

ミニポートを生成する必要があります、 [ **NDIS\_状態\_ポート\_状態**](https://msdn.microsoft.com/library/windows/hardware/ff567415)状態の変更の上にあるドライバーに通知する状態を示す値。

 

 




