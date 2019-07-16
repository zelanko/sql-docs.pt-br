---
title: sys.dm_fts_memory_pools (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/29/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_fts_memory_pools_TSQL
- sys.dm_fts_memory_pools_TSQL
- sys.dm_fts_memory_pools
- dm_fts_memory_pools
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_fts_memory_pools dynamic management view
ms.assetid: 24747239-cd78-4d55-a00a-19233a457f42
author: pmasl
ms.author: pelopes
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 19f2c09140fdebda5810079aeedcd5444124fcc4
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67900907"
---
# <a name="sysdmftsmemorypools-transact-sql"></a>sys.dm_fts_memory_pools (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Retorna informações sobre os pools de memória compartilhada disponíveis para o componente Full-Text Gatherer em um rastreamento de texto completo ou um intervalo de rastreamento de texto completo.  
   
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**pool_id**|**int**|ID do pool de memória alocada.<br /><br /> 0 = Buffers pequenos<br /><br /> 1 = Buffers grandes|  
|**buffer_size**|**int**|Tamanho de cada buffer alocado no pool de memória.|  
|**min_buffer_limit**|**int**|Número mínimo de buffers permitido no pool de memória.|  
|**max_buffer_limit**|**int**|Número máximo de buffers permitido no pool de memória.|  
|**buffer_count**|**int**|Número atual de buffers de memória compartilhada no pool de memória.|  
  
## <a name="permissions"></a>Permissões  

Na [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], requer `VIEW SERVER STATE` permissão.   
Em [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)], requer a permissão `VIEW DATABASE STATE` no banco de dados.   
 
## <a name="physical-joins"></a>Junções físicas  
 ![Junções significativas dessa exibição de gerenciamento dinâmico](../../relational-databases/system-dynamic-management-views/media/join-dm-fts-memory-pools-1.gif "junções significativas dessa exibição de gerenciamento dinâmico")  
  
## <a name="relationship-cardinalities"></a>Cardinalidades de relações  
  
|De|Para|Relação|  
|----------|--------|------------------|  
|dm_fts_memory_buffers.pool_id|dm_fts_memory_pools.pool_id|Muitos para um|  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir retorna o total de memória compartilhada de propriedade do componente Full-Text Gatherer [!INCLUDE[msCoName](../../includes/msconame-md.md)] do processo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
```  
SELECT SUM(buffer_size * buffer_count) AS "total memory"   
    FROM sys.dm_fts_memory_pools;  
```  
  
## <a name="see-also"></a>Consulte também  
 [Pesquisa de texto completo e funções e exibições de gerenciamento dinâmico de pesquisa semântica &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/full-text-and-semantic-search-dynamic-management-views-functions.md)  
  
  
