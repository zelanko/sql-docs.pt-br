---
title: 'Especificando o atributo SQL: inverso em SQL: relationship (SQLXML 4,0) | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 5b0781102371b98cced72a5a0edee70c9567c372
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85003069"
---
# <a name="specifying-the-sqlinverse-attribute-on-sqlrelationship-sqlxml-40"></a>Especificando o atributo sql:inverse em sql:relationship (SQLXML 4.0)
  O atributo `sql:inverse` só é útil quando o esquema XSD é usado no carregamento em massa ou por um diagrama de atualização. O `sql:inverse` atributo pode ser especificado no **\<sql:relationship>** elemento. Em diagramas de atualização, a lógica do diagrama de atualização interpreta o esquema ao determinar as tabelas e as colunas atualizadas pela operação do diagrama. As relações de pai/filho especificadas no esquema determinam a ordem na qual os registros são modificados (inseridos ou excluídos).  
  
 Se você tiver um esquema XSD no qual a relação pai/filho é especificada na ordem inversa da relação chave primária/chave estrangeira entre as colunas de banco de dados correspondentes, a operação do diagrama de atualização de inserção ou exclusão falhará por conta da violação da chave primária/chave estrangeira. Nesses casos, o `sql:inverse` atributo é especificado ( `sql:inverse="true"` ) no **\<sql:relationship>** elemento e a lógica updategram inversa sua interpretação da relação pai-filho especificada no esquema.  
  
 O atributo `sql:inverse` usa um valor booliano (0=false, 1=true). Os valores aceitáveis são 0, 1, true e false.  
  
 Para obter um exemplo funcional usando a `sql:inverse` anotação, consulte [especificando um esquema de mapeamento anotado em um updategram](../sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/specifying-an-annotated-mapping-schema-in-an-updategram-sqlxml-4-0.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Especificando relações usando SQL: relationship &#40;SQLXML 4,0&#41;](specifying-relationships-using-sql-relationship-sqlxml-4-0.md)  
  
  
