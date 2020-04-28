---
title: Criando e executando um comando simples | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Command object [ADO], creating and executing
- commands [ADO], creating and executing
ms.assetid: 0b81af6f-b9ae-4f7c-b59b-b5bdd775036f
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 7ae9cc9066f66d10d94370336e8a46155f1a03c2
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67925733"
---
# <a name="creating-and-executing-a-simple-command"></a>Criar e executar um comando simples
Um comando simples é aquele que não é parametrizado e não requer persistência. Há três maneiras de criar e executar um comando simples.  
  
-   Usando um objeto de **comando**  
  
-   Usando um objeto **Connection**  
  
-   Usando um objeto **Recordset**  
  
## <a name="using-a-command-object"></a>Usando um objeto de comando  
 Para criar um comando simples usando um objeto **Command** , você deve atribuir a instrução à propriedade **CommandText** de um objeto **Command** e definir o valor apropriado para a propriedade **CommandType** . A execução do comando requer que uma conexão aberta seja atribuída à propriedade **ActiveConnection** do objeto **Command** , seguida por uma chamada para o método **Execute** no objeto **Command** .  
  
 O trecho de código a seguir mostra o método básico de usar o objeto **Command** para executar um comando em uma fonte de dados. Este exemplo usa um comando de retorno de linha e retorna os resultados da execução do comando como um objeto **Recordset** .  
  
```  
    'BeginBasicCmd  
    On Error GoTo ErrHandler:  
  
    Dim objConn As New ADODB.Connection  
    Dim objCmd As New ADODB.Command  
    Dim objRs As New ADODB.Recordset  
  
    objCmd.CommandText = "SELECT OrderID, OrderDate, " & _  
                         "RequiredDate, ShippedDate " & _  
                         "FROM Orders " & _  
                         "WHERE CustomerID = 'ALFKI' " & _  
                         "ORDER BY OrderID"  
    objCmd.CommandType = adCmdText  
  
    ' Connect to the data source.  
    Set objConn = GetNewConnection  
    objCmd.ActiveConnection = objConn  
  
    ' Execute once and display...  
    Set objRs = objCmd.Execute  
  
    Debug.Print "ALFKI"  
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
'EndBasicCmd  
  
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
  
## <a name="using-a-recordset-object"></a>Usando um objeto Recordset  
 Você também pode criar um comando como uma cadeia de texto e o Pas it para o método **Open** em um objeto **Recordset** , junto com o tipo de comando (adCmdText), para execução. O trecho de código a seguir demonstra isso.  
  
```  
  
Const DS = "MySqlServer"  
Const DB = "Northwind"  
Const DP = "SQLOLEDB"  
  
Dim objRs As New ADODB.Recordset  
Dim CommandText As String  
Dim ConnctionString As String  
  
CommandText = "SELECT OrderID, OrderDate, " & _  
                     "RequiredDate, ShippedDate " & _  
                     "FROM Orders " & _  
                     "WHERE CustomerID = 'ALFKI' " & _  
                     "ORDER BY OrderID"  
ConnectionString = "Provider=" & DP & _  
                   ";Data Source=" & DS & _  
                   ";Initial Catalog=" & DB & _  
                   ";Integrated Security=SSPI;"  
  
' Connect to data source and execute the SQL command.  
objRs.Open CommandText, ConnectionString, _  
            adOpenStatic, adLockReadOnly, adCmdText  
  
Debug.Print "ALFKI"  
Do While Not objRs.EOF  
    Debug.Print vbTab & objRs(0) & vbTab & objRs(1) & vbTab & _  
                objRs(2) & vbTab & objRs(3)  
    objRs.MoveNext  
Loop  
  
'Clean up.  
objRs.Close  
Set objRs = Nothing  
```  
  
## <a name="using-a-connection-object"></a>Usando um objeto Connection  
 Você também pode executar um comando em um objeto de conexão aberta. O exemplo de código anterior agora se torna o seguinte:  
  
```  
Const DS = "MySqlServer"  
Const DB = "Northwind"  
Const DP = "SQLOLEDB"  
  
Dim objConn As New ADODB.Connection  
Dim objRs As New ADODB.Recordset  
  
CommandText = "SELECT OrderID, OrderDate, " & _  
                     "RequiredDate, ShippedDate " & _  
                     "FROM Orders " & _  
                     "WHERE CustomerID = 'ALFKI' " & _  
                     "ORDER BY OrderID"  
  
ConnectionString = "Provider=" & DP & _  
                   ";Data Source=" & DS & _  
                   ";Initial Catalog=" & DB & _  
                   ";Integrated Security=SSPI;"  
  
' Connect to the data source.  
objConn.Open ConnectionString  
  
' Execute command through the connection and display...  
Set objRs = objConn.Execute(CommandText)  
  
Debug.Print "ALFKI"  
Do While Not objRs.EOF  
    Debug.Print vbTab & objRs(0) & vbTab & objRs(1) & vbTab & _  
                objRs(2) & vbTab & objRs(3)  
    objRs.MoveNext  
Loop  
  
'Clean up.  
objRs.Close  
objConn.Close  
Set objRs = Nothing  
Set objConn = Nothing  
```
