---
title: KILL (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/31/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: t-sql|language-elements
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- KILL_TSQL
- KILL
dev_langs:
- TSQL
helpviewer_keywords:
- WITH STATUSONLY option
- terminating distributed transactions
- distributed transactions [SQL Server], terminating
- in-doubt transactions
- IDs [SQL Server], user processes
- ending distributed transactions [SQL Server]
- stopping distributed transactions
- session IDs [SQL Server]
- system process termination [SQL Server]
- stopping processes
- ending processes [SQL Server]
- UOW [SQL Server]
- orphaned transactions [SQL Server]
- unit of work [SQL Server]
- process termination [SQL Server]
- KILL statement
- terminating process
ms.assetid: 071cf260-c794-4b45-adc0-0e64097938c0
caps.latest.revision: 61
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Active
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 6460d8ae1b48e99305b6361a29b47ba06e9213f1
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="kill-transact-sql"></a>KILL (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Finaliza um processo de usuário baseado na ID da sessão ou na UOW (unidade de trabalho). Se a ID da sessão ou UOW especificada tiver muito trabalho a ser desfeito, a instrução KILL poderá demorar algum tempo para ser concluída, principalmente quando envolver a reversão de uma transação longa.  
  
 A instrução KILL pode ser usada para finalizar uma conexão normal, o que finaliza internamente as transações associadas à ID da sessão especificada. A instrução também pode ser usada para finalizar transações distribuídas órfãs e incertas quando o MS DTC ([!INCLUDE[msCoName](../../includes/msconame-md.md)] Distributed Transaction Coordinator) estiver em uso.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
-- Syntax for SQL Server  
  
KILL { session ID | UOW } [ WITH STATUSONLY ]   
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
KILL 'session_id'  
[;]   
```  
  
## <a name="arguments"></a>Argumentos  
 *session ID*  
 É a ID da sessão do processo a ser finalizado. *session ID* é um inteiro exclusivo (**int**) que é atribuído a cada conexão de usuário quando esta é estabelecida. O valor do ID de sessão está vinculado à conexão pela duração da conexão. Quando a conexão for finalizada, o valor inteiro será liberado e poderá ser reatribuído a uma nova conexão.  
A seguinte consulta pode ajudá-lo a identificar o `session_id` que você deseja encerrar:  
 ```sql  
 SELECT conn.session_id, host_name, program_name,
     nt_domain, login_name, connect_time, last_request_end_time 
FROM sys.dm_exec_sessions AS sess
JOIN sys.dm_exec_connections AS conn
    ON sess.session_id = conn.session_id;
```  
  
*UOW*  
**Aplica-se a**: (do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
 Identifica a ID da UOW (Unidade de Trabalho) de transações distribuídas. *UOW* é um GUID que pode ser obtido na coluna request_owner_guid da exibição de gerenciamento dinâmico sys.dm_tran_locks. *UOW* também pode ser obtido no log de erros ou por meio do monitor do MS DTC. Para obter mais informações sobre como monitorar transações distribuídas, consulte a documentação do MS DTC.  
  
 Use KILL *UOW* para encerrar transações distribuídas órfãs. Essas transações não são associadas a nenhum ID de sessão real, mas em vez disso, são associadas artificialmente ao ID de sessão = '-2'. Esse ID de sessão facilita a identificação de transações órfãs pela consulta da coluna de ID de sessão nas exibições de gerenciamento dinâmico sys.dm_tran_locks, sys.dm_exec_sessions ou sys.dm_exec_requests.  
  
 WITH STATUSONLY  
 Gera um relatório de progresso sobre uma *session ID* especificada ou uma *UOW* que está sendo revertida devido a uma instrução KILL anterior. KILL WITH STATUSONLY não encerra nem reverte a *session ID* ou a *UOW*; o comando somente exibe o andamento atual da reversão.  
  
## <a name="remarks"></a>Remarks  
 KILL normalmente é usado para finalizar um processo que esteja bloqueando outros processos importantes com bloqueios ou um processo que esteja executando uma consulta que use recursos necessários do sistema. Os processos do sistema e os processos que estejam executando um procedimento armazenado estendido não podem ser finalizados.  
  
 Use KILL com cuidado, especialmente quando processos críticos estiverem em execução. Você não pode eliminar seu próprio processo. Outros processos que você não deve eliminar incluem:  
  
-   AWAITING COMMAND  
-   CHECKPOINT SLEEP  
-   LAZY WRITER  
-   LOCK MONITOR  
-   SIGNAL HANDLER  
  
Use @@SPID para exibir o valor de ID da sessão atual.  
  
 Para obter um relatório de valores de ID de sessão ativas, é possível consultar a coluna session_id das exibições de gerenciamento dinâmico sys.dm_tran_locks, sys.dm_exec_sessions e sys.dm_exec_requests. Você também pode exibir a coluna SPID que é retornada pelo procedimento armazenado de sistema sp_who. Se uma reversão estiver em andamento para um SPID específico, a coluna cmd do conjunto de resultados sp_who desse SPID indicará KILLED/ROLLBACK.  
  
 Quando uma conexão específica tiver um bloqueio em um recurso de banco de dados e bloquear o andamento de outra conexão, a ID da sessão da conexão responsável pelo bloqueio será mostrada na coluna `blocking_session_id` de `sys.dm_exec_requests` ou na coluna `blk` retornada por `sp_who`.  
  
 O comando KILL pode ser usado para resolver transações distribuídas em dúvida. Essas transações são do tipo distribuídas não resolvidas que ocorrem devido a reinícios não planejados do servidor de banco de dados ou do coordenador do MS DTC. Para obter mais informações sobre transações incertas, consulte a seção "Confirmação de duas fases" em [Usar transações marcadas para recuperar bancos de dados relacionados de forma consistente &#40;modelo de recuperação completa&#41;](../../relational-databases/backup-restore/use-marked-transactions-to-recover-related-databases-consistently.md).  
  
## <a name="using-with-statusonly"></a>Usando WITH STATUSONLY  
 KILL WITH STATUSONLY gera um relatório apenas se a ID de sessão ou a UOW está sendo atualmente revertida devido a uma instrução KILL *session ID*|*UOW* anterior. O relatório de progresso indica a quantidade concluída da reversão (em porcentagem) e o período de tempo restante estimado (em segundos), no seguinte formato:  
  
 `Spid|UOW <xxx>: Transaction rollback in progress. Estimated rollback completion: <yy>% Estimated time left: <zz> seconds`  
  
 Se a reversão da ID da sessão ou da UOW tiver sido concluída quando a instrução KILL *session ID*|*UOW* WITH STATUSONLY for executada ou se nenhuma ID da sessão ou UOW estiver sendo revertida, KILL *session ID*|*UOW* WITH STATUSONLY retornará o seguinte erro:  
  
 ```
"Msg 6120, Level 16, State 1, Line 1"  
"Status report cannot be obtained. Rollback operation for Process ID <session ID> is not in progress."
```  
  
 O mesmo relatório de progresso pode ser obtido pela repetição da mesma instrução KILL *session ID*|*UOW* sem usar a opção WITH STATUSONLY. No entanto, isso não é recomendável. A repetição de uma instrução KILL *session ID* pode encerrar um novo processo se a reversão foi concluída e a ID da sessão foi reatribuída a uma nova tarefa antes que a nova instrução KILL seja executada. A especificação de WITH STATUSONLY impede que isso ocorra.  
  
## <a name="permissions"></a>Permissões  
 **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:** exige a permissão ALTER ANY CONNECTION. ALTER ANY CONNECTION é incluída com associação nas funções de servidor fixas sysadmin ou processadmin.  
  
 **[!INCLUDE[ssSDS](../../includes/sssds-md.md)]:** exige a permissão KILL DATABASE CONNECTION. O logon da entidade de segurança no nível do servidor tem a permissão KILL DATABASE CONNECTION.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-using-kill-to-terminate-a-session"></a>A. Usando KILL para finalizar uma sessão  
 O exemplo a seguir mostra como finalizar o ID de sessão `53`.  
  
```sql  
KILL 53;  
GO  
```  
  
### <a name="b-using-kill-session-id-with-statusonly-to-obtain-a-progress-report"></a>B. Usando ID de sessão KILL WITH STATUSONLY para obter um relatório de andamento  
 O exemplo a seguir gera um status do processo de reversão para o ID de sessão específico.  
  
```sql  
KILL 54;  
KILL 54 WITH STATUSONLY;  
GO  
  
--This is the progress report.  
spid 54: Transaction rollback in progress. Estimated rollback completion: 80% Estimated time left: 10 seconds.  
```  
  
### <a name="c-using-kill-to-terminate-an-orphaned-distributed-transaction"></a>C. Usando KILL para finalizar uma transação distribuída órfã  
 O exemplo a seguir mostra como encerrar uma transação distribuída órfã (ID de sessão = -2) com uma *UOW* igual a `D5499C66-E398-45CA-BF7E-DC9C194B48CF`.  
  
```sql  
KILL 'D5499C66-E398-45CA-BF7E-DC9C194B48CF';  
```  

  
## <a name="see-also"></a>Consulte Também  
 [KILL STATS JOB &#40;Transact-SQL&#41;](../../t-sql/language-elements/kill-stats-job-transact-sql.md)   
 [KILL QUERY NOTIFICATION SUBSCRIPTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/kill-query-notification-subscription-transact-sql.md)   
 [Funções internas &#40;Transact-SQL&#41;](~/t-sql/functions/functions.md)   
 [SHUTDOWN &#40;Transact-SQL&#41;](../../t-sql/language-elements/shutdown-transact-sql.md)   
 [@@SPID &#40;Transact-SQL&#41;](../../t-sql/functions/spid-transact-sql.md)   
 [sys.dm_exec_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)   
 [sys.dm_exec_sessions &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sessions-transact-sql.md)   
 [sys.dm_tran_locks &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-tran-locks-transact-sql.md)   
 [sp_lock &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-lock-transact-sql.md)   
 [sp_who &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-who-transact-sql.md)  
  
  
