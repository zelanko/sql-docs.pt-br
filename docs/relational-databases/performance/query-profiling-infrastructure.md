---
title: Infraestrutura de criação de perfil de consulta | Microsoft Docs
ms.custom: ''
ms.date: 04/23/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- query plans [SQL Server]
- execution plans [SQL Server]
- query profiling
- lightweight query profiling
- lightweight profiling
- lwp
ms.assetid: 07f8f594-75b4-4591-8c29-d63811d7753e
author: pmasl
ms.author: pelopes
manager: amitban
ms.openlocfilehash: e4c2a2e56f9dab75bfe3873e721ccfca0bd16df3
ms.sourcegitcommit: 64e96ad1ce6c88c814e3789f0fa6e60185ec479c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/27/2020
ms.locfileid: "77705901"
---
# <a name="query-profiling-infrastructure"></a>Infraestrutura de Criação de Perfil de Consulta
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

O [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] fornece a capacidade de acessar informações de runtime nos planos de execução de consulta. Uma das ações mais importantes quando ocorre um problema de desempenho é obter a compreensão precisa sobre a carga de trabalho que está em execução e como o uso de recursos está sendo controlado. Para isso, o acesso ao [plano de execução real](../../relational-databases/performance/display-an-actual-execution-plan.md) é importante.

Enquanto a conclusão da consulta é um pré-requisito para a disponibilidade de um plano de consulta real, as [estatísticas de consulta dinâmica](../../relational-databases/performance/live-query-statistics.md) podem fornecer informações em tempo real sobre o processo de execução de consulta como os fluxos de dados de um [operador de plano de consulta](../../relational-databases/showplan-logical-and-physical-operators-reference.md) para outro. O plano de consulta ao vivo exibe o progresso geral da consulta e as estatísticas de tempo de execução do nível de operador, como o número de linhas produzido, tempo decorrido, progresso do operador, etc. Como esses dados estão disponíveis em tempo real sem a necessidade de aguardar a conclusão da consulta, essas estatísticas de execução são extremamente úteis para depurar problemas de desempenho de consulta, como consultas de execução longa e consultas que são executadas indefinidamente e nunca são concluídas.

## <a name="the-standard-query-execution-statistics-profiling-infrastructure"></a>A infraestrutura de perfil de estatísticas de execução de consulta padrão

A *infraestrutura do perfil de estatísticas de execução de consulta* ou a criação de perfil padrão, deve ser habilitada para coletar informações sobre planos de execução, ou seja, a contagem de linhas, uso de CPU e E/S. Os métodos de coleta de informações de plano de execução a seguir para uma **sessão de destino** aproveitam a infraestrutura de criação de perfil padrão:

- [SET STATISTICS XML](../../t-sql/statements/set-statistics-xml-transact-sql.md) 
- [SET STATISTICS PROFILE](../../t-sql/statements/set-statistics-profile-transact-sql.md)
- [Estatísticas de consulta dinâmica](../../relational-databases/performance/live-query-statistics.md)

