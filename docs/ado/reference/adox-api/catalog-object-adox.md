---
description: Objeto Catalog (ADOX)
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 968142adb0cb633a19a574c2d0994360faa3fadb
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88771195"
---
# <a name="catalog-object-adox"></a>Objeto Catalog (ADOX)
Contém coleções ([tabelas](./tables-collection-adox.md), [exibições](./views-collection-adox.md), [usuários](./users-collection-adox.md), [grupos](./groups-collection-adox.md)e [procedimentos](./procedures-collection-adox.md)) que descrevem o catálogo de esquema de uma fonte de dados.  
  
## <a name="remarks"></a>Comentários  
 Você pode modificar o objeto de **Catálogo** adicionando ou removendo objetos ou modificando objetos existentes. Alguns provedores podem não dar suporte a todos os objetos de **Catálogo** ou podem dar suporte apenas à exibição de informações de esquema.  
  
 Com as propriedades e métodos de um objeto de **Catálogo** , você pode:  
  
-   Abra o catálogo definindo a propriedade [ActiveConnection](./activeconnection-property-adox.md) como um objeto de [conexão](../ado-api/connection-object-ado.md) ADO ou uma cadeia de conexão válida.  
  
-   Crie um novo catálogo com o método [Create](./create-method-adox.md) .  
  
-   Determine os proprietários dos objetos em um **Catálogo** com os métodos [GetObjectOwner](./getobjectowner-method-adox.md) e [SetObjectOwner](./setobjectowner-method.md) .  
  
 Esta seção contém o tópico a seguir.  
  
-   [Propriedades, Métodos e Eventos do objeto Catalog](./catalog-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo da propriedade ActiveConnection do catálogo (VB)](./catalog-activeconnection-property-example-vb.md)   
 [Exemplo das propriedades Command e CommandText (VB)](./command-and-commandtext-properties-example-vb.md)   
 [Método Connection Close, exemplo da propriedade de tipo Table (VB)](./connection-close-method-table-type-property-example-vb.md)   
 [Exemplo do método Create (VB)](./create-method-example-vb.md)   
 [Exemplo das propriedades método, tipo de chave, RelatedColumn, RELATEDTABLE e UpdateRule da tecla Append (VB)](./keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [Coleção Parameters, exemplo da Propriedade Command (VB)](./parameters-collection-command-property-example-vb.md)   
 [Exemplo da propriedade ParentCatalog (VB)](./parentcatalog-property-example-vb.md)   
 [Exemplo do método Append Procedures (VB)](./procedures-append-method-example-vb.md)   
 [Exemplo do método Delete de procedimentos (VB)](./procedures-delete-method-example-vb.md)   
 [Exemplo do método Refresh de procedimentos (VB)](./procedures-refresh-method-example-vb.md)   
 [Exemplo de coleções de exibições e campos (VB)](./views-and-fields-collections-example-vb.md)   
 [Exemplo do método Append views (VB)](./views-append-method-example-vb.md)   
 [Coleção views, exemplo da propriedade CommandText (VB)](./views-collection-commandtext-property-example-vb.md)   
 [Exemplo do método Delete de views (VB)](./views-delete-method-example-vb.md)   
 [Exemplo do método Refresh de exibições (VB)](./views-refresh-method-example-vb.md)   
 [Coleção groups (ADOX)](./groups-collection-adox.md)   
 [Coleção de procedimentos (ADOX)](./procedures-collection-adox.md)   
 [Coleção Tables (ADOX)](./tables-collection-adox.md)   
 [Coleção Users (ADOX)](./users-collection-adox.md)   
 [Coleção Views (ADOX)](./views-collection-adox.md)