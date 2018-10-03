---
title: sys.dm_exec_cached_plan_dependent_objects (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_exec_cached_plan_dependent_objects
- dm_exec_cached_plan_dependent_objects_TSQL
- sys.dm_exec_cached_plan_dependent_objects_TSQL
- dm_exec_cached_plan_dependent_objects
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_cached_plan_dependent_objects dynamic management function
ms.assetid: 9b6cf5f7-b267-44fb-aac8-f49c9aa10cc1
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 1efc815873a3018f8f8350e2bf24440ca0204fa9
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47733758"
---
# <a name="sysdmexeccachedplandependentobjects-transact-sql"></a>sys.dm_exec_cached_plan_dependent_objects (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Retorna uma linha para cada plano de execução [!INCLUDE[tsql](../../includes/tsql-md.md)], plano de execução CLR (Common Language Runtime) e cursor associado a um plano.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
dm_exec_cached_plan_dependent_objects(plan_handle)  
```  
  
## <a name="arguments"></a>Argumentos  
 *plan_handle*  
 Identifica exclusivamente um plano de execução de consulta para um lote que foi executado e seu plano reside no cache de plano. *plan_handle* está **varbinary(64)**. O *plan_handle* pode ser obtido dos seguintes objetos de gerenciamento dinâmico:  
  
-   [sys.dm_exec_cached_plans &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cached-plans-transact-sql.md)  
  
-   [sys.dm_exec_query_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md)  
  
-   [sys.dm_exec_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)  
  
## <a name="table-returned"></a>Tabela retornada  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**usecounts**|**int**|Número de vezes em que o contexto de execução ou cursor foi usado.<br /><br /> A coluna não é anulável.|  
|**memory_object_address**|**varbinary(8)**|Endereço de memória do contexto de execução ou cursor.<br /><br /> A coluna não é anulável.|  
|**cacheobjtype**|**nvarchar(50)**|O tipo de objeto do cache do plano. A coluna não é anulável. Os valores possíveis são:<br /><br /> Plano executável<br /><br /> Função compilada CLR <br /><br /> Procedimento compilado<br /><br /> Cursor|  
  
## <a name="permissions"></a>Permissões  
 , é necessário ter permissão VIEW SERVER STATE no servidor.  
  
## <a name="physical-joins"></a>Junções físicas  
 ![Diagrama de relação](../../relational-databases/system-dynamic-management-views/media/dm-dependent-objects.gif "diagrama de relação")  
  
## <a name="relationship-cardinalities"></a>Cardinalidades de relações  
  
|De|Para|Em|Relação|  
|----------|--------|--------|------------------|  
|**dm_exec_cached_plan_dependent_objects**|**dm_os_memory_objects**|**memory_object_address**|Um para um|  
  
## <a name="see-also"></a>Consulte também  
 [Funções e exibições de gerenciamento dinâmico relacionadas à execução &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)   
 [Exibições e funções de gerenciamento dinâmico &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [sys.syscacheobjects &#40;Transact-SQL&#41;](../../relational-databases/system-compatibility-views/sys-syscacheobjects-transact-sql.md)  
  
  
