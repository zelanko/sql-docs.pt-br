---
title: Determinar quais consultas estão mantendo bloqueios | Microsoft Docs
ms.custom: ''
ms.date: 10/18/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xevents
ms.topic: tutorial
helpviewer_keywords:
- queries [SQL Server], extended events
- queries [SQL Server], holding locks
- xe
- extended events [SQL Server], locks
- extended events [SQL Server], holding locks
ms.assetid: bdfce092-3cf1-4b5e-99d5-fd8c6f9ad560
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 7f6bdf2ed730330e03068473e5db9f82015caacc
ms.sourcegitcommit: 49fd567e28bfd6e94efafbab422eaed4ce913eb3
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/18/2019
ms.locfileid: "72589979"
---
# <a name="determine-which-queries-are-holding-locks"></a>Determinar quais consultas estão mantendo bloqueios

[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

Muitas vezes, os administradores de banco de dados precisam identificar a origem de bloqueios que estão obstruindo o desempenho do banco de dados.  
  
Por exemplo, digamos que você suspeite que um problema de desempenho em seu servidor pode estar sendo causado por bloqueios. Ao consultar sys.dm_exec_requests, você descobre várias sessões em modo suspenso, com um tipo de espera indicativo de que o recurso que se está aguardando é um bloqueio.  
  
Você consulta sys.dm_tran_locks e os resultados mostram que há vários bloqueios pendentes, mas as sessões às quais eles foram concedidos não têm nenhuma solicitação ativa exibida em sys.dm_exec_requests.  
  
Este exemplo demonstra um método de determinar qual consulta efetuou o bloqueio, o plano da consulta e a pilha [!INCLUDE[tsql](../../includes/tsql-md.md)] no momento em que o bloqueio foi efetuado. Este exemplo também ilustra como o destino de emparelhamento é usado em uma sessão de Eventos Estendidos.  
  
A realização dessa tarefa envolve o uso do Editor de Consultas no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para aplicar o procedimento a seguir.  
  
> [!NOTE]  
>  Este exemplo usa o banco de dados AdventureWorks.  
  
### <a name="to-determine-which-queries-are-holding-locks"></a>Para determinar quais consultas estão mantendo bloqueios  
  
1.  No Editor de Consultas, emita as seguintes instruções:  
  
    ```sql
    -- Perform cleanup.   
    IF EXISTS(SELECT * FROM sys.server_event_sessions WHERE name='FindBlockers')  
        DROP EVENT SESSION FindBlockers ON SERVER  
    GO  
    -- Use dynamic SQL to create the event session and allow creating a -- predicate on the AdventureWorks database id.  
    --  
    DECLARE @dbid int  
  
    SELECT @dbid = db_id('AdventureWorks')  
  
    IF @dbid IS NULL  
    BEGIN  
        RAISERROR('AdventureWorks is not installed. Install AdventureWorks before proceeding', 17, 1)  
        RETURN  
    END  
  
    DECLARE @sql nvarchar(1024)  
    SET @sql = '  
    CREATE EVENT SESSION FindBlockers ON SERVER  
    ADD EVENT sqlserver.lock_acquired   
        (action   
            ( sqlserver.sql_text, sqlserver.database_id, sqlserver.tsql_stack,  
             sqlserver.plan_handle, sqlserver.session_id)  
        WHERE ( database_id=' + cast(@dbid as nvarchar) + ' AND resource_0!=0)   
        ),  
    ADD EVENT sqlserver.lock_released   
        (WHERE ( database_id=' + cast(@dbid as nvarchar) + ' AND resource_0!=0 ))  
    ADD TARGET package0.pair_matching   
        ( SET begin_event=''sqlserver.lock_acquired'',   
                begin_matching_columns=''database_id, resource_0, resource_1, resource_2, transaction_id, mode'',   
                end_event=''sqlserver.lock_released'',   
                end_matching_columns=''database_id, resource_0, resource_1, resource_2, transaction_id, mode'',  
        respond_to_memory_pressure=1)  
    WITH (max_dispatch_latency = 1 seconds)'  
  
    EXEC (@sql)  
    --   
    -- Create the metadata for the event session  
    -- Start the event session  
    --  
    ALTER EVENT SESSION FindBlockers ON SERVER  
    STATE = START  
    ```  
  
2.  Após a execução de uma carga de trabalho no servidor, emita as instruções a seguir no Editor de Consultas para descobrir se ainda há consultas mantendo bloqueios.  
  
    ```sql
    --  
    -- The pair matching targets report current unpaired events using   
    -- the sys.dm_xe_session_targets dynamic management view (DMV)  
    -- in XML format.  
    -- The following query retrieves the data from the DMV and stores  
    -- key data in a temporary table to speed subsequent access and  
    -- retrieval.  
    --  
    SELECT   
    objlocks.value('(action[@name="session_id"]/value)[1]', 'int')  
            AS session_id,  
        objlocks.value('(data[@name="database_id"]/value)[1]', 'int')   
            AS database_id,  
        objlocks.value('(data[@name="resource_type"]/text)[1]', 'nvarchar(50)' )   
            AS resource_type,  
        objlocks.value('(data[@name="resource_0"]/value)[1]', 'bigint')   
            AS resource_0,  
        objlocks.value('(data[@name="resource_1"]/value)[1]', 'bigint')   
            AS resource_1,  
        objlocks.value('(data[@name="resource_2"]/value)[1]', 'bigint')   
            AS resource_2,  
        objlocks.value('(data[@name="mode"]/text)[1]', 'nvarchar(50)')   
            AS mode,  
        objlocks.value('(action[@name="sql_text"]/value)[1]', 'varchar(MAX)')   
            AS sql_text,  
        CAST(objlocks.value('(action[@name="plan_handle"]/value)[1]', 'varchar(MAX)') AS xml)   
            AS plan_handle,      
        CAST(objlocks.value('(action[@name="tsql_stack"]/value)[1]', 'varchar(MAX)') AS xml)   
            AS tsql_stack  
    INTO #unmatched_locks  
    FROM (  
        SELECT CAST(xest.target_data as xml)   
            lockinfo  
        FROM sys.dm_xe_session_targets xest  
        JOIN sys.dm_xe_sessions xes ON xes.address = xest.event_session_address  
        WHERE xest.target_name = 'pair_matching' AND xes.name = 'FindBlockers'  
    ) heldlocks  
    CROSS APPLY lockinfo.nodes('//event[@name="lock_acquired"]') AS T(objlocks)  
  
    --  
    -- Join the data acquired from the pairing target with other   
    -- DMVs to return provide additional information about blockers  
    --  
    SELECT ul.*  
        FROM #unmatched_locks ul  
        INNER JOIN sys.dm_tran_locks tl ON ul.database_id = tl.resource_database_id AND ul.resource_type = tl.resource_type  
        WHERE resource_0 IS NOT NULL  
        AND session_id IN   
            (SELECT blocking_session_id FROM sys.dm_exec_requests WHERE blocking_session_id != 0)  
        AND tl.request_status='wait'  
        AND REPLACE(ul.mode, 'LCK_M_', '' ) = tl.request_mode  
  
    ```  
  
3.  Depois de identificar os problemas, descarte todas as tabelas temporárias e a sessão de evento.  
  
    ```sql
    DROP TABLE #unmatched_locks  
    DROP EVENT SESSION FindBlockers ON SERVER  
    ```  

> [!NOTE]
> Os exemplos de código Transact-SQL anteriores são executados no SQL Server local, mas podem _não ser bem executados no Banco de Dados SQL do Azure._ As partes principais do exemplo que envolvem Eventos diretamente, como `ADD EVENT sqlserver.lock_acquired`, também funcionam no Banco de Dados SQL do Azure. Porém, os itens preliminares, como `sys.server_event_sessions`, devem ser editados em seus equivalentes do Banco de Dados SQL do Azure como `sys.database_event_sessions` para que o exemplo seja executado.
> Para obter mais informações sobre essas diferenças secundárias entre o SQL Server local versus o Banco de Dados SQL do Azure, confira os seguintes artigos:
> - [Eventos estendidos no Banco de Dados SQL do Azure](/azure/sql-database/sql-database-xevent-db-diff-from-svr#transact-sql-differences)
> - [Objetos do sistema que dão suporte a eventos estendidos](xevents-references-system-objects.md)

## <a name="see-also"></a>Consulte Também  
 [CREATE EVENT SESSION &#40;Transact-SQL&#41;](../../t-sql/statements/create-event-session-transact-sql.md)   
 [ALTER EVENT SESSION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-event-session-transact-sql.md)   
 [DROP EVENT SESSION &#40;Transact-SQL&#41;](../../t-sql/statements/drop-event-session-transact-sql.md)   
 [sys.dm_xe_session_targets &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-xe-session-targets-transact-sql.md)   
 [sys.dm_xe_sessions &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-xe-sessions-transact-sql.md)  
  
  
