---
title: 印刷 Web ページの ASP 変数
description: 印刷 Web ページの ASP 変数
ms.assetid: eab0d5e0-0e20-443c-b714-a2b2327894e4
keywords:
- カスタマイズされた印刷 Web ページ WDK、ASP の変数
- ASP 変数 WDK プリンター
- セッション変数 WDK プリンター
- WDK 印刷の Web ページ、ASP の変数
- Web ページの WDK プリンター、ASP の変数
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: baa8aa3dcbf93262ad5be4b3d4ebe39d9bd9e9d6
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67380702"
---
# <a name="asp-variables-for-print-web-pages"></a>印刷 Web ページの ASP 変数





Microsoft では、印刷のカスタマイズされた Web ページによって使用される一連の ASP セッション変数を提供します。 次の表は、セッション変数を一覧表示します。 カスタマイズされた ASP ファイルは、これらの変数を変更する必要があります。 示されるように、いくつかの変数は有効なは、Microsoft の TCP/IP ポート モニタは、プリンターの使用されている場合のみです。

いくつかの変数は、URL の装飾を使用して他のユーザーが渡されたときにセッション変数としてに渡されます。 セッション変数にセッションを使用してアクセスできます ("*VariableName*")。 装飾の URL で渡されるパラメーターは、要求を使用してアクセスできます ("*VariableName*")。 [状態] ページを自動的に更新する場合、redecorate URL ページに必要な変数を使用する必要するがあります。 URL では、要求の変数を渡す必要があります、ために、エンコードおよびデコードする ANSI から Unicode 表現への変換する必要があります。 "OlePrn.OleCvt"を持つ COM ProgID には、ヘルパー オブジェクトは、エンコードおよびデコードの URL および Unicode で使用される、ANSI との間に有効にする用意されています。 このオブジェクトの 2 つのメソッド[ **IOleCvt::EncodeUnicodeName**](https://docs.microsoft.com/windows-hardware/drivers/print/iolecvt-encodeunicodename)、および[ **IOleCvt::DecodeUnicodeName**](https://docs.microsoft.com/windows-hardware/drivers/print/iolecvt-decodeunicodename)に変換するために使用できますANSI、unicode と ansi、Unicode からそれぞれします。 この変換は、セッション変数に対して実行する必要はありません。

変数値の TCP/IP ポート変数をエンコードしますか。
監視のみですか。
型の MS\_ASP1

最初の Web ページがプリンター固有の詳細を記述するために使用するディレクトリ パス。

X

要求

X

MS\_コミュニティ

プリント サーバーの SNMP コミュニティ名。

〇

要求

X

MS\_コンピューター

プリント サーバーのコンピューターの名前。

X

セッション

X

MS\_DefaultPage

プリンター固有の詳細情報の既定の ASP ファイル。

X

セッション

X

MS\_デバイス

プリンターの SNMP デバイスのインデックス。

〇

要求

X

MS\_DHTMLEnabled

**TRUE**クライアントは、動的 HTML; をサポートしている場合それ以外の場合**FALSE**します。

X

セッション

X

MS\_IPAddress

プリンターの IP アドレスです。

〇

要求

X

MS\_LocalServer

プリント サーバーの識別子です。 これには、IP アドレスまたはコンピューター名のいずれかがあります。

X

セッション

X

MS\_モデル

プリンター ドライバーの名前。

X

要求

〇

MS\_Portname

プリンターのポートの名前。

X

要求

〇

MS\_プリンター

プリンターの名前。

X

要求

〇

MS\_SNMP

**TRUE**それ以外の場合に、プリンターの SNMP を使用したしているか**FALSE**します。

〇

要求

X

MS\_URLPrinter

エンコードされた URL の形式でのプリンターの名前。

X

要求

〇

 

セッションの変数は、ASP ページが呼び出されたプリンターは、「現在」プリンターのプロパティを指定します。 現在のプリンターの追加のプリンターのプロパティを取得する、または別のプリンターのプロパティを取得するを参照してください。 [ActiveX オブジェクト印刷 Web ページの](activex-objects-for-print-web-pages.md)します。

 

 




