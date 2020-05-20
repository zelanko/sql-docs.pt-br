---
title: Passando parâmetros para um comando nomeado | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- named commands [ADO]
- commands [ADO], passing parameters to a named command
ms.assetid: 36e0cdbe-7f50-40f5-af0d-700f5d8dc75a
author: rothja
ms.author: jroth
ms.openlocfilehash: afa230584bd7ee93d56f814a998c886e433a9417
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82764767"
---
# <a name="passing-parameters-to-a-named-command"></a>Passar parâmetros para um comando nomeado
Assim como o resultado do comando é passado como uma variável *out* do comando nomeado, os parâmetros para um comando com parâmetros podem ser passados como *em* variáveis para o comando nomeado.  
  
 O exemplo de código a seguir tenta recuperar todos os pedidos feitos pelo cliente cujo **CustomerID** é "ALKFI" do banco de dados Northwind. O valor de **CustomerID** é fornecido no momento em que o comando nomeado é chamado.  
  
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
  
 Observe que todos os parâmetros de entrada devem preceder qualquer variável de saída e os tipos de dados de parâmetros devem corresponder ou podem ser convertidos para aqueles dos campos correspondentes. A instrução a seguir-  
  
```  
objConn.GetOrdersOf 12345, objRs  
```  
  
 -resultará em um erro de tipos de dados incompatíveis, pois o parâmetro de entrada necessário é de um tipo de **cadeia de caracteres** , não de um tipo **inteiro** .  
  
 A seguinte chamada-  
  
```  
objConn.GetOrdersOf "12345", objRs  
```  
  
 -é válido, mas produzirá um conjunto de resultados vazio porque não existem registros desse tipo no banco de dados.  
  
## <a name="see-also"></a>Consulte Também  
 [Objeto Connection (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)
