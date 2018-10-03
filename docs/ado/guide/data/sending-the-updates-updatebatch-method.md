---
title: 'Enviar as atualizações: método UpdateBatch | Microsoft Docs'
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 87123797-831f-48e0-94b5-f669f9ca194a
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3da407de4489ec829151696793f547e31541e6df
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47655614"
---
# <a name="sending-the-updates-updatebatch-method"></a>Enviar as atualizações: método UpdateBatch
O código a seguir abre um conjunto de registros no modo de lote definindo a propriedade LockType adLockBatchOptimistic e CursorLocation para adUseClient. Ele adiciona dois novos registros e altera o valor de um campo em um registro existente, salvar os valores originais e, em seguida, chama UpdateBatch para enviar que as alterações de volta para a fonte de dados.  
  
## <a name="remarks"></a>Comentários  
  
```  
'BeginBatchUpdate  
    strConn = "Provider=SQLOLEDB;Initial Catalog=Northwind;" & _  
              "Data Source=MySQLServer;Integrated Security=SSPI;"  
  
    strSQL = "SELECT ShipperId, CompanyName, Phone FROM Shippers"  
  
    Set objRs1 = New ADODB.Recordset  
    objRs1.CursorLocation = adUseClient  
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
  
    ' Send the updates  
    objRs1.UpdateBatch  
'EndBatchUpdate  
```  
  
 Se você estiver editando o registro atual ou adicionar um novo registro, quando você chama o método UpdateBatch, ADO automaticamente chamar o método Update para salvar as alterações pendentes no registro atual antes de transmitir as alterações em lote para o provedor.  
  
## <a name="see-also"></a>Consulte também  
 [Modo de lote](../../../ado/guide/data/batch-mode.md)
