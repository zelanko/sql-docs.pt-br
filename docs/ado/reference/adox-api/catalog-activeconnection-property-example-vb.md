---
title: "Catálogo de exemplo da propriedade ActiveConnection (VB) | Microsoft Docs"
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
helpviewer_keywords: ActiveConnection property [ADOX], Visual Basic example
ms.assetid: bb3274b1-764d-43a7-a49f-ef55680ecd26
caps.latest.revision: "9"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 8122300ca528db3e775d306ab43bff72654e7a12
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="catalog-activeconnection-property-example-vb"></a>Exemplo de propriedade ActiveConnection do catálogo (VB)
Definindo o [ActiveConnection](../../../ado/reference/adox-api/activeconnection-property-adox.md) o catálogo de propriedade para uma conexão válida, abra "abre". De um catálogo aberto, você pode acessar os objetos do esquema contidos no catálogo.  
  
```  
' BeginOpenConnectionVB  
Sub Main()  
    On Error GoTo OpenConnectionError  
  
    Dim cnn As New ADODB.Connection  
    Dim cat As New ADOX.Catalog  
  
    cnn.Open "Provider='Microsoft.Jet.OLEDB.4.0';" & _  
        "Data Source= 'Northwind.mdb';"  
    Set cat.ActiveConnection = cnn  
    Debug.Print cat.Tables(0).Type  
  
    'Clean up  
    cnn.Close  
    Set cat = Nothing  
    Set cnn = Nothing  
    Exit Sub  
  
OpenConnectionError:  
  
    Set cat = Nothing  
  
    If Not cnn Is Nothing Then  
        If cnn.State = adStateOpen Then cnn.Close  
    End If  
    Set cnn = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
End Sub  
' EndOpenConnectionVB  
```  
  
 Definindo o **ActiveConnection** propriedade como uma cadeia de caracteres de conexão válido também "abre" o catálogo.  
  
```  
Attribute VB_Name = "Catalog"  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Propriedade ActiveConnection (ADOX)](../../../ado/reference/adox-api/activeconnection-property-adox.md)   
 [Objeto de catálogo (ADOX)](../../../ado/reference/adox-api/catalog-object-adox.md)   
 [Objeto de tabela (ADOX)](../../../ado/reference/adox-api/table-object-adox.md)   
 [Coleção de tabelas (ADOX)](../../../ado/reference/adox-api/tables-collection-adox.md)   
 [Propriedade Type (Table) (ADOX)](../../../ado/reference/adox-api/type-property-table-adox.md)
