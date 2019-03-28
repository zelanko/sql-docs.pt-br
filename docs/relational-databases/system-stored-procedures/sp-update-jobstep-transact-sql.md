---
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
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f1ab6c1408b9f9c2de2e4070ab35e34ea8a458df
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/27/2019
ms.locfileid: "58526758"
---
# <a name="spupdatejobstep-transact-sql"></a>sp_update_jobstep (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Altera a configuração para uma etapa em um trabalho que é usado para executar atividades automatizadas.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
`[ @job_id = ] job_id` O número de identificação do trabalho ao qual a etapa pertence. *job_id*está **uniqueidentifier**, com um padrão NULL. Qualquer um dos *job_id* ou *job_name* deve ser especificado, mas não podem ser especificados.  
  
`[ @job_name = ] 'job_name'` O nome do trabalho ao qual a etapa pertence. *job_name*está **sysname**, com um padrão NULL. Qualquer um dos *job_id* ou *job_name* deve ser especificado, mas não podem ser especificados.  
  
`[ @step_id = ] step_id` O número de identificação da etapa de trabalho a ser modificado. Esse número não pode ser alterado. *step_id*está **int**, sem padrão.  
  
`[ @step_name = ] 'step_name'` É um novo nome para a etapa. *step_name*está **sysname**, com um padrão NULL.  
  
`[ @subsystem = ] 'subsystem'` O subsistema usado pelo Microsoft SQL Server Agent para executar *comando*. *subsistema* está **nvarchar(40)**, com um padrão NULL.  
  
`[ @command = ] 'command'` O comando a ser executado por meio *subsistema*. *comando* está **nvarchar (max)**, com um padrão NULL.  
  
`[ @additional_parameters = ] 'parameters'` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
`[ @cmdexec_success_code = ] success_code` O valor retornado por uma **CmdExec** comando de subsistema para indicar que *comando* foi executada com êxito. *success_code* está **int**, com um padrão NULL.  
  
`[ @on_success_action = ] success_action` A ação a ser executada se a etapa tiver êxito. *success_action* é **tinyint**, com um padrão de NULL, e pode ser um destes valores.  
  
|Valor|Descrição (ação)|  
|-----------|----------------------------|  
|**1**|Sair com êxito.|  
|**2**|Sair com falha.|  
|**3**|Ir para a próxima etapa.|  
|**4**|Vá para a etapa *success_step_id.*|  
  
`[ @on_success_step_id = ] success_step_id` O número de identificação da etapa neste trabalho a ser executado se a etapa tiver êxito e *success_action* é **4**. *success_step_id* está **int**, com um padrão NULL.  
  
`[ @on_fail_action = ] fail_action` A ação a ser executada se a etapa falhar. *fail_action* está **tinyint**, com um padrão de NULL e pode ter um destes valores.  
  
|Valor|Descrição (ação)|  
|-----------|----------------------------|  
|**1**|Sair com êxito.|  
|**2**|Sair com falha.|  
|**3**|Ir para a próxima etapa.|  
|**4**|Vá para a etapa *fail_step_id * *.*|  
  
`[ @on_fail_step_id = ] fail_step_id` O número de identificação da etapa neste trabalho a ser executado se a etapa falhar e *fail_action* é **4**. *fail_step_id* está **int**, com um padrão NULL.  
  
`[ @server = ] 'server'` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)] *servidor* está **nvarchar (128)**, com um padrão NULL.  
  
`[ @database_name = ] 'database'` O nome do banco de dados no qual executar um [!INCLUDE[tsql](../../includes/tsql-md.md)] etapa. *banco de dados*está **sysname**. Os nomes entre colchetes ([ ]) não são permitidos. O valor padrão é NULL.  
  
`[ @database_user_name = ] 'user'` O nome da conta de usuário para usar ao executar um [!INCLUDE[tsql](../../includes/tsql-md.md)] etapa. *usuário*está **sysname**, com um padrão NULL.  
  
`[ @retry_attempts = ] retry_attempts` O número de novas tentativas a ser usado se a etapa atual falhar. *retry_attempts*está **int**, com um padrão NULL.  
  
`[ @retry_interval = ] retry_interval` A quantidade de tempo em minutos entre as tentativas de repetição. *intervalo_de_repetição* está **int**, com um padrão NULL.  
  
`[ @os_run_priority = ] run_priority` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
`[ @output_file_name = ] 'file_name'` O nome do arquivo no qual a saída desta etapa é salvo. *file_name* está **nvarchar(200)**, com um padrão NULL. Este parâmetro é válido somente com comandos executados nos subsistemas do [!INCLUDE[tsql](../../includes/tsql-md.md)] ou CmdExec.  
  
 Para definir output_file_name novamente como NULL, você deve definir *output_file_name* em uma cadeia de caracteres vazia (' ') ou em uma cadeia de caracteres em branco, mas você não pode usar o **CHAR(32)** função. Por exemplo, defina este argumento como uma cadeia de caracteres vazios como segue:  
  
 **@output_file_name = ' '**  
  
`[ @flags = ] flags` Uma opção que controla comportamento. *sinalizadores* está **int**, e pode ser um destes valores.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**0** (padrão)|Substitui o arquivo de saída.|  
|**2**|Anexa a um arquivo de saída|  
|**4**|Grava a saída da etapa de trabalho do Transact-SQL no histórico de etapas|  
|**8**|Grava o log na tabela (substitui o histórico existente)|  
|**16**|Grava o log na tabela (anexa ao histórico existente)|  
  
`[ @proxy_id = ] proxy_id` O número de identificação do que a etapa de trabalho é executado como proxy. *proxy_id* é do tipo **int**, com um padrão NULL. Se nenhum *proxy_id* for especificado, nenhum *proxy_name* for especificado e nenhuma *user_name* for especificado, a etapa de trabalho é executado como a conta de serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] agente.  
  
`[ @proxy_name = ] 'proxy_name'` O nome do que a etapa de trabalho é executado como proxy. *proxy_name* é do tipo **sysname**, com um padrão NULL. Se nenhum *proxy_id* for especificado, nenhum *proxy_name* for especificado e nenhuma *user_name* for especificado, a etapa de trabalho é executado como a conta de serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] agente.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_update_jobstep** deve ser executado a partir de **msdb** banco de dados.  
  
 A atualização de uma etapa de trabalho incrementa o número de versão do trabalho.  
  
## <a name="permissions"></a>Permissões  
 Por padrão, os membros da função de servidor fixa **sysadmin** podem executar este procedimento armazenado. Deve ser concedida a outros usuários uma das seguintes funções de banco de dados fixas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent no banco de dados **msdb** :  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 Para obter detalhes sobre as permissões dessas funções, consulte [Funções de banco de dados fixas do SQL Server Agent](../../ssms/agent/sql-server-agent-fixed-database-roles.md).  
  
 Somente os membros da **sysadmin** pode atualizar uma etapa de trabalho pertence a outro usuário.  
  
 Se a etapa de trabalho requer acesso a um proxy, o criador da etapa de trabalho deve ter acesso ao proxy para a etapa de trabalho. Todos os subsistemas, menos o Transact-SQL, requerem uma conta proxy. Os membros **sysadmin** têm acesso a todos os proxies e pode usar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] conta de serviço de agente para o proxy.  
  
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
  
## <a name="see-also"></a>Consulte também  
 [Exibir ou modificar trabalhos](../../ssms/agent/view-or-modify-jobs.md)   
 [sp_delete_jobstep &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-jobstep-transact-sql.md)   
 [sp_help_jobstep &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-jobstep-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
