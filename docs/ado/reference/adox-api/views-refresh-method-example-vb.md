---
description: Exemplo do método Refresh de exibições (VB)
title: Exemplo do método Refresh de exibições (VB) | Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 3112670df34b0e74e359ef0e514d9acdc8620788
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88439268"
---
# <a name="views-refresh-method-example-vb"></a>Exemplo do método Refresh de exibições (VB)
O código a seguir mostra como atualizar a coleção [views](../../../ado/reference/adox-api/views-collection-adox.md) de um [Catálogo](../../../ado/reference/adox-api/catalog-object-adox.md). Isso é necessário antes que os objetos de [exibição](../../../ado/reference/adox-api/view-object-adox.md) do **Catálogo** possam ser acessados.  
  
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
  
## <a name="see-also"></a>Consulte Também  
 [Método Refresh (ADO)](../../../ado/reference/ado-api/refresh-method-ado.md)   
 [Coleção Views (ADOX)](../../../ado/reference/adox-api/views-collection-adox.md)
