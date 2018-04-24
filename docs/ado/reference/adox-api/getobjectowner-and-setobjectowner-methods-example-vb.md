---
title: GetObjectOwner e exemplo dos métodos SetObjectOwner (VB) | Microsoft Docs
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
- SetObjectOwner method [ADOX], Visual Basic example
- GetObjectOwner method [ADOX], Visual Basic example
ms.assetid: e44ec3d4-42ae-447d-aaed-bdea53cb0cca
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 6a10869852225f7d50f44ad4ef174cf285d1cf0f
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/18/2018
---
# <a name="getobjectowner-and-setobjectowner-methods-example-vb"></a>Exemplo de métodos de SetObjectOwner (VB) e GetObjectOwner
Este exemplo demonstra o [GetObjectOwner](../../../ado/reference/adox-api/getobjectowner-method-adox.md) e [SetObjectOwner](../../../ado/reference/adox-api/setobjectowner-method.md) métodos. Esse código supõe a existência do grupo de estatísticas (consulte o [grupos e usuários anexar, o exemplo de métodos ChangePassword (VB)](../../../ado/reference/adox-api/groups-and-users-append-changepassword-methods-example-vb.md) para ver como adicionar esse grupo para o sistema). O proprietário da tabela de categorias é definido para contabilidade.  
  
```  
' BeginOwnersVB  
Sub OwnersX()  
  
    Dim tblLoop As New ADOX.Table  
    Dim cat As New ADOX.Catalog  
    Dim strOwner As String  
  
    ' Open the Catalog.  
    cat.ActiveConnection = "Provider=Microsoft.Jet.OLEDB.4.0;" & _  
        "Data Source=c:\Program Files\" & _  
        "Microsoft Office\Office\Samples\Northwind.mdb;" & _  
        "jet oledb:system database=" & _  
        "c:\Program Files\Microsoft Office\Office\system.mdw"  
  
    ' Print the original owner of Categories  
    strOwner = cat.GetObjectOwner("Categories", adPermObjTable)  
    Debug.Print "Owner of Categories: " & strOwner  
  
    ' Set the owner of Categories to Accounting  
    cat.SetObjectOwner "Categories", adPermObjTable, "Accounting"  
  
    ' List the owners of all tables and columns in the catalog.  
    For Each tblLoop In cat.Tables  
        Debug.Print "Table: " & tblLoop.Name  
        Debug.Print "   Owner: " & _  
            cat.GetObjectOwner(tblLoop.Name, adPermObjTable)  
    Next tblLoop  
  
    ' Restore the original owner of Categories  
    cat.SetObjectOwner "Categories", adPermObjTable, strOwner  
  
End Sub  
' EndOwnersVB  
```  
  
## <a name="see-also"></a>Consulte também  
 [Objeto de catálogo (ADOX)](../../../ado/reference/adox-api/catalog-object-adox.md)   
 [Método GetObjectOwner (ADOX)](../../../ado/reference/adox-api/getobjectowner-method-adox.md)   
 [Método SetObjectOwner](../../../ado/reference/adox-api/setobjectowner-method.md)
