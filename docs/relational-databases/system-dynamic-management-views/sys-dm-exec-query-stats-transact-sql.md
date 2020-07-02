---
title: sys. dm_exec_query_stats (Transact-SQL) | Microsoft Docs
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
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: a2df86c9850dddb7532602476d2ce9ffcaebad62
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85734697"
---
# <a name="sysdm_exec_query_stats-transact-sql"></a>sys.dm_exec_query_stats (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

Retorna estatísticas de desempenho de agregação de planos de consulta em cache no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. A exibição contém uma linha por instrução de consulta dentro do plano em cache e o tempo de vida das linhas é ligado ao próprio plano. Quando um plano é removido do cache, as linhas correspondentes são eliminadas desta exibição.  
  
> [!NOTE]
> - Os resultados de **Sys. dm_exec_query_stats** podem variar com cada execução, já que os dados refletem apenas as consultas concluídas e não os que ainda estão em andamento.
> - Para chamá-lo de [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] ou [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] , use o nome **Sys. dm_pdw_nodes_exec_query_stats**.    

  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**sql_handle**|**varbinary(64)**  |É um token que identifica exclusivamente o lote ou o procedimento armazenado do qual a consulta faz parte.<br /><br /> Pode ser usado **sql_handle**, junto com **statement_start_offset** e **statement_end_offset**, para recuperar o texto SQL da consulta, chamando a função de gerenciamento dinâmico **sys.dm_exec_sql_text**.|  
