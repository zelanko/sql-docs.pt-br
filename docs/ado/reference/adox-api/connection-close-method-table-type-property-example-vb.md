---
description: Método Connection Close, Exemplo da propriedade Table Type (VB)
title: Método Connection Close, exemplo da propriedade de tipo Table (VB) | Microsoft Docs
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
- Close method [ADOX], Visual Basic example
- Type property [ADOX], Visual Basic example
ms.assetid: f88e7a3b-19ed-46e2-b2ce-3b611d9b8166
author: rothja
ms.author: jroth
ms.openlocfilehash: acd8183389276b47502b7ef14978eac855c74743
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88984879"
---
# <a name="connection-close-method-table-type-property-example-vb"></a>Método Connection Close, Exemplo da propriedade Table Type (VB)
Definir a propriedade [ActiveConnection](./activeconnection-property-adox.md) como **Nothing** deve fechar a conexão com o catálogo. As coleções associadas estarão vazias. Todos os objetos que foram criados a partir de objetos de esquema no catálogo ficarão órfãos. Todas as propriedades nesses objetos que foram armazenados em cache ainda estarão disponíveis, mas uma tentativa de ler propriedades que exigem uma chamada para o provedor falhará.  
  
```  
' BeginCloseConnectionVB  
Sub Main()  
    On Error GoTo CloseConnectionByNothingError  
  
    Dim cnn As New ADODB.Connection  
    Dim cat As New ADOX.Catalog  
    Dim tbl As ADOX.Table  
  
    cnn.Open "Provider='Microsoft.Jet.OLEDB.4.0';" & _  
        "Data Source= 'Northwind.mdb';"  
    Set cat.ActiveConnection = cnn  
    Set tbl = cat.Tables(0)  
    Debug.Print tbl.Type    ' Cache tbl.Type info  
    Set cat.ActiveConnection = Nothing  
    Debug.Print tbl.Type    ' tbl is orphaned  
    ' Previous line will succeed if this info was cached.  
    Debug.Print tbl.Columns(0).DefinedSize  
    ' Previous line will fail if this info has not been cached.  
  
    'Clean up.  
    cnn.Close  
    Set cat = Nothing  
    Set cnn = Nothing  
    Exit Sub  
  
CloseConnectionByNothingError:  
    Set cat = Nothing  
  
    If Not cnn Is Nothing Then  
        If cnn.State = adStateOpen Then cnn.Close  
    End If  
    Set cnn = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
End Sub  
' EndCloseConnectionVB  
```  
  
 Fechar um objeto de [conexão](../ado-api/connection-object-ado.md) que foi usado para abrir o catálogo deve ter o mesmo efeito que definir a propriedade **ActiveConnection** como **Nothing**.  
  
```  
Attribute VB_Name = "Connection"  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Propriedade ActiveConnection (ADOX)](./activeconnection-property-adox.md)   
 [Objeto de catálogo (ADOX)](./catalog-object-adox.md)   
 [Objeto Column (ADOX)](./column-object-adox.md)   
 [Coleção Columns (ADOX)](./columns-collection-adox.md)   
 [Objeto Table (ADOX)](./table-object-adox.md)   
 [Coleção Tables (ADOX)](./tables-collection-adox.md)   
 [Propriedade Type (Table) (ADOX)](./type-property-table-adox.md)