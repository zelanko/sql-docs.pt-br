---
title: Chamar um procedimento armazenado com um comando | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- calling stored procedures [ADO]
- stored procedures [ADO]
- commands [ADO]
ms.assetid: 685f7652-2271-4ede-b552-2eeb8c756b4c
caps.latest.revision: "15"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: e6c22f098efcb2352e450c07aece8f88c8f32b4d
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="calling-a-stored-procedure-with-a-command"></a>Chamar um procedimento armazenado com um comando
Você pode usar um comando para chamar um procedimento armazenado. O exemplo de código no final deste tópico se refere a um procedimento armazenado, o banco de dados de exemplo Northwind, chamado CustOrdersOrders, que é definido da seguinte maneira.  
  
```  
CREATE PROCEDURE CustOrdersOrders @CustomerID nchar(5) AS  
SELECT OrderID, OrderDate, RequiredDate, ShippedDate  
FROM Orders  
WHERE CustomerID = @CustomerID  
ORDER BY OrderID  
```  
  
 Consulte a documentação do SQL Server para obter mais informações sobre como definir e chamadas de procedimentos armazenados.  
  
 Esse procedimento armazenado é semelhante ao usado no comando [parâmetros de objeto de comando](../../../ado/guide/data/command-object-parameters.md). Ele usa o parâmetro de ID de um cliente e retorna informações sobre pedidos do cliente. O exemplo de código a seguir usa esse procedimento armazenado como a origem de ADO **registros**.  
  
 Usando o procedimento armazenado permite que você acesse outro recurso do ADO: o **parâmetros** coleção **atualização** método. Usando esse método, ADO pode preencher automaticamente todas as informações sobre os parâmetros exigidos pelo comando em tempo de execução. Há uma penalidade de desempenho usando essa técnica, porque ADO deve consultar a fonte de dados para obter as informações sobre os parâmetros.  
  
 Existem outras diferenças importantes entre o exemplo de código e o código em [parâmetros de objeto de comando](../../../ado/guide/data/command-object-parameters.md), onde os parâmetros que foram inseridos manualmente. Primeiro, esse código não define o **preparado** propriedade **True** porque ele é um procedimento armazenado do SQL Server e é pré-compilado por definição. Segundo, o **CommandType** propriedade o **comando** o objeto alterado para **adCmdStoredProc** no segundo exemplo para informar o ADO que o comando foi um procedimento armazenado.  
  
 Por fim, no segundo exemplo o parâmetro deve ser chamado pelo índice ao definir o valor, porque você não poderá saber o nome do parâmetro em tempo de design. Se você souber o nome do parâmetro, você pode definir o novo [NamedParameters](../../../ado/reference/ado-api/namedparameters-property-ado.md) propriedade o **comando** do objeto como True e consulte o nome da propriedade. Você talvez esteja se perguntando por que a posição do primeiro parâmetro mencionado no procedimento armazenado (@CustomerID) é 1, em vez de 0 (`objCmd(1) = "ALFKI"`). Isso ocorre porque o parâmetro 0 contém um valor de retorno do procedimento armazenado do SQL Server.  
  
```  
'BeginAutoParamCmd  
    On Error GoTo ErrHandler:  
  
    Dim objConn As New ADODB.Connection  
    Dim objCmd As New ADODB.Command  
    Dim objParm1 As New ADODB.Parameter  
    Dim objRs As New ADODB.Recordset  
  
    ' Set CommandText equal to the stored procedure name.  
    objCmd.CommandText = "CustOrdersOrders"  
    objCmd.CommandType = adCmdStoredProc  
  
    ' Connect to the data source.  
    Set objConn = GetNewConnection  
    objCmd.ActiveConnection = objConn  
  
    ' Automatically fill in parameter info from stored procedure.  
    objCmd.Parameters.Refresh  
  
    ' Set the param value.  
    objCmd(1) = "ALFKI"  
  
    ' Execute once and display...  
    Set objRs = objCmd.Execute  
  
    Debug.Print objParm1.Value  
    Do While Not objRs.EOF  
        Debug.Print vbTab & objRs(0) & vbTab & objRs(1) & vbTab & _  
                    objRs(2) & vbTab & objRs(3)  
        objRs.MoveNext  
    Loop  
  
    ' ...then set new param value, re-execute command, and display.  
    objCmd(1) = "CACTU"  
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
'EndAutoParamCmd  
  
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
  
## <a name="see-also"></a>Consulte Também  
 [Artigo da Base de dados de Conhecimento 117500](http://go.microsoft.com/fwlink/?LinkId=117500)
