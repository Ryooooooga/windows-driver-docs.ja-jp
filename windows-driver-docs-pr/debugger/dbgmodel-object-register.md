---
title: Debugger Data Model - レジスタ オブジェクト
description: 内機械語命令のオペランドで使用されるレジスタは、レジスタ オブジェクトによって記述されます。
ms.date: 12/12/2018
ms.localizationpriority: medium
ms.openlocfilehash: fc14a492fb02de3ff93104ea08517075592babb1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63373396"
---
# <a name="register-objects"></a>登録オブジェクト 
## <a name="summary"></a>概要
内機械語命令のオペランドで使用されるレジスタは、レジスタ オブジェクトによって記述されます。 Register オブジェクトの文字列の変換では、レジスタの名前です。
## <a name="object-properties"></a>オブジェクトのプロパティ
|名前|説明|
|--- |--- |
|ID|レジスタの (特定のアーキテクチャのドメイン) 内で一意の識別子。|

## <a name="remarks"></a>注釈
現時点では、登録の名前は、文字列の変換によってのみ取得できます。