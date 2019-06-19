---
title: Exemplo da propriedade ActiveCommand (VB) | Microsoft Docs
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
- ActiveCommand property [ADO], Visual Basic example
ms.assetid: 23b06499-62df-4f46-88eb-6da392f9b456
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 75c75540433e077cc5d96bb9b2f0c88c05a62bd6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66704038"
---
# <a name="activecommand-property-example-vb"></a>Exemplo da propriedade ActiveCommand (VB)
Este exemplo demonstra a [ActiveCommand](../../../ado/reference/ado-api/activecommand-property-ado.md) propriedade.  
  
 Uma sub-rotina é fornecida uma [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md) do objeto cuja **ActiveCommand** propriedade é usada para exibir o texto do comando e parâmetro que criou o **conjunto de registros**.  
  
```  
'BeginActiveCommandVB  
  
    'To integrate this code  
    'replace the data source and initial catalog values  
    'in the connection string  
  
Public Sub Main()  
    On Error GoTo ErrorHandler  
  
        'recordset and connection variables  
    Dim cmd As ADODB.Command  
    Dim rst As ADODB.Recordset  
    Dim Cnxn As ADODB.Connection  
    Dim strCnxn As String  
        'record variables  
    Dim strPrompt As String  
    Dim strName As String  
  
    Set Cnxn = New ADODB.Connection  
    Set cmd = New ADODB.Command  
  
    strPrompt = "Enter an author's name (e.g., Ringer): "  
    strName = Trim(InputBox(strPrompt, "ActiveCommandX Example"))  
    strCnxn = "Provider='sqloledb';Data Source='MySqlServer';" & _  
        "Initial Catalog='Pubs';Integrated Security='SSPI';"  
  
        'create SQL command string  
    cmd.CommandText = "SELECT * FROM Authors WHERE au_lname = ?"  
    cmd.Parameters.Append cmd.CreateParameter("LastName", adChar, adParamInput, 20, strName)  
  
    Cnxn.Open strCnxn  
    cmd.ActiveConnection = Cnxn  
  
        'create the recordset by executing command string  
    Set rst = cmd.Execute(, , adCmdText)  
        'see the results  
    Call ActiveCommandXprint(rst)  
  
    ' clean up  
    Cnxn.Close  
    Set rst = Nothing  
    Set Cnxn = Nothing  
    Exit Sub  
  
ErrorHandler:  
    ' clean up  
    If Not rst Is Nothing Then  
        If rst.State = adStateOpen Then rst.Close  
    End If  
    Set rst = Nothing  
  
    If Not Cnxn Is Nothing Then  
        If Cnxn.State = adStateOpen Then Cnxn.Close  
    End If  
    Set Cnxn = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
End Sub  
'EndActiveCommandVB  
```  
  
 O **ActiveCommandXprint** rotina é fornecida somente uma **conjunto de registros** do objeto, mas ele deve imprimir o texto do comando e parâmetro que criou o **conjunto de registros**. Isso pode ser feito porque o **conjunto de registros** do objeto **ActiveCommand** propriedade produz associado [comando](../../../ado/reference/ado-api/command-object-ado.md) objeto.  
  
 O **comando** do objeto [CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md) propriedade produz o comando com parâmetros que criou o **conjunto de registros**. O **comando** do objeto [parâmetros](../../../ado/reference/ado-api/parameters-collection-ado.md) coleção produz o valor que foi substituído por espaço reservado de parâmetro do comando (" **?** ").  
  
 Por fim, uma mensagem de erro ou o nome do autor e ID são impressos.  
  
```  
'BeginActiveCommandPrintVB  
Public Sub ActiveCommandXprint(rstp As ADODB.Recordset)  
  
    Dim strName As String  
  
    strName = rstp.ActiveCommand.Parameters.Item("LastName").Value  
  
    Debug.Print "Command text = '"; rstp.ActiveCommand.CommandText; "'"  
    Debug.Print "Parameter = '"; strName; "'"  
  
    If rstp.BOF = True Then  
       Debug.Print "Name = '"; strName; "', not found."  
    Else  
       Debug.Print "Name = '"; rstp!au_fname; " "; rstp!au_lname; _  
             "', author ID = '"; rstp!au_id; "'"  
    End If  
  
    rstp.Close  
    Set rstp = Nothing  
End Sub  
'EndActiveCommandPrintVB  
```  
  
## <a name="see-also"></a>Consulte também  
 [Propriedade ActiveCommand (ADO)](../../../ado/reference/ado-api/activecommand-property-ado.md)   
 [Objeto de comando (ADO)](../../../ado/reference/ado-api/command-object-ado.md)   
 [Objeto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
