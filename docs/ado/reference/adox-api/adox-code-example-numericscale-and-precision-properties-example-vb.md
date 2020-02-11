---
title: Exemplo das propriedades NumericScale e Precision (VB) | Microsoft Docs
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
- Precision property [ADOX], Visual Basic example
- NumericScale property [ADOX], Visual Basic example
ms.assetid: ea2ec614-34c8-41b7-8ebd-063798bd56b4
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 671e7f144ff70bedf1556b506ead6c51d05ebd08
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67952162"
---
# <a name="adox-code-example-numericscale-and-precision-properties-example-vb"></a>Exemplo de código ADOX: NumericScale e exemplo de propriedades Precision (VB)
Este exemplo demonstra as propriedades [NumericScale](../../../ado/reference/adox-api/numericscale-property-adox.md) e [Precision](../../../ado/reference/adox-api/precision-property-adox.md) do objeto [Column](../../../ado/reference/adox-api/column-object-adox.md) . Esse código exibe seu valor para a tabela **detalhes do pedido** do banco de dados *Northwind* .  
  
```  
' BeginNumericScalePrecVB  
Sub Main()  
    On Error GoTo NumericScalePrecXError  
  
    Dim cnn As New ADODB.Connection  
    Dim cat As New ADOX.Catalog  
    Dim tblOD As ADOX.Table  
    Dim colLoop As ADOX.Column  
  
    ' Connect the catalog.  
    cnn.Open "Provider='Microsoft.Jet.OLEDB.4.0';" & _  
        "data source='Northwind.mdb';"  
    Set cat.ActiveConnection = cnn  
  
    ' Retrieve the Order Details table  
    Set tblOD = cat.Tables("Order Details")  
  
    ' Display numeric scale and precision of  
    ' small integer fields.  
    For Each colLoop In tblOD.Columns  
        If colLoop.Type = adSmallInt Then  
            MsgBox "Column: " & colLoop.Name & vbCr & _  
                "Numeric scale: " & _  
                colLoop.NumericScale & vbCr & _  
                "Precision: " & colLoop.Precision  
        End If  
    Next colLoop  
  
    'Clean up  
    cnn.Close  
    Set cat = Nothing  
    Set cnn = Nothing  
    Exit Sub  
  
NumericScalePrecXError:  
    Set cat = Nothing  
  
    If Not cnn Is Nothing Then  
        If cnn.State = adStateOpen Then cnn.Close  
    End If  
    Set cnn = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
End Sub  
' EndNumericScalePrecVB  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Objeto Column (ADOX)](../../../ado/reference/adox-api/column-object-adox.md)   
 [Propriedade NumericScale (ADOX)](../../../ado/reference/adox-api/numericscale-property-adox.md)   
 [Propriedade Precision (ADOX)](../../../ado/reference/adox-api/precision-property-adox.md)
