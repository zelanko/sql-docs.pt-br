---
title: 'Enviando o método Updates: UpdateBatch | Microsoft Docs'
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 87123797-831f-48e0-94b5-f669f9ca194a
author: rothja
ms.author: jroth
ms.openlocfilehash: abb0051ef336a145b2da75906831d7adc168e6e3
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82760882"
---
# <a name="sending-the-updates-updatebatch-method"></a>Enviar as atualizações: método UpdateBatch
O código a seguir abre um conjunto de registros no modo de lote, definindo a propriedade LockType como adLockBatchOptimistic e CursorLocation como adUseClient. Ele adiciona dois novos registros e altera o valor de um campo em um registro existente, salvando os valores originais e, em seguida, chama UpdateBatch para enviar as alterações de volta para a fonte de dados.  
  
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
  
 Se você estiver editando o registro atual ou adicionando um novo registro ao chamar o método UpdateBatch, o ADO chamará automaticamente o método Update para salvar as alterações pendentes no registro atual antes de transmitir as alterações em lote para o provedor.  
  
## <a name="see-also"></a>Consulte Também  
 [Modo de lote](../../../ado/guide/data/batch-mode.md)
