---
title: Usando um objeto de conjunto de registros | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- connections [ADO]
ms.assetid: 01c630d8-eb35-4bd0-a99f-7c0f85316cc1
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 985cb58b860c594e8cfc3e405934fafd9cfb245a
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63184960"
---
# <a name="using-a-recordset-object"></a>Usar um objeto Recordset
Como alternativa, você pode usar **Recordset.Open** implicitamente estabelecer uma conexão e emitir um comando ao longo dessa conexão em uma única operação. Por exemplo, no Visual Basic:  
  
```  
Dim oRs As ADODB.Recordset  
Dim sConn As String  
Dim sSQL as String  
  
sConn = "Provider='SQLOLEDB';Data Source='MySqlServer';" & _             "Initial Catalog='Northwind';Integrated Security='SSPI';"  
  
sSQL = "SELECT ProductID, ProductName, CategoryID, UnitPrice " & _  
             "FROM Products"  
  
' Create and Open the Recordset object.  
Set oRs = New ADODB.Recordset  
oRs.CursorLocation = adUseClient  
oRs.Open sSQL, sConn, adOpenStatic, _  
               adLockBatchOptimistic, adCmdText  
  
MsgBox oRs.RecordCount  
  
oRs.MarshalOptions = adMarshalModifiedOnly  
' Disconnect the Recordset.  
Set oRs.ActiveConnection = Nothing  
oRs.Close          
Set oRs = Nothing  
```  
  
 Observe que **oRs.Open** usa uma cadeia de caracteres de conexão (*sConn*), em vez de um **Conexão** objeto (*oConn*), como o valor do seu  **ActiveConnection** parâmetro. Também o tipo de cursor do lado do cliente é imposto, definindo o **CursorLocation** propriedade no **Recordset** objeto. Novamente, compare isso com o **HelloData** exemplo.
