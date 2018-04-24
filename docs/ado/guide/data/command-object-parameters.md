---
title: Parâmetros de objeto de comando | Microsoft Docs
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Command object [ADO], parameters
ms.assetid: 10e7ef4a-78bf-4e91-931e-cbc6c065dd4c
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d55af0ad3553a9129ff9e54308b68b14a622c154
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/18/2018
---
# <a name="command-object-parameters"></a>Parâmetros do objeto de comando
O tópico anterior discutido [criar e executar um comando simples](../../../ado/guide/data/creating-and-executing-a-simple-command.md). Use uma mais interessante para o [comando](../../../ado/reference/ado-api/command-object-ado.md) objeto é mostrado no exemplo a seguir, no qual o comando SQL foi parametrizado. Essa modificação possibilita a reutilização de comando, passando um valor diferente para o parâmetro de cada vez. Porque o [propriedade preparado](../../../ado/reference/ado-api/prepared-property-ado.md) propriedade o **comando** objeto é definido como **true**, ADO exigirá o provedor compilar o comando especificado em [ CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md) antes de executá-lo pela primeira vez. Ele também manterão o comando compilado na memória. Isso reduz a execução do comando ligeiramente na primeira vez que ele é executado por causa da sobrecarga necessária para preparar, mas resulta em um ganho de desempenho de cada vez que o comando é chamado depois disso. Portanto, comandos devem ser preparados somente se eles serão usados mais de uma vez.  
  
```  
'BeginManualParamCmd  
    On Error GoTo ErrHandler:  
  
    Dim objConn As New ADODB.Connection  
    Dim objCmd As New ADODB.Command  
    Dim objParm1 As New ADODB.Parameter  
    Dim objRs As New ADODB.Recordset  
  
    ' Set the CommandText as a parameterized SQL query.  
    objCmd.CommandText = "SELECT OrderID, OrderDate, " & _  
                         "RequiredDate, ShippedDate " & _  
                         "FROM Orders " & _  
                         "WHERE CustomerID = ? " & _  
                         "ORDER BY OrderID"  
    objCmd.CommandType = adCmdText  
  
    ' Prepare command because we will be executing it more than once.  
    objCmd.Prepared = True  
  
    ' Create new parameter for CustomerID. Initial value is ALFKI.  
    Set objParm1 = objCmd.CreateParameter("CustId", adChar, _  
                    adParamInput, 5, "ALFKI")  
    objCmd.Parameters.Append objParm1  
  
    ' Connect to the data source.  
    Set objConn = GetNewConnection  
    objCmd.ActiveConnection = objConn  
  
    ' Execute once and display.  
    Set objRs = objCmd.Execute  
  
    Debug.Print objParm1.Value  
    Do While Not objRs.EOF  
        Debug.Print vbTab & objRs(0) & vbTab & objRs(1) & vbTab & _  
                    objRs(2) & vbTab & objRs(3)  
        objRs.MoveNext  
    Loop  
  
    ' .Set new param value, re-execute command, and display.  
    objCmd("CustId") = "CACTU"  
    Set objRs = objCmd.Execute  
  
    Debug.Print objParm1.Value  
    Do While Not objRs.EOF  
        Debug.Print vbTab & objRs(0) & vbTab & objRs(1) & vbTab & _  
                    objRs(2) & vbTab & objRs(3)  
        objRs.MoveNext  
    Loop  
  
    'clean up  
    objRs.Close  
    objConn.Close  
    Set objRs = Nothing  
    Set objConn = Nothing  
    Set objCmd = Nothing  
    Set objParm1 = Nothing  
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
    Set objParm1 = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
'EndManualParamCmd  
  
'BeginNewConnection  
Private Function GetNewConnection() As ADODB.Connection  
    Dim oCn As New ADODB.Connection  
    Dim sCnStr As String  
  
    sCnStr = "Provider='SQLOLEDB';Data Source='MySqlServer';" & _  
             "Integrated Security='SSPI';Initial Catalog='Northwind';"  
    oCn.Open sCnStr  
  
    If oCn.State = adStateOpen Then  
        Set GetNewConnection = oCn  
    End If  
  
End Function  
'EndNewConnection  
```  
  
 Nem todos os provedores oferecem suporte a comandos preparados. Se o provedor não oferece suporte a preparação de comando, ele pode retornar um erro assim que essa propriedade é definida como **True**. Se ele não retorna um erro, que ignora a solicitação para preparar o comando e conjuntos de **preparado** propriedade **false**.
