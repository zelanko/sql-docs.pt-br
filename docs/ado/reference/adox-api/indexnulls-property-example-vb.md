---
title: Exemplo da propriedade IndexNulls (VB) | Microsoft Docs
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
- IndexNulls property [ADOX], Visual Basic example
ms.assetid: 45204669-32c0-4690-aab9-ddf0fd71ae48
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: fc1a2db077a08b37ddd6143ea7a76ebd257f2a48
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66706489"
---
# <a name="indexnulls-property-example-vb"></a>Exemplo da propriedade IndexNulls (VB)
Este exemplo demonstra a [IndexNulls](../../../ado/reference/adox-api/indexnulls-property-adox.md) propriedade de um [índice](../../../ado/reference/adox-api/index-object-adox.md). O código cria um novo índice e define o valor de **IndexNulls** com base na entrada do usuário (de uma caixa de listagem chamada List1). Em seguida, o **índice** é acrescentado para o **funcionários** [tabela](../../../ado/reference/adox-api/table-object-adox.md) no *Northwind* [catálogo](../../../ado/reference/adox-api/catalog-object-adox.md). O novo **índice** é aplicado a um [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md) com base no **funcionários** tabela e o **Recordset** é aberto. Um novo registro é adicionado para o **funcionários** tabela, com um **nulo** valor no campo indexado. Se este novo registro é exibido depende da configuração das **IndexNulls** propriedade.  
  
```  
' BeginIndexNullsVB  
Private Sub cmdIndexNulls_Click()  
    IndexNullsX  
End Sub  
  
Sub IndexNullsX()  
  
    Dim cnn As New ADODB.Connection  
    Dim catNorthwind As New ADOX.Catalog  
    Dim idxNew As New ADOX.Index  
    Dim rstEmployees As New ADODB.Recordset  
    Dim varBookmark As Variant  
  
    ' Connect the catalog.  
    cnn.Open "Provider=Microsoft.Jet.OLEDB.4.0;" & _  
        "data source=c:\Program Files\" & _  
        "Microsoft Office\Office\Samples\Northwind.mdb;"  
  
    Set catNorthwind.ActiveConnection = cnn  
  
    ' Append Country column to new index  
    idxNew.Columns.Append "Country"  
    idxNew.Name = "NewIndex"  
  
    ' Set IndexNulls based on user selection in listbox List1  
    Select Case List1.List(List1.ListIndex)  
        Case "Allow"  
            idxNew.IndexNulls = adIndexNullsAllow  
        Case "Ignore"  
            idxNew.IndexNulls = adIndexNullsIgnore  
        Case Else  
            End  
    End Select  
  
    'Append new index to Employees table  
    catNorthwind.Tables("Employees").Indexes.Append idxNew  
  
    rstEmployees.Index = idxNew.Name  
    rstEmployees.Open "Employees", cnn, adOpenKeyset, _  
        adLockOptimistic, adCmdTableDirect  
  
    With rstEmployees  
        ' Add a new record to the Employees table.  
        .AddNew  
        !FirstName = "Gary"  
        !LastName = "Haarsager"  
        .Update  
  
        ' Bookmark the newly added record  
        varBookmark = .Bookmark  
  
        ' Use the new index to set the order of the records.  
        .MoveFirst  
  
        Debug.Print "Index = " & .Index & _  
            ", IndexNulls = " & idxNew.IndexNulls  
        Debug.Print "  Country - Name"  
  
        ' Enumerate the Recordset. The value of the  
        ' IndexNulls property will determine if the newly  
        ' added record appears in the output.  
        Do While Not .EOF  
            Debug.Print "    " & _  
                IIf(IsNull(!Country), "[Null]", !Country) & _  
                " - " & !FirstName & " " & !LastName  
            .MoveNext  
        Loop  
  
        ' Delete new record because this is a demonstration.  
        .Bookmark = varBookmark  
        .Delete  
  
        .Close  
    End With  
  
    ' Delete new Index because this is a demonstration.  
    catNorthwind.Tables("Employees").Indexes.Delete idxNew.Name  
    Set catNorthwind = Nothing  
  
End Sub  
' EndIndexNullsVB  
```  
  
## <a name="see-also"></a>Consulte também  
 [Objeto Index (ADOX)](../../../ado/reference/adox-api/index-object-adox.md)   
 [Propriedade IndexNulls (ADOX)](../../../ado/reference/adox-api/indexnulls-property-adox.md)
