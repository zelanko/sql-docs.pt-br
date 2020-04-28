---
title: sys. table_types (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- table_types_TSQL
- sys.table_types
- sys.table_types_TSQL
- table_types
dev_langs:
- TSQL
helpviewer_keywords:
- table types [SQL Server]
- table-valued parameters, sys.table_types
- sys.table_types
- UDTT
ms.assetid: c05fd873-aff2-4a89-9936-a54c2ea09996
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: bc4e77bd978432bf6e1e11930c121e0e7fc6b6ea
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "73982106"
---
# <a name="systable_types-transact-sql"></a>sys.table_types (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Exibe propriedades de tipos de tabela definidos pelo usuário no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Um tipo de tabela é um tipo do qual é possível declarar variáveis de tabela ou parâmetros com valor de tabela. Cada tipo de tabela tem um **type_table_object_id** que é uma chave estrangeira na exibição do catálogo [Sys. Objects](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md) . Você pode usar essa coluna de ID para consultar várias exibições de catálogo, de forma semelhante a uma coluna de **object_id** de uma tabela normal, para descobrir a estrutura do tipo de tabela, como suas colunas e restrições.    
 
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|*\<colunas herdadas>*||Para obter uma lista de colunas que essa exibição herda, consulte [Sys. types &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-types-transact-sql.md).|  
|**type_table_object_id**|**int**|Número de identificação do objeto. Esse número é exclusivo de um banco de dados.|  
|**is_memory_optimized**|**bit**|**Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior.<br /><br /> O valores possíveis são os seguintes:<br /><br /> 0 = não é otimizado em memória<br /><br /> 1 = é otimizado em memória<br /><br /> Um valor de 0 é o valor padrão.<br /><br /> Os tipos de tabela sempre são criados com DURABILITY = SCHEMA_ONLY. Somente o esquema é mantido em disco.|  
  
## <a name="permissions"></a>Permissões  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições de catálogo de objetos &#40;&#41;Transact-SQL](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [Usar parâmetros com valor de tabela &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/tables/use-table-valued-parameters-database-engine.md)   
 [OLTP in-memory &#40;Otimização na memória&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  
