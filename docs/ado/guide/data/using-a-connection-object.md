---
description: Usar um objeto Connection
title: Usando um objeto de conexão | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- connections [ADO]
ms.assetid: 4b34f971-5699-43e7-9b15-137d334fa66e
author: rothja
ms.author: jroth
ms.openlocfilehash: b63c3925fd70f6075ab1131c275fa5e52a6e3ac8
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88979117"
---
# <a name="using-a-connection-object"></a>Usar um objeto Connection
Antes de abrir um objeto de **conexão** , você deve definir determinadas informações sobre a fonte de dados e o tipo de conexão. A maioria dessas informações é mantida pelo parâmetro *ConnectionString* do [método Open](../../../ado/reference/ado-api/open-method-ado-connection.md) no objeto **Connection** ou pela [Propriedade ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md) no objeto **Connection** . Uma cadeia de conexão consiste em uma lista de pares de argumento/valor separados por ponto e vírgula, com os valores entre aspas simples. Por exemplo:  
  
```  
Dim sConn As String  
sConn = "Provider='SQLOLEDB';Data Source='MySqlServer';" & _  
             "Initial Catalog='Northwind';Integrated Security='SSPI';"  
```  
  
> [!NOTE]
>  Você também pode especificar um nome de fonte de dados ODBC (DSN) ou um arquivo de vínculo de dados (UDL) em uma cadeia de conexão. Para obter mais informações sobre DSNs, consulte [Managing Data Sources](../../../odbc/admin/managing-data-sources.md) in the ODBC Programmer ' s Reference. Para obter mais informações sobre UDLs, consulte [visão geral da API de vínculo de dados](https://msdn.microsoft.com/95c180ea-bd4f-4dca-b95a-576afd135bbc) na referência do programador de OLE DB.  
  
 Normalmente, você estabelece uma conexão chamando o método **Connection. Open** com uma *cadeia de conexão* apropriada como seu parâmetro. Um exemplo é mostrado no trecho de código Visual Basic a seguir:  
  
```  
Dim oConn As ADODB.Connection  
Dim oRs As ADODB.Recordset  
Dim sConn As String  
Dim sSQL as String  
  
' Open a connection.  
Set oConn = New ADODB.Connection  
.Open   
  
' Make a query over the connection.  
sSQL = "SELECT ProductID, ProductName, CategoryID, UnitPrice " & _  
             "FROM Products"  
Set oRs = New ADODB.Recordset  
oRs.Open sSQL, , adOpenStatic, adLockBatchOptimistic, adCmdText  
  
MsgBox oRs.RecordCount  
  
' Close the connection.  
oConn.Close  
Set oConn = Nothing  
  
```  
  
 Aqui, o **oRs. Open** usa uma variável de objeto de **conexão** (*oConn*) como o valor de seu parâmetro *ActiveConnection* . Além disso, a propriedade **Connection. CursorLocation** pressupõe o valor padrão de **adUseServer**. Compare isso ao exemplo de [HelloData](../../../ado/guide/data/hellodata-a-simple-ado-application.md) na seção anterior. A instrução a seguir resultaria em erros de tempo de execução.  
  
```  
oRs.MarshalOptions = adMarshalModifiedOnly  
' Disconnect the Recordset.  
Set oRs.ActiveConnection = Nothing  
```
