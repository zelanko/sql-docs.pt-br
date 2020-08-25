---
description: Exemplo do método Refresh de procedimentos (VB)
title: Exemplo do método Refresh de procedimentos (VB) | Microsoft Docs
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
- Refresh method [ADOX], Visual Basic example
ms.assetid: 499679bd-287b-487d-bdfb-3803abffec1c
author: rothja
ms.author: jroth
ms.openlocfilehash: 0bc0bd69e4b184b91c1d337d6b9e1b9c490b3116
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88769555"
---
# <a name="procedures-refresh-method-example-vb"></a>Exemplo do método Refresh de procedimentos (VB)
O código a seguir mostra como atualizar a coleção de [procedimentos](./procedures-collection-adox.md) de um [Catálogo](./catalog-object-adox.md). Isso é necessário antes que os objetos de [procedimento](./procedure-object-adox.md) do **Catálogo** possam ser acessados.  
  
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
  
## <a name="see-also"></a>Consulte Também  
 [Objeto de catálogo (ADOX)](./catalog-object-adox.md)   
 [Coleção de procedimentos (ADOX)](./procedures-collection-adox.md)   
 [Método Refresh (ADO)](../ado-api/refresh-method-ado.md)