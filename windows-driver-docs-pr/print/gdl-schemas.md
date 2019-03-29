---
title: GDL スキーマ
description: GDL スキーマ
ms.assetid: 1020bec8-3b34-4391-9e75-9ffcd8b07785
keywords:
- GDL WDK、スキーマ
- WDK GDL スキーマ
- WDK GDL、例のスキーマ
- WDK GDL、例を構築します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8f4f642c799cab763952b8b66e9e6d6843e3205a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56570965"
---
# <a name="gdl-schemas"></a>GDL スキーマ


GDL パーサーを作成してデータに基づくスキーマを実装できます。 スキーマは、指定した場合、パーサーを実行、スキーマを検証し、データを変換します。

A*スキーマ*構造と関連付けられている GDL ソース ファイル内のデータの形式について説明します。 自体 GDL ソース データ ファイル内でスキーマを定義することができますか GDL ソース データ ファイルによって参照する別のファイルであることができます。 スキーマは、各構成体および各属性を定義する時間数内で表示できるデータ エントリを定義します。 たとえば、人を記述するコンス トラクターを定義できます。 コンストラクトをユーザーの名前、birthdate、高さ、重量、自宅の住所、およびいくつかの雇用の情報を含めることができます。

GDL データは、次のコード例のようなものになります。

```cpp
*Person: person_ID
{
  *Name:
  *Birthdate:
  *Height:
  *Weight:
  *HomeAddress:
  *EmploymentInfo:
} 
```

\*HomeAddress と\*EmploymentInfo 情報の論理的なグループを表す、次のコード例のように、構成要素として定義することもできます。

```cpp
*HomeAddress:
{
  *StreetAddress:
  *Apt_Number:
  *City:
  *State:
  *Zip:
}

*EmploymentInfo:
{
  *Employer:
  *Address:
  *Position:
  *Salary:
  *StartDate:
}
```

前の例に示すような GDL コンストラクトは、それらの構造と内容の任意の構文規則を定義してください。 たとえば、することが 2 つのインスタンス、\*人が構築を指定する 1 つ\*キログラムと、その他の重みを指定する\*ポンド単位で重み。 これらの複数のインスタンスには、不整合を可能性があります。

GDL スキーマでは、正式に構造とデータを受信する必要がありますに準拠しているコンテンツを指定するメソッドを提供します。 パーサーは、このスキーマに対してデータを検証し、データまたはデータの構造体が、スキーマに準拠していないかどうかに警告されます。 エントリは必須またはオプション (Apt) のようなまたは、複数回のエントリができるかどうかが定義されたかどうかを指定できます。 たとえば、 \*Apt\_番号は省略可能な可能性がありますが、1 人のユーザーは、2 つのジョブを保持できます。

スキーマでは、共有し、継承されるエントリの定義ができます。 スキーマ定義など\*アドレス\*で共有できる EmploymentInfo \*HomeAddress。 スキーマは、既存の定義から派生する新しい定義を許可します。 2 つのアドレス構造は、バリアントは、一般的な継承された定義から派生することができるので、同一である必要はありません。

指定された属性値の形式を指定するスキーマを使用できます。 たとえば、スキーマでは、年-月-日形式で日付の値を指定することを要求できます。 パーサーの構成要素に複合型の値式を分解し、それらをスナップショットに表示することもできます。 など、クライアント アプリケーションでは、として次のコード例は、次の 3 つの個別のフィールドに分解する日付をする可能性があります。

```cpp
*Date:
{
  *Month: Jan
  *Day: 1
  *Year: 2001
}
```

継承をサポートするスキーマの機能は、その他の影響を与えます。 当然ながら、継承を使用すると、互換性を維持しながら、スキーマを拡張できます。 別のスキーマに派生スキーマに準拠したデータ ファイルから派生したスキーマが自動的にある場合は、元のスキーマに準拠しても。 この継承により、そのスキーマをカスタマイズするベンダー (と暗黙のデータ ファイル) マスター スキーマ (および、すべてのスキーマ マスターへの準拠を必要とするアプリケーション) との互換性を維持したままです。 実際には、仕入先がのみマスターのスキーマを定義するファイルを参照およびマスター スキーマの定義から継承する新しい定義を作成する必要があります。 仕入先は、スキーマ マスターのプライベート コピーを作成または任意の方法でマスターのスキーマを変更する必要はありません。 このような状況により、ベンダーは、マスターのスキーマが、その後に変更された場合、対処は必要ありません。

前の例に示す、継承を使用すると、一般的なパターンを考慮して、定義と付属のメンテナンスの不要な重複を避けるためです。 その結果、スキーマとそれが表すデータ セットは考え抜かと論理的に構造化に指定できます。

継承に基づくスキーマを使用する方法の詳細については、次を参照してください。 [GDL テンプレート](gdl-template-structure.md)します。

 

 



