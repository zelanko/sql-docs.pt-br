---
title: Filtrando registros atualizados | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- filtering for updated records [ADO]
ms.assetid: 4a798921-d7bb-47c9-a252-550fd9463ec9
caps.latest.revision: 4
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: b633f10b4bac5ec6347879510e1867e7d5d14741
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="filtering-for-updated-records"></a>Filtrando os registros atualizados
Antes de chamar UpdateBatch, você pode usar a propriedade de filtro do conjunto de registros para exibir somente os registros que foram alterados desde que o conjunto de registros foi aberto ou a última chamada a UpdateBatch. Para fazer isso, defina filtro igual a adFilterPendingRecords para determinar quantos registros serão atualizados, conforme mostrado no exemplo de código na próxima seção.  
  
## <a name="remarks"></a>Comentários  
 Este exemplo estende UpdateBatch exemplo anterior, o conjunto de registros de filtragem antes que ele chama o UpdateBatch, mostrando o usuário irá alterar quais registros e permitindo que ela cancelar a atualização (usando o método CancelBatch).  
  
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

