---
title: コンテキストとデータ フローの関連付け
description: コンテキストとデータ フローの関連付け
ms.assetid: 75f5838e-626d-4a59-810e-fec9a40640ed
keywords:
- コールアウトの分類 WDK Windows フィルタリングプラットフォーム、データフローに関連付けられたコンテキスト
- コンテキスト WDK Windows フィルタリングプラットフォーム
- flowContext パラメーター WDK Windows フィルタリングプラットフォーム
- コンテキストとデータフローの関連付け (WDK Windows フィルタリングプラットフォーム)
ms.date: 01/14/2019
ms.localizationpriority: medium
ms.openlocfilehash: 92dda65f7dce594d8e7bc0535a5b115a80ae3326
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838233"
---
# <a name="associating-context-with-a-data-flow"></a>コンテキストとデータ フローの関連付け


データフローをサポートするフィルター処理レイヤーでデータを処理するコールアウトの場合、コールアウトドライバーは、コンテキストを各データフローに関連付けることができます。 このようなコンテキストは、フィルターエンジンに対して非透過的です。 コールアウトの[classid](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)関数は、このコンテキストを使用して、次にそのデータフローのフィルターエンジンによって呼び出されたときのデータフローに固有の状態情報を保存できます。 フィルターエンジンは、 *flowcontext*パラメーターを使用して、コールアウトの classid 関数にこのコンテキストを渡します。 コンテキストがデータフローに関連付けられていない場合、 *Flowcontext*パラメーターは0になります。

コンテキストをデータフローに関連付けるために、コールアウトの[classid](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)は、 [**FwpsFlowAssociateContext0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsflowassociatecontext0)関数を呼び出します。 次に、例を示します。

```cpp
// Context structure to be associated with data flows
typedef struct FLOW_CONTEXT_ {
  .
  .  // Driver-specific content
  .
} FLOW_CONTEXT, *PFLOW_CONTEXT;

#define FLOW_CONTEXT_POOL_TAG 'fcpt'

// classifyFn callout function
VOID NTAPI
 ClassifyFn(
    IN const FWPS_INCOMING_VALUES0  *inFixedValues,
    IN const FWPS_INCOMING_METADATA_VALUES0  *inMetaValues,
    IN OUT VOID  *layerData,
    IN const FWPS_FILTER0  *filter,
    IN UINT64  flowContext,
    IN OUT FWPS_CLASSIFY_OUT  *classifyOut
  )
{
  PFLOW_CONTEXT context;
  UINT64 flowHandle;
  NTSTATUS status;

  ...

  // Check for the flow handle in the metadata
  if (FWPS_IS_METADATA_FIELD_PRESENT(
      inMetaValues,
      FWPS_METADATA_FIELD_FLOW_HANDLE))
  {
    // Get the flow handle
    flowHandle = inMetaValues->flowHandle;

    // Allocate the flow context structure
    context =
      (PFLOW_CONTEXT)ExAllocatePoolWithTag(
        NonPagedPool,
        sizeof(FLOW_CONTEXT),
        FLOW_CONTEXT_POOL_TAG
      );

    // Check the result of the memory allocation
    if (context == NULL) 
    {
 
      // Handle memory allocation error
      ...
    }
    else
    {

      // Initialize the flow context structure
      ...

      // Associate the flow context structure with the data flow
      status = FwpsFlowAssociateContext0(
                flowHandle,
                FWPS_LAYER_STREAM_V4,
                calloutId,
                (UINT64)context
              );

      // Check the result
      if (status != STATUS_SUCCESS)
      {
        // Handle error
        ...
      }
    }
  }

  ...

}
```

コンテキストが既にデータフローに関連付けられている場合、新しいコンテキストがデータフローに関連付けられるようにするには、まずそのコンテキストを削除する必要があります。 データフローからコンテキストを削除するために、コールアウトの[classid の classid](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)関数は、 [**FwpsFlowRemoveContext0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsflowremovecontext0)関数を呼び出します。 次に、例を示します。

```C++
// Context structure to be associated with data flows
typedef struct FLOW_CONTEXT_ {
  ...
} FLOW_CONTEXT, *PFLOW_CONTEXT;

#define FLOW_CONTEXT_POOL_TAG 'fcpt'

// classifyFn callout function
VOID NTAPI
 ClassifyFn(
    IN const FWPS_INCOMING_VALUES0  *inFixedValues,
    IN const FWPS_INCOMING_METADATA_VALUES0  *inMetaValues,
    IN OUT VOID  *layerData,
    IN const FWPS_FILTER0  *filter,
    IN UINT64  flowContext,
    OUT FWPS_CLASSIFY_OUT  *classifyOut
  )
{
  PFLOW_CONTEXT context;
  UINT64 flowHandle;
  NTSTATUS status;

  ...

  // Check for the flow handle in the metadata
 if (FWPS_IS_METADATA_FIELD_PRESENT(
    inMetaValues,
    FWPS_METADATA_FIELD_FLOW_HANDLE))
  {
    // Get the flow handle
     flowHandle = inMetaValues->flowHandle;

    // Check whether there is a context associated with the data flow
     if (flowContext != 0) 
     {
        // Get a pointer to the flow context structure
        context = (PFLOW_CONTEXT)flowContext;

        // Remove the flow context structure from the data flow
        status = FwpsFlowRemoveContext0(
                  flowHandle,
                  FWPS_LAYER_STREAM_V4,
                  calloutId
                );

      // Check the result
      if (status != STATUS_SUCCESS)
      {
        // Handle error
        ...
      }

      // Cleanup the flow context structure
      ...

      // Free the memory for the flow context structure
      ExFreePoolWithTag(
        context,
        FLOW_CONTEXT_POOL_TAG
        );
    }
  }

  ...

}
```

前の例では、 *Calloutid*変数にコールアウトの実行時識別子が含まれています。 実行時識別子は、コールアウトドライバーがコールアウトをフィルターエンジンに登録したときにコールアウトドライバーに返されたものと同じ識別子です。