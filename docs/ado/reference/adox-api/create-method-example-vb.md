---
title: Criar o exemplo do método (VB) | Microsoft Docs
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
- Create method [ADOX], Visual Basic example
ms.assetid: d7ea0244-596a-404e-8f30-71cadab8d8fc
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 9fb207d7ba30c12b1d694bbef5337c51e1062440
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66703328"
---
# <a name="create-method-example-vb"></a>Criar um exemplo de método (VB)
O código a seguir mostra como criar um novo banco de dados Microsoft Jet com o [criar](../../../ado/reference/adox-api/create-method-adox.md) método.  
  
```  
Attribute VB_Name = "Create"  
Option Explicit  
  
' BeginCreateDatabaseVB  
Sub CreateDatabase()  
    On Error GoTo CreateDatabaseError  
  
    Dim cat As New ADOX.Catalog  
    cat.Create "Provider='Microsoft.Jet.OLEDB.4.0';Data Source='new.mdb'"  
  
    'Clean up  
    Set cat = Nothing  
    Exit Sub  
  
CreateDatabaseError:  
    Set cat = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
End Sub  
' EndCreateDatabaseVB  
```  
  
## <a name="see-also"></a>Consulte também  
 [Objeto Catalog (ADOX)](../../../ado/reference/adox-api/catalog-object-adox.md)   
 [Método Create (ADOX)](../../../ado/reference/adox-api/create-method-adox.md)
