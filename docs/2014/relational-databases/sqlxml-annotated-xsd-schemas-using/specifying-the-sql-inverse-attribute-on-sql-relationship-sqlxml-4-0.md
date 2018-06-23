---
title: 'Especificando o atributo SQL: Inverse em SQL: Relationship (SQLXML 4.0) | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
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
caps.latest.revision: 26
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 66cbeee228a5f186317eb69d4b0dad899c9c1252
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36118291"
---
# <a name="specifying-the-sqlinverse-attribute-on-sqlrelationship-sqlxml-40"></a>Especificando o atributo sql:inverse em sql:relationship (SQLXML 4.0)
  O atributo `sql:inverse` só é útil quando o esquema XSD é usado no carregamento em massa ou por um diagrama de atualização. O `sql:inverse` atributo pode ser especificado no  **\<SQL: Relationship >** elemento. Em diagramas de atualização, a lógica do diagrama de atualização interpreta o esquema ao determinar as tabelas e as colunas atualizadas pela operação do diagrama. As relações de pai/filho especificadas no esquema determinam a ordem na qual os registros são modificados (inseridos ou excluídos).  
  
 Se você tiver um esquema XSD no qual a relação pai/filho é especificada na ordem inversa da relação chave primária/chave estrangeira entre as colunas de banco de dados correspondentes, a operação do diagrama de atualização de inserção ou exclusão falhará por conta da violação da chave primária/chave estrangeira. Nesses casos, o `sql:inverse` atributo for especificado (`sql:inverse="true"`) no  **\<SQL: Relationship >** elemento e a inverso uma lógica do diagrama de atualização sua interpretação da relação pai-filho especificada no esquema.  
  
 O atributo `sql:inverse` usa um valor booliano (0=false, 1=true). Os valores aceitáveis são 0, 1, true e false.  
  
 Para um exemplo funcional usando a `sql:inverse` anotação, consulte [especificando um esquema de mapeamento anotado em um diagrama de atualização](../sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/specifying-an-annotated-mapping-schema-in-an-updategram-sqlxml-4-0.md).  
  
## <a name="see-also"></a>Consulte também  
 [Especificando relações usando SQL: Relationship &#40;SQLXML 4.0&#41;](specifying-relationships-using-sql-relationship-sqlxml-4-0.md)  
  
  