---
title: sys.dm_xtp_system_memory_consumers (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dm_xtp_system_memory_consumers
- sys.dm_xtp_system_memory_consumers_TSQL
- sys.dm_xtp_system_memory_consumers
- dm_xtp_system_memory_consumers_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_xtp_system_memory_consumers dynamic management view
ms.assetid: 9eb0dd82-7920-42e0-9e50-7ce6e7ecee8b
caps.latest.revision: 22
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 3363fa2208f735c38ebd696b782fced80e5c49ce
ms.sourcegitcommit: 7019ac41524bdf783ea2c129c17b54581951b515
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2018
ms.locfileid: "34468632"
---
# <a name="sysdmxtpsystemmemoryconsumers-transact-sql"></a>sys.dm_xtp_system_memory_consumers (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2014-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-xxxx-xxxx-xxx-md.md)]

  Relata os consumidores de memória no nível do sistema para [!INCLUDE[hek_2](../../includes/hek-2-md.md)]. A memória desses consumidores vêm do pool padrão (quando a alocação está no contexto de um thread do usuário) ou do pool interno (se a alocação estiver no contexto de um thread do sistema).  
  
```  
-- system memory consumers @ instance  
select * from sys.dm_xtp_system_memory_consumers  
```  
  
 Para obter mais informações, veja [OLTP in-memory &#40;Otimização na memória&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md).  
  
|Nome da coluna|Tipo|Description|  
|-----------------|----------|-----------------|  
|memory_consumer_id|**bigint**|ID interna do consumidor de memória.|  
|memory_consumer_type|**Int**|Um inteiro que representa o tipo do consumidor de memória com um dos seguintes valores:<br /><br /> 0 – Não deve ser exibido. Agrega o uso de memória de dois ou mais consumidores.<br /><br /> 1 – LOOKASIDE: Rastreia o consumo de memória para a parte de um sistema.<br /><br /> 2 - VARHEAP: Rastreia o consumo de memória para um heap de comprimento variável.<br /><br /> 4 - pool da página e/s: rastreia o consumo de memória para um pool de página do sistema usado para operações de e/s.|  
|memory_consumer_type_desc|**nvarchar(16)**|A descrição do tipo do consumidor de memória:<br /><br /> 0 – Não deve ser exibido.<br /><br /> 1 – LOOKASIDE<br /><br /> 2 - VARHEAP<br /><br /> 4 - PGPOOL|  
|memory_consumer_desc|**nvarchar(64)**|Descrição da instância do consumidor de memória:<br /><br /> VARHEAP: <br />Heap do sistema. Uso geral. Atualmente usado apenas para alocar itens de trabalho de coleta de lixo.<br />-Ou-<br />A parte de heap. Usado por partes quando o número de itens contidos na lista de partes alcançar um valor predeterminado (normalmente em torno de 5.000 itens).<br /><br /> PGPOOL: Para o sistema de e/s existe pools são três pool da página sistema 4K tamanhos diferentes, o pool de página do sistema 64K e pool da página sistema 256K.|  
|lookaside_id|**bigint**|A ID do provedor de memória de direções de local de thread.|  
|pagepool_id|**bigint**|A ID do provedor de memória do pool de páginas de local de thread.|  
|allocated_bytes|**bigint**|Número de bytes reservados para o consumidor.|  
|used_bytes|**bigint**|Bytes usados por este consumidor. Aplica-se somente a consumidores de memória de varheap.|  
|allocation_count|**Int**|Número de alocações.|  
|partition_count|**Int**|Somente para uso interno.|  
|sizeclass_count|**Int**|Somente para uso interno.|  
|min_sizeclass|**Int**|Somente para uso interno.|  
|max_sizeclass|**Int**|Somente para uso interno.|  
|memory_consumer_address|**varbinary**|Endereço interno do consumidor.|  
  
## <a name="permissions"></a>Permissões  
 Requer as permissões VIEW SERVER STATE no servidor.  
  
## <a name="user-scenario"></a>Cenário de uso  
  
```  
-- system memory consumers @ instance  
selectmemory_consumer_type_desc,   
allocated_bytes/1024 as allocated_bytes_kb,   
used_bytes/1024 as used_bytes_kb, allocation_count  
from sys.dm_xtp_system_memory_consumers  
```  
  
 A saída mostra todos os consumidores de memória no nível do sistema. Por exemplo, há consumidores para o registro de transações.  
  
```  
memory_consumer_type_name           memory_consumer_desc                           allocated_bytes_kb   used_bytes_kb        allocation_count  
-------------------------------          ---------------------                          -------------------  --------------        ----------------  
VARHEAP                                  Lookaside heap                                 0                    0                    0  
VARHEAP                                  System heap                                    768                  0                    2  
LOOKASIDE                                GC transaction map entry                       64                   64                   910  
LOOKASIDE                                Redo transaction map entry                     128                  128                  1260  
LOOKASIDE                                Recovery table cache entry                     448                  448                  8192  
LOOKASIDE                                Transaction recent rows                        3264                 3264                 4444  
LOOKASIDE                                Range cursor                                   0                    0                    0  
LOOKASIDE                                Hash cursor                                    3200                 3200                 11070  
LOOKASIDE                                Transaction save-point set entry               0                    0                    0  
LOOKASIDE                                Transaction partially-inserted rows set        704                  704                  1287  
LOOKASIDE                                Transaction constraint set                     576                  576                  1940  
LOOKASIDE                                Transaction save-point set                     0                    0                    0  
LOOKASIDE                                Transaction write set                          704                  704                  672  
LOOKASIDE                                Transaction scan set                           320                  320                  156  
LOOKASIDE                                Transaction read set                           704                  704                  343  
LOOKASIDE                                Transaction                                    4288                 4288                 1459  
PGPOOL                                   System 256K page pool                          5120                 5120                 20  
PGPOOL                                   System 64K page pool                           0                    0                    0  
PGPOOL                                   System 4K page pool                            24                   24                   6  
```  
  
 Para ver a memória total consumida por alocadores do sistema:  
  
```  
select sum(allocated_bytes)/(1024*1024) as total_allocated_MB, sum(used_bytes)/(1024*1024) as total_used_MB   
from sys.dm_xtp_system_memory_consumers  
  
total_allocated_MB   total_used_MB  
-------------------- --------------------  
2                    2  
```  
  
## <a name="see-also"></a>Consulte também  
 [Exibições de gerenciamento dinâmico de tabela de otimização de memória &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/memory-optimized-table-dynamic-management-views-transact-sql.md)  
  
  
