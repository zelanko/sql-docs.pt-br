---
title: sp_add_job (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_add_job_TSQL
- sp_add_job
dev_langs:
- TSQL
helpviewer_keywords:
- sp_add_job
ms.assetid: 6ca8fe2c-7b1c-4b59-b4c7-e3b7485df274
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 1c9b6b7e6118fc23ef821d85ea6d0ac2f040e69b
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47603034"
---
# <a name="spaddjob-transact-sql"></a>sp_add_job (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Adiciona um novo trabalho executado pelo serviço SQLServerAgent.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_add_job [ @job_name = ] 'job_name'  
     [ , [ @enabled = ] enabled ]   
     [ , [ @description = ] 'description' ]   
     [ , [ @start_step_id = ] step_id ]   
     [ , [ @category_name = ] 'category' ]   
     [ , [ @category_id = ] category_id ]   
     [ , [ @owner_login_name = ] 'login' ]   
     [ , [ @notify_level_eventlog = ] eventlog_level ]   
     [ , [ @notify_level_email = ] email_level ]   
     [ , [ @notify_level_netsend = ] netsend_level ]   
     [ , [ @notify_level_page = ] page_level ]   
     [ , [ @notify_email_operator_name = ] 'email_name' ]   
          [ , [ @notify_netsend_operator_name = ] 'netsend_name' ]   
     [ , [ @notify_page_operator_name = ] 'page_name' ]   
     [ , [ @delete_level = ] delete_level ]   
     [ , [ @job_id = ] job_id OUTPUT ]   
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@job_name =** ] **'***job_name***'**  
 O nome do trabalho. O nome deve ser exclusivo e não pode conter a porcentagem (**%**) caracteres. *job_name*está **nvarchar (128)**, sem padrão.  
  
 [  **@enabled =** ] *habilitado*  
 Indica o status do trabalho adicionado. *habilitada*está **tinyint**, com um padrão de 1 (habilitado). Se **0**, o trabalho não está habilitado e não é executado de acordo com a sua agenda; no entanto, ele pode ser executado manualmente.  
  
 [  **@description =** ] **'***descrição***'**  
 A descrição do trabalho. *Descrição* está **nvarchar(512)**, com um padrão NULL. Se *descrição* for não omitido, será usada "Nenhuma descrição disponível".  
  
 [  **@start_step_id =** ] *step_id*  
 O número de identificação da primeira etapa a ser executada para o trabalho. *step_id*está **int**, com um padrão de 1.  
  
 [  **@category_name =** ] **'***categoria***'**  
 A categoria do trabalho. *categoria*está **sysname**, com um padrão NULL.  
  
 [  **@category_id =** ] *category_id*  
 Um mecanismo independente de idioma para especificar uma categoria de trabalho. *category_id*está **int**, com um padrão NULL.  
  
 [  **@owner_login_name =** ] **'***logon***'**  
 O nome do logon que é o proprietário do trabalho. *login*está **sysname**, com um padrão NULL, que é interpretado como o nome de logon atual. Somente os membros dos **sysadmin** função de servidor fixa pode definir ou alterar o valor para **@owner_login_name**. Se os usuários que não são membros do **sysadmin** função definir ou alterar o valor de **@owner_login_name**, falha na execução deste procedimento armazenado e um erro será retornado.  
  
 [  **@notify_level_eventlog =** ] *eventlog_level*  
 Um valor que indica quando colocar uma entrada no log de aplicativo do Microsoft Windows para este trabalho. *eventlog_level*está **int**, e pode ser um destes valores.  
  
|Valor|Description|  
|-----------|-----------------|  
|**0**|Never|  
|**1**|Caso haja êxito|  
|**2** (padrão)|Caso haja falha|  
|**3**|Always|  
  
 [  **@notify_level_email =** ] *email_level*  
 Um valor que indica quando enviar um email após a conclusão deste trabalho. *email_level*está **int**, com um padrão de **0**, que indica nunca. *email_level*usa os mesmos valores *eventlog_level*.  
  
 [  **@notify_level_netsend =** ] *netsend_level*  
 Um valor que indica quando enviar uma mensagem da rede após a conclusão deste trabalho. *netsend_level*está **int**, com um padrão de **0**, que indica nunca. *netsend_level* usa os mesmos valores *eventlog_level*.  
  
 [  **@notify_level_page =** ] *page_level*  
 Um valor que indica quando enviar uma página após a conclusão deste trabalho. *page_level*está **int**, com um padrão de **0**, que indica nunca. *page_level*usa os mesmos valores *eventlog_level*.  
  
 [  **@notify_email_operator_name =** ] **'***email_name***'**  
 O nome de email da pessoa para enviar email quando *email_level* for atingido. *email_name* está **sysname**, com um padrão NULL.  
  
 [  **@notify_netsend_operator_name =** ] **'***netsend_name***'**  
 O nome do operador para quem a mensagem da rede será enviada após a conclusão deste trabalho. *netsend_name*está **sysname**, com um padrão NULL.  
  
 [  **@notify_page_operator_name =** ] **'***page_name***'**  
 O nome da pessoa para quem uma mensagem de pager será enviada após a conclusão deste trabalho. *page_name*está **sysname**, com um padrão NULL.  
  
 [  **@delete_level =** ] *delete_level*  
 Um valor que indica quando excluir o trabalho. *delete_value*está **int**, com um padrão de 0, o que significa nunca. *delete_level*usa os mesmos valores *eventlog_level*.  
  
