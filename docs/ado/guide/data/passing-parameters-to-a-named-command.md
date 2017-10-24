---
title: "Passando parâmetros para um comando nomeado | Microsoft Docs"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- named commands [ADO]
- commands [ADO], passing parameters to a named command
ms.assetid: 36e0cdbe-7f50-40f5-af0d-700f5d8dc75a
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 33d1ee3fe4e24695deccd0615f17868bfdfd988c
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="passing-parameters-to-a-named-command"></a>Passando parâmetros para um comando nomeado
Assim como o resultado do comando é passado a como um *out* variável do comando nomeado, parâmetros para um comando parametrizado pode foi passada como *em* variáveis para o comando nomeado.  
  
 O código a seguir exemplo tenta recuperar todos os pedidos colocados pelo cliente cuja **CustomerID** é "ALKFI" do banco de dados Northwind. O valor de **CustomerID** é fornecido no momento em que o comando nomeado é chamado.  
  
```  
Const DS = "MySqlServer"  
Const DB = "Northwind"  
Const DP = "SQLOLEDB"  
  
Dim objConn As New ADODB.Connection  
Dim objRs As New ADODB.Recordset  
Dim objComm As New ADODB.Command  
  
CommandText = "SELECT OrderID, OrderDate, " & _  
                     "RequiredDate, ShippedDate " & _  
                     "FROM Orders " & _  
                     "WHERE CustomerID = ? " & _  
                     "ORDER BY OrderID"  
  
ConnectionString = "Provider=" & DP & _  
                   ";Data Source=" & DS & _  
                   ";Initial Catalog=" & DB & _  
                   ";Integrated Security=SSPI;"  
  
' Connect to the data source.  
objConn.Open ConnectionString  
  
' Set a named command.  
objComm.CommandText = CommandText  
objComm.CommandType = adCmdText  
objComm.Name = "GetOrdersOf"  
Set objComm.ActiveConnection = objConn  
  
' Call the named command, passing a CustomerID value  
' as the input parameter.   
'    "ALFKI" is the required input parameter,  
'    objRs is the resultant output variable.  
objConn.GetOrdersOf "ALKFI", objRs  
  
' Display the result.  
Debug.Print "All orders by ALFKI:"  
Do While Not objRs.EOF  
    Debug.Print vbTab & objRs(0) & vbTab & objRs(1) & vbTab & _  
                objRs(2) & vbTab & objRs(3)  
    objRs.MoveNext  
Loop  
  
' Clean up.  
objRs.Close  
objConn.Close  
Set objRs = Nothing  
Set objConn = Nothing  
Set objComm = Nothing  
```  
  
 Observe que todos os parâmetros de entrada devem preceder qualquer variável de saída e os tipos de dados dos parâmetros devem corresponder ou podem ser convertidos para os campos correspondentes. A instrução a seguir:  
  
```  
objConn.GetOrdersOf 12345, objRs  
```  
  
 — resultará em um erro de tipos de dados incompatíveis, porque o parâmetro de entrada necessário é de um **cadeia de caracteres** tipo, não de um **inteiro** tipo.  
  
 A chamada a seguir:  
  
```  
objConn.GetOrdersOf "12345", objRs  
```  
  
 — é válido, mas produzirá um resultado vazio definido porque esses registros não existem no banco de dados.  
  
## <a name="see-also"></a>Consulte também  
 [Objeto Connection (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)

