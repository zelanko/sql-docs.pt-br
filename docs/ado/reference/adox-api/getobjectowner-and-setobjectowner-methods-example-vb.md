---
title: GetObjectOwner e Setobjectowner (VB) métodos | Microsoft Docs
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
- SetObjectOwner method [ADOX], Visual Basic example
- GetObjectOwner method [ADOX], Visual Basic example
ms.assetid: e44ec3d4-42ae-447d-aaed-bdea53cb0cca
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 03850fdaef19ece963bb7b196ab14edccd290fde
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67966381"
---
# <a name="getobjectowner-and-setobjectowner-methods-example-vb"></a>Exemplo dos métodos GetObjectOwner e SetObjectOwner (VB)
Este exemplo demonstra a [GetObjectOwner](../../../ado/reference/adox-api/getobjectowner-method-adox.md) e [SetObjectOwner](../../../ado/reference/adox-api/setobjectowner-method.md) métodos. Esse código supõe a existência do grupo Contabilidade (consulte a [grupos e usuários Append, ChangePassword métodos de exemplo (VB)](../../../ado/reference/adox-api/groups-and-users-append-changepassword-methods-example-vb.md) para ver como adicionar esse grupo para o sistema). O proprietário da tabela de categorias é definido como contabilidade.  
  
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
 [Objeto Catalog (ADOX)](../../../ado/reference/adox-api/catalog-object-adox.md)   
 [Método GetObjectOwner (ADOX)](../../../ado/reference/adox-api/getobjectowner-method-adox.md)   
 [Método SetObjectOwner](../../../ado/reference/adox-api/setobjectowner-method.md)
