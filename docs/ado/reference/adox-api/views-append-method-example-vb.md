---
title: Append de exibições de exemplo do método (VB) | Microsoft Docs
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
- Append method [ADOX]
ms.assetid: b5b4c082-ac29-4f49-a8b8-e21b554c9b0d
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: cc555b4c464f064a3b92091cfc7443110ccbd6d8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66697069"
---
# <a name="views-append-method-example-vb"></a>Exemplo do método Append de exibições (VB)
O código a seguir demonstra como usar um [comando](../../../ado/reference/ado-api/command-object-ado.md) objeto e o [exibições](../../../ado/reference/adox-api/views-collection-adox.md) coleção [Append](../../../ado/reference/adox-api/append-method-adox-views.md) método para criar uma nova exibição na fonte de dados subjacente.  
  
```  
' BeginCreateViewVB  
Sub Main()  
    On Error GoTo CreateViewError  
  
    Dim cmd As New ADODB.Command  
    Dim cat As New ADOX.Catalog  
  
    ' Open the Catalog  
    cat.ActiveConnection = _  
        "Provider='Microsoft.Jet.OLEDB.4.0';" & _  
        "Data Source='Northwind.mdb';"  
  
    ' Create the command representing the view.  
    cmd.CommandText = "Select * From Customers"  
  
    ' Create the new View  
    cat.Views.Append "AllCustomers", cmd  
  
    'Clean up  
    Set cat.ActiveConnection = Nothing  
    Set cat = Nothing  
    Set cmd = Nothing  
    Exit Sub  
  
CreateViewError:  
  
    Set cat = Nothing  
    Set cmd = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
End Sub  
' EndCreateViewVB  
```  
  
## <a name="see-also"></a>Consulte também  
 [Propriedade ActiveConnection (ADOX)](../../../ado/reference/adox-api/activeconnection-property-adox.md)   
 [Acrescentar o método (exibições do ADOX)](../../../ado/reference/adox-api/append-method-adox-views.md)   
 [Objeto Catalog (ADOX)](../../../ado/reference/adox-api/catalog-object-adox.md)   
 [Objeto View (ADOX)](../../../ado/reference/adox-api/view-object-adox.md)   
 [Coleção Views (ADOX)](../../../ado/reference/adox-api/views-collection-adox.md)