> [!NOTE]
> Clicar no botão *Incluir estatísticas de consulta ao vivo* em [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] aproveita a infraestrutura de criação de perfil padrão.    
> Em versões posteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], se a [infraestrutura de criação de perfil leve](#lwp) estiver habilitada, ela será usada por estatísticas de consulta ao vivo, em vez de criação de perfil padrão quando exibida por meio do [Monitor de Atividade](../../relational-databases/performance-monitor/activity-monitor.md) ou consultando diretamente o DMV [exec_query_profiles](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-profiles-transact-sql.md). 

Os métodos de coleta de informações de plano de execução a seguir para **todas as sessão** aproveitam a infraestrutura de criação de perfil padrão:

-  O evento ***query_post_execution_showplan***. Para habilitar eventos estendidos, consulte [Monitor System Activity Using Extended Events](../../relational-databases/extended-events/monitor-system-activity-using-extended-events.md).  
- O evento de rastreamento **Showplan XML** no [Rastreamento do SQL](../../relational-databases/sql-trace/sql-trace.md) e [SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md). Para obter mais informações sobre o evento de rastreamento, confira [Classe de evento Showplan XML](../../relational-databases/event-classes/showplan-xml-event-class.md).

Ao executar uma sessão de eventos estendidos que usa o evento *query_post_execution_showplan*, o DMV [sys.dm_exec_query_profiles](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-profiles-transact-sql.md) também é populado, o que permite estatísticas de consulta dinâmica para todas as sessões, usando o [Monitor de Atividade](../../relational-databases/performance-monitor/activity-monitor.md) ou consultando diretamente o DMV. Para obter mais informações, consulte [Live Query Statistics](../../relational-databases/performance/live-query-statistics.md).

## <a name="lwp"></a> A infraestrutura de criação de perfil de estatísticas de execução de consulta leve

Começando com o [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] SP2 e [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], uma nova *infraestrutura de criação de perfil de estatísticas de execução de consulta leve* ou **criação de perfil leve** foi introduzida. 

> [!NOTE]
> Os procedimentos armazenados compilados nativamente não são compatíveis com a criação de perfil leve.  

### <a name="lightweight-query-execution-statistics-profiling-infrastructure-v1"></a>Infraestrutura de criação de perfil de estatísticas de execução de consulta leve v1

**Aplica-se ao**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] SP2 a [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]). 
  
Começando com o [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] SP2 e [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], a sobrecarga de desempenho para coletar informações sobre planos de execução foi reduzida com a introdução da criação de perfil leve. Ao contrário da criação de perfil padrão, a criação de perfil leve não coleta informações de runtime de CPU. No entanto, a criação de perfil leve ainda coleta informações de uso de E/S e de contagem de linhas.

Um novo evento ***query_thread_profile*** estendido que utiliza a criação de perfil leve também foi introduzido. Esse evento estendido expõe estatísticas de execução por operador, permitindo mais informações sobre o desempenho de cada nó e thread. Uma sessão de exemplo usando este evento estendido pode ser configurada como no exemplo abaixo:

```sql
CREATE EVENT SESSION [NodePerfStats] ON SERVER
ADD EVENT sqlserver.query_thread_profile(
  ACTION(sqlos.scheduler_id,sqlserver.database_id,sqlserver.is_system,
    sqlserver.plan_handle,sqlserver.query_hash_signed,sqlserver.query_plan_hash_signed,
    sqlserver.server_instance_name,sqlserver.session_id,sqlserver.session_nt_username,
    sqlserver.sql_text))
ADD TARGET package0.ring_buffer(SET max_memory=(25600))
WITH (MAX_MEMORY=4096 KB,
  EVENT_RETENTION_MODE=ALLOW_SINGLE_EVENT_LOSS,
  MAX_DISPATCH_LATENCY=30 SECONDS,
  MAX_EVENT_SIZE=0 KB,
  MEMORY_PARTITION_MODE=NONE,
  TRACK_CAUSALITY=OFF,
  STARTUP_STATE=OFF);
```

> [!NOTE]
> Para obter mais informações sobre a sobrecarga de desempenho da criação de perfil de consulta, confira a postagem no blog [Developers Choice: Query progress – anytime, anywhere](https://blogs.msdn.microsoft.com/sql_server_team/query-progress-anytime-anywhere/) (Escolha dos desenvolvedores: consultar o andamento – a qualquer momento, em qualquer lugar). 

Ao executar uma sessão de eventos estendidos que usa o evento *query_thread_profile*, o DMV [sys.dm_exec_query_profiles](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-profiles-transact-sql.md) também é populado usando a criação de perfil leve, o que permite estatísticas de consulta dinâmica para todas as sessões, usando o [Monitor de Atividade](../../relational-databases/performance-monitor/activity-monitor.md) ou consultando diretamente o DMV.

### <a name="lightweight-query-execution-statistics-profiling-infrastructure-v2"></a>Infraestrutura de criação de perfil de estatísticas de execução de consulta leve v2

**Aplica-se ao**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1 a [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]). 

