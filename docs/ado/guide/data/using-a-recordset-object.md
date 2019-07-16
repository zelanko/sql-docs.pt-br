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
ms.openlocfilehash: dda89464598ddc4ecfee0078b36aadd01b4486f5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67923638"
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
