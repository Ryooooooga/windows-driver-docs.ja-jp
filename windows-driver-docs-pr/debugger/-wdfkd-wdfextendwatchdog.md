---
title: wdfkd.wdfextendwatchdog
description: Wdfkd.wdfextendwatchdog 拡張機能は、電源の遷移中に、フレームワークのウォッチドッグのタイマーの (10 分 ~ 24 時間) からのタイムアウト期間を拡張します。
ms.assetid: 6feb922f-0016-468c-8dd2-963db6874977
keywords:
- デバッグ wdfkd.wdfextendwatchdog Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wdfkd.wdfextendwatchdog
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 0e1f512d9629a13f17a7daac8bd4413b6e5d4c99
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63341719"
---
# <a name="wdfkdwdfextendwatchdog"></a>!wdfkd.wdfextendwatchdog


**! Wdfkd.wdfextendwatchdog**拡張機能の拡張、タイムアウト期間 (24 時間に 10 分) から、フレームワークのウォッチドッグのタイマーの電源の遷移中にします。

```dbgcmd
!wdfkd.wdfextendwatchdog Handle [Extend]
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______Handle______"></span><span id="_______handle______"></span><span id="_______HANDLE______"></span> *ハンドル*   
WDFDEVICE に型指定されたオブジェクトへのハンドル。

<span id="_______Extend______"></span><span id="_______extend______"></span><span id="_______EXTEND______"></span> *拡張*   
(省略可能)。 有効またはタイムアウト期間の拡張機能を無効にするかどうかを示す値。 場合*拡張*0 は、拡張機能を無効にすると、およびタイムアウト期間は 10 分です。 場合*拡張*は 1、拡張機能が有効になっている、およびタイムアウト期間は 24 時間です。 既定値は 1 です。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Wdfkd.dll

### <a name="span-idframeworksspanspan-idframeworksspanspan-idframeworksspanframeworks"></a><span id="Frameworks"></span><span id="frameworks"></span><span id="FRAMEWORKS"></span>フレームワーク

KMDF 1

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

詳細については、次を参照してください。[カーネル モード ドライバー フレームワークのデバッグ](kernel-mode-driver-framework-debugging.md)します。

<a name="remarks"></a>注釈
-------

それを呼び出すたびに、電源ポリシーまたは電源イベントのコールバック関数の電源がオフのドライバーに対してページング可能なフレームワークが、内部ウォッチドッグ タイマーを開始 (操作は、\_POWER\_ページング可能なビットがクリアされて)。 コールバック関数がページング i/o、ためブロックされた場合は、要求の処理を使用可能なページングのデバイスがないため、オペレーティング システムがハングします。

タイムアウト期間が経過すると、フレームワークのバグ チェック 0x10D 問題 (WDF\_違反)。 詳細については、次を参照してください。 [**バグ チェック 0x10D**](bug-check-0x10d---wdf-violation.md)します。

 

 





