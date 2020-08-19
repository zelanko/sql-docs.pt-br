---
description: Comandos nomeados
title: Comandos nomeados | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- named commands [ADO]
- commands [ADO]
ms.assetid: 5a0ec8f9-5ba3-4f9f-b80d-2073aa049586
author: rothja
ms.author: jroth
ms.openlocfilehash: 607142ec89a1032fe42bab87c0dfad0f2a276387
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88453148"
---
# <a name="named-commands"></a>Comandos nomeados
[Criar e executar um comando simples](../../../ado/guide/data/creating-and-executing-a-simple-command.md) mostra uma maneira de executar um comando. Há outra maneira: você pode torná-lo um comando nomeado e, em seguida, chamar esse comando nomeado diretamente no objeto de **conexão** (atribuído à propriedade **ActiveConnection** do objeto **Command** ). Nomear um comando significa atribuir um nome à propriedade **Name** de um objeto **Command** . Por exemplo,  
  
```  
objCmd.Name = "GetCustomers"  
objCmd.ActiveConnection = objConn  
objConn.GetCustomers objRs  
```  
  
 O comando nomeado atua como se fosse um "método personalizado" no objeto de **conexão** . O resultado do comando é retornado como um parâmetro out desse "método personalizado".  
  
 O exemplo a seguir ilustra esse recurso.  
  
```  
'BeginNamedCmd  
    On Error GoTo ErrHandler:  
  
    Dim objConn As New ADODB.Connection  
    Dim objCmd As New ADODB.Command  
    Dim objRs As New ADODB.Recordset  
  
    ' Connect to the data source.  
    Set objConn = GetNewConnection  
  
    objCmd.CommandText = "SELECT CustomerID, CompanyName FROM Customers"  
    objCmd.CommandType = adCmdText  
  
    'Name the command.  
    objCmd.Name = "GetCustomers"  
  
    objCmd.ActiveConnection = objConn  
  
    ' Execute using Command.Name from the Connection.  
    objConn.GetCustomers objRs  
  
    ' Display.  
    Do While Not objRs.EOF  
        Debug.Print objRs(0) & vbTab & objRs(1)  
        objRs.MoveNext  
    Loop  
  
    'clean up  
    objRs.Close  
    objConn.Close  
    Set objRs = Nothing  
    Set objConn = Nothing  
    Set objCmd = Nothing  
    Exit Sub  
  
ErrHandler:  
    'clean up  
    If objRs.State = adStateOpen Then  
        objRs.Close  
    End If  
  
    If objConn.State = adStateOpen Then  
        objConn.Close  
    End If  
  
    Set objRs = Nothing  
    Set objConn = Nothing  
    Set objCmd = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
'EndNamedCmd  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Objeto Connection (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)
