---
title: Objeto Catalog (ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Catalog
helpviewer_keywords:
- Catalog object [ADOX]
ms.assetid: bb651639-a488-4e38-b6de-0ed99fa4dd92
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 7cdadbf3db6447f46fefac19d4979c266165905f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66708080"
---
# <a name="catalog-object-adox"></a>Objeto Catalog (ADOX)
Contém coleções ([tabelas](../../../ado/reference/adox-api/tables-collection-adox.md), [exibições](../../../ado/reference/adox-api/views-collection-adox.md), [usuários](../../../ado/reference/adox-api/users-collection-adox.md), [grupos](../../../ado/reference/adox-api/groups-collection-adox.md), e [procedimentos](../../../ado/reference/adox-api/procedures-collection-adox.md)) que Descreva o catálogo de esquema de fonte de dados.  
  
## <a name="remarks"></a>Comentários  
 Você pode modificar os **catálogo** objeto adicionando ou removendo objetos ou modificando objetos existentes. Alguns provedores podem não dar suporte a todos os **catálogo** suporte somente para exibir informações de esquema ou objetos.  
  
 Com as propriedades e métodos de um **catálogo** do objeto, você pode:  
  
-   Abra o catálogo, definindo o [ActiveConnection](../../../ado/reference/adox-api/activeconnection-property-adox.md) propriedade ADO [Conexão](../../../ado/reference/ado-api/connection-object-ado.md) objeto ou uma cadeia de caracteres de conexão válida.  
  
-   Criar um novo catálogo com o [criar](../../../ado/reference/adox-api/create-method-adox.md) método.  
  
-   Determinar os proprietários dos objetos em uma **catálogo** com o [GetObjectOwner](../../../ado/reference/adox-api/getobjectowner-method-adox.md) e [SetObjectOwner](../../../ado/reference/adox-api/setobjectowner-method.md) métodos.  
  
 Esta seção contém o tópico a seguir.  
  
-   [Propriedades, Métodos e Eventos do objeto Catalog](../../../ado/reference/adox-api/catalog-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Consulte também  
 [Exemplo da propriedade ActiveConnection de catálogo (VB)](../../../ado/reference/adox-api/catalog-activeconnection-property-example-vb.md)   
 [Exemplo Command e CommandText propriedades (VB)](../../../ado/reference/adox-api/command-and-commandtext-properties-example-vb.md)   
 [Método Close da Conexão, exemplo da propriedade Table Type (VB)](../../../ado/reference/adox-api/connection-close-method-table-type-property-example-vb.md)   
 [Criar o exemplo do método (VB)](../../../ado/reference/adox-api/create-method-example-vb.md)   
 [Chaves de acrescentar o método, tipo de chave, RelatedColumn, RelatedTable e exemplo das propriedades UpdateRule (VB)](../../../ado/reference/adox-api/keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [Coleção de parâmetros de exemplo da propriedade Command (VB)](../../../ado/reference/adox-api/parameters-collection-command-property-example-vb.md)   
 [Exemplo da propriedade ParentCatalog (VB)](../../../ado/reference/adox-api/parentcatalog-property-example-vb.md)   
 [Append de procedimentos de exemplo do método (VB)](../../../ado/reference/adox-api/procedures-append-method-example-vb.md)   
 [Delete de procedimentos de exemplo do método (VB)](../../../ado/reference/adox-api/procedures-delete-method-example-vb.md)   
 [Procedimentos de atualização de exemplo do método (VB)](../../../ado/reference/adox-api/procedures-refresh-method-example-vb.md)   
 [Modos de exibição e o exemplo de coleções de campos (VB)](../../../ado/reference/adox-api/views-and-fields-collections-example-vb.md)   
 [Append de exibições de exemplo do método (VB)](../../../ado/reference/adox-api/views-append-method-example-vb.md)   
 [Coleção Views, exemplo da propriedade CommandText (VB)](../../../ado/reference/adox-api/views-collection-commandtext-property-example-vb.md)   
 [Modos de exibição excluir exemplo de método (VB)](../../../ado/reference/adox-api/views-delete-method-example-vb.md)   
 [Atualização de exibições de exemplo do método (VB)](../../../ado/reference/adox-api/views-refresh-method-example-vb.md)   
 [Coleção Groups (ADOX)](../../../ado/reference/adox-api/groups-collection-adox.md)   
 [Coleção Procedures (ADOX)](../../../ado/reference/adox-api/procedures-collection-adox.md)   
 [Coleção Tables (ADOX)](../../../ado/reference/adox-api/tables-collection-adox.md)   
 [Coleção Users (ADOX)](../../../ado/reference/adox-api/users-collection-adox.md)   
 [Coleção Views (ADOX)](../../../ado/reference/adox-api/views-collection-adox.md)
