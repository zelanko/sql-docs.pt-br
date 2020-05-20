---
title: Chamando um procedimento armazenado com um comando | Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 998bda7d2c940b16f298fdfe436a2d60b27f09ba
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82761212"
---
# <a name="calling-a-stored-procedure-with-a-command"></a>Chamar um procedimento armazenado com um comando
Você pode usar um comando para chamar um procedimento armazenado. O exemplo de código no final deste tópico refere-se a um procedimento armazenado no banco de dados de exemplo Northwind, chamado CustOrdersOrders, que é definido da seguinte maneira.  
  
```  
CREATE PROCEDURE CustOrdersOrders @CustomerID nchar(5) AS  
SELECT OrderID, OrderDate, RequiredDate, ShippedDate  
FROM Orders  
WHERE CustomerID = @CustomerID  
ORDER BY OrderID  
```  
  
 Consulte a documentação do SQL Server para obter mais informações sobre como definir e chamar procedimentos armazenados.  
  
 Esse procedimento armazenado é semelhante ao comando usado em [parâmetros de objeto de comando](../../../ado/guide/data/command-object-parameters.md). Ele usa um parâmetro de ID do cliente e retorna informações sobre os pedidos desse cliente. O exemplo de código a seguir usa esse procedimento armazenado como a origem de um **conjunto de registros**ADO.  
  
 O uso do procedimento armazenado permite que você acesse outro recurso do ADO: o método de **atualização** da coleção **Parameters** . Usando esse método, o ADO pode preencher automaticamente todas as informações sobre os parâmetros exigidos pelo comando em tempo de execução. Há uma penalidade de desempenho no uso dessa técnica, porque o ADO deve consultar a fonte de dados para obter as informações sobre os parâmetros.  
  
 Existem outras diferenças importantes entre o exemplo de código a seguir e o código em [parâmetros de objeto de comando](../../../ado/guide/data/command-object-parameters.md), em que os parâmetros foram inseridos manualmente. Primeiro, esse código não define a propriedade **preparada** como **true** porque é um procedimento armazenado SQL Server e é pré-compilado por definição. Em segundo lugar, a propriedade **CommandType** do objeto **Command** foi alterada para **adCmdStoredProc** no segundo exemplo para informar ao ADO que o comando era um procedimento armazenado.  
  
 Por fim, no segundo exemplo, o parâmetro deve ser referenciado pelo índice ao definir o valor, porque talvez você não saiba o nome do parâmetro em tempo de design. Se você souber o nome do parâmetro, poderá definir a nova propriedade [namedParameters](../../../ado/reference/ado-api/namedparameters-property-ado.md) do objeto **Command** como true e se referir ao nome da propriedade. Você deve estar imaginando por que a posição do primeiro parâmetro mencionado no procedimento armazenado ( @CustomerID ) é 1 em vez de 0 ( `objCmd(1) = "ALFKI"` ). Isso ocorre porque o parâmetro 0 contém um valor de retorno do procedimento armazenado SQL Server.  
  
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
 [Artigo 117500 da base de dados de conhecimento](https://go.microsoft.com/fwlink/?LinkId=117500)
