---
title: sys.dm_fts_memory_pools (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/29/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
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
caps.latest.revision: 29
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: dd8fff01d2ec00d893bbf56d86ecf345d6fec579
ms.sourcegitcommit: 8b332c12850c283ae413e0b04b2b290ac2edb672
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/05/2018
---
# <a name="sysdmftsmemorypools-transact-sql"></a>sys.dm_fts_memory_pools (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Retorna informações sobre os pools de memória compartilhada disponíveis para o componente Full-Text Gatherer em um rastreamento de texto completo ou um intervalo de rastreamento de texto completo.  
   
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**pool_id**|**Int**|ID do pool de memória alocada.<br /><br /> 0 = Buffers pequenos<br /><br /> 1 = Buffers grandes|  
|**buffer_size**|**Int**|Tamanho de cada buffer alocado no pool de memória.|  
|**min_buffer_limit**|**Int**|Número mínimo de buffers permitido no pool de memória.|  
|**max_buffer_limit**|**Int**|Número máximo de buffers permitido no pool de memória.|  
|**buffer_count**|**Int**|Número atual de buffers de memória compartilhada no pool de memória.|  
  
## <a name="permissions"></a>Permissões  

Em [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], requer `VIEW SERVER STATE` permissão.   
Em [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)], requer o `VIEW DATABASE STATE` no banco de dados.   
 
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
  
  
