---
description: Coleção Views, exemplo da propriedade CommandText (VB)
title: Coleção views, exemplo da propriedade CommandText (VB) | Microsoft Docs
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
- CommandText property [ADOX]
- Views collection [ADOX], Visual Basic example
ms.assetid: a05a0190-352d-44ff-9488-0c94e9fb656e
author: rothja
ms.author: jroth
ms.openlocfilehash: 645dd3602c97f8ca4bb4fd7df832352bb4cdded0
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88768905"
---
# <a name="views-collection-commandtext-property-example-vb"></a>Coleção Views, exemplo da propriedade CommandText (VB)
O código a seguir demonstra como usar a propriedade [Command](./command-property-adox.md) para atualizar o texto de uma exibição.  
  
```  
' BeginViewsCollectionVB  
Sub Main()  
    On Error GoTo ViewTextError  
  
    Dim cnn As New ADODB.Connection  
    Dim cat As New ADOX.Catalog  
    Dim cmd As New ADODB.Command  
  
    ' Open the connection.  
    cnn.Open _  
        "Provider='Microsoft.Jet.OLEDB.4.0';" & _  
        "Data Source='Northwind.mdb';"  
  
    ' Open the catalog.  
    Set cat.ActiveConnection = cnn  
  
    ' Get the command.  
    Set cmd = cat.Views("AllCustomers").Command  
  
    ' Update the CommandText of the command.  
    cmd.CommandText = _  
    "Select CustomerId, CompanyName, ContactName From Customers"  
  
    ' Update the view.  
    Set cat.Views("AllCustomers").Command = cmd  
  
    'Clean up.  
    cnn.Close  
    Set cat = Nothing  
    Set cmd = Nothing  
    Set cnn = Nothing  
    Exit Sub  
  
ViewTextError:  
  
    Set cat = Nothing  
    Set cmd = Nothing  
  
    If Not cnn Is Nothing Then  
        If cnn.State = adStateOpen Then cnn.Close  
    End If  
    Set cnn = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
End Sub  
' EndViewsCollectionVB  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Propriedade ActiveConnection (ADOX)](./activeconnection-property-adox.md)   
 [Objeto de catálogo (ADOX)](./catalog-object-adox.md)   
 [Propriedade Command (ADOX)](./command-property-adox.md)   
 [Objeto View (ADOX)](./view-object-adox.md)   
 [Coleção Views (ADOX)](./views-collection-adox.md)