O [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1 inclui uma versão revisada da criação de perfil leve com sobrecarga mínima. A criação de perfil leve também pode ser habilitada globalmente usando o [sinalizador de rastreamento 7412](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) para as versões mencionadas acima em *Aplica-se a*. Um novo DMF [DM exec_query_statistics_xml](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-statistics-xml-transact-sql.md) é introduzido para retornar o plano de execução de consulta para as solicitações em trânsito.

Começando com o [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP2 CU3 e [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] CU11, se a criação de perfil leve não estiver habilitada globalmente, o novo argumento de [dica de consulta USE HINT](../../t-sql/queries/hints-transact-sql-query.md#use_hint)**QUERY_PLAN_PROFILE** poderá ser usado para habilitar a criação de perfil leve no nível da consulta, para qualquer sessão. Quando uma consulta que contém essas nova dica termina, um novo evento estendido ***query_plan_profile*** também é a saída que fornece um plano de execução real XML semelhante ao evento estendido *query_post_execution_showplan*. 

> [!NOTE]
> O evento estendido *query_plan_profile* também se beneficia da criação de perfil leve, mesmo se a dica de consulta não é usada. 

Uma sessão de exemplo usando o evento estendido *query_plan_profile* pode ser configurado como o exemplo a seguir:

```sql
CREATE EVENT SESSION [PerfStats_LWP_Plan] ON SERVER
ADD EVENT sqlserver.query_plan_profile(
  ACTION(sqlos.scheduler_id,sqlserver.database_id,sqlserver.is_system,
    sqlserver.plan_handle,sqlserver.query_hash_signed,sqlserver.query_plan_hash_signed,
    sqlserver.server_instance_name,sqlserver.session_id,sqlserver.session_nt_username,
    sqlserver.sql_text))
ADD TARGET package0.ring_buffer(SET max_memory=(25600))
WITH (MAX_MEMORY=4096 KB,
  EVENT_RETENTION_MODE=ALLOW_SINGLE_EVENT_LOSS,
  MAX_DISPATCH_LATENCY=30 SECONDS,
  MAX_EVENT_SIZE=0 KB,
  MEMORY_PARTITION_MODE=NONE,
  TRACK_CAUSALITY=OFF,
  STARTUP_STATE=OFF);
```

### <a name="lightweight-query-execution-statistics-profiling-infrastructure-v3"></a>Infraestrutura de criação de perfil de estatísticas de execução de consulta leve v3

**Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (começando com [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)]) e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]

[!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] incluem uma versão revisada recentemente da criação de perfil leve coletando informações de contagem de linha de todas as execuções. A criação de perfil leve está habilitada por padrão em [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]. Do [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] em diante, o sinalizador de rastreamento 7412 não tem nenhum efeito. A criação de perfil leve pode ser desabilitada no nível de banco de dados usando a [configuração de escopo do banco de dados](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md) LIGHTWEIGHT_QUERY_PROFILING: `ALTER DATABASE SCOPED CONFIGURATION SET LIGHTWEIGHT_QUERY_PROFILING = OFF;`.

Um novo DMF [sys.dm_exec_query_plan_stats](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-plan-stats-transact-sql.md) é introduzido para retornar o equivalente do último plano de execução real conhecido para a maioria das consultas e é chamado de *últimas estatísticas do plano de consulta*. As últimas estatísticas do plano de consulta podem ser habilitadas no nível de banco de dados usando a [configuração de escopo do banco de dados](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md) LAST_QUERY_PLAN_STATS: `ALTER DATABASE SCOPED CONFIGURATION SET LAST_QUERY_PLAN_STATS = ON;`.

Um novo evento estendido *query_post_execution_plan_profile* coleta o equivalente a um plano de execução real com base em criação de perfil leve, ao contrário de *query_post_execution_showplan*, que usa a criação de perfil padrão. Uma sessão de exemplo usando o evento estendido *query_post_execution_plan_profile* pode ser configurada como o exemplo a seguir:

```sql
CREATE EVENT SESSION [PerfStats_LWP_All_Plans] ON SERVER
ADD EVENT sqlserver.query_post_execution_plan_profile(
  ACTION(sqlos.scheduler_id,sqlserver.database_id,sqlserver.is_system,
    sqlserver.plan_handle,sqlserver.query_hash_signed,sqlserver.query_plan_hash_signed,
    sqlserver.server_instance_name,sqlserver.session_id,sqlserver.session_nt_username,
    sqlserver.sql_text))
ADD TARGET package0.ring_buffer(SET max_memory=(25600))
WITH (MAX_MEMORY=4096 KB,
  EVENT_RETENTION_MODE=ALLOW_SINGLE_EVENT_LOSS,
  MAX_DISPATCH_LATENCY=30 SECONDS,
  MAX_EVENT_SIZE=0 KB,
  MEMORY_PARTITION_MODE=NONE,
  TRACK_CAUSALITY=OFF,
  STARTUP_STATE=OFF);
```

#### <a name="example-1---extended-event-session-using-standard-profiling"></a>Exemplo 1 – sessão de evento estendido usando a criação de perfil padrão

```sql
CREATE EVENT SESSION [QueryPlanOld] ON SERVER 
ADD EVENT sqlserver.query_post_execution_showplan(
    ACTION(sqlos.task_time, sqlserver.database_id, 
    sqlserver.database_name, sqlserver.query_hash_signed, 
    sqlserver.query_plan_hash_signed, sqlserver.sql_text))
ADD TARGET package0.event_file(SET filename = N'C:\Temp\QueryPlanStd.xel')
WITH (MAX_MEMORY=4096 KB, EVENT_RETENTION_MODE=ALLOW_SINGLE_EVENT_LOSS, 
    MAX_DISPATCH_LATENCY=30 SECONDS, MAX_EVENT_SIZE=0 KB, 
    MEMORY_PARTITION_MODE=NONE, TRACK_CAUSALITY=OFF, STARTUP_STATE=OFF);
```

#### <a name="example-2---extended-event-session-using-lightweight-profiling"></a>Exemplo 2 – sessão de evento estendido usando a criação de perfil leve

```sql
CREATE EVENT SESSION [QueryPlanLWP] ON SERVER 
ADD EVENT sqlserver.query_post_execution_plan_profile(
    ACTION(sqlos.task_time, sqlserver.database_id, 
    sqlserver.database_name, sqlserver.query_hash_signed, 
    sqlserver.query_plan_hash_signed, sqlserver.sql_text))
ADD TARGET package0.event_file(SET filename=N'C:\Temp\QueryPlanLWP.xel')
WITH (MAX_MEMORY=4096 KB, EVENT_RETENTION_MODE=ALLOW_SINGLE_EVENT_LOSS, 
    MAX_DISPATCH_LATENCY=30 SECONDS, MAX_EVENT_SIZE=0 KB, 
    MEMORY_PARTITION_MODE=NONE, TRACK_CAUSALITY=OFF, STARTUP_STATE=OFF);
```

## <a name="query-profiling-infrastruture-usage-guidance"></a>Diretrizes de uso da infraestrutura de criação de perfil de consulta
A tabela a seguir resume as ações para habilitar a criação de perfil padrão ou de perfil leve, tanto globalmente (no nível do servidor) como em uma única sessão. Também inclui a versão mais antiga para a qual a ação está disponível. 

|Escopo|Criação de perfil padrão|Criação de perfil leve|
|---------------|---------------|---------------|
|Global|Sessão xEvent com o `query_post_execution_showplan` XE; a partir do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]|Sinalizador de rastreamento 7412; a partir do [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1|
|Global|Rastreamento do SQL e SQL Server Profiler com o evento de rastreamento `Showplan XML`; a partir do SQL Server 2000|Sessão xEvent com o `query_thread_profile` XE; a partir do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] SP2|
|Global|-|Sessão xEvent com o `query_post_execution_plan_profile` XE; a partir do [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)]|
|Session|Use `SET STATISTICS XML ON`; a partir do SQL Server 2000|Use a dica de consulta `QUERY_PLAN_PROFILE` com uma sessão de xEvent com o `query_plan_profile` XE; a partir do [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] CU3 SP2 e do [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] CU11|
|Session|Use `SET STATISTICS PROFILE ON`; a partir do SQL Server 2000|-|
|Session|Clique no botão [Estatísticas de consulta dinâmica](../../relational-databases/performance/live-query-statistics.md) no SSMS; a partir do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] SP2|-|

