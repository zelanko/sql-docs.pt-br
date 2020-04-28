---
title: Filtrando registros atualizados | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- filtering for updated records [ADO]
ms.assetid: 4a798921-d7bb-47c9-a252-550fd9463ec9
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0b5afe84664719da5a1dbc7777aef524be28c459
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67925333"
---
# <a name="filtering-for-updated-records"></a>Filtrar os registros atualizados
Antes de chamar UpdateBatch, você pode usar a propriedade filtro do conjunto de registros para exibir somente os registros que foram alterados desde que o conjunto de registros foi aberto ou a última chamada para UpdateBatch. Para fazer isso, defina Filter igual a adFilterPendingRecords para determinar quantos registros serão atualizados, conforme mostrado no exemplo de código na próxima seção.  
  
## <a name="remarks"></a>Comentários  
 Este exemplo estende o exemplo de UpdateBatch anterior filtrando o conjunto de registros antes de chamar o UpdateBatch, mostrando o usuário quais registros serão alterados e permitindo que ele cancele a atualização (usando o método CancelBatch).  
  
```  
'BeginFilterPend  
    '...  
    objRs1.Open strSQL, strConn, adOpenStatic, adLockBatchOptimistic, adCmdText  
  
    ' Change value of Phone field for first record in Recordset, saving value  
    ' for later restoration.  
    intId = objRs1("ShipperId")  
    sPhone = objRs1("Phone")  
  
    objRs1("Phone") = "(111) 555-1111"  
  
    'Add two new records  
    For i = 0 To 1  
        objRs1.AddNew  
        objRs1(1) = "New Shipper #" & CStr((i + 1))  
        objRs1(2) = "(nnn) 555-" & i & i & i & i  
    Next i  
  
    objRs1.Filter = adFilterPendingRecords  
  
    MsgBox "There are " & objRs1.RecordCount & " records pending.", _  
            , "Filter Pending"  
  
    ' Cancel the updates  
    objRs1.CancelBatch  
'EndFilterPend  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Modo de lote](../../../ado/guide/data/batch-mode.md)
