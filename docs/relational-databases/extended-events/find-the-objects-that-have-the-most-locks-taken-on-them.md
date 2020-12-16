---
title: Localizar objetos com mais bloqueios usando Eventos Estendidos
description: Este artigo mostra como localizar os objetos que têm a maioria dos bloqueios. Os administradores de banco de dados podem precisar localizar os objetos mais bloqueados para aprimorar o desempenho do banco de dados.
ms.date: 10/18/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xevents
ms.topic: tutorial
helpviewer_keywords:
- objects [SQL Server], extended events
- xe
- extended events [SQL Server], locks
- objects [SQL Server], locks
ms.assetid: fcbadbda-c91c-43f0-a1b5-601e40110e07
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 522017d6ced6039cd7e5b9a30cf60404eee9249a
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97465497"
---
# <a name="find-the-objects-that-have-the-most-locks-taken-on-them"></a>Localizar os objetos que detêm a maioria dos bloqueios

[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]

Muitas vezes, os administradores de banco de dados precisam identificar a origem de bloqueios que estão obstruindo o desempenho do banco de dados.  
  
Por exemplo, digamos que você esteja monitorando seu servidor de produção quanto a possíveis gargalos. Você suspeita que existem recursos altamente disputados e gostaria de saber quantos bloqueios esses objetos detêm. Uma vez identificados os objetos bloqueados com maior frequência, algumas medidas podem ser tomadas para otimizar o acesso aos objetos disputados.  
  
Para fazer isso, use o Editor de Consultas em [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
### <a name="to-find-the-objects-that-have-the-most-locks"></a>Para localizar os objetos que detêm a maioria dos bloqueios  
  
1. No Editor de Consultas, emita as seguintes instruções:

    ```sql
    -- Find objects in a particular database that have the most
    -- lock acquired. This sample uses AdventureWorksDW2012.
    -- Create the session and add an event and target.
    
    IF EXISTS(SELECT * FROM sys.server_event_sessions WHERE name='LockCounts')
        DROP EVENT session LockCounts ON SERVER;
    GO
    DECLARE @dbid int;
  
    SELECT @dbid = db_id('AdventureWorksDW2012');
  
    DECLARE @sql nvarchar(1024);
    SET @sql = '
        CREATE event session LockCounts ON SERVER
            ADD EVENT sqlserver.lock_acquired (WHERE database_id ='
                + CAST(@dbid AS nvarchar) +')
            ADD TARGET package0.histogram(
                SET filtering_event_name=''sqlserver.lock_acquired'',
                    source_type=0, source=''resource_0'')';
  
    EXEC (@sql);
    GO
    ALTER EVENT session LockCounts ON SERVER
        STATE=start;
    GO
    -- Create a simple workload that takes locks.
    
    USE AdventureWorksDW2012;
    GO
    SELECT TOP 1 * FROM dbo.vAssocSeqLineItems;
    GO
    -- The histogram target output is available from the
    -- sys.dm_xe_session_targets dynamic management view in
    -- XML format.
    -- The following query joins the bucketizing target output with
    -- sys.objects to obtain the object names.
    
    SELECT name, object_id, lock_count
        FROM
        (
        SELECT objstats.value('.','bigint') AS lobject_id,
            objstats.value('@count', 'bigint') AS lock_count
            FROM (
                SELECT CAST(xest.target_data AS XML)
                    LockData
                FROM     sys.dm_xe_session_targets xest
                    JOIN sys.dm_xe_sessions        xes  ON xes.address = xest.event_session_address
                    JOIN sys.server_event_sessions ses  ON xes.name    = ses.name
                WHERE xest.target_name = 'histogram' AND xes.name = 'LockCounts'
                 ) Locks
            CROSS APPLY LockData.nodes('//HistogramTarget/Slot') AS T(objstats)
        ) LockedObjects
        INNER JOIN sys.objects o  ON LockedObjects.lobject_id = o.object_id
        WHERE o.type != 'S' AND o.type = 'U'
        ORDER BY lock_count desc;
    GO
    
    -- Stop the event session.
    
    ALTER EVENT SESSION LockCounts ON SERVER
        state=stop;
    GO
    ```

> [!NOTE]
> O exemplo de código Transact-SQL anterior é executado no SQL Server local, mas pode _não ser bem executado no Banco de Dados SQL do Azure._ As partes principais do exemplo que envolvem Eventos diretamente, como `ADD EVENT sqlserver.lock_acquired`, também funcionam no Banco de Dados SQL do Azure. Porém, os itens preliminares, como `sys.server_event_sessions`, devem ser editados em seus equivalentes do Banco de Dados SQL do Azure como `sys.database_event_sessions` para que o exemplo seja executado.
> Para obter mais informações sobre essas diferenças secundárias entre o SQL Server local versus o Banco de Dados SQL do Azure, confira os seguintes artigos:
> - [Eventos estendidos no Banco de Dados SQL do Azure](/azure/sql-database/sql-database-xevent-db-diff-from-svr#transact-sql-differences)
> - [Objetos do sistema que dão suporte a eventos estendidos](xevents-references-system-objects.md)

Depois que as instruções no script Transact-SQL anterior forem concluídas, a guia **Resultados** do Editor de Consulta exibe as seguintes colunas:
  
- name
- object_id
- lock_count
  
## <a name="see-also"></a>Consulte Também

[CREATE EVENT SESSION &#40;Transact-SQL&#41;](../../t-sql/statements/create-event-session-transact-sql.md)  
[ALTER EVENT SESSION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-event-session-transact-sql.md)  
[sys.dm_xe_session_targets &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-xe-session-targets-transact-sql.md)  
[sys.dm_xe_sessions &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-xe-sessions-transact-sql.md)  
[sys.server_event_sessions &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-event-sessions-transact-sql.md)  
