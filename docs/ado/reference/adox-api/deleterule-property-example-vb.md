---
description: Exemplo da propriedade DeleteRule (VB)
title: Exemplo da propriedade DeleteRule (VB) | Microsoft Docs
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
- DeleteRule property [ADOX], Visual Basic example
ms.assetid: 9ba00118-a80d-4a6d-a7d6-4f5492fb7ded
author: rothja
ms.author: jroth
ms.openlocfilehash: d662516dd705ede8bd62f9a92866bd569120807f
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88770565"
---
# <a name="deleterule-property-example-vb"></a>Exemplo da propriedade DeleteRule (VB)
Este exemplo demonstra a propriedade [DeleteRule](./deleterule-property-adox.md) de um objeto de [chave](./key-object-adox.md) . O código acrescenta uma nova [tabela](./table-object-adox.md) e, em seguida, define uma nova chave primária, definindo **DeleteRule** como **adRICascade**.  
  
```  
' BeginDeleteRuleVB  
Sub Main()  
    On Error GoTo DeleteRuleXError  
  
    Dim kyPrimary As New ADOX.Key  
    Dim cat As New ADOX.Catalog  
    Dim tblNew As New ADOX.Table  
  
    ' Connect the catalog  
    cat.ActiveConnection = "Provider='Microsoft.Jet.OLEDB.4.0';" & _  
                     "data source='Northwind.mdb';"  
  
    ' Name new table  
    tblNew.Name = "NewTable"  
  
    ' Append a numeric and a text field to new table.  
    tblNew.Columns.Append "NumField", adInteger, 20  
    tblNew.Columns.Append "TextField", adVarWChar, 20  
  
    ' Append the new table  
    cat.Tables.Append tblNew  
  
    ' Define the Primary key  
    kyPrimary.Name = "NumField"  
    kyPrimary.Type = adKeyPrimary  
    kyPrimary.RelatedTable = "Customers"  
    kyPrimary.Columns.Append "NumField"  
    kyPrimary.Columns("NumField").RelatedColumn = "CustomerId"  
    kyPrimary.DeleteRule = adRICascade  
  
    ' Append the primary key  
    cat.Tables("NewTable").Keys.Append kyPrimary  
    Debug.Print "The primary key is appended."  
  
    'Delete the table as this is a demonstration.  
    cat.Tables.Delete tblNew.Name  
    Debug.Print "The primary key is deleted."  
  
    'Clean up  
    Set cat.ActiveConnection = Nothing  
    Set cat = Nothing  
    Set kyPrimary = Nothing  
    Set tblNew = Nothing  
    Exit Sub  
  
DeleteRuleXError:  
  
    Set cat = Nothing  
    Set kyPrimary = Nothing  
    Set tblNew = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
  
End Sub  
' EndDeleteRuleVB  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Propriedade DeleteRule (ADOX)](./deleterule-property-adox.md)   
 [Objeto Key (ADOX)](./key-object-adox.md)