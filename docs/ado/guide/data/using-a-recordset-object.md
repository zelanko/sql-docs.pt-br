---
title: Usando um objeto Recordset | Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 183c8b3379d2ac90fa089f2f2834b46473961abf
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82763077"
---
# <a name="using-a-recordset-object"></a>Usar um objeto Recordset
Como alternativa, você pode usar **Recordset. Open** para estabelecer implicitamente uma conexão e emitir um comando nessa conexão em uma única operação. Por exemplo, em Visual Basic:  
  
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
  
 Observe que o **oRs. Open** usa uma cadeia de conexão (*sConn*), no lugar de um objeto de **conexão** (*oConn*), como o valor de seu parâmetro **ActiveConnection** . Além disso, o tipo de cursor do lado do cliente é imposto definindo a propriedade **CursorLocation** no objeto **Recordset** . Novamente, compare com o exemplo **HelloData** .
