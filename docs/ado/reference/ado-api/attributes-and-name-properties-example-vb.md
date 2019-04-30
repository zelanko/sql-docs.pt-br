---
title: Exemplo de propriedades de nome (VB) e atributos | Microsoft Docs
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
- Attributes property [ADO], Visual Basic example
- Name property [ADO], Visual Basic example
ms.assetid: 258bdce3-1819-44a2-9217-105879c789ef
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: eb69a3f9da2ed86411c2a6506cf2ea7a8defcc7f
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63248331"
---
# <a name="attributes-and-name-properties-example-vb"></a>Exemplos das propriedades Attributes e Name (VB)
Este exemplo exibe o valor de [atributos](../../../ado/reference/ado-api/attributes-property-ado.md) propriedade para [Conexão](../../../ado/reference/ado-api/connection-object-ado.md), [campo](../../../ado/reference/ado-api/field-object.md), e [propriedade](../../../ado/reference/ado-api/property-object-ado.md) objetos. Ele usa o [nome](../../../ado/reference/ado-api/name-property-ado.md) propriedade para exibir o nome de cada **campo** e **propriedade** objeto.  
  
```  
' BeginAttributesVB  
Sub Main()  
    On Error GoTo AttributesXError  
  
    Dim cnn As New ADODB.Connection  
    Dim cat As New ADOX.Catalog  
    Dim colTemp As New ADOX.Column  
    Dim rstEmployees As New Recordset  
    Dim strMessage As String  
    Dim strInput As String  
    Dim tblEmp As ADOX.Table  
  
    ' Connect the catalog.  
    cnn.Open "Provider='Microsoft.Jet.OLEDB.4.0';data source=" & _  
        "'Northwind.mdb';"  
    Set cat.ActiveConnection = cnn  
  
    Set tblEmp = cat.Tables("Employees")  
  
    ' Create a new Field object and append it to the Fields  
    ' collection of the Employees table.  
    colTemp.Name = "FaxPhone"  
    colTemp.Type = adVarWChar  
    colTemp.DefinedSize = 24  
    colTemp.Attributes = adColNullable  
    cat.Tables("Employees").Columns.Append colTemp.Name, adWChar, 24  
  
    ' Open the Employees table for updating as a Recordset  
    rstEmployees.Open "Employees", cnn, adOpenKeyset, adLockOptimistic, adCmdTable  
  
    With rstEmployees  
        ' Get user input.  
        strMessage = "Enter fax number for " & _  
            !FirstName & " " & !LastName & "." & vbCr & _  
            "[? - unknown, X - has no fax]"  
        strInput = UCase(InputBox(strMessage))  
        If strInput <> "" Then  
            Select Case strInput  
                Case "?"  
                    !FaxPhone = Null  
                Case "X"  
                    !FaxPhone = ""  
                Case Else  
                    !FaxPhone = strInput  
            End Select  
            .Update  
  
            ' Print report.  
            Debug.Print "Name - Fax number"  
            Debug.Print !FirstName & " " & !LastName & " - ";  
  
            If IsNull(!FaxPhone) Then  
                Debug.Print "[Unknown]"  
            Else  
                If !FaxPhone = "" Then  
                    Debug.Print "[Has no fax]"  
                Else  
                    Debug.Print !FaxPhone  
                End If  
            End If  
  
        End If  
  
        .Close  
    End With  
  
    'Clean up  
    tblEmp.Columns.Delete colTemp.Name  
    cnn.Close  
    Set rstEmployees = Nothing  
    Set cat = Nothing  
    Set colTemp = Nothing  
    Set cnn = Nothing  
    Exit Sub  
  
AttributesXError:  
  
    If Not rstEmployees Is Nothing Then  
        If rstEmployees.State = adStateOpen Then rstEmployees.Close  
    End If  
    Set rstEmployees = Nothing  
  
    If Not tblEmp Is Nothing Then tblEmp.Columns.Delete colTemp.Name  
  
    Set cat = Nothing  
    Set colTemp = Nothing  
  
    If Not cnn Is Nothing Then  
        If cnn.State = adStateOpen Then cnn.Close  
    End If  
    Set cnn = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
  
End Sub  
' EndAttributesVB  
```  
  
## <a name="see-also"></a>Consulte também  
 [Propriedade Attributes (ADO)](../../../ado/reference/ado-api/attributes-property-ado.md)   
 [Objeto de Conexão (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)   
 [Objeto Field](../../../ado/reference/ado-api/field-object.md)   
 [Propriedade Name (ADO)](../../../ado/reference/ado-api/name-property-ado.md)   
 [Objeto Property (ADO)](../../../ado/reference/ado-api/property-object-ado.md)
