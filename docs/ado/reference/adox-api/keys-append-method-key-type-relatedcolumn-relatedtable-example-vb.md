---
description: Exemplo das propriedades UpdateRule e RelatedTable, RelatedColumn, Key Type e do método Keys Append (VB)
title: Criar uma nova relação de chave estrangeira entre as tabelas exemplo (VB) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
dev_langs:
- VB
helpviewer_keywords:
- Key Type property [ADOX], Visual Basic example
- RelatedTable property [ADOX], Visual Basic example
- Keys Append method [ADOX], Visual Basic example
- UpdateRule property [ADOX], Visual Basic example
- RelatedColumn property [ADOX], Visual Basic example
ms.assetid: 13b5b1c3-6af6-439e-bb65-976578ba6bc2
author: rothja
ms.author: jroth
ms.openlocfilehash: edc38c1506e472eddb6640c9d7ca121154dcc4cb
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88984057"
---
# <a name="keys-append-method-key-type-relatedcolumn-relatedtable-and-updaterule-properties-example-vb"></a>Exemplo das propriedades UpdateRule e RelatedTable, RelatedColumn, Key Type e do método Keys Append (VB)
O código a seguir demonstra como criar uma nova relação de chave estrangeira entre duas tabelas existentes denominadas **Customers** e **Orders**.  
  
```  
' BeginCreateKeyVB  
Sub Main()  
    On Error GoTo CreateKeyError  
  
    Dim kyForeign As New ADOX.Key  
    Dim cat As New ADOX.Catalog  
  
    ' Connect to the catalog.  
    cat.ActiveConnection = "Provider='Microsoft.Jet.OLEDB.4.0';" & _  
        "Data Source='Northwind.mdb';"  
  
    ' Define the foreign key.  
    kyForeign.Name = "CustOrder"  
    kyForeign.Type = adKeyForeign  
    kyForeign.RelatedTable = "Customers"  
    kyForeign.Columns.Append "CustomerId"  
    kyForeign.Columns("CustomerId").RelatedColumn = "CustomerId"  
    kyForeign.UpdateRule = adRICascade  
  
    ' Append the foreign key to the keys collection.  
    cat.Tables("Orders").Keys.Append kyForeign  
  
    'Delete the key t demonstrate the Delete method.  
    cat.Tables("Orders").Keys.Delete kyForeign.Name  
  
    'Clean up.  
    Set cat.ActiveConnection = Nothing  
    Set cat = Nothing  
    Set kyForeign = Nothing  
    Exit Sub  
  
CreateKeyError:  
    Set cat = Nothing  
    Set kyForeign = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
  
End Sub  
' EndCreateKeyVB  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Método Append (colunas ADOX)](./append-method-adox-columns.md)   
 [Método Append (chaves ADOX)](./append-method-adox-keys.md)   
 [Objeto de catálogo (ADOX)](./catalog-object-adox.md)   
 [Objeto Column (ADOX)](./column-object-adox.md)   
 [Coleção Columns (ADOX)](./columns-collection-adox.md)   
 [Objeto de chave (ADOX)](./key-object-adox.md)   
 [Coleção Keys (ADOX)](./keys-collection-adox.md)   
 [Propriedade Name (ADOX)](./name-property-adox.md)   
 [Propriedade RelatedColumn (ADOX)](./relatedcolumn-property-adox.md)   
 [Propriedade RelatedTable (ADOX)](./relatedtable-property-adox.md)   
 [Objeto Table (ADOX)](./table-object-adox.md)   
 [Coleção Tables (ADOX)](./tables-collection-adox.md)   
 [Propriedade Type (chave) (ADOX)](./type-property-key-adox.md)   
 [Propriedade UpdateRule (ADOX)](./updaterule-property-adox.md)