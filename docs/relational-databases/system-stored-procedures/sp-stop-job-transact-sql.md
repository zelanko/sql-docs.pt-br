---
title: sp_stop_job (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/01/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_stop_job_TSQL
- sp_stop_job
dev_langs:
- TSQL
helpviewer_keywords:
- sp_stop_job
ms.assetid: 64b4cc75-99a0-421e-b418-94e37595bbb0
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: eda439b53c72e41154d4891495470fc271028aee
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/27/2019
ms.locfileid: "58529508"
---
# <a name="spstopjob-transact-sql"></a>sp_stop_job (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Instrui o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent a parar a execução de um trabalho.  

  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_stop_job   
      [@job_name =] 'job_name'  
    | [@job_id =] job_id   
    | [@originating_server =] 'master_server'  
    | [@server_name =] 'target_server'  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @job_name = ] 'job_name'` O nome do trabalho a ser interrompido. *job_name* está **sysname**, com um padrão NULL.  
  
`[ @job_id = ] job_id` O número de identificação do trabalho a ser interrompido. *job_id* está **uniqueidentifier**, com um padrão NULL.  
  
`[ @originating_server = ] 'master_server'` O nome do servidor mestre. Se for especificado, todos os trabalhos multisservidor serão interrompidos. *master_server* está **nvarchar (128)**, com um padrão NULL. Especifique esse parâmetro somente ao chamar **sp_stop_job** em um servidor de destino.  
  
> [!NOTE]  
>  Apenas um dos três primeiros parâmetros pode ser especificado.  
  
`[ @server_name = ] 'target_server'` O nome do servidor de destino específico no qual interromper um trabalho multisservidor. *target_server* está **nvarchar (128)**, com um padrão NULL. Especifique esse parâmetro somente ao chamar **sp_stop_job** em um servidor mestre para um trabalho multisservidor.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 None  
  
## <a name="remarks"></a>Comentários  
 **sp_stop_job** envia um sinal de parada para o banco de dados. Alguns processos podem ser interrompidos imediatamente e alguns devem atingir um ponto estável (ou um ponto de entrada para o caminho do código) antes que eles possam interromper. Algumas instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] longas como BACKUP, RESTORE e alguns comandos DBCC podem levar muito tempo para terminar. Quando eles estiverem em execução, ele pode demorar um pouco antes do trabalho é cancelado. A interrupção de um trabalho faz com que uma entrada "Trabalho Cancelado" seja registrada no histórico de trabalho.  
  
 Se um trabalho estiver executando atualmente uma etapa do tipo **CmdExec** ou **PowerShell**, o processo em execução (por exemplo, MyProgram.exe) será forçado a terminar prematuramente. O fim prematuro pode resultar em comportamento imprevisível, como arquivos em uso pelo processo serem mantidos abertos. Consequentemente, **sp_stop_job** deve ser usado somente em circunstâncias extremas se o trabalho contiver etapas do tipo **CmdExec** ou **PowerShell**.  
  
## <a name="permissions"></a>Permissões  
 Por padrão, os membros da função de servidor fixa **sysadmin** podem executar este procedimento armazenado. Deve ser concedida a outros usuários uma das seguintes funções de banco de dados fixas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent no banco de dados **msdb** :  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 Para obter detalhes sobre as permissões dessas funções, consulte [Funções de banco de dados fixas do SQL Server Agent](../../ssms/agent/sql-server-agent-fixed-database-roles.md).  
  
 Os membros **SQLAgentUserRole** e **SQLAgentReaderRole** só podem parar trabalhos que possuem. Os membros **SQLAgentOperatorRole** pode interromper todos os trabalhos locais, incluindo aqueles que pertencem a outros usuários. Os membros **sysadmin** podem parar todos os trabalhos locais e multisservidor.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir para um trabalho denominado `Weekly Sales Data Backup`.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_stop_job  
    N'Weekly Sales Data Backup' ;  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [sp_delete_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-job-transact-sql.md)   
 [sp_help_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-job-transact-sql.md)   
 [sp_start_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-start-job-transact-sql.md)   
 [sp_update_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-update-job-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
