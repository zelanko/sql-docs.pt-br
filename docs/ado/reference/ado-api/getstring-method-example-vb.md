---
title: Exemplo do método GetString (VB) | Microsoft Docs
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
- GetString method [ADO], Visual Basic example
ms.assetid: 14c96d71-46a8-4782-b474-80ce348e8bff
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6928d870c00fce0f712e7a9fc01cc2a2a33a57d9
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67918507"
---
# <a name="getstring-method-example-vb"></a>Exemplo do método GetString (VB)
Este exemplo demonstra o método [GetString](../../../ado/reference/ado-api/getstring-method-ado.md) .  
  
 Suponha que você esteja Depurando um problema de acesso a dados e queira uma maneira rápida e simples de imprimir o conteúdo atual de um pequeno [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md).  
  
```  
'BeginGetStringVB  
  
    'To integrate this code  
    'replace the data source and initial catalog values  
    'in the connection string  
  
Public Sub Main()  
    On Error GoTo ErrorHandler  
  
     ' connection variables  
    Dim Cnxn As ADODB.Connection  
    Dim rstAuthors As ADODB.Recordset  
    Dim strCnxn As String  
    Dim strSQLAuthors As String  
    Dim varOutput As Variant  
  
     ' specific variables  
    Dim strPrompt As String  
    Dim strState As String  
  
     ' open connection  
    Set Cnxn = New ADODB.Connection  
    strCnxn = "Provider='sqloledb';Data Source='MySqlServer';" & _  
        "Initial Catalog='Pubs';Integrated Security='SSPI';"  
    Cnxn.Open strCnxn  
  
     ' get user input  
    strPrompt = "Enter a state (CA, IN, KS, MD, MI, OR, TN, UT): "  
    strState = Trim(InputBox(strPrompt, "GetString Example"))  
  
     ' open recordset  
    Set rstAuthors = New ADODB.Recordset  
    strSQLAuthors = "SELECT au_fname, au_lname, address, city FROM Authors " & _  
                "WHERE state = '" & strState & "'"  
    rstAuthors.Open strSQLAuthors, Cnxn, adOpenStatic, adLockReadOnly, adCmdText  
  
    If Not rstAuthors.EOF Then  
    ' Use all defaults: get all rows, TAB as column delimiter,  
    ' CARRIAGE RETURN as row delimiter, EMPTY-string as null delimiter  
       varOutput = rstAuthors.GetString(adClipString)  
        ' print output  
       Debug.Print "State = '" & strState & "'"  
       Debug.Print "Name             Address             City" & vbCr  
       Debug.Print varOutput  
    Else  
       Debug.Print "No rows found for state = '" & strState & "'" & vbCr  
    End If  
  
    ' clean up  
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
'EndGetStringVB  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Método GetString (ADO)](../../../ado/reference/ado-api/getstring-method-ado.md)   
 [Objeto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
