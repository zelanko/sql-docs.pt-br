---
description: Exemplo da propriedade Clustered (VB)
title: Exemplo da propriedade Clustered (VB) | Microsoft Docs
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
- Clustered property [ADOX], Visual Basic example
ms.assetid: 1cd30769-c8af-43e7-be27-12ed0434daa1
author: rothja
ms.author: jroth
ms.openlocfilehash: c8e0d1b03b4aa56d0db19d1d692f459bc7d9f613
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88985177"
---
# <a name="clustered-property-example-vb"></a>Exemplo da propriedade Clustered (VB)
Este exemplo demonstra a propriedade [clusterizada](./clustered-property-adox.md) de um [índice](./index-object-adox.md). Observe que os bancos de dados do Microsoft Jet não dão suporte a índices clusterizados, portanto, este exemplo retornará **false** para a propriedade **clusterizada** de todos os índices no banco de dados **Northwind** .  
  
```  
' BeginClusteredVB  
Sub Main()  
    On Error GoTo ClusteredXError  
  
    Dim cnn As New ADODB.Connection  
    Dim cat As New ADOX.Catalog  
    Dim tblLoop As ADOX.Table  
    Dim idxLoop As ADOX.Index  
    Dim strCnn As String  
  
    strCnn = "Provider='SQLOLEDB';Data Source='MySqlServer';Initial Catalog='pubs';" & _  
        "Integrated Security='SSPI';"  
    ' Connect to the catalog.  
    cnn.Open strCnn  
    cat.ActiveConnection = cnn  
  
    ' Enumerate the tables.  
    For Each tblLoop In cat.Tables  
        'Enumerate the indexes.  
        For Each idxLoop In tblLoop.Indexes  
            Debug.Print tblLoop.Name & " " & _  
                idxLoop.Name & " " & idxLoop.Clustered  
        Next idxLoop  
    Next tblLoop  
  
    'Clean up.  
    cnn.Close  
    Set cat = Nothing  
    Set cnn = Nothing  
    Exit Sub  
  
ClusteredXError:  
  
    Set cat = Nothing  
  
    If Not cnn Is Nothing Then  
        If cnn.State = adStateOpen Then cnn.Close  
    End If  
    Set cnn = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
End Sub  
' EndClusteredVB  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Objeto de catálogo (ADOX)](./catalog-object-adox.md)   
 [Propriedade Clustered (ADOX)](./clustered-property-adox.md)   
 [Objeto Index (ADOX)](./index-object-adox.md)   
 [Objeto Table (ADOX)](./table-object-adox.md)