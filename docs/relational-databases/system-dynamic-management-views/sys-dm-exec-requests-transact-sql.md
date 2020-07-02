---
title: sys. dm_exec_requests (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/01/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_exec_requests_TSQL
- sys.dm_exec_requests
- dm_exec_requests_TSQL
- dm_exec_requests
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_requests dynamic management view
ms.assetid: 4161dc57-f3e7-4492-8972-8cfb77b29643
author: pmasl
ms.author: pelopes
ms.reviewer: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 44c20aeed09468b9f2e0cc7047364f563e463daf
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85734689"
---
# <a name="sysdm_exec_requests-transact-sql"></a>sys.dm_exec_requests (Transact-SQL)

[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

Retorna informações sobre cada solicitação que está sendo executada no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para obter mais informações sobre solicitações, consulte o [Guia de arquitetura de threads e tarefas](../../relational-databases/thread-and-task-architecture-guide.md).
   
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|session_id|**smallint**|ID da sessão a que esta solicitação está relacionada. Não permite valor nulo.|  
|request_id|**int**|ID da solicitação. Exclusiva no contexto da sessão. Não permite valor nulo.|  
|start_time|**datetime**|Carimbo de data e hora em que a solicitação chegou. Não permite valor nulo.|  
|status|**nvarchar(30)**|Status da solicitação. Pode ser um dos seguintes:<br /><br /> Segundo plano<br />Executando<br />Executável<br />Hibernando<br />Suspenso<br /><br /> Não permite valor nulo.|  
|.|**nvarchar(32)**|Identifica o tipo atual de comando que está sendo processado. Os tipos de comando comuns incluem:<br /><br /> SELECT<br />INSERT<br />UPDATE<br />Delete (excluir)<br />BACKUP LOG<br />BACKUP DATABASE<br />DBCC<br />FOR<br /><br /> O texto da solicitação pode ser recuperado usando sys.dm_exec_sql_text com o sql_handle correspondente para a solicitação. Os processos de sistema internos definem o comando com base no tipo de tarefa que eles executam. As tarefas podem incluir o seguinte:<br /><br /> LOCK MONITOR<br />CHECKPOINTLAZY<br />WRITER<br /><br /> Não permite valor nulo.|  
|sql_handle|**varbinary(64)**|É um token que identifica exclusivamente o lote ou o procedimento armazenado do qual a consulta faz parte. Permite valor nulo.| 
|statement_start_offset|**int**|Indica, em bytes, começando com 0, a posição inicial da instrução atualmente em execução para o lote ou objeto persistente em execução no momento. Pode ser usado junto com o `sql_handle` , o `statement_end_offset` e a `sys.dm_exec_sql_text` função de gerenciamento dinâmico para recuperar a instrução atualmente em execução para a solicitação. Permite valor nulo.|  
|statement_end_offset|**int**|Indica, em bytes, começando com 0, a posição final da instrução atualmente em execução para o lote ou objeto persistente em execução no momento. Pode ser usado junto com o `sql_handle` , o `statement_start_offset` e a `sys.dm_exec_sql_text` função de gerenciamento dinâmico para recuperar a instrução atualmente em execução para a solicitação. Permite valor nulo.|  
|plan_handle|**varbinary(64)**|É um token que identifica exclusivamente um plano de execução de consulta para um lote em execução no momento. Permite valor nulo.|  
|database_id|**smallint**|ID do banco de dados no qual a solicitação está em execução. Não permite valor nulo.|  
|user_id|**int**|ID do usuário que enviou a solicitação. Não permite valor nulo.|  
|connection_id|**uniqueidentifier**|ID da conexão em que a solicitação chegou. Permite valor nulo.|  
|blocking_session_id|**smallint**|ID da sessão que está bloqueando a solicitação. Se esta coluna for nula ou igual a 0, a solicitação não será bloqueada ou as informações da sessão da sessão de bloqueio não estarão disponíveis (ou não poderão ser identificadas).<br /><br /> -2 = O recurso de bloqueio pertence a uma transação distribuída órfã.<br /><br /> -3 = O recurso de bloqueio pertence a uma transação de recuperação adiada.<br /><br /> -4 = A ID da sessão do proprietário da trava de bloqueio não pôde ser determinada neste momento devido a transições internas de estado da trava.|  
|wait_type|**nvarchar(60)**|Se a solicitação estiver bloqueada, esta coluna retornará o tipo de espera. Permite valor nulo.<br /><br /> Para obter informações sobre os tipos de esperas, consulte [Sys. dm_os_wait_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md).|  
|wait_time|**int**|Se a solicitação estiver bloqueada, esta coluna retornará a duração, em milissegundos, da espera atual. Não permite valor nulo.|  
|last_wait_type|**nvarchar(60)**|Se esta solicitação tiver sido previamente bloqueada, esta coluna retornará o tipo da última espera. Não permite valor nulo.|  
|wait_resource|**nvarchar(256)**|Se a solicitação estiver bloqueada, esta coluna retornará o recurso pelo qual a solicitação está esperando atualmente. Não permite valor nulo.|  
|open_transaction_count|**int**|Número de transações abertas para esta solicitação. Não permite valor nulo.|  
|open_resultset_count|**int**|Número de conjuntos de resultados abertos para esta solicitação. Não permite valor nulo.|  
|transaction_id|**bigint**|ID da transação na qual esta solicitação é executada. Não permite valor nulo.|  
|context_info|**varbinary(128)**|CONTEXT_INFO valor da sessão. Permite valor nulo.|  
|percent_complete|**real**|Porcentagem de trabalho concluída para os comandos a seguir:<br /><br /> ALTER INDEX REORGANIZE<br />Opção AUTO_SHRINK com ALTER DATABASE<br />BACKUP DATABASE<br />DBCC CHECKDB<br />DBCC CHECKFILEGROUP<br />DBCC CHECKTABLE<br />DBCC INDEXDEFRAG<br />DBCC SHRINKDATABASE<br />DBCC SHRINKFILE<br />RECOVERY<br />RESTORE DATABASE<br />ROLLBACK<br />TDE ENCRYPTION<br /><br /> Não permite valor nulo.|  
|estimated_completion_time|**bigint**|Somente interno. Não permite valor nulo.|  
|cpu_time|**int**|Tempo da CPU, em milissegundos, usado pela solicitação. Não permite valor nulo.|  
|total_elapsed_time|**int**|Tempo total decorrido em milissegundos desde que a solicitação chegou. Não permite valor nulo.|  
|scheduler_id|**int**|ID do agendador que está programando esta solicitação. Não permite valor nulo.|  
|task_address|**varbinary (8)**|Endereço de memória alocado à tarefa associada a esta solicitação. Permite valor nulo.|  
|reads|**bigint**|Número de leituras executadas por esta solicitação. Não permite valor nulo.|  
|writes|**bigint**|Número de gravações executadas por esta solicitação. Não permite valor nulo.|  
|logical_reads|**bigint**|Número de leituras lógicas executadas pela solicitação. Não permite valor nulo.|  
|text_size|**int**|Configuração TEXTSIZE para esta solicitação. Não permite valor nulo.|  
|Linguagem|**nvarchar(128)**|Configuração de idioma para a solicitação. Permite valor nulo.|  
|date_format|**nvarchar (3)**|Configuração DATEFORMAT para a solicitação. Permite valor nulo.|  
|date_first|**smallint**|Configuração DATEFIRST para a solicitação. Não permite valor nulo.|  
|quoted_identifier|**bit**|1 = QUOTED_IDENTIFIER é ON para a solicitação. Caso contrário, é 0.<br /><br /> Não permite valor nulo.|  
|arithabort|**bit**|1 = configuração ARITHABORT é ON para a solicitação. Caso contrário, é 0.<br /><br /> Não permite valor nulo.|  
|ansi_null_dflt_on|**bit**|1 = configuração ANSI_NULL_DFLT_ON é ON para a solicitação. Caso contrário, é 0.<br /><br /> Não permite valor nulo.|  
|ansi_defaults|**bit**|1 = configuração ANSI_DEFAULTS é ON para a solicitação. Caso contrário, é 0.<br /><br /> Não permite valor nulo.|  
|ansi_warnings|**bit**|1 = configuração ANSI_WARNINGS é ON para a solicitação. Caso contrário, é 0.<br /><br /> Não permite valor nulo.|  
|ansi_padding|**bit**|1 = configuração ANSI_PADDING é ON para a solicitação.<br /><br /> Caso contrário, é 0.<br /><br /> Não permite valor nulo.|  
|ansi_nulls|**bit**|1 = configuração ANSI_NULLS é ON para a solicitação. Caso contrário, é 0.<br /><br /> Não permite valor nulo.|  
|concat_null_yields_null|**bit**|1 = configuração CONCAT_NULL_YIELDS_NULL é ON para a solicitação. Caso contrário, é 0.<br /><br /> Não permite valor nulo.|  
|transaction_isolation_level|**smallint**|Nível de isolamento com que a transação desta solicitação é criada. Não permite valor nulo.<br /> 0 = Não Especificado<br /> 1 = Leitura Não Confirmada<br /> 2 = Leitura Confirmada<br /> 3 = Repetível<br /> 4 = Serializável<br /> 5 = Instantâneo|  
|lock_timeout|**int**|Tempo limite de bloqueio em milissegundos desta solicitação. Não permite valor nulo.|  
|deadlock_priority|**int**|Configuração DEADLOCK_PRIORITY da solicitação. Não permite valor nulo.|  
|row_count|**bigint**|Número de linhas que foram retornadas ao cliente por esta solicitação. Não permite valor nulo.|  
|prev_error|**int**|Último erro ocorrido durante a execução da solicitação. Não permite valor nulo.|  
|nest_level|**int**|Nível de aninhamento atual do código sendo executado na solicitação. Não permite valor nulo.|  
|granted_query_memory|**int**|Número de páginas alocadas à execução de uma consulta na solicitação. Não permite valor nulo.|  
|executing_managed_code|**bit**|Indica se uma solicitação específica está atualmente executando objetos de Common Language runtime, como rotinas, tipos e gatilhos. É definida para todo o tempo em que um objeto de Common Language runtime estiver na pilha, mesmo durante a execução de [!INCLUDE[tsql](../../includes/tsql-md.md)] no Common Language runtime. Não permite valor nulo.|  
|group_id|**int**|ID do grupo de carga de trabalho a que pertence esta consulta. Não permite valor nulo.|  
|query_hash|**binário (8)**|Valor de hash binário calculado na consulta e usado para identificar consultas com lógica semelhante. Você pode usar o hash de consulta para determinar o recurso de agregação usado para consultas que são diferentes apenas nos valores literais.|  
|query_plan_hash|**binário (8)**|Valor de hash binário calculado no plano de execução de consulta e usado para identificar planos de execução de consulta semelhantes. Você pode usar o hash de plano de consulta para localizar o custo cumulativo de consultas com planos de execução semelhantes.|  
|statement_sql_handle|**varbinary(64)**|**Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior.<br /><br /> Identificador SQL da consulta individual.<br /><br />Esta coluna será nula se Repositório de Consultas não estiver habilitada para o banco de dados. |  
|statement_context_id|**bigint**|**Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior.<br /><br /> A chave estrangeira opcional para sys. query_context_settings.<br /><br />Esta coluna será nula se Repositório de Consultas não estiver habilitada para o banco de dados. |  
|dop |**int** |**Aplica-se a**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] e posterior.<br /><br /> O grau de paralelismo da consulta. |  
|parallel_worker_count |**int** |**Aplica-se a**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] e posterior.<br /><br /> O número de operadores paralelos reservados se esta for uma consulta paralela.  |  
|external_script_request_id |**uniqueidentifier** |**Aplica-se a**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] e posterior.<br /><br /> A ID de solicitação de script externo associada à solicitação atual. |  
|is_resumable |**bit** |**Aplica-se a**: [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] e posterior.<br /><br /> Indica se a solicitação é uma operação de índice retomável. |  
|page_resource |**binário (8)** |**Aplica-se ao**: [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)]<br /><br /> Uma representação hexadecimal de 8 bytes do recurso de página se a `wait_resource` coluna contiver uma página. Para obter mais informações, consulte [Sys. fn_PageResCracker](../../relational-databases/system-functions/sys-fn-pagerescracker-transact-sql.md). |  
|page_server_reads|**bigint**|**Aplica-se a**: hiperescala do banco de dados SQL do Azure<br /><br /> Número de leituras de servidor de página executadas por essa solicitação. Não permite valor nulo.|  
| &nbsp; | &nbsp; | &nbsp; |

