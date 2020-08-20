---
description: sys.dm_os_tasks (Transact-SQL)
title: sys. dm_os_tasks (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/13/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_os_tasks
- sys.dm_os_tasks_TSQL
- dm_os_tasks_TSQL
- dm_os_tasks
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_tasks dynamic management view
ms.assetid: 180a3c41-e71b-4670-819d-85ea7ef98bac
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: efad6c04a5a2f2e2705b24f639fd798197a2b26d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88493599"
---
# <a name="sysdm_os_tasks-transact-sql"></a>sys.dm_os_tasks (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Retorna uma linha para cada tarefa que está ativa na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Uma tarefa é a unidade básica de execução no SQL Server. Exemplos de tarefas incluem uma consulta, um logon, um logoff e tarefas do sistema, como atividade de limpeza de fantasma, atividade de ponto de verificação, gravador de log, atividade de refazer paralela. Para obter mais informações sobre tarefas, consulte o [Guia de arquitetura de threads e tarefas](../../relational-databases/thread-and-task-architecture-guide.md).
  
> [!NOTE]  
> Para chamá-lo de [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] ou [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] , use o nome **Sys. dm_pdw_nodes_os_tasks**.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**task_address**|**varbinary (8)**|Endereço de memória do objeto.|  
|**task_state**|**nvarchar(60)**|O estado da tarefa. Pode ser um dos seguintes:<br /><br /> PENDING: Esperando por um thread de trabalho.<br /><br /> RUNNABLE: Executável, mas esperando receber um quantum.<br /><br /> RUNNING: Atualmente em execução no agendador.<br /><br /> SUSPENDED: Tem um trabalhador, mas está esperando por um evento.<br /><br /> DONE: Concluído.<br /><br /> SPINLOOP: Preso em um spinlock.|  
|**context_switches_count**|**int**|Número de alternâncias de contexto de agendador que esta tarefa completou.|  
|**pending_io_count**|**int**|Número de E/Ss físicas executadas por esta tarefa.|  
|**pending_io_byte_count**|**bigint**|Contagem total de bytes de E/Ss que são executadas por esta tarefa.|  
|**pending_io_byte_average**|**int**|Contagem média de bytes de E/Ss que são executadas por esta tarefa.|  
|**scheduler_id**|**int**|ID do agendador pai. Este é um identificador das informações de agendador para esta tarefa. Para obter mais informações, consulte [Sys. dm_os_schedulers &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-schedulers-transact-sql.md).|  
|**session_id**|**smallint**|ID da sessão que está associado à tarefa.|  
|**exec_context_id**|**int**|ID do contexto de execução que está associado à tarefa.|  
|**request_id**|**int**|ID da solicitação da tarefa. Para obter mais informações, consulte [Sys. dm_exec_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md).|  
|**worker_address**|**varbinary (8)**|Endereço de memória do trabalhador que está executando a tarefa.<br /><br /> NULL = A tarefa está esperando que um trabalhador possa ser executado ou a execução da tarefa foi recém-concluída.<br /><br /> Para obter mais informações, consulte [Sys. dm_os_workers &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-workers-transact-sql.md).|  
|**host_address**|**varbinary (8)**|Endereço de memória do host.<br /><br /> 0 = A hospedagem não foi usada para criar a tarefa. Isto ajuda a identificar o host que foi usado para criar esta tarefa.<br /><br /> Para obter mais informações, consulte [Sys. dm_os_hosts &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-hosts-transact-sql.md).|  
|**parent_task_address**|**varbinary (8)**|Endereço de memória da tarefa que é pai do objeto.|  
|**pdw_node_id**|**int**|**Aplica-se a**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] , [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> O identificador do nó em que essa distribuição está.|  
  
## <a name="permissions"></a>Permissões
Ativado [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] , requer `VIEW SERVER STATE` permissão.   
Nas [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] camadas Premium, o requer a `VIEW DATABASE STATE` permissão no banco de dados. Nas [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] camadas Standard e Basic, o requer o  **administrador do servidor** ou uma conta de **administrador do Azure Active Directory** .   

## <a name="examples"></a>Exemplos  
  
### <a name="a-monitoring-parallel-requests"></a>a. Monitorando solicitações paralelas  
 Para solicitações executadas em paralelo, você verá várias linhas para a mesma combinação de ( \<**session_id**> , \<**request_id**> ). Use a consulta a seguir para localizar a [opção de configuração de servidor definir o grau máximo de paralelismo](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md) para todas as solicitações ativas.  
  
> [!NOTE]  
>  Um **request_id** é exclusivo dentro de uma sessão.  
  
```sql  
SELECT  
    task_address,  
    task_state,  
    context_switches_count,  
    pending_io_count,  
    pending_io_byte_count,  
    pending_io_byte_average,  
    scheduler_id,  
    session_id,  
    exec_context_id,  
    request_id,  
    worker_address,  
    host_address  
  FROM sys.dm_os_tasks  
  ORDER BY session_id, request_id;  
```  
  
### <a name="b-associating-session-ids-with-windows-threads"></a>B. Associando IDs de sessão a threads do Windows  
 Você pode usar a consulta a seguir para associar um valor de ID de sessão a um ID de thread do Windows. Depois, poderá monitorar o desempenho do thread no Monitor de Desempenho do Windows. A consulta a seguir não retorna informações de sessões que estão suspensas.  
  
```sql  
SELECT STasks.session_id, SThreads.os_thread_id  
  FROM sys.dm_os_tasks AS STasks  
  INNER JOIN sys.dm_os_threads AS SThreads  
    ON STasks.worker_address = SThreads.worker_address  
  WHERE STasks.session_id IS NOT NULL  
  ORDER BY STasks.session_id;  
GO  
```  

## <a name="see-also"></a>Consulte Também  
[SQL Server exibições de gerenciamento dinâmico relacionadas ao sistema operacional &#40;&#41;Transact-SQL ](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)    
[Guia de arquitetura de thread e tarefa](../../relational-databases/thread-and-task-architecture-guide.md)     
  


