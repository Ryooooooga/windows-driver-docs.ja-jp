---
title: 動的な形式の変更
description: 動的な形式の変更
ms.assetid: 41e6ec8c-3a96-4103-a991-3b9ba6acad6c
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f9823ff3b834baf340a14bdc00af82332eb3cb2f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558853"
---
# <a name="dynamic-format-change"></a>動的な形式の変更


動的な形式の変更は、Windows 7 および以降のバージョン形式を動的に変更するオーディオのアプリケーションとオーディオのアダプターの間にオーディオ データをストリーミングするために使用できる Windows オペレーティング システムの機能です。 動的な形式の変更は、高品位のマルチ メディア インターフェイス (HDMI) デバイスでオーディオ ストリーミングの動作に対応します。 このトピックでは、動的形式の変更の概要を説明し、そのしくみについて説明します。

動的な形式の変更が使用されているシナリオを以下に示します。

-   **HDMI デバイスは、新しい機能を提示します。** オーディオおよびビデオの転送に使用される HDMI 帯域幅の合計は固定されて、HDMI デバイス ストリーム オーディオまたはビデオ データまたはその両方とビデオのシグナルが容量の割り当ての基本設定を指定します。 これは、コンピューターに接続されているデバイスを表示、HDMI があり、ディスプレイの解像度を変更する場合に影響するコンピューターにオーディオ データ転送用に残っている帯域幅のサイズを意味します。

    たとえば、HDMI デバイスが最初に、192 KHz、特定の表示モードでの 16 ビット ステレオに設定されているデータ形式で構成されているものとします。 別の表示モードに変更するとストリーミング オーディオ データの残りの帯域幅が十分でない 192 KHz 形式。 デバイス ドライバーを表示モードの変更について、接続されているコンピューターのオーディオのサービスに通知すると、これにより、オーディオ ドライバー、およびオーディオ データ形式を再ネゴシエートするオーディオ サービス。 残りの帯域幅内で現在選択されている 192 KHz 形式をストリーミングすることはできません、新しい形式が選択されます。 形式のネゴシエーション プロセスの詳細については、次を参照してください。[形式ネゴシエーション](format-negotiation.md)します。

    HDMI 関連の動的形式変更のもう 1 つのシナリオで、オーディオ デバイスを取り外してと新しい、HDMI 対応デバイスを接続します。 HDMI デバイスのデバイス ドライバーは、形式変更イベントを生成し、オーディオのサービスにデバイス ドライバーを使用したオーディオ データ形式が再度ネゴシエートします。

-   **いくつかのスタンドアロンのオーディオ デバイスは、オーディオ データ形式を変更するユーザーが使用できるハードウェア コントロールを提供します。** このシナリオで、ユーザーなど、オーディオ データ形式を選択するサラウンド サウンド アンプ上のコントロールのノブを操作します。 スタンドアロンのオーディオ デバイスに接続されているコンピューターの場合、この新しく選択したデータ形式が原因データ形式を外し、場合によっては、変更するコンピューターに接続されているオーディオ ドライバー。

-   **コントロール パネルの サウンド アプレットのサード パーティ製の UI では、有効またはシステムの効果を無効にするためのオプションを提供します。** 独自システム エフェクト オーディオのオブジェクト (sAPOs) の処理を開発する際にも用のカスタム UI を提供できます、**サウンド**コントロール パネル にします。 このカスタム UI の変更を含めることができます、**エンハンス**または**詳細**のタブ、**サウンド**アプレットまたはその両方です。 このシナリオでユーザーがチェック ボックスを選択、**エンハンス**タブを有効または変更するオーディオ データ形式を必要とするグローバル システム エフェクト (GFX) 機能を無効にします。 ユーザーによる選択が原因の形式の変更イベントを生成する HDMI ドライバー。 オーディオのサービスでは、このイベントに関する通知を受信し、オーディオ ドライバー、オーディオ データの新しい形式を選択すると再度ネゴシエートします。

HDMI と IEC61937 準拠圧縮 Dolby Digital とデジタル シアター サウンド (DTS) などのオーディオ形式のサポートを提供する Windows 7 およびそれ以降の Windows オペレーティング システムでサブタイプ Guid (KS) プロパティをストリーミングするカーネルで使用するための新しいセットが提供し、構造体。 電気技術標準機関 IEC (国際) の standard、IEC 61937 は、非線形を転送するデジタル オーディオ インターフェイスに適用されます[PCM](pcm-stream-data-format.md)ビット ストリームにエンコードします。 サブタイプ Guid の詳細についてを参照してください、KSDATAFORMAT\_サブタイプ\_IEC61937\_Ksmedia.h で Xxx Guid。

**注**  エンドポイント ビルダーが新しい既定のデバイスのデータ形式を再計算し、オーディオ エンドポイント ビルダーが動的形式の変更通知を受信し、デバイス ドライバーでは、提案されたデータの形式はサポートされていない、ときにします。

デバイスの既定の形式として、新しい形式を選択するエンドポイント ビルダーを強制的にオーディオ ドライバーを再設計された新しい形式がサポートするようになりましたの場合。 デバイスの既定値として新しい形式に強制的に、移行をオーディオ ドライバーは古い形式に関する受信した形式のサポート クエリに失敗する必要があります。 失敗した形式のサポート クエリは、形式変更通知をトリガーし、エンドポイント ビルダーでは、デバイスの新しい既定の形式を計算します。

 

 

 



