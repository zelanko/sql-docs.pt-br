---
title: Chamar um procedimento armazenado com um comando | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- calling stored procedures [ADO]
- stored procedures [ADO]
- commands [ADO]
ms.assetid: 685f7652-2271-4ede-b552-2eeb8c756b4c
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 4763939e3eccd0bf4783df87141619cbc0fb011c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66702330"
---
# <a name="calling-a-stored-procedure-with-a-command"></a>Chamar um procedimento armazenado com um comando
Você pode usar um comando para chamar um procedimento armazenado. O exemplo de código no final deste tópico se refere a um procedimento armazenado no banco de dados de exemplo do Northwind, chamado CustOrdersOrders, que é definido da seguinte maneira.  
  
```  
CREATE PROCEDURE CustOrdersOrders @CustomerID nchar(5) AS  
SELECT OrderID, OrderDate, RequiredDate, ShippedDate  
FROM Orders  
WHERE CustomerID = @CustomerID  
ORDER BY OrderID  
```  
  
 Consulte a documentação do SQL Server para obter mais informações sobre como definir e chamar de procedimentos armazenados.  
  
 Esse procedimento armazenado é semelhante ao comando usado na [parâmetros de objeto de comando](../../../ado/guide/data/command-object-parameters.md). Ele usa o parâmetro de ID de um cliente e retorna informações sobre pedidos do cliente. O exemplo de código a seguir usa esse procedimento armazenado como a origem de ADO **conjunto de registros**.  
  
 Usando o procedimento armazenado permite que você acessar outro recurso do ADO: o **parâmetros** coleção **atualizar** método. Usando esse método, ADO pode preencher automaticamente todas as informações sobre os parâmetros necessários para o comando em tempo de execução. Há uma penalidade de desempenho usando essa técnica, porque ADO deve consultar a fonte de dados para obter as informações sobre os parâmetros.  
  
 Outras diferenças importantes existem entre o seguinte exemplo de código e o código em [parâmetros de objeto de comando](../../../ado/guide/data/command-object-parameters.md), onde os parâmetros que foram inseridos manualmente. Em primeiro lugar, esse código não define o **preparado** propriedade a ser **verdadeiro** porque ele é um procedimento armazenado do SQL Server e é pré-compilado por definição. Segundo, o **CommandType** propriedade da **comando** objeto alterado para **adCmdStoredProc** no segundo exemplo para informar ao ADO que o comando teve um procedimento armazenado.  
  
 Por fim, no segundo exemplo o parâmetro deve ser referenciado por índice ao definir o valor, porque você talvez não saiba o nome do parâmetro em tempo de design. Se você souber o nome do parâmetro, você pode definir o novo [NamedParameters](../../../ado/reference/ado-api/namedparameters-property-ado.md) propriedade da **comando** do objeto como True e se referir ao nome da propriedade. Você talvez esteja se perguntando por que a posição do primeiro parâmetro mencionado no procedimento armazenado (@CustomerID) é 1 em vez de 0 (`objCmd(1) = "ALFKI"`). Isso ocorre porque o parâmetro 0 contém um valor de retorno do procedimento armazenado do SQL Server.  
  
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
  
## <a name="see-also"></a>Consulte também  
 [Artigo da Base de dados de Conhecimento 117500](https://go.microsoft.com/fwlink/?LinkId=117500)
