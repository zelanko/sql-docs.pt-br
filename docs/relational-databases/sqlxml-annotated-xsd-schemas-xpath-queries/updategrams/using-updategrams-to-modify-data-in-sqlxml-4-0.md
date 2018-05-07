---
title: Usando diagramas de atualização para modificar dados no SQLXML 4.0 | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: sqlxml
ms.reviewer: ''
ms.suite: sql
ms.technology: xml
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SQLXML, updategrams
- data insertions [SQLXML]
- data deletions [SQLXML]
- updating data [SQLXML]
- modifying data [SQLXML]
- OPENXML function
- updategrams [SQLXML]
- database modifications [SQLXML]
- data updates [SQLXML]
- modifying databases
- data modifications [SQLXML]
- deleting data
- inserting data
ms.assetid: b8b3b892-cb73-41d0-b945-bce148d81d9b
caps.latest.revision: 26
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 09ddba31de38f515cf6810d455d4d2264fb6ab97
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="using-updategrams-to-modify-data-in-sqlxml-40"></a>Usando diagramas de atualização para modificar dados no SQLXML 4.0
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Você pode modificar (Inserir, atualizar ou excluir) um banco de dados [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] de um existente documento XML usando um diagrama de atualização ou o OPENXML [!INCLUDE[tsql](../../../includes/tsql-md.md)] função.  
  
 Esta seção fornece informações sobre diagramas de atualização e exemplos de uso.  
  
## <a name="in-this-section"></a>Nesta seção  
 [Introdução aos diagramas de atualização &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/introduction-to-updategrams-sqlxml-4-0.md)  
 Fornece informações e exemplos básicos de diagramas de atualização.  
  
 [Especificando um esquema de mapeamento anotado em um diagrama de atualização &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/specifying-an-annotated-mapping-schema-in-an-updategram-sqlxml-4-0.md)  
 Explica e fornece exemplos de esquemas de mapeamento anotados em diagramas de atualização.  
  
 [Tratamento de nulos &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/null-handling-sqlxml-4-0.md)  
 Descreve como especificar NULL para valores de elemento e atributo.  
  
 [Inserindo dados usando diagramas de atualização XML &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/inserting-data-using-xml-updategrams-sqlxml-4-0.md)  
 Descreve e fornece exemplos de uso de diagramas de atualização para inserir dados.  
  
 [Excluindo dados usando diagramas de atualização XML &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/deleting-data-using-xml-updategrams-sqlxml-4-0.md)  
 Descreve e fornece exemplos de uso de diagramas de atualização para excluir dados.  
  
 [Atualizando dados usando diagramas de atualização XML &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/updating-data-using-xml-updategrams-sqlxml-4-0.md)  
 Descreve e fornece exemplos de uso de diagramas de atualização para modificar os dados existentes.  
  
 [Passando parâmetros para diagramas de atualização &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/passing-parameters-to-updategrams-sqlxml-4-0.md)  
 Descreve e fornece exemplos de passagem de parâmetros para diagramas de atualização.  
  
 [Tratamento de problemas de simultaneidade de banco de dados em diagramas de atualização &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/handling-database-concurrency-issues-in-updategrams-sqlxml-4-0.md)  
 Descreve os vários níveis de proteção possíveis para tratar assuntos de simultaneidade em diagramas de atualização e fornece exemplos.  
  
 [Aplicativos de exemplo de diagrama de atualização &#40;SQLXML 4.0&#41;](http://msdn.microsoft.com/library/d2287e10-4007-4ba4-ad84-4e2b6adfede5)  
 Fornece exemplos de aplicativos que usam diagramas de atualização.  
  
 [Diretrizes e limitações dos diagramas de atualização XML &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/guidelines-and-limitations-of-xml-updategrams-sqlxml-4-0.md)  
 Lista alguns lembretes para trabalhar com diagramas de atualização.  
  
  
