---
description: sp_update_jobstep (Transact-SQL)
title: sp_update_jobstep (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_update_jobstep
- sp_update_jobstep_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_update_jobstep
ms.assetid: e158802c-c347-4a5d-bf75-c03e5ae56e6b
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 0a7161fd475b1fdac439e1c14e59034de2d7bbfe
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88473512"
---
# <a name="sp_update_jobstep-transact-sql"></a>sp_update_jobstep (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Altera a configuração para uma etapa em um trabalho que é usado para executar atividades automatizadas.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_update_jobstep   
     {   [@job_id =] job_id   
       | [@job_name =] 'job_name' } ,  
     [@step_id =] step_id  
     [ , [@step_name =] 'step_name' ]  
     [ , [@subsystem =] 'subsystem' ]   
     [ , [@command =] 'command' ]  
     [ , [@additional_parameters =] 'parameters' ]  
     [ , [@cmdexec_success_code =] success_code ]  
     [ , [@on_success_action =] success_action ]   
     [ , [@on_success_step_id =] success_step_id ]  
     [ , [@on_fail_action =] fail_action ]   
     [ , [@on_fail_step_id =] fail_step_id ]  
     [ , [@server =] 'server' ]   
     [ , [@database_name =] 'database' ]  
     [ , [@database_user_name =] 'user' ]   
     [ , [@retry_attempts =] retry_attempts ]  
     [ , [@retry_interval =] retry_interval ]   
     [ , [@os_run_priority =] run_priority ]  
     [ , [@output_file_name =] 'file_name' ]   
     [ , [@flags =] flags ]  
     [ ,  {   [ @proxy_id = ] proxy_id   
            | [ @proxy_name = ] 'proxy_name' }   
```  
  
## <a name="arguments"></a>Argumentos  
`[ @job_id = ] job_id` O número de identificação do trabalho ao qual a etapa pertence. *job_id*é **uniqueidentifier**, com um padrão de NULL. *Job_id* ou *job_name* deve ser especificado, mas ambos não podem ser especificados.  
  
`[ @job_name = ] 'job_name'` O nome do trabalho ao qual a etapa pertence. *job_name*é **sysname**, com um padrão de NULL. *Job_id* ou *job_name* deve ser especificado, mas ambos não podem ser especificados.  
  
`[ @step_id = ] step_id` O número de identificação da etapa de trabalho a ser modificada. Esse número não pode ser alterado. *step_id*é **int**, sem padrão.  
  
`[ @step_name = ] 'step_name'` É um novo nome para a etapa. *step_name*é **sysname**, com um padrão de NULL.  
  
`[ @subsystem = ] 'subsystem'` O subsistema usado pelo agente de Microsoft SQL Server para executar o *comando*. *subsistema* é **nvarchar (40)**, com um padrão de NULL.  
  
`[ @command = ] 'command'` Os comandos a serem executados por meio do *subsistema*. o *comando* é **nvarchar (max)**, com um padrão de NULL.  
  
`[ @additional_parameters = ] 'parameters'` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
`[ @cmdexec_success_code = ] success_code` O valor retornado por um comando de subsistema **CmdExec** para indicar que o *comando* foi executado com êxito. *success_code* é **int**, com um padrão de NULL.  
  
`[ @on_success_action = ] success_action` A ação a ser executada se a etapa for concluída com sucesso. *success_action* é **tinyint**, com um padrão de NULL, e pode ser um desses valores.  
  
|Valor|Descrição (ação)|  
|-----------|----------------------------|  
|**1**|Sair com êxito.|  
|**2**|Sair com falha.|  
|**3**|Ir para a próxima etapa.|  
|**4**|Vá para a etapa *success_step_id.*|  
  
`[ @on_success_step_id = ] success_step_id` O número de identificação da etapa neste trabalho a ser executado se a etapa for bem sucedido e *success_action* for **4**. *success_step_id* é **int**, com um padrão de NULL.  
  
`[ @on_fail_action = ] fail_action` A ação a ser executada se a etapa falhar. *fail_action* é **tinyint**, com um padrão de NULL e pode ter um desses valores.  
  
|Valor|Descrição (ação)|  
|-----------|----------------------------|  
|**1**|Sair com êxito.|  
|**2**|Sair com falha.|  
|**3**|Ir para a próxima etapa.|  
|**4**|Vá para a etapa *fail_step_id * *.*|  
  
`[ @on_fail_step_id = ] fail_step_id` O número de identificação da etapa neste trabalho a ser executado se a etapa falhar e *fail_action* for **4**. *fail_step_id* é **int**, com um padrão de NULL.  
  
`[ @server = ] 'server'`[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]o *servidor* é **nvarchar (128)**, com um padrão de NULL.  
  
`[ @database_name = ] 'database'` O nome do banco de dados no qual executar uma [!INCLUDE[tsql](../../includes/tsql-md.md)] etapa. o *banco de dados*é **sysname**. Os nomes entre colchetes ([ ]) não são permitidos. O valor padrão é NULL.  
  
`[ @database_user_name = ] 'user'` O nome da conta de usuário a ser usada ao executar uma [!INCLUDE[tsql](../../includes/tsql-md.md)] etapa. o *usuário*é **sysname**, com um padrão de NULL.  
  
`[ @retry_attempts = ] retry_attempts` O número de tentativas de repetição a serem usadas se essa etapa falhar. *retry_attempts*é **int**, com um padrão de NULL.  
  
`[ @retry_interval = ] retry_interval` A quantidade de tempo em minutos entre as tentativas de repetição. *retry_interval* é **int**, com um padrão de NULL.  
  
`[ @os_run_priority = ] run_priority` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
`[ @output_file_name = ] 'file_name'` O nome do arquivo no qual a saída desta etapa é salva. *file_name* é **nvarchar (200)**, com um padrão de NULL. Este parâmetro é válido somente com comandos executados nos subsistemas do [!INCLUDE[tsql](../../includes/tsql-md.md)] ou CmdExec.  
  
 Para definir output_file_name de volta para NULL, você deve definir *output_file_name* como uma cadeia de caracteres vazia (' ') ou com uma cadeia de caracteres em branco, mas não pode usar a função **Char (32)** . Por exemplo, defina este argumento como uma cadeia de caracteres vazios como segue:  
  
 **@output_file_name = ' '**  
  
`[ @flags = ] flags` Uma opção que controla o comportamento. *flags* é **int**e pode ser um desses valores.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**0** (padrão)|Substitui o arquivo de saída.|  
|**2**|Anexa a um arquivo de saída|  
|**4**|Grava a saída da etapa de trabalho do Transact-SQL no histórico de etapas|  
|**8**|Grava o log na tabela (substitui o histórico existente)|  
|**16**|Grava o log na tabela (anexa ao histórico existente)|  
  
`[ @proxy_id = ] proxy_id` O número de ID do proxy que a etapa de trabalho executa como. *proxy_id* é do tipo **int**, com um padrão de NULL. Se nenhum *proxy_id* for especificado, nenhum *proxy_name* será especificado e nenhum *user_name* será especificado, a etapa de trabalho será executada como a conta de serviço para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  
  
`[ @proxy_name = ] 'proxy_name'` O nome do proxy que a etapa de trabalho executa como. *proxy_name* é o tipo **sysname**, com um padrão de NULL. Se nenhum *proxy_id* for especificado, nenhum *proxy_name* será especificado e nenhum *user_name* será especificado, a etapa de trabalho será executada como a conta de serviço para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_update_jobstep** deve ser executado do banco de dados **msdb** .  
  
 A atualização de uma etapa de trabalho incrementa o número de versão do trabalho.  
  
## <a name="permissions"></a>Permissões  
 Por padrão, os membros da função de servidor fixa **sysadmin** podem executar este procedimento armazenado. Deve ser concedida a outros usuários uma das seguintes funções de banco de dados fixas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent no banco de dados **msdb** :  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 Para obter detalhes sobre as permissões dessas funções, consulte [Funções de banco de dados fixas do SQL Server Agent](../../ssms/agent/sql-server-agent-fixed-database-roles.md).  
  
 Somente os membros do **sysadmin** podem atualizar uma etapa de trabalho de propriedade de outro usuário.  
  
 Se a etapa de trabalho requer acesso a um proxy, o criador da etapa de trabalho deve ter acesso ao proxy para a etapa de trabalho. Todos os subsistemas, menos o Transact-SQL, requerem uma conta proxy. Os membros de **sysadmin** têm acesso a todos os proxies e podem usar a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] conta de serviço do Agent para o proxy.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir altera o número de tentativas da primeira etapa do trabalho `Weekly Sales Data Backup`. Depois de executar este exemplo, o número de tentativas será `10`.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_update_jobstep  
    @job_name = N'Weekly Sales Data Backup',  
    @step_id = 1,  
    @retry_attempts = 10 ;  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Exibir ou modificar trabalhos](../../ssms/agent/view-or-modify-jobs.md)   
 [&#41;&#40;Transact-SQL de sp_delete_jobstep ](../../relational-databases/system-stored-procedures/sp-delete-jobstep-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_help_jobstep ](../../relational-databases/system-stored-procedures/sp-help-jobstep-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
