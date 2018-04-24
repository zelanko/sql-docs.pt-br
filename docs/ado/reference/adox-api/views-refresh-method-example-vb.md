---
title: Exibições de atualização de exemplo do método (VB) | Microsoft Docs
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
dev_langs:
- VB
helpviewer_keywords:
- Refresh method [ADOX]
ms.assetid: cdad2d66-6ade-40dc-9e74-e40cfa9bc127
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 0dbcb1ed8bf9b22309ade18efe4ad2e8c9dcbd6e
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/18/2018
---
# <a name="views-refresh-method-example-vb"></a>Exemplo de método (VB) de atualização de modos de exibição
O código a seguir mostra como atualizar o [exibições](../../../ado/reference/adox-api/views-collection-adox.md) coleção de um [catálogo](../../../ado/reference/adox-api/catalog-object-adox.md). Isso é necessário antes de [exibição](../../../ado/reference/adox-api/view-object-adox.md) de objetos a partir de **catálogo** pode ser acessado.  
  
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
 [Atualizar o método (ADO)](../../../ado/reference/ado-api/refresh-method-ado.md)   
 [Coleção Views (ADOX)](../../../ado/reference/adox-api/views-collection-adox.md)
