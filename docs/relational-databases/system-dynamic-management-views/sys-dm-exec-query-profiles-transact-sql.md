---
title: sys.dm_exec_query_profiles (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/16/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_exec_query_profiles_TSQL
- sys.dm_exec_query_profiles_TSQL
- dm_exec_query_profiles
- sys.dm_exec_query_profiles
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_query_profiles dynamic management view
ms.assetid: 54efc6cb-eea8-4f6d-a4d0-aa05eeb54081
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 87488f36a4b4b01181cd973a75d6e5c7f2e233d7
ms.sourcegitcommit: 2de5446fbc57787f18a907dd5deb02a7831ec07d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/02/2019
ms.locfileid: "58860717"
---
# <a name="sysdmexecqueryprofiles-transact-sql"></a>sys.dm_exec_query_profiles (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2014-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-asdb-xxxx-xxx-md.md)]

Monitora o progresso da consulta em tempo real, enquanto a consulta está em execução. Por exemplo, use este DMV para determinar que parte da consulta está executando lentamente. Adicione esse DMV com outros DMVs de sistema usando as colunas identificadas no campo de descrição. Ou, adicione esse DMV com outros contadores de desempenho (como o Monitor de Desempenho, xperf) usando colunas de carimbo de data/hora.  
  
## <a name="table-returned"></a>Tabela retornada  
Os contadores retornados são por operador por thread. Os resultados são dinâmicos e não coincidem, como os resultados das opções existentes `SET STATISTICS XML ON` que só cria saída quando a consulta é concluída.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|session_id|**SMALLINT**|Identifica a sessão na qual esta consulta é executada. Referencia dm_exec_sessions.session_id.|  
|request_id|**INT**|Identifica a solicitação de destino. Referencia dm_exec_sessions.request_id.|  
|sql_handle|**varbinary(64)**|É um token que identifica exclusivamente o lote ou procedimento armazenado que a consulta faz parte. Referencia dm_exec_query_stats.sql_handle.|  
|plan_handle|**varbinary(64)**|É um token que identifica exclusivamente um plano de execução de consulta para um lote que foi executado e seu plano reside no cache de plano ou em execução no momento. References dm_exec_query_stats.plan_handle.|  
|physical_operator_name|**nvarchar(256)**|Nome do operador físico.|  
|node_id|**INT**|Identifica um nó do operador na árvore de consulta.|  
|thread_id|**INT**|Distingue os threads (para uma consulta paralela) que pertencem ao mesmo nó do operador de consulta.|  
|task_address|**varbinary(8)**|Identifica a tarefa do sistema operacional SQL que esse thread está usando. Referencia dm_os_tasks.task_address.|  
|row_count|**BIGINT**|Número de linhas retornadas pelo operador até o momento.|  
|rewind_count|**BIGINT**|Número de retrocessos até o momento.|  
|rebind_count|**BIGINT**|Número de reassociações até o momento.|  
|end_of_scan_count|**BIGINT**|Número de término de exames até o momento.|  
|estimate_row_count|**BIGINT**|Número estimado de linhas. Pode ser útil comparar estimated_row_count com o row_count real.|  
|first_active_time|**BIGINT**|A hora, em milissegundos, em que operador foi chamado primeiro.|  
|last_active_time|**BIGINT**|A hora, em milissegundos, em que operador foi chamado por último.|  
|open_time|**BIGINT**|Carimbo de data/hora quando aberto (em milissegundos).|  
|first_row_time|**BIGINT**|Carimbo de data/hora quando a primeira linha foi aberta (em milissegundos).|  
|last_row_time|**BIGINT**|Carimbo de data/hora quando a última linha foi aberta (em milissegundos).|  
|close_time|**BIGINT**|Carimbo de data/hora quando fechado (em milissegundos).|  
|elapsed_time_ms|**BIGINT**|Tempo total decorrido (em milissegundos) usado por operações do nó de destino até o momento.|  
|cpu_time_ms|**BIGINT**|Total de uso de tempo (em milissegundos) de CPU por operações do nó de destino até o momento.|  
|database_id|**SMALLINT**|ID do banco de dados que contém o objeto no qual as leituras e gravações estão sendo realizadas.|  
|object_id|**INT**|O identificador do objeto no qual as leituras e gravações estão sendo realizadas. Referências sys.objects.object_id.|  
|index_id|**INT**|O índice (se houver) no qual o conjunto de linhas é aberto.|  
|scan_count|**BIGINT**|Número de verificações de tabela/índice até o momento.|  
|logical_read_count|**BIGINT**|Número de leituras lógicas até o momento.|  
|physical_read_count|**BIGINT**|Número de leituras físicas até o momento.|  
|read_ahead_count|**BIGINT**|Número de read-aheads até o momento.|  
|write_page_count|**BIGINT**|Número de gravações de página até o momento devido ao derramamento.|  
|lob_logical_read_count|**BIGINT**|Número de leituras lógicas LOB até o momento.|  
|lob_physical_read_count|**BIGINT**|Número de leituras físicas LOB até o momento.|  
|lob_read_ahead_count|**BIGINT**|Número de read-aheads LOB até o momento.|  
|segment_read_count|**INT**|Número de read-aheads de segmento até o momento.|  
|segment_skip_count|**INT**|Número de segmentos ignorados até o momento.| 
|actual_read_row_count|**BIGINT**|Número de linhas lidas por um operador antes da aplicação de predicado residual.| 
|estimated_read_row_count|**BIGINT**|**Aplica-se a:** Começando com [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] SP1. <br/>Número estimado de linhas a serem lidos por um operador antes da aplicação de predicado residual.|  
  
## <a name="general-remarks"></a>Comentários gerais  
 Se o nó do plano de consulta não tiver nenhuma e/s, todos os I/O-related contadores são definidos como NULL.  
  
 Os contadores de I/O-related relatados por esta DMV são mais granulares do que aqueles relatados pelo `SET STATISTICS IO` duas maneiras a seguir:  
  
-   `SET STATISTICS IO` agrupa os contadores para todas as e/s para uma determinada tabela junto. Com essa DMV você terá contadores separados para cada nó no plano de consulta que realiza e/s na tabela.  
  
-   Se houver uma varredura paralela, este DMV relata os contadores para cada um das threads paralelas que trabalham na varredura.
 
Começando com [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1, o *infraestrutura de criação de perfil de estatísticas de execução de consulta padrão* existir lado a lado com uma *infraestrutura de criação de perfil de estatísticas de execução de consulta leve* . `SET STATISTICS XML ON` e `SET STATISTICS PROFILE ON` sempre usam o *infraestrutura de criação de perfil de estatísticas de execução de consulta padrão*. Para `sys.dm_exec_query_profiles` para ser preenchido, uma da consulta infra-estruturas de criação de perfil deve ser habilitada. Para obter mais informações, confira [Infraestrutura de Criação de Perfil de Consulta](../../relational-databases/performance/query-profiling-infrastructure.md).    

>[!NOTE]
> A consulta sob investigação deve começar **após** a consulta a infraestrutura de criação de perfil foi habilitada, permitindo que ele depois que a consulta iniciada não produzirá os resultados em `sys.dm_exec_query_profiles`. Para obter mais informações sobre como habilitar a consulta infra-estruturas de criação de perfil, consulte [a infraestrutura de criação de perfil de consulta](../../relational-databases/performance/query-profiling-infrastructure.md).

## <a name="permissions"></a>Permissões  

Na [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], requer `VIEW SERVER STATE` permissão.   
Na [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)], requer o `VIEW DATABASE STATE` permissão no banco de dados.   
   
## <a name="examples"></a>Exemplos  
 Etapa 1: Faça logon em uma sessão na qual você planeja executar a consulta que você analisará com `sys.dm_exec_query_profiles`. Para configurar a consulta para uso de perfil `SET STATISTICS PROFILE ON`. Execute a consulta nessa mesma sessão.  
  
```sql  
--Configure query for profiling with sys.dm_exec_query_profiles  
SET STATISTICS PROFILE ON;  
GO  

--Or enable query profiling globally under SQL Server 2016 SP1 or above (not needed in SQL Server 2019)  
DBCC TRACEON (7412, -1);  
GO 
  
--Next, run your query in this session, or in any other session if query profiling has been enabled globally 
```  
  
 Etapa 2: Faça logon em uma segunda sessão, diferente da sessão em que sua consulta está sendo executada.  
  
 A instrução a seguir resume os progressos realizado pela consulta atualmente em execução na sessão 54. Para fazer isso, ela calcula o número total de linhas de saída de todos as threads para cada nó e o compara com o número estimado de linhas de saída para esse nó.  
  
```sql  
--Run this in a different session than the session in which your query is running. 
--Note that you may need to change session id 54 below with the session id you want to monitor.
SELECT node_id,physical_operator_name, SUM(row_count) row_count, 
  SUM(estimate_row_count) AS estimate_row_count, 
  CAST(SUM(row_count)*100 AS float)/SUM(estimate_row_count)  
FROM sys.dm_exec_query_profiles   
WHERE session_id=54
GROUP BY node_id,physical_operator_name  
ORDER BY node_id;  
```  
  
## <a name="see-also"></a>Consulte também  
 [Exibições e funções de gerenciamento dinâmico &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Funções e exibições de gerenciamento dinâmico relacionadas à execução &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)  
 
