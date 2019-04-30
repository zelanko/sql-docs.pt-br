---
title: Atualização de exibições de exemplo do método (VB) | Microsoft Docs
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
- Refresh method [ADOX]
ms.assetid: cdad2d66-6ade-40dc-9e74-e40cfa9bc127
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 123d7abe3248868295e8433d75d9e2a935cdc58d
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63281493"
---
# <a name="views-refresh-method-example-vb"></a>Exemplo do método Refresh de exibições (VB)
O código a seguir mostra como atualizar o [modos de exibição](../../../ado/reference/adox-api/views-collection-adox.md) coleção de uma [catálogo](../../../ado/reference/adox-api/catalog-object-adox.md). Isso é necessário antes de [modo de exibição](../../../ado/reference/adox-api/view-object-adox.md) objetos das **catálogo** pode ser acessado.  
  
```  
' BeginViewsRefreshVB  
Sub Main()  
    On Error GoTo ProcedureViewsRefreshError  
  
    Dim cat As New ADOX.Catalog  
  
    ' Open the catalog.  
    cat.ActiveConnection = "Provider='Microsoft.Jet.OLEDB.4.0';" & _  
        "Data Source='Northwind.mdb';"  
  
    ' Refresh the Procedures collection.  
    cat.Views.Refresh  
  
    'Clean up  
    Set cat = Nothing  
    Exit Sub  
  
ProcedureViewsRefreshError:  
  
    If Not cat Is Nothing Then  
        Set cat = Nothing  
    End If  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
End Sub  
' EndViewsRefreshVB  
```  
  
## <a name="see-also"></a>Consulte também  
 [Método Refresh (ADO)](../../../ado/reference/ado-api/refresh-method-ado.md)   
 [Coleção Views (ADOX)](../../../ado/reference/adox-api/views-collection-adox.md)
