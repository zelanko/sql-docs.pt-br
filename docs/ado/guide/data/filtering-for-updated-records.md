---
title: Filtragem de atualizado registros | Microsoft Docs
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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67925333"
---
# <a name="filtering-for-updated-records"></a>Filtrar os registros atualizados
Antes de chamar UpdateBatch, você pode usar a propriedade de filtro de conjunto de registros para exibir somente os registros que foram alterados desde que o conjunto de registros foi aberto ou a última chamada para UpdateBatch. Para fazer isso, defina filtro igual a adFilterPendingRecords para determinar quantos registros serão atualizados, conforme mostrado no exemplo de código na próxima seção.  
  
## <a name="remarks"></a>Comentários  
 Este exemplo estende o exemplo de UpdateBatch anterior, o conjunto de registros de filtragem antes que ele chama o UpdateBatch, mostrando que o usuário que registros serão alterado e permitindo dela cancelar a atualização (usando o método CancelBatch).  
  
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
  
## <a name="see-also"></a>Consulte também  
 [Modo de lote](../../../ado/guide/data/batch-mode.md)