|**statement_start_offset**|**int**|Indica, em bytes, começando com 0, a posição inicial da consulta que a linha descreve dentro do texto de seu lote ou objeto persistente.|  
|**statement_end_offset**|**int**|Indica, em bytes, começando com 0, a posição final da consulta que a linha descreve dentro do texto de seu lote ou objeto persistente. Para versões anteriores [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] , um valor de-1 indica o final do lote. Comentários à direita não são mais incluídos.|  
|**plan_generation_num**|**bigint**|Um número de sequência que pode ser usado para distinguir entre instâncias de planos após uma recompilação.|  
|**plan_handle**|**varbinary(64)**|É um token que identifica exclusivamente um plano de execução de consulta para um lote que foi executado e seu plano reside no cache de planos ou está em execução no momento. Este valor pode ser transmitido à função de gerenciamento dinâmico [sys.dm_exec_query_plan](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-plan-transact-sql.md) para a obtenção do plano de consulta.<br /><br /> Sempre será 0x000 quando um procedimento armazenado compilado nativamente consultar uma tabela com otimização de memória.|  
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
|**last_logical_writes**|**bigint**|Número de páginas do pool de buffers sujos durante a execução concluída mais recentemente do plano.<br /><br />Depois que uma página é lida, a página se torna suja somente na primeira vez que ela é modificada. Quando uma página é suja, esse número é incrementado. As modificações subsequentes de uma página já suja não afetam esse número.<br /><br />Esse número será sempre 0 ao consultar uma tabela com otimização de memória.|  
|**min_logical_writes**|**bigint**|Número mínimo de gravações lógicas que este plano efetuou durante uma única execução.<br /><br /> Sempre será 0 ao consultar uma tabela com otimização de memória.|  
|**max_logical_writes**|**bigint**|Número máximo de gravações lógicas que este plano efetuou durante uma única execução.<br /><br /> Sempre será 0 ao consultar uma tabela com otimização de memória.|  
|**total_logical_reads**|**bigint**|Número total de leituras lógicas efetuadas por execuções deste plano desde sua compilação.<br /><br /> Sempre será 0 ao consultar uma tabela com otimização de memória.|  
|**last_logical_reads**|**bigint**|Número de leituras lógicas efetuadas na última vez em que o plano foi executado.<br /><br /> Sempre será 0 ao consultar uma tabela com otimização de memória.|  
|**min_logical_reads**|**bigint**|Número mínimo de leituras lógicas que este plano efetuou durante uma única execução.<br /><br /> Sempre será 0 ao consultar uma tabela com otimização de memória.|  
|**max_logical_reads**|**bigint**|Número máximo de leituras lógicas que este plano efetuou durante uma única execução.<br /><br /> Sempre será 0 ao consultar uma tabela com otimização de memória.|  
|**total_clr_time**|**bigint**|Tempo, relatado em microssegundos (mas preciso apenas em milissegundos), consumido dentro [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] de objetos Common Language Runtime (CLR) por execuções deste plano desde que ele foi compilado. Os objetos CLR podem ser procedimentos armazenados, funções, gatilhos, tipos e agregações.|  
|**last_clr_time**|**bigint**|Tempo, relatado em microssegundos (mas só preciso em milissegundos), consumido pela execução dentro de objetos CLR [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] durante a última execução desse plano. Os objetos CLR podem ser procedimentos armazenados, funções, gatilhos, tipos e agregações.|  
|**min_clr_time**|**bigint**|Tempo mínimo, relatado em microssegundos (mas preciso somente em milissegundos), que esse plano já consumiu dentro de objetos CLR [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] durante uma única execução. Os objetos CLR podem ser procedimentos armazenados, funções, gatilhos, tipos e agregações.|  
|**max_clr_time**|**bigint**|Tempo máximo, relatado em microssegundos (mas preciso somente em milissegundos), que esse plano já consumiu dentro de CLR [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] durante uma única execução. Os objetos CLR podem ser procedimentos armazenados, funções, gatilhos, tipos e agregações.|  
|**total_elapsed_time**|**bigint**|Tempo total decorrido, relatado em microssegundos (mas preciso somente em milissegundos), para execuções concluídas desse plano.|  
|**last_elapsed_time**|**bigint**|Tempo decorrido, relatado em microssegundos (mas preciso somente em milissegundos), para a execução completa mais recente desse plano.|  
|**min_elapsed_time**|**bigint**|Tempo decorrido mínimo, relatado em microssegundos (mas preciso somente em milissegundos), para qualquer execução concluída desse plano.|  
|**max_elapsed_time**|**bigint**|Tempo decorrido máximo, relatado em microssegundos (mas preciso somente em milissegundos), para qualquer execução concluída desse plano.|  
|**query_hash**|**Binário (8)**|Valor de hash binário calculado na consulta e usado para identificar consultas com lógica semelhante. Você pode usar o hash de consulta para determinar o recurso de agregação usado para consultas que são diferentes apenas nos valores literais.|  
|**query_plan_hash**|**binário (8)**|Valor de hash binário calculado no plano de execução de consulta e usado para identificar planos de execução de consulta semelhantes. Você pode usar o hash de plano de consulta para localizar o custo cumulativo de consultas com planos de execução semelhantes.<br /><br /> Sempre será 0x000 quando um procedimento armazenado compilado nativamente consultar uma tabela com otimização de memória.|  
|**total_rows**|**bigint**|O número total de linhas retornadas pela consulta. Não pode ser nulo.<br /><br /> Sempre será 0 quando um procedimento armazenado compilado nativamente consultar uma tabela com otimização de memória.|  
|**last_rows**|**bigint**|O número total de linhas retornadas pela última execução da consulta. Não pode ser nulo.<br /><br /> Sempre será 0 quando um procedimento armazenado compilado nativamente consultar uma tabela com otimização de memória.|  
|**min_rows**|**bigint**|Número mínimo de linhas já retornadas pela consulta durante uma execução. Não pode ser nulo.<br /><br /> Sempre será 0 quando um procedimento armazenado compilado nativamente consultar uma tabela com otimização de memória.|  
|**max_rows**|**bigint**|Número máximo de linhas já retornadas pela consulta durante uma execução. Não pode ser nulo.<br /><br /> Sempre será 0 quando um procedimento armazenado compilado nativamente consultar uma tabela com otimização de memória.|  
|**statement_sql_handle**|**varbinary(64)**|**Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior.<br /><br /> Populado com valores não nulos somente se Repositório de Consultas estiver ativado e coletando as estatísticas para essa consulta específica.|  
|**statement_context_id**|**bigint**|**Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior.<br /><br /> Populado com valores não nulos somente se Repositório de Consultas estiver ativado e coletando as estatísticas para essa consulta específica.|  
|**total_dop**|**bigint**|A soma total do grau de paralelismo que este plano usou desde que foi compilado. Será sempre 0 para consultar uma tabela com otimização de memória.<br /><br /> **Aplica-se a**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] e posterior.|  
|**last_dop**|**bigint**|O grau de paralelismo quando este plano foi executado pela última vez. Será sempre 0 para consultar uma tabela com otimização de memória.<br /><br /> **Aplica-se a**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] e posterior.|  
|**min_dop**|**bigint**|O grau mínimo de paralelismo que esse plano já usou durante uma execução. Será sempre 0 para consultar uma tabela com otimização de memória.<br /><br /> **Aplica-se a**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] e posterior.|  
|**max_dop**|**bigint**|O grau máximo de paralelismo que esse plano já usou durante uma execução. Será sempre 0 para consultar uma tabela com otimização de memória.<br /><br /> **Aplica-se a**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] e posterior.|  
|**total_grant_kb**|**bigint**|A quantidade total de concessão de memória reservada em KB que este plano recebeu desde que foi compilado. Será sempre 0 para consultar uma tabela com otimização de memória.<br /><br /> **Aplica-se a**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] e posterior.|  
|**last_grant_kb**|**bigint**|A quantidade de concessão de memória reservada em KB quando este plano foi executado pela última vez. Será sempre 0 para consultar uma tabela com otimização de memória.<br /><br /> **Aplica-se a**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] e posterior.|  
|**min_grant_kb**|**bigint**|A quantidade mínima de concessão de memória reservada em KB que esse plano já recebeu durante uma execução. Será sempre 0 para consultar uma tabela com otimização de memória.<br /><br /> **Aplica-se a**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] e posterior.|  
|**max_grant_kb**|**bigint**|A quantidade máxima de concessão de memória reservada em KB que esse plano já recebeu durante uma execução. Será sempre 0 para consultar uma tabela com otimização de memória.<br /><br /> **Aplica-se a**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] e posterior.|  
|**total_used_grant_kb**|**bigint**|A quantidade total de concessão de memória reservada em KB que este plano usou desde que foi compilado. Será sempre 0 para consultar uma tabela com otimização de memória.<br /><br /> **Aplica-se a**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] e posterior.|  
|**last_used_grant_kb**|**bigint**|A quantidade de concessão de memória usada em KB quando este plano foi executado pela última vez. Será sempre 0 para consultar uma tabela com otimização de memória.<br /><br /> **Aplica-se a**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] e posterior.|  
|**min_used_grant_kb**|**bigint**|A quantidade mínima de concessão de memória usada em KB que esse plano já usou durante uma execução. Será sempre 0 para consultar uma tabela com otimização de memória.<br /><br /> **Aplica-se a**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] e posterior.|  
|**max_used_grant_kb**|**bigint**|A quantidade máxima de concessão de memória usada em KB que esse plano já usou durante uma execução. Será sempre 0 para consultar uma tabela com otimização de memória.<br /><br /> **Aplica-se a**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] e posterior.|  
|**total_ideal_grant_kb**|**bigint**|A quantidade total de concessão de memória ideal em KB que este plano estimou desde que foi compilado. Será sempre 0 para consultar uma tabela com otimização de memória.<br /><br /> **Aplica-se a**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] e posterior.|  
|**last_ideal_grant_kb**|**bigint**|A quantidade de concessão de memória ideal em KB quando este plano foi executado pela última vez. Será sempre 0 para consultar uma tabela com otimização de memória.<br /><br /> **Aplica-se a**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] e posterior.|  
|**min_ideal_grant_kb**|**bigint**|A quantidade mínima de concessão de memória ideal em KB que esse plano já estimou durante uma execução. Será sempre 0 para consultar uma tabela com otimização de memória.<br /><br /> **Aplica-se a**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] e posterior.|  
|**max_ideal_grant_kb**|**bigint**|A quantidade máxima de concessão de memória ideal em KB que esse plano já estimou durante uma execução. Será sempre 0 para consultar uma tabela com otimização de memória.<br /><br /> **Aplica-se a**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] e posterior.|  
|**total_reserved_threads**|**bigint**|A soma total de threads paralelos reservados que esse plano já usou desde que foi compilado. Será sempre 0 para consultar uma tabela com otimização de memória.<br /><br /> **Aplica-se a**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] e posterior.|  
|**last_reserved_threads**|**bigint**|O número de threads paralelos reservados quando este plano foi executado pela última vez. Será sempre 0 para consultar uma tabela com otimização de memória.<br /><br /> **Aplica-se a**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] e posterior.|  
|**min_reserved_threads**|**bigint**|O número mínimo de threads paralelos reservados que esse plano já usou durante uma execução.  Será sempre 0 para consultar uma tabela com otimização de memória.<br /><br /> **Aplica-se a**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] e posterior.|  
|**max_reserved_threads**|**bigint**|O número máximo de threads paralelos reservados que esse plano já usou durante uma execução. Será sempre 0 para consultar uma tabela com otimização de memória.<br /><br /> **Aplica-se a**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] e posterior.|  
|**total_used_threads**|**bigint**|A soma total de threads paralelos usados que este plano já usou desde que foi compilado. Será sempre 0 para consultar uma tabela com otimização de memória.<br /><br /> **Aplica-se a**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] e posterior.|  
|**last_used_threads**|**bigint**|O número de threads paralelos usados quando este plano foi executado pela última vez. Será sempre 0 para consultar uma tabela com otimização de memória.<br /><br /> **Aplica-se a**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] e posterior.|  
|**min_used_threads**|**bigint**|O número mínimo de threads paralelos usados que esse plano já usou durante uma execução. Será sempre 0 para consultar uma tabela com otimização de memória.<br /><br /> **Aplica-se a**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] e posterior.|  
|**max_used_threads**|**bigint**|O número máximo de threads paralelos usados que esse plano já usou durante uma execução. Será sempre 0 para consultar uma tabela com otimização de memória.<br /><br /> **Aplica-se a**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] e posterior.|  
|**total_columnstore_segment_reads**|**bigint**|A soma total de segmentos columnstore lidos pela consulta. Não pode ser nulo.<br /><br /> **Aplica-se a: a**partir do [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP2 e do [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] Cu3|    
|**last_columnstore_segment_reads**|**bigint**|O número de segmentos columnstore lidos pela última execução da consulta. Não pode ser nulo.<br /><br /> **Aplica-se a: a**partir do [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP2 e do [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] Cu3|    
|**min_columnstore_segment_reads**|**bigint**|O número mínimo de segmentos columnstore já lidos pela consulta durante uma execução. Não pode ser nulo.<br /><br /> **Aplica-se a: a**partir do [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP2 e do [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] Cu3|    
|**max_columnstore_segment_reads**|**bigint**|O número máximo de segmentos columnstore já lidos pela consulta durante uma execução. Não pode ser nulo.<br /><br /> **Aplica-se a: a**partir do [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP2 e do [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] Cu3|    
|**total_columnstore_segment_skips**|**bigint**|A soma total de segmentos columnstore ignorada pela consulta. Não pode ser nulo.<br /><br /> **Aplica-se a: a**partir do [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP2 e do [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] Cu3|    
|**last_columnstore_segment_skips**|**bigint**|O número de segmentos columnstore ignorados pela última execução da consulta. Não pode ser nulo.<br /><br /> **Aplica-se a: a**partir do [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP2 e do [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] Cu3|    
|**min_columnstore_segment_skips**|**bigint**|O número mínimo de segmentos columnstore já ignorados pela consulta durante uma execução. Não pode ser nulo.<br /><br /> **Aplica-se a: a**partir do [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP2 e do [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] Cu3|    
|**max_columnstore_segment_skips**|**bigint**|O número máximo de segmentos columnstore já ignorados pela consulta durante uma execução. Não pode ser nulo.<br /><br /> **Aplica-se a: a**partir do [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP2 e do [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] Cu3|
|**total_spills**|**bigint**|O número total de páginas despejadas pela execução desta consulta desde sua compilação.<br /><br /> **Aplica-se a: a**partir do [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP2 e do [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] Cu3|  
|**last_spills**|**bigint**|O número de páginas despejadas na última vez em que a consulta foi executada.<br /><br /> **Aplica-se a: a**partir do [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP2 e do [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] Cu3|  
|**min_spills**|**bigint**|O número mínimo de páginas que essa consulta já excedeu durante uma única execução.<br /><br /> **Aplica-se a: a**partir do [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP2 e do [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] Cu3|  
|**max_spills**|**bigint**|O número máximo de páginas que essa consulta já excedeu durante uma única execução.<br /><br /> **Aplica-se a: a**partir do [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP2 e do [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] Cu3|  
|**pdw_node_id**|**int**|O identificador do nó em que essa distribuição está.<br /><br /> **Aplica-se a**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] ,[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]| 
|**total_page_server_reads**|**bigint**|Número total de leituras de servidor de página remota executadas por execuções deste plano desde sua compilação.<br /><br /> **Aplica-se a:** Hiperescala do BD SQL do Azure |  
|**last_page_server_reads**|**bigint**|Número de leituras de servidor de página remota executadas na última vez em que o plano foi executado.<br /><br /> **Aplica-se a:** Hiperescala do BD SQL do Azure |  
|**min_page_server_reads**|**bigint**|O número mínimo de servidores de página remotos lê que esse plano já realizou durante uma única execução.<br /><br /> **Aplica-se a:** Hiperescala do BD SQL do Azure |  
|**max_page_server_reads**|**bigint**|O número máximo de servidores de páginas remotos lê que esse plano já realizou durante uma única execução.<br /><br /> **Aplica-se a:** Hiperescala do BD SQL do Azure |  
> [!NOTE]
> <sup>1</sup> para procedimentos armazenados compilados nativamente quando a coleta de estatísticas está habilitada, o tempo de trabalho é coletado em milissegundos. Se a consulta for executada em menos de um milissegundo, o valor será 0.  
  
## <a name="permissions"></a>Permissões  

Ativado [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] , requer `VIEW SERVER STATE` permissão.   
Nas [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] camadas Premium, o requer a `VIEW DATABASE STATE` permissão no banco de dados. Nas [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] camadas Standard e Basic, o requer o **administrador do servidor** ou uma conta de **administrador do Azure Active Directory** .   
   
## <a name="remarks"></a>Comentários  
 As estatísticas na exibição são atualizadas quando uma consulta é concluída.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-finding-the-top-n-queries"></a>a. Localizando as consultas TOP N  
 O exemplo a seguir retorna informações sobre as cinco principais consultas classificadas pelo tempo médio de CPU. Este exemplo agrega as consultas de acordo com o hash de consulta para que as consultas logicamente equivalentes sejam agrupadas pelo respectivo consumo de recursos cumulativo.  
  
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
  
## <a name="see-also"></a>Veja também  
[Funções e exibições de gerenciamento dinâmico relacionadas à execução &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)    
[sys. dm_exec_sql_text &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sql-text-transact-sql.md)    
[sys. dm_exec_query_plan &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-plan-transact-sql.md)    
[sys. dm_exec_procedure_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-procedure-stats-transact-sql.md)     
[sys. dm_exec_trigger_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-trigger-stats-transact-sql.md)     
[sys.dm_exec_cached_plans &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cached-plans-transact-sql.md)    
  


