---
description: Exemplo da propriedade Optimize (VB)
title: Exemplo da propriedade Optimize (VB) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
dev_langs:
- VB
helpviewer_keywords:
- Optimize property [ADO], Visual Basic example
ms.assetid: 652194af-cfa4-4aa0-a6d6-fa409bbc3f98
author: rothja
ms.author: jroth
ms.openlocfilehash: 5ee1d8d211c0ceeed02408f559c63b5942aafe05
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88773625"
---
# <a name="optimize-property-example-vb"></a>Exemplo da propriedade Optimize (VB)
Este exemplo demonstra a propriedade de **otimização** dinâmica do objeto [Field](./field-object.md) . O campo ***zip*** da tabela ***autores*** no banco de dados ***pubs*** não está indexado. Definir a propriedade [Optimize](./optimize-property-dynamic-ado.md) como **true** no campo ***zip*** autoriza o ADO a criar um índice que melhora o desempenho do método [Find](./find-method-ado.md) .  
  
```  
'BeginOptimizeVB  
Public Sub Main()  
    On Error GoTo ErrorHandler  
  
    'To integrate this code  
    'replace the data source and initial catalog values  
    'in the connection string.  
  
    ' Declare the recordset and connection variables.  
    Dim Cnxn As ADODB.Connection  
    Dim rstAuthors As ADODB.Recordset  
    Dim strCnxn As String  
    Dim strSQLAuthors As String  
  
     ' Open connection.  
    strCnxn = "Provider='sqloledb';Data Source='MySqlServer';" & _  
        "Initial Catalog='Pubs';Integrated Security='SSPI';"  
    Set Cnxn = New ADODB.Connection  
    Cnxn.Open strCnxn  
  
     ' open recordset client-side to enable index creation.  
    Set rstAuthors = New ADODB.Recordset  
    rstAuthors.CursorLocation = adUseClient  
    strSQLAuthors = "SELECT * FROM Authors"  
    rstAuthors.Open strSQLAuthors, Cnxn, adOpenStatic, adLockReadOnly, adCmdText  
     ' Create the index.  
    rstAuthors!zip.Properties("Optimize") = True  
     ' Find Akiko Yokomoto  
    rstAuthors.Find "zip = '94595'"  
  
     ' Show results.  
    Debug.Print rstAuthors!au_fname & " " & rstAuthors!au_lname & " " & _  
             rstAuthors!address & " " & rstAuthors!city & " " & rstAuthors!State  
    rstAuthors!zip.Properties("Optimize") = False  'Delete the index.  
  
    ' Clean up.  
    rstAuthors.Close  
    Cnxn.Close  
    Set rstAuthors = Nothing  
    Set Cnxn = Nothing  
    Exit Sub  
  
ErrorHandler:  
    ' clean up  
    If Not rstAuthors Is Nothing Then  
        If rstAuthors.State = adStateOpen Then rstAuthors.Close  
    End If  
    Set rstAuthors = Nothing  
  
    If Not Cnxn Is Nothing Then  
        If Cnxn.State = adStateOpen Then Cnxn.Close  
    End If  
    Set Cnxn = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
End Sub  
'EndOptimizeVB  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Objeto Field](./field-object.md)   
 [Otimizar a propriedade dinâmica (ADO)](./optimize-property-dynamic-ado.md)