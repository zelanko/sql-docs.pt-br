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
ms.openlocfilehash: 35fa08ba0d93a7adacf6d58338f4808e2a5eba9e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88440378"
---
# <a name="catalog-object-adox"></a>Objeto Catalog (ADOX)
Contém coleções ([tabelas](../../../ado/reference/adox-api/tables-collection-adox.md), [exibições](../../../ado/reference/adox-api/views-collection-adox.md), [usuários](../../../ado/reference/adox-api/users-collection-adox.md), [grupos](../../../ado/reference/adox-api/groups-collection-adox.md)e [procedimentos](../../../ado/reference/adox-api/procedures-collection-adox.md)) que descrevem o catálogo de esquema de uma fonte de dados.  
  
## <a name="remarks"></a>Comentários  
 Você pode modificar o objeto de **Catálogo** adicionando ou removendo objetos ou modificando objetos existentes. Alguns provedores podem não dar suporte a todos os objetos de **Catálogo** ou podem dar suporte apenas à exibição de informações de esquema.  
  
 Com as propriedades e métodos de um objeto de **Catálogo** , você pode:  
  
-   Abra o catálogo definindo a propriedade [ActiveConnection](../../../ado/reference/adox-api/activeconnection-property-adox.md) como um objeto de [conexão](../../../ado/reference/ado-api/connection-object-ado.md) ADO ou uma cadeia de conexão válida.  
  
-   Crie um novo catálogo com o método [Create](../../../ado/reference/adox-api/create-method-adox.md) .  
  
-   Determine os proprietários dos objetos em um **Catálogo** com os métodos [GetObjectOwner](../../../ado/reference/adox-api/getobjectowner-method-adox.md) e [SetObjectOwner](../../../ado/reference/adox-api/setobjectowner-method.md) .  
  
 Esta seção contém o tópico a seguir.  
  
-   [Propriedades, Métodos e Eventos do objeto Catalog](../../../ado/reference/adox-api/catalog-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo da propriedade ActiveConnection do catálogo (VB)](../../../ado/reference/adox-api/catalog-activeconnection-property-example-vb.md)   
 [Exemplo das propriedades Command e CommandText (VB)](../../../ado/reference/adox-api/command-and-commandtext-properties-example-vb.md)   
 [Método Connection Close, exemplo da propriedade de tipo Table (VB)](../../../ado/reference/adox-api/connection-close-method-table-type-property-example-vb.md)   
 [Exemplo do método Create (VB)](../../../ado/reference/adox-api/create-method-example-vb.md)   
 [Exemplo das propriedades método, tipo de chave, RelatedColumn, RELATEDTABLE e UpdateRule da tecla Append (VB)](../../../ado/reference/adox-api/keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [Coleção Parameters, exemplo da Propriedade Command (VB)](../../../ado/reference/adox-api/parameters-collection-command-property-example-vb.md)   
 [Exemplo da propriedade ParentCatalog (VB)](../../../ado/reference/adox-api/parentcatalog-property-example-vb.md)   
 [Exemplo do método Append Procedures (VB)](../../../ado/reference/adox-api/procedures-append-method-example-vb.md)   
 [Exemplo do método Delete de procedimentos (VB)](../../../ado/reference/adox-api/procedures-delete-method-example-vb.md)   
 [Exemplo do método Refresh de procedimentos (VB)](../../../ado/reference/adox-api/procedures-refresh-method-example-vb.md)   
 [Exemplo de coleções de exibições e campos (VB)](../../../ado/reference/adox-api/views-and-fields-collections-example-vb.md)   
 [Exemplo do método Append views (VB)](../../../ado/reference/adox-api/views-append-method-example-vb.md)   
 [Coleção views, exemplo da propriedade CommandText (VB)](../../../ado/reference/adox-api/views-collection-commandtext-property-example-vb.md)   
 [Exemplo do método Delete de views (VB)](../../../ado/reference/adox-api/views-delete-method-example-vb.md)   
 [Exemplo do método Refresh de exibições (VB)](../../../ado/reference/adox-api/views-refresh-method-example-vb.md)   
 [Coleção groups (ADOX)](../../../ado/reference/adox-api/groups-collection-adox.md)   
 [Coleção de procedimentos (ADOX)](../../../ado/reference/adox-api/procedures-collection-adox.md)   
 [Coleção Tables (ADOX)](../../../ado/reference/adox-api/tables-collection-adox.md)   
 [Coleção Users (ADOX)](../../../ado/reference/adox-api/users-collection-adox.md)   
 [Coleção Views (ADOX)](../../../ado/reference/adox-api/views-collection-adox.md)