> [!NOTE]  
>  Quando *delete_level* é **3**, o trabalho é executado apenas uma vez, independentemente de quaisquer agendas definidas para o trabalho. Além disso, se um trabalho excluir a si próprio, todo o histórico do trabalho também será excluído.  
  
 [  **@job_id =** ] *job_id * * * saída**  
 O número de identificação atribuído ao trabalho caso ele seja criado com êxito. *job_id*é uma variável de saída do tipo **uniqueidentifier**, com um padrão NULL.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 None  
  
## <a name="remarks"></a>Comentários  
 **@originating_server** existe no **sp_add_job,** , mas não está listado em argumentos. **@originating_server** é reservado para uso interno.  
  
 Após **sp_add_job** foi executado para adicionar um trabalho **sp_add_jobstep** pode ser usado para adicionar etapas que executam as atividades para o trabalho. **sp_add_jobschedule** pode ser usado para criar a agenda que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa o serviço de agente para executar o trabalho. Use **sp_add_jobserver** para definir o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instância onde o trabalho é executado, e **sp_delete_jobserver** para remover o trabalho da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instância.  
  
 Se o trabalho será executado em um ou mais servidores de destino em um ambiente multisservidor, use **sp_apply_job_to_targets** para definir os servidores de destino ou grupos de servidores para o trabalho de destino. Para remover trabalhos de servidores de destino ou grupos de servidores de destino, use **sp_remove_job_from_targets**.  
  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] gerencia trabalhos de forma fácil e com representação gráfica. Além disso, ele é recomendado para criar e gerenciar a infraestrutura de trabalhos.  
  
## <a name="permissions"></a>Permissões  
 Para executar esse procedimento armazenado, os usuários devem ser um membro do **sysadmin** função de servidor fixa ou receber um dos seguintes [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] funções de banco de dados, que residem em fixas Agent a **msdb** banco de dados:  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 Para obter informações sobre as permissões específicas que estão associados a cada uma dessas fixo funções de banco de dados, consulte [funções de banco de dados fixas do SQL Server Agent](../../ssms/agent/sql-server-agent-fixed-database-roles.md).  
  
 Somente os membros dos **sysadmin** função de servidor fixa pode definir ou alterar o valor para **@owner_login_name**. Se os usuários que não são membros do **sysadmin** função definir ou alterar o valor de **@owner_login_name**, falha na execução deste procedimento armazenado e um erro será retornado.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-adding-a-job"></a>A. Adicionando um trabalho  
 Este exemplo adiciona um novo trabalho denominado `NightlyBackups`.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_add_job  
    @job_name = N'NightlyBackups' ;  
GO  
```  
  
### <a name="b-adding-a-job-with-pager-e-mail-and-net-send-information"></a>B. Adicionando um trabalho com informações de pager, email e net send  
 Este exemplo cria um trabalho denominado `Ad hoc Sales Data Backup` que notifica `François Ajenstat` (por pager, email ou mensagem pop-up de rede) se o trabalho falhar, excluindo o trabalho após a conclusão com êxito.  
  
> [!NOTE]  
>  Este exemplo supõe que já exista um operador denominado `François Ajenstat` e um logon nomeado `françoisa`.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_add_job  
    @job_name = N'Ad hoc Sales Data Backup',   
    @enabled = 1,  
    @description = N'Ad hoc backup of sales data',  
    @owner_login_name = N'françoisa',  
    @notify_level_eventlog = 2,  
    @notify_level_email = 2,  
    @notify_level_netsend = 2,  
    @notify_level_page = 2,  
    @notify_email_operator_name = N'François Ajenstat',  
    @notify_netsend_operator_name = N'François Ajenstat',   
    @notify_page_operator_name = N'François Ajenstat',  
    @delete_level = 1 ;  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [sp_add_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)   
 [sp_add_jobstep &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-jobstep-transact-sql.md)   
 [sp_add_jobserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-jobserver-transact-sql.md)   
 [sp_apply_job_to_targets &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-apply-job-to-targets-transact-sql.md)   
 [sp_delete_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-job-transact-sql.md)   
 [sp_delete_jobserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-jobserver-transact-sql.md)   
 [sp_remove_job_from_targets &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-remove-job-from-targets-transact-sql.md)   
 [sp_help_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-job-transact-sql.md)   
 [sp_help_jobstep &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-jobstep-transact-sql.md)   
 [sp_update_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-update-job-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
