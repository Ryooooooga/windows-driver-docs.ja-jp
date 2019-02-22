---
title: ハンドルの管理
description: ハンドルの管理
ms.assetid: 09d9c836-1754-4a50-92a3-229a3ae05ccb
keywords:
- WDK のファイル システムを処理します。
- 脅威を最小限に抑え、セキュリティ WDK ファイル システム
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0845ab39acdb99bf15bce48f5714355f8d924339
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530365"
---
# <a name="handle-management"></a>ハンドルの管理


## <span id="ddk_handle_management_if"></span><span id="DDK_HANDLE_MANAGEMENT_IF"></span>


ドライバー内でのセキュリティの問題の重要なソースは、ユーザー モードとカーネル モード コンポーネント間で渡されるハンドルの使用です。 次のカーネルの環境内でハンドルの使用状況と既知の問題のいくつか。

-   カーネル ドライバーには間違った種類のハンドルを渡すアプリケーション。 ファイル オブジェクトが必要な場所にイベント オブジェクトを使用しようとしています。 カーネル ドライバーがクラッシュする可能性があります。

-   アプリケーションで必要なアクセスがないオブジェクトへのハンドルを渡します。 カーネル ドライバーでは、ユーザーはそのためには適切なアクセス許可を持っていなくて、カーネル モードからの呼び出しが含まれているためにを動作する操作を実行可能性があります。

-   値を通過するアプリケーションは、アドレス空間で有効なハンドルではありませんが、システムに対して悪意のある操作を実行するシステム ハンドルとしてマークされます。

-   値を通過するアプリケーションは、デバイス オブジェクト (このドライバーを作成していないハンドル) の適切なハンドルではありません。

これらの問題を防止するには、カーネル ドライバーは特にそれに渡されたハンドルが有効であることを確認するように注意してくださいにあります。 最も安全なポリシーでは、ドライバーのコンテキスト内のすべての必要なハンドルを作成します。 カーネル ドライバー、によって作成されたこれらのハンドルは、OBJ を指定する必要があります\_カーネル\_ハンドル オプションではハンドルを作成、有効な任意のプロセスのコンテキストとカーネル モードの呼び出し元からのみアクセスできる 1 つであり、します。

アプリケーション プログラムによって作成されたハンドルを使用するドライバー、これらのハンドルの使用を十分注意して行う必要があります。

-   ベスト プラクティスは、呼び出すことによって、ハンドルをオブジェクト ポインターに変換する[ **ObReferenceObjectByHandle**](https://msdn.microsoft.com/library/windows/hardware/ff558679)、適切なを指定する*AccessMode* (通常は Irpから&gt;Requestormode で)、 *DesiredAccess*、および*ObjectType* IoFileObjectType または ExEventObjectType などのパラメーター。

-   呼び出し内で直接ハンドルを使用する場合は、関数の Nt バリアントではなく、Zw 系の関数を使用することをお勧めします。 前のモードになるため、オペレーティング システムによってパラメーターのチェックおよびハンドルの検証が適用されますこの**UserMode**および信頼されていないためです。 以前のモードの場合に、ポインターである Nt 関数に渡されるパラメーターが検証を失敗可能性がありますので注意して**UserMode**します。 Nt と Zw ルーチンを返す、 *IoStatusBlock* parameterwith のエラー情報をエラーを確認する必要があります。

-   エラーする必要がありますが適切にトラップを使用しても\_\_お試しくださいと\_\_に応じてを除きます。 さまざまなキャッシュ マネージャー (Cc)、メモリ マネージャー (Mm)、およびファイル システムのランタイム ライブラリ ルーチン (FsRtl) エラーが発生したときに、例外が発生します。

ドライバーはこれまで使用してハンドル上で適切な対策を講じることがなく、ユーザー モード アプリケーションから渡されるパラメーター。

ファイルを開くには、Nt バリアントを使用する場合、Nt バリアントする必要がありますも使用すること、ファイルを閉じることに注意してください。

 

 



