---
title: Object Reference Tracing
description: Object Reference Tracing
ms.assetid: b5af0ab0-954b-4da1-a074-df88d2d039f8
keywords:
- Object Reference Tracing
- オブジェクトの参照をトレースの概要
- GFlags、オブジェクト参照のトレース
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: b9a5d24abbcafb770b7cee6f97ff9117c21592f8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56573635"
---
# <a name="object-reference-tracing"></a>Object Reference Tracing


**オブジェクト参照トレース**機能は、各オブジェクトの参照カウンターをインクリメントする時間またはデクリメントのシーケンシャルなスタック トレースを記録します。 トレースは、二重逆参照、エラーを参照するオブジェクトを逆参照の失敗など、オブジェクト参照エラーを検出するのに役立ちます。 この機能は、Windows Vista および Windows の以降のバージョンでのみサポートされます。

機能のオブジェクト参照のトレースを構成する方法については、**グローバル フラグ**ダイアログ ボックスを参照してください[オブジェクト参照トレースの構成](configuring-object-reference-tracing.md)します。 コマンド プロンプトで、オブジェクト参照のトレース機能を構成する方法の詳細については、次を参照してください。 [ **GFlags コマンド**](gflags-commands.md)します。 例については、次を参照してください。[例 15。オブジェクト参照のトレースを使用して](example-15--using-object-reference-tracing.md)します。

オブジェクト参照のトレースは、特定のオブジェクトが参照されていないことが疑われる場合に最も役に立つまたはも逆参照正しく、通常オブジェクトがリークしていること、またはプロセスまたはセッションを終了することはできません、増加のプールの使用率が示されているため、そのハンドル数には 0 です。 後で確認できるログに記録されたトレースとは異なりオブジェクト参照のトレースは、オブジェクトの中のプロセスが実行中、リアルタイムで使用するに設計されています参照され、逆参照します。 使用して、デバッガーで、オブジェクト参照のトレースを表示する、 [ **! デバッガー拡張が obtrace**](-obtrace.md)します。 この拡張機能には、指定したオブジェクトのアドレスが必要であるために必要がありますがあらかじめわかっているオブジェクトは、エラーの原因。

オブジェクトの参照をトレースに、次の規則が適用されます。

-   一度に 1 つのオブジェクト参照のトレースを行うことができます。

-   カーネル全体のトレースが実用的でないため、トレースは、指定されたプール タグで作成したオブジェクトまたは (イメージ ファイルの名前で示されます)、指定したプロセスまたはその両方によって作成されるオブジェクトを制限する必要があります。

-   トレースごとに 1 つだけのイメージ ファイルを指定することができます。 イメージ ファイルを指定する場合は、トレースは、イメージを表すプロセスによって作成されるオブジェクトに制限されています。 オブジェクト、プロセスによって参照されるが、別のプロセスによって作成されますがトレースされません。

-   各トレースに対して 16 のプール タグの最大数を指定できます。 指定されたプール タグのいずれかを持つオブジェクトがトレースされます。

-   イメージ ファイルと 1 つまたは複数のプール タグの両方を指定する場合は、トレースはプロセスによって作成されていて、指定されたプール タグのいずれかのオブジェクトに制限されています。

-   オブジェクト参照のトレース、トレースが開始されたときに既に実行されているプロセスをトレースできません。 トレースには、トレースが開始した後に起動するプロセスのオブジェクトのみが含まれます。

-   トレース用にマークされているオブジェクトは、オブジェクトが破棄されるか、トレースが無効にするまでにトレースされます。 既定では、オブジェクトのトレースを「永続的な」トレースを指定することが、オブジェクトが破棄されるまでのみ保持されます (**/p**)、トレースがトレースを無効になるまでに保持されます。

-   オブジェクト参照のトレースの構成は、レジストリ設定またはカーネル フラグ (実行時) の設定として格納できます。 レジストリとカーネル フラグの設定の両方がある場合は、実行時の設定は優先順位が、シャット ダウンまたは再起動すると失われます。

 

 




