---
description: Exemplo dos métodos MoveFirst, MoveLast, MoveNext e MovePrevious (VB)
title: Mover ponteiro de registro do exemplo de conjunto de registros (VB) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
dev_langs:
- VB
helpviewer_keywords:
- MovePrevious method [ADO], Visual Basic example
- MoveLast method [ADO], Visual Basic example
- MoveFirst method [ADO], Visual Basic example
- MoveNext method [ADO], Visual Basic example
ms.assetid: 31d3b083-c677-423e-8d26-a212eaeea281
author: rothja
ms.author: jroth
ms.openlocfilehash: a38a79354ad90faff75ed92c96310df838784a0d
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88990537"
---
# <a name="movefirst-movelast-movenext-and-moveprevious-methods-example-vb"></a>Exemplo dos métodos MoveFirst, MoveLast, MoveNext e MovePrevious (VB)
Este exemplo usa os métodos [MoveFirst](./movefirst-movelast-movenext-and-moveprevious-methods-ado.md), [MoveLast](./movefirst-movelast-movenext-and-moveprevious-methods-ado.md), [MoveNext](./movefirst-movelast-movenext-and-moveprevious-methods-ado.md)e [MovePrevious](./movefirst-movelast-movenext-and-moveprevious-methods-ado.md) para mover o ponteiro de registro de um [conjunto de registros](./recordset-object-ado.md) com base no comando fornecido. O procedimento MoveAny é necessário para que este procedimento seja executado.  
  
```  
'BeginMoveFirstVB  
  
    'To integrate this code  
    'replace the data source and initial catalog values  
    'in the connection string  
  
Public Sub Main()  
    On Error GoTo ErrorHandler  
  
    ' connection and recordset variables  
    Dim rstAuthors As ADODB.Recordset  
    Dim Cnxn As ADODB.Connection  
    Dim strCnxn As String  
    Dim strSQLAuthors  
     ' record variables  
    Dim strMessage As String  
    Dim intCommand As Integer  
  
    ' Open connection  
    Set Cnxn = New ADODB.Connection  
    strCnxn = "Provider='sqloledb';Data Source='MySqlServer';" & _  
        "Initial Catalog='Pubs';Integrated Security='SSPI';"  
    Cnxn.Open strCnxn  
  
    ' Open recordset from Authors table  
    Set rstAuthors = New ADODB.Recordset  
    rstAuthors.CursorLocation = adUseClient  
    ' Use client cursor to enable AbsolutePosition property  
    strSQLAuthors = "Authors"  
    rstAuthors.Open strSQLAuthors, Cnxn, adOpenStatic, adLockReadOnly, adCmdTable  
  
    ' Show current record information and get user's method choice  
    Do  
        strMessage = "Name: " & rstAuthors!au_fname & " " & _  
            rstAuthors!au_lname & vbCr & "Record " & _  
            rstAuthors.AbsolutePosition & " of " & _  
            rstAuthors.RecordCount & vbCr & vbCr & _  
            "[1 - MoveFirst, 2 - MoveLast, " & vbCr & _  
            "3 - MoveNext, 4 - MovePrevious]"  
        intCommand = Val(Left(InputBox(strMessage), 1))  
  
         ' for exiting the loop  
        If intCommand < 1 Or intCommand > 4 Then  
            MsgBox "You either entered a non-number or canceled the input box. Exit the application."  
            Exit Do  
        End If  
  
        ' Use specified method while trapping for BOF and EOF  
        Select Case intCommand  
            Case 1  
                rstAuthors.MoveFirst  
            Case 2  
                rstAuthors.MoveLast  
            Case 3  
                rstAuthors.MoveNext  
                If rstAuthors.EOF Then  
                    MsgBox "Already at end of recordset!"  
                    rstAuthors.MoveLast  
                End If  
            Case 4  
                rstAuthors.MovePrevious  
                If rstAuthors.BOF Then  
                    MsgBox "Already at beginning of recordset!"  
                    rstAuthors.MoveFirst  
                End If  
        End Select  
    Loop  
  
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
  
'EndMoveFirstVB  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Métodos MoveFirst, MoveLast, MoveNext e MovePrevious (ADO)](./movefirst-movelast-movenext-and-moveprevious-methods-ado.md)   
 [Objeto Recordset (ADO)](./recordset-object-ado.md)