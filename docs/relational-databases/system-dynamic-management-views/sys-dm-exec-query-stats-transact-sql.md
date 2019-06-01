---
title: sys.dm_exec_query_stats (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/30/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_exec_query_stats_TSQL
- dm_exec_query_stats
- sys.dm_exec_query_stats
- sys.dm_exec_query_stats_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_query_stats dynamic management view
ms.assetid: eb7b58b8-3508-4114-97c2-d877bcb12964
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 821eaa4b7c54d8d2f449b2b071582480ac806378
ms.sourcegitcommit: 5905c29b5531cef407b119ebf5a120316ad7b713
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66429021"
---
# <a name="sysdmexecquerystats-transact-sql"></a>sys.dm_exec_query_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Retorna estatísticas de desempenho de agregação de planos de consulta em cache no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. A exibição contém uma linha por instrução de consulta dentro do plano em cache e o tempo de vida das linhas é ligado ao próprio plano. Quando um plano é removido do cache, as linhas correspondentes são eliminadas desta exibição.  
  
> [!NOTE]
> Uma consulta inicial de **DM exec_query_stats** pode produzir resultados inexatos se houver uma carga de trabalho atualmente em execução no servidor. Mais resultados precisos podem ser determinados pela reexecução da consulta.  
  
> [!NOTE]
> Chamá-lo partir [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] ou [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], use o nome **sys.dm_pdw_nodes_exec_query_stats**.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**sql_handle**|**varbinary(64)**  |É um token que identifica exclusivamente o lote ou procedimento armazenado que a consulta faz parte.<br /><br /> **sql_handle**, junto com **statement_start_offset** e **statement_end_offset**, pode ser usado para recuperar o texto SQL da consulta, chamando o **sys.dm_exec_sql_ texto** função de gerenciamento dinâmico.|  
|**statement_start_offset**|**int**|Indica, em bytes, começando com 0, a posição inicial da consulta que a linha descreve dentro do texto de seu lote ou objeto persistente.|  
|**statement_end_offset**|**int**|Indica, em bytes, começando com 0, a posição final da consulta que a linha descreve dentro do texto de seu lote ou objeto persistente. Para versões anteriores [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)], um valor -1 indica o final do lote. Comentários à direita não estão incluídos.|  
|**plan_generation_num**|**bigint**|Um número de sequência que pode ser usado para distinguir entre instâncias de planos após uma recompilação.|  
|**plan_handle**|**varbinary(64)**|É um token que identifica exclusivamente um plano de execução de consulta para um lote que foi executado e seu plano reside no cache de plano ou em execução no momento. Esse valor pode ser passado para o [. DM exec_query_plan](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-plan-transact-sql.md) a função de gerenciamento dinâmico para obter o plano de consulta.<br /><br /> Sempre será 0x000 quando um procedimento armazenado compilado nativamente consultar uma tabela com otimização de memória.|  
|**creation_time**|**datetime**|Hora em que o plano foi compilado.|  
|**last_execution_time**|**datetime**|Hora do início da execução do plano.|  
|**execution_count**|**bigint**|Número de vezes que o plano foi executado desde sua última compilação.|  
|**total_worker_time**|**bigint**|Tempo total da CPU, relatado em microssegundos (mas preciso somente em milissegundos), que foi consumido pelas execuções desse plano desde que foi compilado.<br /><br /> Para procedimentos armazenados compilados de modo nativo, o **total_worker_time** pode não ser preciso se várias execuções levarem menos de 1 milissegundo.|  
|**last_worker_time**|**bigint**|Tempo de CPU, relatado em microssegundos (mas preciso somente em milissegundos), consumido na última vez em que o plano foi executado. <sup>1</sup>|  
|**min_worker_time**|**bigint**|Tempo de CPU mínimo, relatado em microssegundos (mas preciso somente em milissegundos), que esse plano já consumiu durante uma única execução. <sup>1</sup>|  
|**max_worker_time**|**bigint**|Tempo de CPU máximo, relatado em microssegundos (mas preciso somente em milissegundos), que esse plano já consumiu durante uma única execução. <sup>1</sup>|  
|**total_physical_reads**|**bigint**|Número total de leituras físicas efetuadas por execuções deste plano desde sua compilação.<br /><br /> Sempre será 0 ao consultar uma tabela com otimização de memória.|  
|**last_physical_reads**|**bigint**|Número de leituras físicas efetuadas na última vez em que o plano foi executado.<br /><br /> Sempre será 0 ao consultar uma tabela com otimização de memória.|  
|**min_physical_reads**|**bigint**|Número mínimo de leituras físicas que este plano efetuou durante uma única execução.<br /><br /> Sempre será 0 ao consultar uma tabela com otimização de memória.|  
|**max_physical_reads**|**bigint**|Número máximo de leituras físicas que este plano efetuou durante uma única execução.<br /><br /> Sempre será 0 ao consultar uma tabela com otimização de memória.|  
|**total_logical_writes**|**bigint**|Número total de gravações lógicas efetuadas por execuções deste plano desde sua compilação.<br /><br /> Sempre será 0 ao consultar uma tabela com otimização de memória.|  
|**last_logical_writes**|**bigint**|Número de páginas de pool de buffer sujas durante a execução concluída mais recente do plano.<br /><br />Depois que uma página é lida, a página ficará suja apenas na primeira vez em que ele é modificado. Quando uma página estiver suja, esse número é incrementado. Modificações subsequentes de uma página suja já não afetam esse número.<br /><br />Esse número sempre será 0 ao consultar uma tabela com otimização de memória.|  
|**min_logical_writes**|**bigint**|Número mínimo de gravações lógicas que este plano efetuou durante uma única execução.<br /><br /> Sempre será 0 ao consultar uma tabela com otimização de memória.|  
|**max_logical_writes**|**bigint**|Número máximo de gravações lógicas que este plano efetuou durante uma única execução.<br /><br /> Sempre será 0 ao consultar uma tabela com otimização de memória.|  
|**total_logical_reads**|**bigint**|Número total de leituras lógicas efetuadas por execuções deste plano desde sua compilação.<br /><br /> Sempre será 0 ao consultar uma tabela com otimização de memória.|  
|**last_logical_reads**|**bigint**|Número de leituras lógicas efetuadas na última vez em que o plano foi executado.<br /><br /> Sempre será 0 ao consultar uma tabela com otimização de memória.|  
|**min_logical_reads**|**bigint**|Número mínimo de leituras lógicas que este plano efetuou durante uma única execução.<br /><br /> Sempre será 0 ao consultar uma tabela com otimização de memória.|  
|**max_logical_reads**|**bigint**|Número máximo de leituras lógicas que este plano efetuou durante uma única execução.<br /><br /> Sempre será 0 ao consultar uma tabela com otimização de memória.|  
|**total_clr_time**|**bigint**|Tempo, relatado em microssegundos (mas preciso somente em milissegundos), consumido dentro [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] common language runtime (CLR) objetos por execuções deste plano desde sua compilação. Os objetos CLR podem ser procedimentos armazenados, funções, gatilhos, tipos e agregações.|  
|**last_clr_time**|**bigint**|Tempo, relatado em microssegundos (mas só preciso em milissegundos), consumido pela execução dentro de objetos CLR [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] durante a última execução desse plano. Os objetos CLR podem ser procedimentos armazenados, funções, gatilhos, tipos e agregações.|  
|**min_clr_time**|**bigint**|Tempo mínimo, relatado em microssegundos (mas preciso somente em milissegundos), que esse plano já consumiu dentro de objetos CLR [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] durante uma única execução. Os objetos CLR podem ser procedimentos armazenados, funções, gatilhos, tipos e agregações.|  
|**max_clr_time**|**bigint**|Tempo máximo, relatado em microssegundos (mas preciso somente em milissegundos), que esse plano já consumiu dentro de CLR [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] durante uma única execução. Os objetos CLR podem ser procedimentos armazenados, funções, gatilhos, tipos e agregações.|  
|**total_elapsed_time**|**bigint**|Tempo total decorrido, relatado em microssegundos (mas preciso somente em milissegundos), para execuções concluídas desse plano.|  
|**last_elapsed_time**|**bigint**|Tempo decorrido, relatado em microssegundos (mas preciso somente em milissegundos), para a execução completa mais recente desse plano.|  
|**min_elapsed_time**|**bigint**|Tempo decorrido mínimo, relatado em microssegundos (mas preciso somente em milissegundos), para qualquer execução concluída desse plano.|  
|**max_elapsed_time**|**bigint**|Tempo decorrido máximo, relatado em microssegundos (mas preciso somente em milissegundos), para qualquer execução concluída desse plano.|  
|**query_hash**|**Binary(8)**|Valor de hash binário calculado na consulta e usado para identificar consultas com lógica semelhante. Você pode usar o hash de consulta para determinar o recurso de agregação usado para consultas que são diferentes apenas nos valores literais.|  
|**query_plan_hash**|**binary(8)**|Valor de hash binário calculado no plano de execução de consulta e usado para identificar planos de execução de consulta semelhantes. Você pode usar o hash de plano de consulta para localizar o custo cumulativo de consultas com planos de execução semelhantes.<br /><br /> Sempre será 0x000 quando um procedimento armazenado compilado nativamente consultar uma tabela com otimização de memória.|  
|**total_rows**|**bigint**|O número total de linhas retornadas pela consulta. Não pode ser nulo.<br /><br /> Sempre será 0 quando um procedimento armazenado compilado nativamente consultar uma tabela com otimização de memória.|  
|**last_rows**|**bigint**|O número total de linhas retornadas pela última execução da consulta. Não pode ser nulo.<br /><br /> Sempre será 0 quando um procedimento armazenado compilado nativamente consultar uma tabela com otimização de memória.|  
|**min_rows**|**bigint**|Número mínimo de linhas retornado pela consulta durante uma execução. Não pode ser nulo.<br /><br /> Sempre será 0 quando um procedimento armazenado compilado nativamente consultar uma tabela com otimização de memória.|  
|**max_rows**|**bigint**|Número máximo de linhas retornado pela consulta durante uma execução. Não pode ser nulo.<br /><br /> Sempre será 0 quando um procedimento armazenado compilado nativamente consultar uma tabela com otimização de memória.|  
|**statement_sql_handle**|**varbinary(64)**|**Aplica-se a**: do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Preenchido com valores não nulos apenas se a consulta Store é ativado e coletar as estatísticas para a consulta específica.|  
|**statement_context_id**|**bigint**|**Aplica-se a**: do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Preenchido com valores não nulos apenas se a consulta Store é ativado e coletar as estatísticas para a consulta específica.|  
|**total_dop**|**bigint**|A soma total do grau de paralelismo esse plano usado desde sua compilação. Além disso, ele sempre será 0 para consultar uma tabela com otimização de memória.<br /><br /> **Aplica-se a**: do [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].|  
|**last_dop**|**bigint**|O grau de paralelismo quando esse plano executado última vez. Além disso, ele sempre será 0 para consultar uma tabela com otimização de memória.<br /><br /> **Aplica-se a**: do [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].|  
|**min_dop**|**bigint**|O nível mínimo de paralelismo esse plano nunca usado durante uma execução. Além disso, ele sempre será 0 para consultar uma tabela com otimização de memória.<br /><br /> **Aplica-se a**: do [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].|  
|**max_dop**|**bigint**|O grau máximo de paralelismo esse plano já usado durante uma execução. Além disso, ele sempre será 0 para consultar uma tabela com otimização de memória.<br /><br /> **Aplica-se a**: do [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].|  
|**total_grant_kb**|**bigint**|A quantidade total de memória reservada conceder a esse plano recebido desde que ele foi compilado em KB. Além disso, ele sempre será 0 para consultar uma tabela com otimização de memória.<br /><br /> **Aplica-se a**: do [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].|  
|**last_grant_kb**|**bigint**|A quantidade de memória reservada conceder em KB, quando esse plano executado última vez. Além disso, ele sempre será 0 para consultar uma tabela com otimização de memória.<br /><br /> **Aplica-se a**: do [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].|  
|**min_grant_kb**|**bigint**|A quantidade mínima de memória reservada conceder a esse plano já recebeu durante uma execução em KB. Além disso, ele sempre será 0 para consultar uma tabela com otimização de memória.<br /><br /> **Aplica-se a**: do [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].|  
|**max_grant_kb**|**bigint**|A quantidade máxima de memória reservada conceder a esse plano já recebeu durante uma execução em KB. Além disso, ele sempre será 0 para consultar uma tabela com otimização de memória.<br /><br /> **Aplica-se a**: do [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].|  
|**total_used_grant_kb**|**bigint**|A quantidade total de memória reservada conceder a esse plano usado, pois ele foi compilado em KB. Além disso, ele sempre será 0 para consultar uma tabela com otimização de memória.<br /><br /> **Aplica-se a**: do [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].|  
|**last_used_grant_kb**|**bigint**|A quantidade de concessão de memória usada em KB, quando esse plano executado última vez. Além disso, ele sempre será 0 para consultar uma tabela com otimização de memória.<br /><br /> **Aplica-se a**: do [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].|  
|**min_used_grant_kb**|**bigint**|A quantidade mínima de memória usada de concessão em KB esse plano já utilizado durante uma execução. Além disso, ele sempre será 0 para consultar uma tabela com otimização de memória.<br /><br /> **Aplica-se a**: do [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].|  
|**max_used_grant_kb**|**bigint**|A quantidade máxima de memória usada de concessão em KB esse plano já utilizado durante uma execução. Além disso, ele sempre será 0 para consultar uma tabela com otimização de memória.<br /><br /> **Aplica-se a**: do [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].|  
|**total_ideal_grant_kb**|**bigint**|A quantidade total de concessão de memória ideal em KB que este plano estimado desde sua compilação. Além disso, ele sempre será 0 para consultar uma tabela com otimização de memória.<br /><br /> **Aplica-se a**: do [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].|  
|**last_ideal_grant_kb**|**bigint**|Concessão, a quantidade de memória ideal em KB quando esse plano executado hora da última. Além disso, ele sempre será 0 para consultar uma tabela com otimização de memória.<br /><br /> **Aplica-se a**: do [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].|  
|**min_ideal_grant_kb**|**bigint**|Conceder a quantidade mínima de memória ideal em KB que este plano estimado nunca durante uma execução. Além disso, ele sempre será 0 para consultar uma tabela com otimização de memória.<br /><br /> **Aplica-se a**: do [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].|  
|**max_ideal_grant_kb**|**bigint**|Conceder a quantidade máxima de memória ideal em KB que este plano estimado nunca durante uma execução. Além disso, ele sempre será 0 para consultar uma tabela com otimização de memória.<br /><br /> **Aplica-se a**: do [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].|  
|**total_reserved_threads**|**bigint**|A soma total dos paralelo reservado threads esse plano já utilizado desde sua compilação. Além disso, ele sempre será 0 para consultar uma tabela com otimização de memória.<br /><br /> **Aplica-se a**: do [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].|  
|**last_reserved_threads**|**bigint**|O número de segmentos paralelos de reservado quando esse plano executado hora da última. Além disso, ele sempre será 0 para consultar uma tabela com otimização de memória.<br /><br /> **Aplica-se a**: do [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].|  
|**min_reserved_threads**|**bigint**|O número mínimo de paralelo reservado threads esse plano já utilizado durante uma execução.  Além disso, ele sempre será 0 para consultar uma tabela com otimização de memória.<br /><br /> **Aplica-se a**: do [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].|  
|**max_reserved_threads**|**bigint**|O número máximo de paralelo reservado threads esse plano já utilizado durante uma execução. Além disso, ele sempre será 0 para consultar uma tabela com otimização de memória.<br /><br /> **Aplica-se a**: do [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].|  
|**total_used_threads**|**bigint**|A soma total dos usados em segmentos paralelos esse plano já utilizado desde sua compilação. Além disso, ele sempre será 0 para consultar uma tabela com otimização de memória.<br /><br /> **Aplica-se a**: do [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].|  
|**last_used_threads**|**bigint**|O número de segmentos paralelos de usado quando esse plano executado última vez. Além disso, ele sempre será 0 para consultar uma tabela com otimização de memória.<br /><br /> **Aplica-se a**: do [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].|  
|**min_used_threads**|**bigint**|O número mínimo de threads paralelos usados que esse plano já utilizado durante uma execução. Além disso, ele sempre será 0 para consultar uma tabela com otimização de memória.<br /><br /> **Aplica-se a**: do [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].|  
|**max_used_threads**|**bigint**|O número máximo de threads paralelos usados que esse plano já utilizado durante uma execução. Além disso, ele sempre será 0 para consultar uma tabela com otimização de memória.<br /><br /> **Aplica-se a**: do [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].|  
|**total_columnstore_segment_reads**|**bigint**|A soma total de segmentos columnstore lidas pela consulta. Não pode ser nulo.<br /><br /> **Aplica-se ao**: Começando com [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP2 e [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] CU3|    
|**last_columnstore_segment_reads**|**bigint**|O número de segmentos columnstore lido pela última execução da consulta. Não pode ser nulo.<br /><br /> **Aplica-se ao**: Começando com [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP2 e [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] CU3|    
|**min_columnstore_segment_reads**|**bigint**|O número mínimo de segmentos columnstore já lidas pela consulta durante uma execução. Não pode ser nulo.<br /><br /> **Aplica-se ao**: Começando com [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP2 e [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] CU3|    
|**max_columnstore_segment_reads**|**bigint**|O número máximo de segmentos columnstore já lidas pela consulta durante uma execução. Não pode ser nulo.<br /><br /> **Aplica-se ao**: Começando com [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP2 e [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] CU3|    
|**total_columnstore_segment_skips**|**bigint**|A soma total de segmentos columnstore ignorados pela consulta. Não pode ser nulo.<br /><br /> **Aplica-se ao**: Começando com [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP2 e [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] CU3|    
|**last_columnstore_segment_skips**|**bigint**|O número de segmentos columnstore ignorados pela última execução da consulta. Não pode ser nulo.<br /><br /> **Aplica-se ao**: Começando com [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP2 e [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] CU3|    
|**min_columnstore_segment_skips**|**bigint**|O número mínimo de segmentos columnstore nunca ignorada pela consulta durante uma execução. Não pode ser nulo.<br /><br /> **Aplica-se ao**: Começando com [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP2 e [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] CU3|    
|**max_columnstore_segment_skips**|**bigint**|O número máximo de segmentos columnstore nunca ignorada pela consulta durante uma execução. Não pode ser nulo.<br /><br /> **Aplica-se ao**: Começando com [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP2 e [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] CU3|
|**total_spills**|**bigint**|O número total de páginas despejados pelos execução dessa consulta, pois ele foi compilado.<br /><br /> **Aplica-se ao**: Começando com [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP2 e [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] CU3|  
|**last_spills**|**bigint**|O número de páginas despejadas a última vez em que a consulta foi executada.<br /><br /> **Aplica-se ao**: Começando com [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP2 e [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] CU3|  
|**min_spills**|**bigint**|O número mínimo de páginas que essa consulta nunca vazou durante uma única execução.<br /><br /> **Aplica-se ao**: Começando com [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP2 e [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] CU3|  
|**max_spills**|**bigint**|O número máximo de páginas que essa consulta nunca vazou durante uma única execução.<br /><br /> **Aplica-se ao**: Começando com [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP2 e [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] CU3|  
|**pdw_node_id**|**int**|O identificador para o nó que essa distribuição é no.<br /><br /> **Aplica-se ao**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]| 
|**total_page_server_reads**|**bigint**|Número total de leituras de servidor remoto página efetuadas por execuções deste plano desde sua compilação.<br /><br /> **Aplica-se a:** Em hiperescala do banco de dados SQL do Azure |  
|**last_page_server_reads**|**bigint**|Número de leituras de servidor remoto página efetuadas na última vez em que o plano foi executado.<br /><br /> **Aplica-se a:** Em hiperescala do banco de dados SQL do Azure |  
|**min_page_server_reads**|**bigint**|Número mínimo de servidor remoto página lê que este plano efetuou durante uma única execução.<br /><br /> **Aplica-se a:** Em hiperescala do banco de dados SQL do Azure |  
|**max_page_server_reads**|**bigint**|Número máximo de servidor remoto página lê que este plano efetuou durante uma única execução.<br /><br /> **Aplica-se a:** Em hiperescala do banco de dados SQL do Azure |  
> [!NOTE]
> <sup>1</sup> para procedimentos armazenados compilados nativamente quando a coleta de estatísticas é habilitada, tempo de trabalho será coletado em milissegundos. Se a consulta é executada em menos de um milissegundo, o valor será 0.  
  
## <a name="permissions"></a>Permissões  

Na [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], requer `VIEW SERVER STATE` permissão.   
Na [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)], requer o `VIEW DATABASE STATE` permissão no banco de dados.   
   
## <a name="remarks"></a>Comentários  
 As estatísticas na exibição são atualizadas quando uma consulta é concluída.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-finding-the-top-n-queries"></a>A. Localizando as consultas TOP N  
 O exemplo a seguir retorna informações sobre as cinco principais consultas classificadas por tempo médio de CPU. Este exemplo agrega as consultas de acordo com o hash de consulta para que as consultas logicamente equivalentes sejam agrupadas pelo respectivo consumo de recursos cumulativo.  
  
```sql  
SELECT TOP 5 query_stats.query_hash AS "Query Hash",   
    SUM(query_stats.total_worker_time) / SUM(query_stats.execution_count) AS "Avg CPU Time",  
    MIN(query_stats.statement_text) AS "Statement Text"  
FROM   
    (SELECT QS.*,   
    SUBSTRING(ST.text, (QS.statement_start_offset/2) + 1,  
    ((CASE statement_end_offset   
        WHEN -1 THEN DATALENGTH(ST.text)  
        ELSE QS.statement_end_offset END   
            - QS.statement_start_offset)/2) + 1) AS statement_text  
     FROM sys.dm_exec_query_stats AS QS  
     CROSS APPLY sys.dm_exec_sql_text(QS.sql_handle) as ST) as query_stats  
GROUP BY query_stats.query_hash  
ORDER BY 2 DESC;  
```  
  
### <a name="b-returning-row-count-aggregates-for-a-query"></a>B. Retornando agregações de contagem de linhas para uma consulta  
 O exemplo a seguir retorna informações de agregações de contagem de linhas (total de linhas, mínimo de linhas, máximo de linhas e últimas linhas) para consultas.  
  
```sql  
SELECT qs.execution_count,  
    SUBSTRING(qt.text,qs.statement_start_offset/2 +1,   
                 (CASE WHEN qs.statement_end_offset = -1   
                       THEN LEN(CONVERT(nvarchar(max), qt.text)) * 2   
                       ELSE qs.statement_end_offset end -  
                            qs.statement_start_offset  
                 )/2  
             ) AS query_text,   
     qt.dbid, dbname= DB_NAME (qt.dbid), qt.objectid,   
     qs.total_rows, qs.last_rows, qs.min_rows, qs.max_rows  
FROM sys.dm_exec_query_stats AS qs   
CROSS APPLY sys.dm_exec_sql_text(qs.sql_handle) AS qt   
WHERE qt.text like '%SELECT%'   
ORDER BY qs.execution_count DESC;  
```  
  
## <a name="see-also"></a>Confira também  
[Funções e exibições de gerenciamento dinâmico relacionadas à execução &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)    
[sys.dm_exec_sql_text &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sql-text-transact-sql.md)    
[sys.dm_exec_query_plan &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-plan-transact-sql.md)    
[sys.dm_exec_procedure_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-procedure-stats-transact-sql.md)     
[sys.dm_exec_trigger_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-trigger-stats-transact-sql.md)     
[sys.dm_exec_cached_plans &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cached-plans-transact-sql.md)    
  


