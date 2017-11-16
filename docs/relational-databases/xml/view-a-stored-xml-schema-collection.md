---
title: "Exibir uma coleção de esquema XML armazenada | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: dbe-xml
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- schema collections [SQL Server], viewing
- XML schemas [SQL Server], viewing
- CREATE XML SCHEMA COLLECTION statement
- xml_schema_namespace function
- XML schema collections [SQL Server], viewing
- displaying XML schema collections
- viewing XML schema collections
ms.assetid: e38031af-22df-4cd9-a14e-e316b822f91b
caps.latest.revision: "30"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 4c460246b6849a83ac096c8f37c001f2d9a1e83f
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="view-a-stored-xml-schema-collection"></a>Exibir uma coleção de esquema XML armazenada
  Depois de você importar uma coleção de esquema XML usando [CREATE XML SCHEMA COLLECTION](../../t-sql/statements/create-xml-schema-collection-transact-sql.md), os componentes do esquema são armazenados nos metadados. É possível usar a função intrínseca [xml_schema_namespace](../../t-sql/xml/xml-schema-namespace.md)para reconstruir a coleção de esquemas XML. Essa função retorna uma instância de tipo de dados **xml** .  
  
 Por exemplo, a consulta a seguir recupera uma coleção de esquema XML (`ProductDescriptionSchemaCollection`) do esquema relacional de produção no banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] .  
  
```  
SELECT xml_schema_namespace(N'Production',N'ProductDescriptionSchemaCollection')  
GO  
```  
  
 Se desejar ver apenas um esquema da coleção de esquemas XML, será possível especificar XQuery em relação ao resultado do tipo **xml** que é retornado pelo `xml_schema_namespace`.  
  
```  
SELECT xml_schema_namespace(N'RelationalSchemaName',N'XmlSchemaCollectionName').query('  
/xs:schema[@targetNamespace="TargetNameSpace"]  
')  
GO  
```  
  
 Por exemplo, a consulta a seguir recupera informações do esquema XML sobre garantia e manutenção do produto da coleção de esquema XML `ProductDescriptionSchemaCollection` .  
  
```  
SELECT xml_schema_namespace(N'Production',N'ProductDescriptionSchemaCollection').query('  
/xs:schema[@targetNamespace="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain"]  
')  
GO  
```  
  
 Também é possível passar o namespace opcional de destino como o terceiro parâmetro para a função `xml_schema_namespace` para recuperar esquema específico da coleção, conforme mostrado na consulta a seguir:  
  
```  
SELECT xml_schema_namespace(N'Production',N'ProductDescriptionSchemaCollection', N'http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain')  
GO  
```  
  
 Quando você cria uma coleção de esquema XML usando CREATE XML SCHEMA COLLECTION no banco de dados, a instrução armazena os componentes do esquema nos metadados. Observe que apenas os componentes de esquema que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] entende são armazenados. Todos os comentários, anotações ou atributos não XSD não são armazenados. Portanto o esquema reconstruído pelo **xml_schema_namespace** é funcionalmente equivalente ao esquema original, mas não necessariamente terá a mesma aparência. Por exemplo, você não verá os mesmos prefixos que existiam no esquema original. O esquema retornado pelo **xml_schema_namespace** usa **t** como o prefixo do namespace de destino e **ns1**, **ns2**e assim por diante, para outros namespaces.  
  
 Para manter uma cópia idêntica dos esquemas XML, é necessário salvar o esquema XML em um arquivo ou em uma tabela do banco de dados em uma coluna de tipo **xml** .  
  
 A exibição de catálogo [sys.xml_schema_collections](../../relational-databases/system-catalog-views/sys-xml-schema-collections-transact-sql.md) também retorna informações sobre coleções de esquemas XML. Essas informações incluem o nome da coleção, a data de criação e o proprietário da coleção.  
  
## <a name="see-also"></a>Consulte também  
 [Coleções de esquemas XML &#40;SQL Server&#41;](../../relational-databases/xml/xml-schema-collections-sql-server.md)  
  
  
