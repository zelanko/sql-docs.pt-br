---
title: "Tabelas e colunas acrescentar métodos, nomes de exemplo da propriedade (VB) | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
dev_langs: VB
helpviewer_keywords:
- Name property [ADOX], Visual Basic example
- Append method [ADOX], Visual Basic example
ms.assetid: 678e5546-df5d-4cd0-bfe9-6cf13cb385c0
caps.latest.revision: "9"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 637f3aa8ebe0fe809b298b3c6d99ddfbd013ef6f
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="columns-and-tables-append-methods-name-property-example-vb"></a>Tabelas e colunas acrescentar métodos, exemplo de nome de propriedade (VB)
O código a seguir demonstra como criar uma nova tabela.  
  
```  
' BeginCreateTableVB  
Sub Main()  
    On Error GoTo CreateTableError  
  
    Dim tbl As New Table  
    Dim cat As New ADOX.Catalog  
  
    ' Open the Catalog.  
    cat.ActiveConnection = "Provider='Microsoft.Jet.OLEDB.4.0';" & _  
        "Data Source='Northwind.mdb';"  
  
    tbl.Name = "MyTable"  
    tbl.Columns.Append "Column1", adInteger  
    tbl.Columns.Append "Column2", adInteger  
    tbl.Columns.Append "Column3", adVarWChar, 50  
    cat.Tables.Append tbl  
    Debug.Print "Table 'MyTable' is added."  
  
    'Delete the table as this is a demonstration.  
    cat.Tables.Delete tbl.Name  
    Debug.Print "Table 'MyTable' is deleted."  
  
    'Clean up  
    Set cat.ActiveConnection = Nothing  
    Set cat = Nothing  
    Set tbl = Nothing  
    Exit Sub  
  
CreateTableError:  
  
    Set cat = Nothing  
    Set tbl = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
End Sub  
' EndCreateTableVB  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Acrescente o método (ADOX colunas)](../../../ado/reference/adox-api/append-method-adox-columns.md)   
 [(Tabelas ADOX) do método append](../../../ado/reference/adox-api/append-method-adox-tables.md)   
 [Objeto de coluna (ADOX)](../../../ado/reference/adox-api/column-object-adox.md)   
 [Coleção de colunas (ADOX)](../../../ado/reference/adox-api/columns-collection-adox.md)   
 [Propriedade Name (ADOX)](../../../ado/reference/adox-api/name-property-adox.md)   
 [Objeto de tabela (ADOX)](../../../ado/reference/adox-api/table-object-adox.md)   
 [Coleção Tables (ADOX)](../../../ado/reference/adox-api/tables-collection-adox.md)
