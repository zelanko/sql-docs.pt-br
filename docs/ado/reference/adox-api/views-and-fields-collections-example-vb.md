---
description: Exemplo de coleções Views e Fields (VB)
title: Exemplo de coleções de exibições e campos (VB) | Microsoft Docs
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
- Views collection [ADOX], Visual Basic example
- Fields collection [ADOX]
ms.assetid: d8304849-3f80-4cf3-9425-529d2a8ebedd
author: rothja
ms.author: jroth
ms.openlocfilehash: 30be1e48aca9a942b0a98d0f119f1f8e8218144b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88439328"
---
# <a name="views-and-fields-collections-example-vb"></a>Exemplo de coleções Views e Fields (VB)
O código a seguir demonstra como usar a propriedade [Command](../../../ado/reference/adox-api/command-property-adox.md) e o objeto [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) para recuperar informações de campo para a exibição.  
  
```  
' BeginViewFieldsVB  
Sub ViewFields()  
    On Error GoTo ViewFieldsError  
  
    Dim cnn As New ADODB.Connection  
    Dim rst As New ADODB.Recordset  
    Dim fld As ADODB.Field  
    Dim cat As New ADOX.Catalog  
  
    ' Open the Connection  
    cnn.Open _  
        "Provider='Microsoft.Jet.OLEDB.4.0';" & _  
        "Data Source='Northwind.mdb';"  
  
    ' Open the catalog  
    Set cat.ActiveConnection = cnn  
  
    ' Set the Source for the Recordset  
    Set rst.Source = cat.Views("AllCustomers").Command  
  
    ' Retrieve Field information  
    rst.Fields.Refresh  
    For Each fld In rst.Fields  
        Debug.Print fld.Name & ":" & fld.Type  
    Next  
  
    'Clean up  
    cnn.Close  
    Set cat = Nothing  
    Set rst = Nothing  
    Set cnn = Nothing  
    Exit Sub  
  
ViewFieldsError:  
  
    If Not cnn Is Nothing Then  
        If cnn.State = adStateOpen Then cnn.Close  
    End If  
  
    Set cat = Nothing  
    Set rst = Nothing  
    Set cnn = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
  
End Sub  
' EndViewFieldsVB  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Propriedade ActiveConnection (ADOX)](../../../ado/reference/adox-api/activeconnection-property-adox.md)   
 [Objeto de catálogo (ADOX)](../../../ado/reference/adox-api/catalog-object-adox.md)   
 [Propriedade Command (ADOX)](../../../ado/reference/adox-api/command-property-adox.md)   
 [Objeto View (ADOX)](../../../ado/reference/adox-api/view-object-adox.md)   
 [Coleção Views (ADOX)](../../../ado/reference/adox-api/views-collection-adox.md)
