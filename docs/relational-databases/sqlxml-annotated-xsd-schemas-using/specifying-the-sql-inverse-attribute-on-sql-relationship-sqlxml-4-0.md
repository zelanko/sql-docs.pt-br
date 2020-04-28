---
title: 'Definir SQL: atributo inverso em SQL: relationship (SQLXML)'
description: 'Saiba como usar o atributo SQL: inverso no elemento SQL: relationship para especificar relações entre colunas de banco de dados em uma operação updategram.'
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- sql:relationship
- bulk load [SQLXML]
- inverse attribute
- relationships [SQLXML], inverse orders
- relationship annotation
- XSD schemas [SQLXML], relationships
- annotated XSD schemas, relationships
- updategrams [SQLXML], relationships
- sql:inverse
ms.assetid: 08904cbd-9c86-493d-90c3-f5e1d13ce59d
author: MightyPen
ms.author: genemi
ms.reviewer: ''
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: fe5409120a3d0c5df3cf05318b0b85fd22d07bdf
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81388090"
---
# <a name="specifying-the-sqlinverse-attribute-on-sqlrelationship-sqlxml-40"></a>Especificando o atributo sql:inverse em sql:relationship (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  O atributo **SQL: inverso** é útil somente quando o esquema XSD é usado para o carregamento em massa ou por um updategram. O atributo **SQL: inverso** pode ser especificado no elemento ** \<SQL: relationship>** . Em diagramas de atualização, a lógica do diagrama de atualização interpreta o esquema ao determinar as tabelas e as colunas atualizadas pela operação do diagrama. As relações de pai/filho especificadas no esquema determinam a ordem na qual os registros são modificados (inseridos ou excluídos).  
  
 Se você tiver um esquema XSD no qual a relação pai/filho é especificada na ordem inversa da relação chave primária/chave estrangeira entre as colunas de banco de dados correspondentes, a operação do diagrama de atualização de inserção ou exclusão falhará por conta da violação da chave primária/chave estrangeira. Nesses casos, o atributo **SQL: inverso** é especificado (**SQL: inverso = "true"**) no elemento ** \<SQL: relationship>** e a lógica updategram inversa sua interpretação da relação pai-filho especificada no esquema.  
  
 O atributo **SQL: inverso** usa um valor booliano (0 = false, 1 = true). Os valores aceitáveis são 0, 1, true e false.  
  
 Para obter um exemplo funcional usando a anotação **SQL: inverso** , consulte [especificando um esquema de mapeamento anotado em um updategram](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/specifying-an-annotated-mapping-schema-in-an-updategram-sqlxml-4-0.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Especificando relações usando SQL: relationship &#40;SQLXML 4,0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/specifying-relationships-using-sql-relationship-sqlxml-4-0.md)  
  
  
