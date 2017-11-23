---
title: sp_update_jobstep (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_update_jobstep
- sp_update_jobstep_TSQL
dev_langs: TSQL
helpviewer_keywords: sp_update_jobstep
ms.assetid: e158802c-c347-4a5d-bf75-c03e5ae56e6b
caps.latest.revision: "33"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 4708d2cfe45f192a80836f592e3f774378eeb03e
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="spupdatejobstep-transact-sql"></a>sp_update_jobstep (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Altera a configuração para uma etapa em um trabalho que é usado para executar atividades automatizadas.  
  
||  
|-|  
|**Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] até a [versão atual](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
 [  **@job_id =**] *job_id*  
 O número de identificação do trabalho ao qual a etapa pertence. *job_id*é **uniqueidentifier**, com um padrão NULL. O *job_id* ou *job_name* devem ser especificados, mas não podem ser especificados.  
  
 [  **@job_name =**] **'***job_name***'**  
 O nome do trabalho ao qual a etapa pertence. *job_name*é **sysname**, com um padrão NULL. O *job_id* ou *job_name* devem ser especificados, mas não podem ser especificados.  
  
 [  **@step_id =**] *step_id*  
 O número de identificação da etapa de trabalho que será modificado. Esse número não pode ser alterado. *step_id*é **int**, sem padrão.  
  
 [  **@step_name =**] **'***step_name***'**  
 É um novo nome para a etapa. *step_name*é **sysname**, com um padrão NULL.  
  
 [  **@subsystem =**] **'***subsistema***'**  
 O subsistema usado pelo Microsoft SQL Server Agent para executar *comando*. *subsistema* é **nvarchar (40)**, com um padrão NULL.  
  
 [  **@command =**] **'***comando***'**  
 O comando a ser executado por meio de *subsistema*. *comando* é **nvarchar (max)**, com um padrão NULL.  
  
 [  **@additional_parameters =**] **'***parâmetros***'**  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
 [  **@cmdexec_success_code =**] *success_code*  
 O valor retornado por uma **CmdExec** comando de subsistema para indicar que *comando* executado com êxito. *success_code* é **int**, com um padrão NULL.  
  
 [  **@on_success_action =**] *success_action*  
 A ação a ser executada se a etapa tiver êxito. *success_action* é **tinyint**, com um padrão NULL, e pode ser um destes valores.  
  
|Valor|Descrição (ação)|  
|-----------|----------------------------|  
|**1**|Sair com êxito.|  
|**2**|Sair com falha.|  
|**3**|Ir para a próxima etapa.|  
|**4**|Vá para a etapa *success_step_id.*|  
  
 [  **@on_success_step_id =**] *success_step_id*  
 O número de identificação da etapa neste trabalho a ser executado se a etapa tiver êxito e *success_action* é **4**. *success_step_id* é **int**, com um padrão NULL.  
  
 [  **@on_fail_action =**] *fail_action*  
 A ação a ser executada se a etapa falhar. *fail_action* é **tinyint**, com um padrão de NULL e pode ter um destes valores.  
  
|Valor|Descrição (ação)|  
|-----------|----------------------------|  
|**1**|Sair com êxito.|  
|**2**|Sair com falha.|  
|**3**|Ir para a próxima etapa.|  
|**4**|Vá para a etapa *fail_step_id**.*|  
  
 [  **@on_fail_step_id =**] *fail_step_id*  
 O número de identificação da etapa neste trabalho a ser executado se a etapa falhar e *fail_action* é **4**. *fail_step_id* é **int**, com um padrão NULL.  
  
 [  **@server =**] **'***servidor***'**  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]*servidor* é **nvarchar (128)**, com um padrão NULL.  
  
 [  **@database_name =**] **'***banco de dados***'**  
 O nome do banco de dados no qual executar uma etapa [!INCLUDE[tsql](../../includes/tsql-md.md)]. *banco de dados*é **sysname**. Os nomes entre colchetes ([ ]) não são permitidos. O valor padrão é NULL.  
  
 [  **@database_user_name =**] **'***usuário***'**  
 O nome da conta de usuário a ser usada ao executar uma etapa [!INCLUDE[tsql](../../includes/tsql-md.md)]. *usuário*é **sysname**, com um padrão NULL.  
  
 [  **@retry_attempts =**] *retry_attempts*  
 O número de novas tentativas a serem usadas se esta etapa apresentar falha. *retry_attempts*é **int**, com um padrão NULL.  
  
 [  **@retry_interval =**] *intervalo_de_repetição*  
 A quantidade de tempo, em minutos, entre as novas tentativas. *intervalo_de_repetição* é **int**, com um padrão NULL.  
  
 [  **@os_run_priority =**] *run_priority*  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
 [  **@output_file_name =**] **'***file_name***'**  
 O nome do arquivo no qual a saída desta etapa é gravado. *file_name* é **nvarchar (200)**, com um padrão NULL. Este parâmetro é válido somente com comandos executados nos subsistemas do [!INCLUDE[tsql](../../includes/tsql-md.md)] ou CmdExec.  
  
 Para definir output_file_name novamente como NULL, você deve definir *output_file_name* para uma cadeia de caracteres vazia (' ') ou em uma cadeia de caracteres em branco, mas você não pode usar o **CHAR(32)** função. Por exemplo, defina este argumento como uma cadeia de caracteres vazios como segue:  
  
 **@output_file_name = ' '**  
  
 [  **@flags =**] *sinalizadores*  
 Uma opção que controla comportamento. *sinalizadores de* é **int**, e pode ser um destes valores.  
  
|Valor|Description|  
|-----------|-----------------|  
|**0** (padrão)|Substitui o arquivo de saída.|  
|**2**|Anexa a um arquivo de saída|  
|**4**|Grava a saída da etapa de trabalho do Transact-SQL no histórico de etapas|  
|**8**|Grava o log na tabela (substitui o histórico existente)|  
|**16**|Grava o log na tabela (anexa ao histórico existente)|  
  
 [  **@proxy_id** =] *proxy_id*  
 O número da ID do proxy com o qual a etapa de trabalho é executada. *proxy_id* é do tipo **int**, com um padrão NULL. Se nenhum *proxy_id* for especificado, nenhum *proxy_name* for especificado e não *user_name* for especificado, a etapa de trabalho é executado como a conta de serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] agente.  
  
 [  **@proxy_name** =] **'***proxy_name***'**  
 O nome do proxy com o qual a etapa de trabalho é executada. *proxy_name* é do tipo **sysname**, com um padrão NULL. Se nenhum *proxy_id* for especificado, nenhum *proxy_name* for especificado e não *user_name* for especificado, a etapa de trabalho é executado como a conta de serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] agente.  
  
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
  
 Para obter detalhes sobre as permissões dessas funções, consulte [Funções de banco de dados fixas do SQL Server Agent](http://msdn.microsoft.com/library/719ce56b-d6b2-414a-88a8-f43b725ebc79).  
  
 Somente membros da **sysadmin** pode atualizar uma etapa de trabalho pertencente a outro usuário.  
  
 Se a etapa de trabalho requer acesso a um proxy, o criador da etapa de trabalho deve ter acesso ao proxy para a etapa de trabalho. Todos os subsistemas, menos o Transact-SQL, requerem uma conta proxy. Membros de **sysadmin** têm acesso a todos os proxies e pode usar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] conta de serviço de agente para o proxy.  
  
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
 [Exibir ou modificar trabalhos](http://msdn.microsoft.com/library/57f649b8-190c-4304-abd7-7ca5297deab7)   
 [sp_delete_jobstep &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-delete-jobstep-transact-sql.md)   
 [sp_help_jobstep &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-help-jobstep-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