## <a name="remarks"></a>Comentários

> [!IMPORTANT]
> Devido a um possível AV aleatório ao executar um procedimento armazenado monitorado que faz referência a [sys.dm_exec_query_statistics_xml](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-statistics-xml-transact-sql.md), verifique se [KB 4078596](https://support.microsoft.com/help/4078596) está instalado em [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] e [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)].

Começando com a criação de perfil leve v2 e a baixa sobrecarga, qualquer servidor que não esteja vinculado à CPU poderá executar a criação de perfil leve **continuamente** e permitir que os profissionais de banco de dados explorem qualquer execução a qualquer momento, por exemplo, usando o Monitor de Atividade ou consultando `sys.dm_exec_query_profiles` diretamente e obtenham o plano de consulta com estatísticas de runtime.

Para obter mais informações sobre a sobrecarga de desempenho da criação de perfil de consulta, confira a postagem no blog [Developers Choice: Query progress – anytime, anywhere](https://techcommunity.microsoft.com/t5/SQL-Server/Developers-Choice-Query-progress-anytime-anywhere/ba-p/385004) (Escolha dos desenvolvedores: consultar o andamento – a qualquer momento, em qualquer lugar). 

> [!NOTE]
> Eventos estendidos que aproveitam a criação de perfil leve usarão informações da criação de perfil padrão se a infraestrutura de criação de perfil padrão já estiver habilitada. Por exemplo, uma sessão de evento estendido usando `query_post_execution_showplan` está em execução e outra sessão usando `query_post_execution_plan_profile` é iniciada. A segunda sessão ainda usará informações de criação de perfil padrão.

## <a name="see-also"></a>Consulte Também  
 [Monitorar e ajustar o desempenho](../../relational-databases/performance/monitor-and-tune-for-performance.md)     
 [Ferramentas para monitoramento e ajuste de desempenho](../../relational-databases/performance/performance-monitoring-and-tuning-tools.md)     
 [Abrir o Monitor de Atividade &#40;SQL Server Management Studio&#41;](../../relational-databases/performance-monitor/open-activity-monitor-sql-server-management-studio.md)     
 [Monitor de atividade](../../relational-databases/performance-monitor/activity-monitor.md)     
 [Monitorando o desempenho com o repositório de consultas](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)     
 [Monitorar a atividade do sistema usando Eventos Estendidos](../../relational-databases/extended-events/monitor-system-activity-using-extended-events.md)      
 [sys.dm_exec_query_statistics_xml](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-statistics-xml-transact-sql.md)     
 [sys.dm_exec_query_profiles](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-profiles-transact-sql.md)     
 [Sinalizadores de rastreamento](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)    
 [Referência de operadores físicos e lógicos de plano de execução](../../relational-databases/showplan-logical-and-physical-operators-reference.md)    
 [plano de execução real](../../relational-databases/performance/display-an-actual-execution-plan.md)    
 [Estatísticas de consulta dinâmica](../../relational-databases/performance/live-query-statistics.md)      
