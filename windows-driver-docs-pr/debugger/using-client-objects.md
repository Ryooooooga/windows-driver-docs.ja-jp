---
title: クライアント オブジェクトの使用
description: クライアント オブジェクトの使用
ms.assetid: 07311a2e-86a7-4985-9dfa-55a876cd7899
keywords:
- デバッガーエンジン、COM インターフェイス
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: a671b96d256c265f66745fb205fba64133c16884
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72834241"
---
# <a name="using-client-objects"></a>クライアント オブジェクトの使用


デバッガーエンジンとの対話におけるクライアントオブジェクトの役割の概要については、「[クライアントオブジェクト](client-objects.md)」を参照してください。

一般に、クライアントのメソッドを呼び出すことができるのは、クライアントが作成されたスレッドからだけです。 通常、間違ったスレッドから呼び出されたメソッドは直ちに失敗します。 このルールの注目すべき例外は、 [**createclient**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-createclient)です。このメソッドは、任意のスレッドから呼び出すことができ、呼び出し元のスレッドで使用できる新しいクライアントを返します。 その他の例外については、「参照」セクションで説明しています。

クライアントオブジェクトを記述する文字列は、 [**GetIdentity**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-getidentity)メソッドによって返されるか、 [**OutputIdentity**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-outputidentity)を使用してエンジンの出力ストリームに書き込むことができます。

### <a name="span-idcom_interfacesspanspan-idcom_interfacesspancom-interfaces"></a><span id="com_interfaces"></span><span id="COM_INTERFACES"></span>COM インターフェイス

デバッガーエンジン API には、COM に似たインターフェイスがいくつか含まれています。**IUnknown**インターフェイスを実装します。

「[デバッグエンジンインターフェイス](https://docs.microsoft.com/windows-hardware/drivers/debugger/client-com-interfaces)」で説明されているインターフェイスは、クライアントによって実装されます (ただし、必ずしも最新バージョンではありません)。 COM メソッド**IUnknown:: QueryInterface**を使用して、これらのインターフェイスを他のいずれからでも取得できます。

クライアントは**IUnknown** COM インターフェイスを実装し、それを使用して参照カウントとインターフェイスの選択を維持します。 ただし、クライアントは登録されている COM オブジェクトではありません。 メソッド**iunknown:: AddRef**は、オブジェクトの参照カウントをインクリメントするために使用され、メソッド**Iunknown:: Release**は参照カウントをデクリメントするために使用されます。 **Iunknown:: QueryInterface**が呼び出されると、参照カウントがインクリメントされます。したがって、クライアントインターフェイスポインターが不要になった場合は、 **Iunknown:: Release**を呼び出して参照カウントをデクリメントする必要があります。

クライアントオブジェクトが[**Debugcreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-debugcreate)または[**debugcreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-debugconnect)を使用して作成されると、参照カウントが1に初期化されます。

参照カウントをインクリメントおよびデクリメントする必要がある場合の詳細については、Platform SDK を参照してください。

**IUnknown:: QueryInterface**、 **debugcreate**、および**debugcreate**はそれぞれ、引数の1つとしてインターフェイス ID を受け取ります。 このインターフェイス ID は、 **\_\_uuidof**演算子を使用して取得できます。 次に、例を示します。

```cpp
IDebugClient * debugClient;
HRESULT Hr = DebugCreate( __uuidof(IDebugClient), (void **)&debugClient );
```

**重要**  idebug\* インターフェイスなど[**のインターフェイス (** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nn-dbgeng-idebugeventcallbacks) com など) は適切な com api ではありません。 マネージコードからこれらのインターフェイスを呼び出すことは、サポートされていないシナリオです。 ガベージコレクションやスレッド所有権などの問題により、マネージコードを使用してインターフェイスを呼び出すと、システムが不安定になる可能性があります。

 

 

 





