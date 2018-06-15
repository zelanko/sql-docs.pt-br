---
title: Procedimentos de atualização de exemplo do método (VB) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
dev_langs:
- VB
helpviewer_keywords:
- Refresh method [ADOX], Visual Basic example
ms.assetid: 499679bd-287b-487d-bdfb-3803abffec1c
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: eb1e831fafeeadd47e87928fe7d829ea83d93e58
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/11/2018
ms.locfileid: "35286775"
---
# <a name="procedures-refresh-method-example-vb"></a>Procedimentos de atualização de exemplo do método (VB)
O código a seguir mostra como atualizar o [procedimentos](../../../ado/reference/adox-api/procedures-collection-adox.md) coleção de um [catálogo](../../../ado/reference/adox-api/catalog-object-adox.md). Isso é necessário antes de [procedimento](../../../ado/reference/adox-api/procedure-object-adox.md) de objetos a partir de **catálogo** pode ser acessado.  
  
```  
' BeginProceduresRefreshVB  
Sub Main()  
    On Error GoTo ProcedureRefreshError  
  
    Dim cat As New ADOX.Catalog  
  
    ' Open the Catalog  
    cat.ActiveConnection = _  
        "Provider='Microsoft.Jet.OLEDB.4.0';" & _  
        "Data Source='Northwind.mdb';"  
  
    ' Refresh the Procedures collection  
    cat.Procedures.Refresh  
  
    'Clean up  
    Set cat.ActiveConnection = Nothing  
    Set cat = Nothing  
    Exit Sub  
  
ProcedureRefreshError:  
    Set cat = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
End Sub  
' EndProceduresRefreshVB  
```  
  
## <a name="see-also"></a>Consulte também  
 [Objeto de catálogo (ADOX)](../../../ado/reference/adox-api/catalog-object-adox.md)   
 [Coleção de procedimentos (ADOX)](../../../ado/reference/adox-api/procedures-collection-adox.md)   
 [Método Refresh (ADO)](../../../ado/reference/ado-api/refresh-method-ado.md)
