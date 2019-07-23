---
title: KILL (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/31/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
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
author: rothja
ms.author: jroth
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 89e1a4d6a9d55caa910a0a7de5349dd06dd60269
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68122283"
---
# <a name="kill-transact-sql"></a>KILL (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Encerra um processo de usuário baseado na ID da sessão ou na UOW (unidade de trabalho). Se a ID da sessão ou UOW especificada tiver muito trabalho a ser desfeito, a instrução KILL poderá demorar um pouco para ser concluída. O processo levará mais tempo para ser concluído, especialmente quando envolver reversão de uma transação longa.  
  
KILL encerra uma conexão normal que, internamente, interrompe as transações que estão associadas à ID de sessão especificada. Às vezes, o Coordenador de Transações Distribuídas da [!INCLUDE[msCoName](../../includes/msconame-md.md)] (MS DTC) pode estar em uso. Se o MS DTC estiver em uso, você também poderá usar a instrução para encerrar transações distribuídas órfãs e incertas.  
  
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
_session ID_  
É a ID da sessão do processo a ser encerrado. _session ID_ é um inteiro exclusivo (**int**) que é atribuído a cada conexão de usuário quando esta é estabelecida. O valor do ID de sessão está vinculado à conexão pela duração da conexão. Quando a conexão for finalizada, o valor inteiro será liberado e poderá ser reatribuído a uma nova conexão.  
A seguinte consulta pode ajudá-lo a identificar o `session_id` que você deseja encerrar:  
 ```sql  
 SELECT conn.session_id, host_name, program_name,
     nt_domain, login_name, connect_time, last_request_end_time 
FROM sys.dm_exec_sessions AS sess
JOIN sys.dm_exec_connections AS conn
    ON sess.session_id = conn.session_id;
```  
  
_UOW_  
**Aplica-se a**: (do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
Identifica a ID da UOW (Unidade de Trabalho) de transações distribuídas. _UOW_ é um GUID que pode ser obtido na coluna request_owner_guid da exibição de gerenciamento dinâmico sys.dm_tran_locks. _UOW_ também pode ser obtido no log de erros ou por meio do monitor do MS DTC. Para obter mais informações sobre como monitorar transações distribuídas, consulte a documentação do MS DTC.  
  
Use KILL _UOW_ para interromper transações distribuídas órfãs. Essas transações não são associadas a qualquer ID de sessão real, mas em vez disso, são associadas artificialmente à ID de sessão = '-2'. Esse ID de sessão facilita a identificação de transações órfãs pela consulta da coluna de ID de sessão nas exibições de gerenciamento dinâmico sys.dm_tran_locks, sys.dm_exec_sessions ou sys.dm_exec_requests.  
  
WITH STATUSONLY  
Gera um relatório de progresso sobre uma _ID de sessão_ ou _UOW_ especificada que está sendo revertida devido a uma instrução KILL anterior. KILL WITH STATUSONLY não encerra nem reverte a _ID de sessão_ ou _UOW_. O comando exibe somente o progresso atual da reversão.  
  
## <a name="remarks"></a>Remarks  
KILL normalmente é usado para encerrar um processo que está bloqueando outros processos importantes com bloqueios. KILL também pode ser usada para interromper um processo que está executando uma consulta que está usando recursos necessários do sistema. Os processos do sistema e os processos executando um procedimento armazenado estendido não podem ser encerrados.  
  
Use KILL com cuidado, especialmente quando processos críticos estiverem em execução. Você não pode encerrar o seu próprio processo. Assim como não deve encerrar os seguintes processos:  
  
-   AWAITING COMMAND  
-   CHECKPOINT SLEEP  
-   LAZY WRITER  
-   LOCK MONITOR  
-   SIGNAL HANDLER  
  
Use @@SPID para exibir o valor de ID da sessão atual.  
  
Para obter um relatório de valores de ID de sessão ativos, consulte a coluna session_id das exibições de gerenciamento dinâmico sys.dm_tran_locks, sys.dm_exec_sessions e sys.dm_exec_requests. Você também pode exibir a coluna SPID que é retornada pelo procedimento armazenado do sistema sp_who. Se uma reversão estiver em andamento para um SPID específico, a coluna cmd do conjunto de resultados sp_who desse SPID indicará KILLED/ROLLBACK.  
  
Quando uma conexão específica tiver um bloqueio em um recurso de banco de dados e bloquear o andamento de outra conexão, a ID da sessão da conexão responsável pelo bloqueio será mostrada na coluna `blocking_session_id` de `sys.dm_exec_requests` ou na coluna `blk` retornada por `sp_who`.  
  
O comando KILL pode ser usado para resolver transações distribuídas em dúvida. Essas transações são do tipo distribuídas não resolvidas que ocorrem devido a reinícios não planejados do servidor de banco de dados ou do coordenador do MS DTC. Para obter mais informações sobre transações incertas, consulte a seção "Confirmação de duas fases" em [Usar transações marcadas para recuperar bancos de dados relacionados de forma consistente &#40;modelo de recuperação completa&#41;](../../relational-databases/backup-restore/use-marked-transactions-to-recover-related-databases-consistently.md).  
  
## <a name="using-with-statusonly"></a>Usando WITH STATUSONLY  
KILL WITH STATUSONLY vai gerar um relatório se a ID de sessão ou a UOW for revertida devido a uma instrução KILL _session ID_|_UOW_ anterior. O relatório de progresso indica a quantidade concluída da reversão (em porcentagem) e o período de tempo restante estimado (em segundos). O relatório indica isso da seguinte forma:  
  
`Spid|UOW <xxx>: Transaction rollback in progress. Estimated rollback completion: <yy>% Estimated time left: <zz> seconds`  
  
Se a reversão da ID de sessão ou UOW for concluída antes que a instrução KILL _session ID_|_UOW_ WITH STATUSONLY seja executada, KILL _session ID_|_UOW_ WITH STATUSONLY retornará o seguinte erro:  
  
```
"Msg 6120, Level 16, State 1, Line 1"  
"Status report cannot be obtained. Rollback operation for Process ID <session ID> is not in progress."
```  
Esse erro também ocorrerá se nenhuma ID de sessão ou UOW estiver sendo revertida


O mesmo relatório de status pode ser obtido pela repetição da mesma instrução KILL _session ID_|_UOW_ sem usar a opção WITH STATUSONLY. No entanto, não é recomendável repetir a opção dessa maneira. Se você repetir a instrução KILL _session ID_, o novo processo poderá ser interrompido se a reversão for concluída e a ID de sessão for reatribuída a uma nova tarefa antes que a nova instrução KILL seja executada. Evite que o novo processo seja interrompido especificando WITH STATUSONLY.  
  
## <a name="permissions"></a>Permissões  
**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:** Exige a permissão ALTER ANY CONNECTION. ALTER ANY CONNECTION é incluída com associação nas funções de servidor fixas sysadmin ou processadmin.  
  
**[!INCLUDE[ssSDS](../../includes/sssds-md.md)]:** Exige a permissão KILL DATABASE CONNECTION. O logon da entidade de segurança no nível do servidor tem a permissão KILL DATABASE CONNECTION.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-using-kill-to-stop-a-session"></a>A. Usar KILL para interromper uma sessão  
 O exemplo a seguir mostra como interromper a ID de sessão `53`.  
  
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
  
### <a name="c-using-kill-to-stop-an-orphaned-distributed-transaction"></a>C. Usar KILL para interromper uma transação distribuída órfã  
O exemplo a seguir mostra como interromper uma transação distribuída órfã (ID de sessão = -2) com uma *UOW* igual a `D5499C66-E398-45CA-BF7E-DC9C194B48CF`.  
  
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
  
  
