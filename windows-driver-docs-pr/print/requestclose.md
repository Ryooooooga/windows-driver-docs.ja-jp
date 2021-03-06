---
title: requestClose 要素
description: 省略可能な requestClose 要素は、クライアントコンピューター上のイベント通知メッセージを閉じるために使用されます。
ms.assetid: b2f21ab2-9205-483c-9f56-1c877edb7da2
keywords:
- requestClose 要素の印刷デバイス
topic_type:
- apiref
api_name:
- requestClose
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: c9541b545622da30f54c10438a6b54e3d2868849
ms.sourcegitcommit: ab64169b631da4db3f0b895600f1c38a22cb7e2e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/03/2020
ms.locfileid: "75652998"
---
# <a name="requestclose-element"></a>requestClose 要素

省略可能な**Requestclose**要素は、クライアントコンピューター上のイベント通知メッセージを閉じるために使用されます。

**Requestclose**要素は、この URI: [https://schemas.microsoft.com/2003/print/asyncui/v1/request](https://schemas.microsoft.com/2003/print/asyncui/v1/request)の*asyncui*名前空間で定義されています。 (このリソースは、一部の言語および国では使用できません。)

## <a name="usage"></a>使用方法

```xml
<requestClose/>
```

## <a name="attributes"></a>属性

属性はありません。

## <a name="child-elements"></a>子要素

子要素はありません。

## <a name="parent-elements"></a>親要素

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>要素</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="asyncprintuirequest.md" data-raw-source="[&lt;strong&gt;asyncPrintUIRequest&lt;/strong&gt;](asyncprintuirequest.md)"><strong>asyncPrintUIRequest</strong></a></p></td>
<td><p></p>
<p>クライアントコンピューターでメッセージを作成するためにプリンタードライバーによって発行された要求を記述する必須の要素。</p></td>
</tr>
</tbody>
</table>

## <a name="examples"></a>例

次のコード例では、 **[OK** ] ボタンのメッセージボックスをクリックした後に、イベント通知を閉じる方法を示しています。

```cpp
<?xml version="1.0" ?>
   <asyncPrintUIResponse
    xmlns="https://schemas.microsoft.com/2003/print/asyncui/v1/response">
    <v1>
      <requestClose>
        <messageBoxUI>
          <buttonID>IDOK</buttonID>
        </messageBoxUI>
      </requestClose>
    </v1>
  </asyncPrintUIResponse>
```

## <a name="see-also"></a>「

[asyncPrintUIRequest](asyncprintuirequest.md)

[requestOpen](requestopen.md)
