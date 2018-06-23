---
title: Exibir uma coleção de esquema XML armazenada | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-xml
ms.tgt_pltfrm: ''
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
caps.latest.revision: 30
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 164b207ab8191486005491eaf64323fed83aaee6
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36006060"
---
# <a name="view-a-stored-xml-schema-collection"></a>Exibir uma coleção de esquema XML armazenada
  Depois de você importar uma coleção de esquema XML usando [CREATE XML SCHEMA COLLECTION](/sql/t-sql/statements/create-xml-schema-collection-transact-sql), os componentes do esquema são armazenados nos metadados. É possível usar a função intrínseca [xml_schema_namespace](/sql/t-sql/xml/xml-schema-namespace)para reconstruir a coleção de esquemas XML. Essa função retorna um `xml` instância de tipo de dados.  
  
 Por exemplo, a consulta a seguir recupera uma coleção de esquema XML (`ProductDescriptionSchemaCollection`) do esquema relacional de produção no banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] .  
  
```  
SELECT xml_schema_namespace(N'Production',N'ProductDescriptionSchemaCollection')  
GO  
```  
  
 Se você deseja ver apenas um esquema da coleção de esquemas XML, você pode especificar XQuery em relação a `xml` tipo de resultado retornado por `xml_schema_namespace`.  
  
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
  
 Para manter uma cópia idêntica dos esquemas XML, você deve salvar o esquema XML em um arquivo ou em uma tabela do banco de dados em uma coluna de tipo `xml`.  
  
 A exibição de catálogo [sys.xml_schema_collections](/sql/relational-databases/system-catalog-views/sys-xml-schema-collections-transact-sql) também retorna informações sobre coleções de esquemas XML. Essas informações incluem o nome da coleção, a data de criação e o proprietário da coleção.  
  
## <a name="see-also"></a>Consulte também  
 [Coleções de esquemas XML &#40;SQL Server&#41;](xml-schema-collections-sql-server.md)  
  
  
