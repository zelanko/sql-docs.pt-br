---
title: table_types (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e9c55e83d67fcd5817575b0b045bb680b0269217
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="systabletypes-transact-sql"></a>sys.table_types (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Exibe propriedades de tipos de tabela definidos pelo usuário no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Um tipo de tabela é um tipo do qual é possível declarar variáveis de tabela ou parâmetros com valor de tabela. Cada tipo de tabela tem um **type_table_object_id** que é uma chave estrangeira para a [sys. Objects](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md) exibição do catálogo. Você pode usar essa coluna de ID para consultar várias exibições do catálogo, de forma semelhante a um **object_id** coluna de uma tabela comum, para descobrir a estrutura do tipo de tabela como suas colunas e restrições.    
 
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|*\<herdado colunas >*||Para obter uma lista de colunas que essa exibição herda valores, consulte [Types &#40; Transact-SQL &#41; ](../../relational-databases/system-catalog-views/sys-types-transact-sql.md).|  
|**type_table_object_id**|**int**|Número de identificação do objeto. Esse número é exclusivo de um banco de dados.|  
|**is_memory_optimized**|**bit**|**Aplica-se a**: do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> O valores possíveis são os seguintes:<br /><br /> 0 = não é otimizado em memória<br /><br /> 1 = é otimizado em memória<br /><br /> Um valor de 0 é o valor padrão.<br /><br /> Os tipos de tabela sempre são criados com DURABILITY = SCHEMA_ONLY. Somente o esquema é mantido em disco.|  
  
## <a name="permissions"></a>Permissões  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte também  
 [Exibições de catálogo de objeto &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [Usar com valor de tabela parâmetros &#40; mecanismo de banco de dados &#41;](../../relational-databases/tables/use-table-valued-parameters-database-engine.md)   
 [OLTP in-memory &#40;Otimização na memória&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  
