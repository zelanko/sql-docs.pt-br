---
description: Exemplo da propriedade ActiveConnection de catálogo (VB)
title: Exemplo da propriedade ActiveConnection do catálogo (VB) | Microsoft Docs
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
- ActiveConnection property [ADOX], Visual Basic example
ms.assetid: bb3274b1-764d-43a7-a49f-ef55680ecd26
author: rothja
ms.author: jroth
ms.openlocfilehash: 582c558222bec95914e73902b69fe9c7ce46161e
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88985231"
---
# <a name="catalog-activeconnection-property-example-vb"></a>Exemplo da propriedade ActiveConnection de catálogo (VB)
Definir a propriedade [ActiveConnection](./activeconnection-property-adox.md) como uma conexão "abrir" válida abre "o catálogo. Em um catálogo aberto, você pode acessar os objetos de esquema contidos nesse catálogo.  
  
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
  
 Definir a propriedade **ActiveConnection** como uma cadeia de conexão válida também "abre" o catálogo.  
  
```  
Attribute VB_Name = "Catalog"  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Propriedade ActiveConnection (ADOX)](./activeconnection-property-adox.md)   
 [Objeto de catálogo (ADOX)](./catalog-object-adox.md)   
 [Objeto Table (ADOX)](./table-object-adox.md)   
 [Coleção Tables (ADOX)](./tables-collection-adox.md)   
 [Propriedade Type (Table) (ADOX)](./type-property-table-adox.md)