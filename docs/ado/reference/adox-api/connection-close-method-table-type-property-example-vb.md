---
title: Conexão feche o método, o exemplo de propriedade de tipo de tabela (VB) | Microsoft Docs
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
dev_langs:
- VB
helpviewer_keywords:
- Close method [ADOX], Visual Basic example
- Type property [ADOX], Visual Basic example
ms.assetid: f88e7a3b-19ed-46e2-b2ce-3b611d9b8166
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 69019c3a7cc9af1d841ea5fbb27be5180fd2c95e
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/18/2018
---
# <a name="connection-close-method-table-type-property-example-vb"></a>Método Close da Conexão, exemplo de propriedade de tipo de tabela (VB)
Definindo o [ActiveConnection](../../../ado/reference/adox-api/activeconnection-property-adox.md) propriedade **nada** deve fechar a conexão para o catálogo. Coleções associadas estará vazias. Todos os objetos que foram criados a partir de objetos de esquema no catálogo serão órfão. As propriedades desses objetos que tiverem sido armazenados em cache ainda estará disponíveis, mas uma tentativa de ler as propriedades que requer uma chamada para o provedor irá falhar.  
  
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
  
 Fechando uma [Conexão](../../../ado/reference/ado-api/connection-object-ado.md) o objeto que foi usado para abrir o catálogo deve ter o mesmo efeito que definir a **ActiveConnection** propriedade **nada**.  
  
```  
Attribute VB_Name = "Connection"  
```  
  
## <a name="see-also"></a>Consulte também  
 [Propriedade ActiveConnection (ADOX)](../../../ado/reference/adox-api/activeconnection-property-adox.md)   
 [Objeto de catálogo (ADOX)](../../../ado/reference/adox-api/catalog-object-adox.md)   
 [Objeto de coluna (ADOX)](../../../ado/reference/adox-api/column-object-adox.md)   
 [Coleção de colunas (ADOX)](../../../ado/reference/adox-api/columns-collection-adox.md)   
 [Objeto de tabela (ADOX)](../../../ado/reference/adox-api/table-object-adox.md)   
 [Coleção de tabelas (ADOX)](../../../ado/reference/adox-api/tables-collection-adox.md)   
 [Propriedade Type (Table) (ADOX)](../../../ado/reference/adox-api/type-property-table-adox.md)
