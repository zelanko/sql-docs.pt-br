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
ms.openlocfilehash: 03e46b4f449f0a937c21c436049692f0c95695cc
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88768835"
---
# <a name="views-refresh-method-example-vb"></a>Exemplo do método Refresh de exibições (VB)
O código a seguir mostra como atualizar a coleção [views](./views-collection-adox.md) de um [Catálogo](./catalog-object-adox.md). Isso é necessário antes que os objetos de [exibição](./view-object-adox.md) do **Catálogo** possam ser acessados.  
  
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
 [Método Refresh (ADO)](../ado-api/refresh-method-ado.md)   
 [Coleção Views (ADOX)](./views-collection-adox.md)