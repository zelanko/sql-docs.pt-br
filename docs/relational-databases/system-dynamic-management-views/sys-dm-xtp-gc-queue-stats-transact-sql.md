---
title: sys.dm_xtp_gc_queue_stats (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/02/2016
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
ms.assetid: addef774-318d-46a7-85df-f93168a800cb
caps.latest.revision: 18
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 8ef266afcab07fbb9d5bb73a48dafcf8eea59844
ms.sourcegitcommit: 7019ac41524bdf783ea2c129c17b54581951b515
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2018
ms.locfileid: "34465942"
---
# <a name="sysdmxtpgcqueuestats-transact-sql"></a>sys.dm_xtp_gc_queue_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2014-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-xxxx-xxxx-xxx-md.md)]

  Envia informações sobre cada fila de trabalhos de coleta de lixo no servidor, e várias estatísticas sobre cada uma delas. Há uma fila por CPU lógica.  
  
 O thread principal de coleta de lixo (thread inativo) rastreia linhas atualizadas, excluídas e inseridas de todas as transações concluídas desde a última chamada do thread principal de coleta de lixo. Quando o thread de coleta de lixo é ativado, ele determina se o carimbo de data/hora da transação ativa mais antiga foi alterado. Se a transação ativa mais antiga tiver sido alterada, o thread inativo enfileirará os itens de trabalho (em partes de 16 linhas) para transações cujos conjuntos de gravações não são mais necessários. Por exemplo, se você excluir 1.024 linhas, acabará vendo 64 itens de trabalho de coleta de lixo enfileirados, cada um contendo 16 linhas excluídas.  Depois que uma transação de usuário é confirmada, ela seleciona todos os itens enfileirados em seu agendador. Se não houver itens enfileirados no agendador, a transação do usuário realizará a pesquisa em qualquer fila do nó NUMA atual.  
  
 Você pode determinar se a coleta de lixo está liberando memória para as linhas excluídas executando sys.dm_xtp_gc_queue_stats para saber se o trabalho enfileirado está sendo processado. Se as entradas em current_queue_depth não estiverem sendo processadas ou se novos itens de trabalho não estão sendo adicionado para current_queue_depth, isso é uma indicação de que a coleta de lixo não está liberando memória. Por exemplo, a coleta de lixo não poderá ser feita se houver uma transação demorada.  
  
 Para obter mais informações, veja [OLTP in-memory &#40;Otimização na memória&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md).  
  

|Nome da coluna|Tipo|Description|  
|-----------------|----------|-----------------|  
|queue_id|**Int**|O identificador exclusivo da fila.|  
|total_enqueues|**bigint**|O número total de itens de trabalho de coleta de lixo enfileirados para essa fila desde que o servidor foi iniciado.|  
|total_dequeues|**bigint**|O número total de itens de trabalho de coleta de lixo removidos dessa fila desde que o servidor foi iniciado.|  
|current_queue_depth|**bigint**|O número atual de itens de trabalho de coleta de lixo presentes nessa fila. Este item pode indicar um ou mais para serem limpos.|  
|maximum_queue_depth|**bigint**|A profundidade máxima que essa fila viu.|  
|last_service_ticks|**bigint**|Os tiques de CPU no momento em que a fila foi atendida por último.|  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão VIEW SERVER STAT.  
  
## <a name="user-scenario"></a>Cenário de uso  
 A saída mostra que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está em execução em 4 núcleos ou a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tem afinidade para 4 núcleos:  
  
 A saída mostra que não há nenhum item de trabalho nas filas para processar. Para a fila 0, o total de itens de trabalho retirados da fila desde a inicialização do SQL é 15625 e a profundidade máxima da fila foi 215625.  
  
```  
queue_id total_enqueues total_dequeues current_queue_depth  maximum_queue_depth  last_service_ticks  
----------------------------------------------------------------------------------------------------  
0        15625                15625    0                    15625                1233573168347  
1        15625                15625    0                    15625                1234123295566  
2        15625                15625    0                    15625                1233569418146  
3        15625                15625    0                    15625                1233571605761  
```  
  
## <a name="see-also"></a>Consulte também  
 [Exibições de gerenciamento dinâmico de tabela de otimização de memória &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/memory-optimized-table-dynamic-management-views-transact-sql.md)  
  
  
