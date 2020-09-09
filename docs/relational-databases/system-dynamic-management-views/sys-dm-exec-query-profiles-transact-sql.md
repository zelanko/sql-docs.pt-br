---
description: sys.dm_exec_query_profiles (Transact-SQL)
title: sys. dm_exec_query_profiles (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/25/2019
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
author: markingmyname
ms.author: maghan
monikerRange: =azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 2b761064191f26a05d565e673428221afb4805b1
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89548574"
---
# <a name="sysdm_exec_query_profiles-transact-sql"></a>sys.dm_exec_query_profiles (Transact-SQL)
[!INCLUDE[sql-asdb-asdbmi](../../includes/applies-to-version/sql-asdb-asdbmi.md)]

Monitora o progresso da consulta em tempo real, enquanto a consulta está em execução. Por exemplo, use este DMV para determinar que parte da consulta está executando lentamente. Adicione esse DMV com outros DMVs de sistema usando as colunas identificadas no campo de descrição. Ou, adicione esse DMV com outros contadores de desempenho (como o Monitor de Desempenho, xperf) usando colunas de carimbo de data/hora.  
  
## <a name="table-returned"></a>Tabela retornada  
Os contadores retornados são por operador por thread. Os resultados são dinâmicos e não correspondem aos resultados das opções existentes, como `SET STATISTICS XML ON` o que cria apenas a saída quando a consulta é concluída.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|session_id|**smallint**|Identifica a sessão na qual esta consulta é executada. Referencia dm_exec_sessions.session_id.|  
|request_id|**int**|Identifica a solicitação de destino. Referencia dm_exec_sessions.request_id.|  
|sql_handle|**varbinary(64)**|É um token que identifica exclusivamente o lote ou o procedimento armazenado do qual a consulta faz parte. Referencia dm_exec_query_stats.sql_handle.|  
|plan_handle|**varbinary(64)**|É um token que identifica exclusivamente um plano de execução de consulta para um lote que foi executado e seu plano reside no cache de planos ou está em execução no momento. Faz referência a dm_exec_query_stats. plan_handle.|  
|physical_operator_name|**nvarchar(256)**|Nome do operador físico.|  
|node_id|**int**|Identifica um nó do operador na árvore de consulta.|  
|thread_id|**int**|Distingue os threads (para uma consulta paralela) que pertencem ao mesmo nó do operador de consulta.|  
|task_address|**varbinary (8)**|Identifica a tarefa do sistema operacional SQL que esse thread está usando. Referencia dm_os_tasks.task_address.|  
|row_count|**bigint**|Número de linhas retornadas pelo operador até o momento.|  
|rewind_count|**bigint**|Número de retrocessos até o momento.|  
|rebind_count|**bigint**|Número de reassociações até o momento.|  
|end_of_scan_count|**bigint**|Número de término de exames até o momento.|  
|estimate_row_count|**bigint**|Número estimado de linhas. Pode ser útil comparar estimated_row_count com o row_count real.|  
|first_active_time|**bigint**|A hora, em milissegundos, em que operador foi chamado primeiro.|  
|last_active_time|**bigint**|A hora, em milissegundos, em que operador foi chamado por último.|  
|open_time|**bigint**|Carimbo de data/hora quando aberto (em milissegundos).|  
|first_row_time|**bigint**|Carimbo de data/hora quando a primeira linha foi aberta (em milissegundos).|  
|last_row_time|**bigint**|Carimbo de data/hora quando a última linha foi aberta (em milissegundos).|  
|close_time|**bigint**|Carimbo de data/hora quando fechado (em milissegundos).|  
|elapsed_time_ms|**bigint**|Tempo total decorrido (em milissegundos) usado pelas operações do nó de destino até o momento.|  
|cpu_time_ms|**bigint**|Tempo total de CPU (em milissegundos) usado pelas operações do nó de destino até o momento.|  
|database_id|**smallint**|ID do banco de dados que contém o objeto no qual as leituras e gravações estão sendo realizadas.|  
|object_id|**int**|O identificador do objeto no qual as leituras e gravações estão sendo realizadas. Referências sys.objects.object_id.|  
|index_id|**int**|O índice (se houver) no qual o conjunto de linhas é aberto.|  
|scan_count|**bigint**|Número de verificações de tabela/índice até o momento.|  
|logical_read_count|**bigint**|Número de leituras lógicas até o momento.|  
|physical_read_count|**bigint**|Número de leituras físicas até o momento.|  
|read_ahead_count|**bigint**|Número de read-aheads até o momento.|  
|write_page_count|**bigint**|Número de gravações de página até o momento devido ao derramamento.|  
|lob_logical_read_count|**bigint**|Número de leituras lógicas LOB até o momento.|  
|lob_physical_read_count|**bigint**|Número de leituras físicas LOB até o momento.|  
|lob_read_ahead_count|**bigint**|Número de read-aheads LOB até o momento.|  
|segment_read_count|**int**|Número de read-aheads de segmento até o momento.|  
|segment_skip_count|**int**|Número de segmentos ignorados até o momento.| 
|actual_read_row_count|**bigint**|Número de linhas lidas por um operador antes da aplicação do predicado residuais.| 
|estimated_read_row_count|**bigint**|**Aplica-se a:** A partir do [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] SP1. <br/>Número estimado de linhas a serem lidas por um operador antes da aplicação do predicado residuais.|  
  
## <a name="general-remarks"></a>Comentários gerais  
 Se o nó do plano de consulta não tiver nenhuma e/s, todos os contadores relacionados à e/s serão definidos como NULL.  
  
 Os contadores relacionados à e/s relatados por essa DMV são mais granulares do que aqueles relatados pelo `SET STATISTICS IO` das duas maneiras a seguir:  
  
-   `SET STATISTICS IO` agrupa os contadores de todas as e/s para uma determinada tabela juntas. Com essa DMV, você obterá contadores separados para cada nó no plano de consulta que executa a e/s na tabela.  
  
-   Se houver uma varredura paralela, este DMV relata os contadores para cada um das threads paralelas que trabalham na varredura.
 
A partir [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] do SP1, a *infraestrutura de criação de perfil de estatísticas de execução de consulta padrão* existe lado a lado com uma infraestrutura de criação de perfil de estatísticas de execução de *consulta leve*. `SET STATISTICS XML ON` e `SET STATISTICS PROFILE ON` sempre use a *infraestrutura de criação de perfil de estatísticas de execução de consulta padrão*. Para `sys.dm_exec_query_profiles` que o seja populado, uma das infraestruturas de criação de perfil de consulta deve ser habilitada. Para obter mais informações, confira [Infraestrutura de Criação de Perfil de Consulta](../../relational-databases/performance/query-profiling-infrastructure.md).    

>[!NOTE]
> A consulta em investigação precisa ser iniciada **depois** que a infraestrutura de criação de perfil de consulta tiver sido habilitada, habilitá-la após a consulta iniciada não produzirá resultados no `sys.dm_exec_query_profiles` . Para saber mais sobre como habilitar as infraestruturas de criação de perfil de consulta, confira [infraestrutura de criação de perfil de consulta](../../relational-databases/performance/query-profiling-infrastructure.md).

## <a name="permissions"></a>Permissões  
No [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] e SQL instância gerenciada do Azure, requer `VIEW DATABASE STATE` permissão e associação da `db_owner` função de banco de dados.   
Nas [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] camadas Premium, o requer a `VIEW DATABASE STATE` permissão no banco de dados. Nas [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] camadas Standard e Basic, o requer o  **administrador do servidor** ou uma conta de **administrador do Azure Active Directory** .   
   
## <a name="examples"></a>Exemplos  
 Etapa 1: faça logon em uma sessão na qual você planeja executar a consulta com a qual irá analisar `sys.dm_exec_query_profiles` . Para configurar a consulta para uso de criação de perfil `SET STATISTICS PROFILE ON` . Execute a consulta nessa mesma sessão.  
  
```sql  
--Configure query for profiling with sys.dm_exec_query_profiles  
SET STATISTICS PROFILE ON;  
GO  

--Or enable query profiling globally under SQL Server 2016 SP1 or above (not needed in SQL Server 2019)  
DBCC TRACEON (7412, -1);  
GO 
  
--Next, run your query in this session, or in any other session if query profiling has been enabled globally 
```  
  
 Etapa 2: faça logon em uma segunda sessão que seja diferente da sessão em que a consulta está em execução.  
  
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
  
## <a name="see-also"></a>Consulte Também  
 [Exibições e funções de gerenciamento dinâmico &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Funções e exibições de gerenciamento dinâmico relacionadas à execução &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)  
 
