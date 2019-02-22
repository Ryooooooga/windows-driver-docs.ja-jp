---
title: WIA\_DPS\_スキャン\_利用可能な\_項目
description: WIA\_DPS\_スキャン\_利用可能な\_項目のプロパティは、アプリケーションがプログラムの制御下で実行するプッシュ スキャン操作の入力ソースの名前を提供します。 WIA ミニドライバーは、作成し、このプロパティを保持します。
ms.assetid: 747cd5bb-4746-4086-8a87-08a6728125bc
keywords:
- WIA_DPS_SCAN_AVAILABLE_ITEM イメージング デバイス
topic_type:
- apiref
api_name:
- WIA_DPS_SCAN_AVAILABLE_ITEM
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 200bb4172435ae06fe6bc04265e3b015078d392f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56557038"
---
# <a name="wiadpsscanavailableitem"></a>WIA\_DPS\_スキャン\_利用可能な\_項目


WIA\_DPS\_スキャン\_利用可能な\_項目のプロパティは、アプリケーションがプログラムの制御下で実行するプッシュ スキャン操作の入力ソースの名前を提供します。 WIA ミニドライバーは、作成し、このプロパティを保持します。

プロパティの種類:VT\_BSTR

有効な値 :WIA\_PROP\_NONE

アクセス権:読み取り専用かどうか

<a name="remarks"></a>注釈
-------

Windows 7 以降、WIA で\_DPS\_スキャン\_利用可能な\_WIA スキャナーのデバイスの WIA 項目ツリーのルート項目のオプションのプロパティの項目です。 アプリケーション (ベッド、自動ドキュメント フィーダー付き、またはフィルム スキャン アダプター) から、スキャンを実行する入力ソースを確認するには、このプロパティまたはストレージの場所からデータを転送するクエリを実行できます。

WIA スキャナーの一部のデバイスには、デバイスのフロント パネルで、スキャン ジョブの入力ソースを選択する、または暗黙的に、入力ソースを選択するなど、デバイス上のフィーダーにドキュメントを挿入して、ユーザーが有効にします。 ユーザーは、デバイスのスキャンを開始 ボタンを押すと、アプリケーションがどの入力でこのソースのスキャン操作を開始できるように、ユーザーが選択したソースを決定する必要があります。

スキャン イベントでは、ユーザーが、スキャンを開始しましたが、イベントが入力ソースを表す WIA 項目の名前を指定していないアプリケーションに通知します。 アプリケーションのイベント ハンドラーは、ルート項目の WIA を照会できます\_DPS\_スキャン\_利用可能な\_入力ソース項目の名前を取得する項目のプロパティ。

WIA ツリーで、ルート項目には、1 つまたは複数子項目 (項目のフラット ベッド、フィーダー付きの項目とフィルムの項目デバイス上の入力ソースを表す) があります。 これらの各項目には、パーツや入力ソースの地域を表す子項目の親があります。 ルート アイテムの子であるし、全体としてベッドを表す、ベッド項目には、フラット ベッド サーフェスの個々 の地域を表す子 (これはまた、フラット ベッド項目) を指定できます。 ルート アイテムの子であるし、自動ドキュメント フィーダーを表すフィーダー項目を子フィーダーを通過するドキュメントのページのフロント エンドとバックエンドの辺のスキャナーを表すことができます。 ルート アイテムの子であるし、全体として、フィルム スキャンのアダプターを表す、フィルム項目には、個々 のフィルムのフレームを表す子 (これはまた、フィルムの項目) を指定できます。 スキャン、WIA のユーザーによって要求された操作に応じて\_DPS\_スキャン\_利用可能な\_項目のプロパティは、フラット ベッド、送り、または、ルートの子であるフィルムの項目を名前できますまたは次のいずれかの子の名前を付けること項目。 これらの項目に関する詳細については、次を参照してください。 [WIA 項目カテゴリ](https://msdn.microsoft.com/library/windows/hardware/ff552678)します。

ドライバーが、WIA をすぐに設定のスキャン イベントが発生する、\_DPS\_スキャン\_利用可能な\_項目プロパティの値、WIA 項目の名前を (によって報告されたとおりに、 [ **WIA\_IPA\_項目\_名前**](wia-ipa-item-name.md)アイテムのプロパティ) スキャン ジョブがこの情報がわかっている場合に使用可能な入力ソースを識別します。 それ以外の場合、入力ソースが不明な場合は、ドライバーは、空の文字列にプロパティの値を設定します。 アプリケーションでは、スキャンのイベントを消費するときのスキャン イベントの変更の状態が非シグナル状態にシグナル状態になり、ドライバー、WIA をリセットします\_DPS\_スキャン\_利用可能な\_項目プロパティの値を空の文字列。

このプロパティの詳細については、次を参照してください。[スキャンのイベントの入力ソースを識別する](https://msdn.microsoft.com/library/windows/hardware/ff542704)します。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Wiadef.h (Wiadef.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**WIA\_IPA\_項目\_名**](wia-ipa-item-name.md)

 

 





