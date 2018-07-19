---
title: sys.dm_xtp_gc_stats (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dm_xtp_gc_stats
- dm_xtp_gc_stats_TSQL
- sys.dm_xtp_gc_stats_TSQL
- sys.dm_xtp_gc_stats
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_xtp_gc_stats dynamic management view
ms.assetid: 8287d611-50e3-43e1-ba8d-3e3793d3ba0e
caps.latest.revision: 20
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: a66e199d232ed96fd194d42e340f3468fee51b6b
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2018
ms.locfileid: "38005648"
---
# <a name="sysdmxtpgcstats-transact-sql"></a>sys.dm_xtp_gc_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2014-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-xxxx-xxxx-xxx-md.md)]

  Fornece informações (estatística geral) sobre o comportamento atual do processo de coleta de lixo do [!INCLUDE[hek_2](../../includes/hek-2-md.md)].  
  
 As linhas são coletadas como lixo durante o processamento de transação regular ou pelo thread principal de coleta de lixo, que é conhecido como trabalhador inativo. Quando uma transação de usuário é confirmada, ela remove um item de trabalho da fila de coleta de lixo ([DM xtp_gc_queue_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-xtp-gc-queue-stats-transact-sql.md)). Qualquer linha que poderia ser coletada como lixo mas não foi acessada pela transação de usuário principal é coletada como lixo por um trabalhador inativo, como parte da verificação de canto sujo (uma verificação das áreas do índice que são menos acessadas).  
  
 Para obter mais informações, veja [OLTP in-memory &#40;Otimização na memória&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md).  
  
|Nome da coluna|Tipo|Description|  
|-----------------|----------|-----------------|  
|rows_examined|**bigint**|O número de linhas verificadas pelo subsistema de coleta de lixo desde que o servidor foi iniciado.|  
|rows_no_sweep_needed|**bigint**|O número de linhas que foram removidas sem uma verificação de canto sujo.|  
|rows_first_in_bucket|**bigint**|O número de linhas verificadas pela coleta de lixo que foi a primeira linha no bucket de hash.|  
|rows_first_in_bucket_removed|**bigint**|O número de linhas verificadas pela coleta de lixo que foi a primeira linha no bucket de hash que foi removida.|  
|rows_marked_for_unlink|**bigint**|O número de linhas verificadas pela coleta de lixo que já foram marcadas como não vinculadas em seus índices com contagem de referência =0.|  
|parallel_assist_count|**bigint**|O número de linhas processadas por transações de usuário.|  
|idle_worker_count|**bigint**|O número de linhas de lixo processadas pelo trabalhador inativo.|  
|sweep_scans_started|**bigint**|O número de verificações de canto sujo realizadas pelo subsistema de coleta de lixo.|  
|sweep_scans_retries|**bigint**|O número de verificações de canto sujo realizadas pelo subsistema de coleta de lixo.|  
|sweep_rows_touched|**bigint**|Linhas lidas pelo processamento de canto sujo.|  
|sweep_rows_expiring|**bigint**|Linhas prestes a expirar lidas pelo processamento de canto sujo.|  
|sweep_rows_expired|**bigint**|Linhas expiradas lidas pelo processamento de canto sujo.|  
|sweep_rows_expired_removed|**bigint**|Linhas expiradas removidas pelo processamento de canto sujo.|  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão VIEW SERVER STATE na instância.  
  
## <a name="usage-scenario"></a>Cenário de uso  
 Veja a seguir uma saída de exemplo:  
  
```  
rows_examined        rows_no_sweep_needed rows_first_in_bucket rows_first_in_bucket_removed  
280085               209512               69905  
rows_first_in_bucket_removed rows_marked_for_unlink parallel_assist_count idle_worker_count  
69905                        0                      8953  
  
idle_worker_count    sweep_scans_started  sweep_scan_retries   sweep_rows_touched  
10306473             670                  0                    1343  
  
sweep_rows_expiring  sweep_rows_expired   sweep_rows_expired_removed  
               0                 673673  
```  
  
## <a name="see-also"></a>Consulte também  
 [Exibições de gerenciamento dinâmico de tabela otimizada em memória &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/memory-optimized-table-dynamic-management-views-transact-sql.md)  
  
  
