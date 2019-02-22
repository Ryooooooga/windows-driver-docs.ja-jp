---
title: SoC ベースのプラットフォームのハードウェア要件
description: ACPI 5.0 仕様には、Windows を実行している SoC ベースのプラットフォームをサポートするためのハードウェア要件の新しいセットが導入されています。
ms.assetid: C8AA4EE1-D9A6-438E-801B-8EDDF8AA0560
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 807841e42f46a4204619df75a9937f510115a2d0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553112"
---
# <a name="hardware-requirements-for-soc-based-platforms"></a>SoC ベースのプラットフォームのハードウェア要件


[ACPI 5.0 仕様](https://www.uefi.org/specifications)Windows を実行している SoC ベースのプラットフォームをサポートするためのハードウェア要件の新しいセットが導入されています。 ACPI 5.0 は、コストを削減するシステムのハードウェア制限の設計をサポートしていますが、長いバッテリ寿命を有効にするコネクテッド スタンバイ電源モデルをサポートしています。

## <a name="hardware-reduced-acpi-platforms"></a>ACPI プラットフォームのハードウェア制限


Soc をサポートするために Windows に「ACPI のハードウェア仕様」ACPI 5.0 仕様の第 4 章で説明されている機能のいずれかを実装するハードウェア プラットフォームは必要ありません。 ACPI は、次などのハードウェア機能の修正は必要ありません。

-   電源管理 (PM) タイマー
-   ウェイク アップ アラームのリアルタイム クロック (RTC)
-   システム コントロール割り込み (SCI)
-   ハードウェアの固定セットを登録する (PMx\_ \*ステータス/イベント/コントロール レジスタ)
-   GPE ブロックを登録します (GPEx\_ \*ステータス/イベント/コントロール レジスタ)
-   埋め込みコント ローラー

ACPI 固定ハードウェア インターフェイスを実装していないプラットフォームと呼びます*ハードウェアに削減*ACPI プラットフォーム。 プラットフォームとハードウェアに削減は、ことを示す、設定、ハードウェア\_減少\_ACPI フラグで固定 ACPI 説明テーブル (FADT)。

固定ハードウェア機能など、ハードウェアに削減 ACPI プラットフォームで*電源ボタン*、 *lid 状態*などを ACPI 定義のハードウェアに実装されていましたが、排他的に置き換えられますによって、ACPI 定義のソフトウェア対応します。 たとえば、コントロールのメソッドの電源ボタンは、固定のハードウェアと同じではなく使用されます。

## <a name="connected-standby"></a>コネクト スタンバイ


コネクテッド スタンバイ電源モデル (InstantGo デバイスの主な機能) を実装するためのプラットフォームは、ACPI 5.0 で定義されている低電力アイドル状態の S0 機能を提供するプラットフォームとして Windows に公開されます。 プラットフォームがコネクト スタンバイをサポートしていることを示すためには、FADT で「低電力 S0 アイドル対応」のフラグを設定する必要があります。

Windows では、ACPI のハードウェアに削減または完全な ACPI を実装するかどうかに関係なく低電力アイドル状態の S0 機能を備えたプラットフォームをサポートします。 ただし、ACPI 5.0 仕様で必要に応じて Windows を使用しません従来スリープ/再開機能 ACPI 構成に関係なく、低電力アイドル状態の S0 機能を持つ複数のプラットフォームで。

スタンバイ電源が接続されているモデルの詳細については、次を参照してください。[最新スタンバイ](https://msdn.microsoft.com/library/windows/hardware/dn915061)します。

## <a name="acpi-events"></a>ACPI イベント


ACPI 5.0 の仕様の第 4「ACPI ハードウェアの仕様」章の一部として、フル機能のメカニズムは、ハードウェア イベントを通知するために定義されます。 Windows は、仕様で定義されている多数のイベントをサポートし、このサポートは、SoC プラットフォームにも引き継がれます。 ただし、ACPI プラットフォームのハードウェア制限は、GPIO 割り込みは ACPI 定義 GPE/SCI ハードウェアではなく、イベントを通知に使用されます。 イベントは、ただしシグナルは、後に、イベント処理は、ハードウェアに削減し、完全な ACPI プラットフォーム間と同じです。 どちらの場合は、ACPI-指定されたイベント処理メカニズムは、最終的に、適切なデバイス ドライバーを ACPI による通知を送信すると、イベントの適切な制御メソッド (ハンドラー) を呼び出します。

ACPI の GPIO 通知イベントの詳細については、ACPI 5.0 仕様のセクション 5.6.5、「GPIO-Signaled ACPI イベント」を参照してください。 ACPI ソフトウェア イベント処理の詳細については、ACPI 5.0 仕様のセクションで「一般的な目的のイベント処理」、5.6.4 を参照してください。

 

 