## <a name="remarks"></a>Comentários 
Para executar código fora do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (por exemplo, procedimentos armazenados estendidos e consultas distribuídas), um thread deve ser executado fora do controle de um agendador não preventivo. Para fazer isso, um trabalhador muda para o modo preventivo. Os valores de tempo retornados por essa exibição de gerenciamento dinâmico não incluem o tempo gasto no modo preventivo.

Ao executar solicitações paralelas no [modo de linha](../../relational-databases/query-processing-architecture-guide.md#row-mode-execution), [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o atribui um thread de trabalho para coordenar os threads de trabalho responsáveis por concluir tarefas atribuídas a eles. Nesse DMV, apenas o thread do coordenador fica visível para a solicitação. As colunas **leituras**, **gravações** **logical_reads**e **row_count** **não são atualizadas** para o thread do coordenador. As colunas **wait_type**, **wait_time**, **last_wait_type**, **wait_resource**e **granted_query_memory** são **atualizadas somente** para o thread do coordenador. Para saber mais, confira o [Guia de arquitetura de threads e tarefas](../../relational-databases/thread-and-task-architecture-guide.md).

## <a name="permissions"></a>Permissões
Se o usuário tiver a `VIEW SERVER STATE` permissão no servidor, o usuário verá todas as sessões em execução na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ; caso contrário, o usuário verá apenas a sessão atual. `VIEW SERVER STATE`Não pode ser concedido no banco de dados SQL do Azure, portanto, `sys.dm_exec_requests` está sempre limitado à conexão atual.

Em cenários Always on, se a réplica secundária estiver definida como **somente intenção de leitura**, a conexão com o secundário deverá especificar sua intenção de aplicativo nos parâmetros da cadeia de conexão adicionando `applicationintent=readonly` . Caso contrário, a verificação de acesso `sys.dm_exec_requests` não passará para bancos de dados no grupo de disponibilidade, mesmo que a `VIEW SERVER STATE` permissão esteja presente.

  
## <a name="examples"></a>Exemplos  
  
### <a name="a-finding-the-query-text-for-a-running-batch"></a>a. Localizando o texto da consulta para um lote em execução

 O exemplo a seguir consulta `sys.dm_exec_requests` para localizar a consulta interessante e copiar o `sql_handle` da saída.  

```sql
SELECT * FROM sys.dm_exec_requests;  
GO  
```  

Em seguida, para obter o texto da instrução, use o `sql_handle` copiado com a função do sistema `sys.dm_exec_sql_text(sql_handle)`.  

```sql
SELECT * FROM sys.dm_exec_sql_text(< copied sql_handle >);  
GO  
```

### <a name="b-finding-all-locks-that-a-running-batch-is-holding"></a>B. Localizando todos os bloqueios que estão sendo mantidos por um lote em execução

O exemplo a seguir consulta **Sys. dm_exec_requests** para localizar o lote interessante e copiar seu `transaction_id` da saída.

```sql
SELECT * FROM sys.dm_exec_requests;  
GO
```

Em seguida, para localizar informações de bloqueio, use o copiado `transaction_id` com a função de sistema **sys. dm_tran_locks**.  

```sql
SELECT * FROM sys.dm_tran_locks
WHERE request_owner_type = N'TRANSACTION'
    AND request_owner_id = < copied transaction_id >;
GO  
```

### <a name="c-finding-all-currently-blocked-requests"></a>C. Localizando todas as solicitações bloqueadas atualmente

O exemplo a seguir consulta **Sys. dm_exec_requests** para encontrar informações sobre solicitações bloqueadas.  

```sql
SELECT session_id ,status ,blocking_session_id  
    ,wait_type ,wait_time ,wait_resource
    ,transaction_id
FROM sys.dm_exec_requests
WHERE status = N'suspended';  
GO  
```  

### <a name="d-ordering-existing-requests-by-cpu"></a>D. Ordenando solicitações existentes por CPU

```sql
SELECT 
   req.session_id
   , req.start_time
   , cpu_time 'cpu_time_ms'
   , object_name(st.objectid,st.dbid) 'ObjectName' 
   , substring
      (REPLACE
        (REPLACE
          (SUBSTRING
            (ST.text
            , (req.statement_start_offset/2) + 1
            , (
               (CASE statement_end_offset
                  WHEN -1
                  THEN DATALENGTH(ST.text)  
                  ELSE req.statement_end_offset
                  END
                    - req.statement_start_offset)/2) + 1)
       , CHAR(10), ' '), CHAR(13), ' '), 1, 512)  AS statement_text  
FROM sys.dm_exec_requests AS req  
   CROSS APPLY sys.dm_exec_sql_text(req.sql_handle) as ST
   ORDER BY cpu_time desc;
GO
```

## <a name="see-also"></a>Consulte Também
[Funções e exibições de gerenciamento dinâmico](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)     
[Funções e exibições de gerenciamento dinâmico relacionadas à execução](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)      
[sys. dm_os_memory_clerks](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-clerks-transact-sql.md)     
[sys. dm_os_sys_info](../../relational-databases/system-dynamic-management-views/sys-dm-os-sys-info-transact-sql.md)     
[sys. dm_exec_query_memory_grants](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-memory-grants-transact-sql.md)    
[sys. dm_exec_query_plan](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-plan-transact-sql.md)    
[sys. dm_exec_sql_text](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sql-text-transact-sql.md)      
[SQL Server, objeto SQL Statistics](../../relational-databases/performance-monitor/sql-server-sql-statistics-object.md)     
[Guia de arquitetura de processamento de consultas](../../relational-databases/query-processing-architecture-guide.md#DOP)       
[Guia de arquitetura de threads e tarefas](../../relational-databases/thread-and-task-architecture-guide.md)    
