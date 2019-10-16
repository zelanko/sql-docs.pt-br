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
ms.openlocfilehash: 7752b8fcb453f545c357c529774d570e41201ed1
ms.sourcegitcommit: 4c75b49599018124f05f91c1df3271d473827e4d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/16/2019
ms.locfileid: "72381908"
---
# <a name="sp_add_job-transact-sql"></a>sp_add_job (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md)]

  Adiciona um novo trabalho executado pelo serviço SQL Agent.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [convenções de sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
 
 > [!IMPORTANT]  
 > No momento, na [Instância Gerenciada do Banco de Dados SQL do Azure](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance), a maioria dos recursos do SQL Server Agent é compatível, mas não todos. Consulte [Azure SQL Database Managed Instance T-SQL differences from SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent) (Diferenças entre o T-SQL da Instância Gerenciada do Banco de Dados SQL do Azure e o SQL Server) para obter detalhes.
 
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
`[ @job_name = ] 'job_name'` o nome do trabalho. O nome deve ser exclusivo e não pode conter o caractere de porcentagem ( **%** ). *job_name*é **nvarchar (128)** , sem padrão.  
  
`[ @enabled = ] enabled` indica o status do trabalho adicionado. *habilitado*é **tinyint**, com um padrão de 1 (habilitado). Se **0**, o trabalho não está habilitado e não é executado de acordo com seu agendamento; no entanto, ele pode ser executado manualmente.  
  
`[ @description = ] 'description'` a descrição do trabalho. a *Descrição* é **nvarchar (512)** , com um padrão de NULL. Se a *Descrição* for omitida, "nenhuma descrição disponível" será usada.  
  
`[ @start_step_id = ] step_id` o número de identificação da primeira etapa a ser executada para o trabalho. *step_id*é **int**, com um padrão de 1.  
  
`[ @category_name = ] 'category'` a categoria para o trabalho. a *categoria*é **sysname**, com um padrão de NULL.  
  
`[ @category_id = ] category_id` um mecanismo independente de linguagem para especificar uma categoria de trabalho. *category_id*é **int**, com um padrão de NULL.  
  
`[ @owner_login_name = ] 'login'` o nome do logon que possui o trabalho. *logon*é **sysname**, com um padrão de NULL, que é interpretado como o nome de logon atual. Somente os membros da função de servidor fixa **sysadmin** podem definir ou alterar o valor de **\@owner_login_name**. Se os usuários que não forem membros da função **sysadmin** definida ou alterarem o valor de **\@owner_login_name**, a execução desse procedimento armazenado falhará e um erro será retornado.  
  
`[ @notify_level_eventlog = ] eventlog_level` um valor que indica quando inserir uma entrada no log de aplicativos do Microsoft Windows para esse trabalho. *eventlog_level*é **int**e pode ser um desses valores.  
  
|Value|Description|  
|-----------|-----------------|  
|**0**|Never|  
|**1**|Caso haja êxito|  
|**2** (padrão)|Caso haja falha|  
|**3**|Always|  
  
`[ @notify_level_email = ] email_level` um valor que indica quando enviar um email após a conclusão deste trabalho. *email_level*é **int**, com um padrão de **0**, que indica nunca. *email_level*usa os mesmos valores de *eventlog_level*.  
  
`[ @notify_level_netsend = ] netsend_level` um valor que indica quando enviar uma mensagem de rede após a conclusão deste trabalho. *netsend_level*é **int**, com um padrão de **0**, que indica nunca. *netsend_level* usa os mesmos valores de *eventlog_level*.  
  
`[ @notify_level_page = ] page_level` um valor que indica quando enviar uma página após a conclusão deste trabalho. *page_level*é **int**, com um padrão de **0**, que indica nunca. *page_level*usa os mesmos valores de *eventlog_level*.  
  
`[ @notify_email_operator_name = ] 'email_name'` o nome de email da pessoa para a qual enviar o email quando *email_level* for atingido. *email_name* é **sysname**, com um padrão de NULL.  
  
`[ @notify_netsend_operator_name = ] 'netsend_name'` o nome do operador para o qual a mensagem de rede é enviada após a conclusão deste trabalho. *netsend_name*é **sysname**, com um padrão de NULL.  
  
`[ @notify_page_operator_name = ] 'page_name'` o nome da pessoa a ser paginada após a conclusão deste trabalho. *page_name*é **sysname**, com um padrão de NULL.  
  
`[ @delete_level = ] delete_level` um valor que indica quando excluir o trabalho. *delete_value*é **int**, com um padrão de 0, o que significa nunca. *delete_level*usa os mesmos valores de *eventlog_level*.  
  
> [!NOTE]  
>  Quando *delete_level* é **3**, o trabalho é executado apenas uma vez, independentemente de quaisquer agendas definidas para o trabalho. Além disso, se um trabalho excluir a si próprio, todo o histórico do trabalho também será excluído.  
  
`[ @job_id = ] _job_idOUTPUT` o número de identificação do trabalho atribuído ao trabalho, se criado com êxito. *job_id*é uma variável de saída do tipo **uniqueidentifier**, com um padrão de NULL.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 None  
  
## <a name="remarks"></a>Remarks  
 **\@originating_server** existe em **sp_add_job,** mas não está listado em argumentos. **\@originating_server** é reservado para uso interno.  
  
 Depois que **sp_add_job** tiver sido executado para adicionar um trabalho, **sp_add_jobstep** poderá ser usado para adicionar etapas que executam as atividades do trabalho. **sp_add_jobschedule** pode ser usado para criar o agendamento que o serviço de agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa para executar o trabalho. Use **sp_add_jobserver** para definir a instância [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em que o trabalho é executado e **sp_delete_jobserver** para remover o trabalho da instância [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Se o trabalho for executado em um ou mais servidores de destino em um ambiente multisservidor, use **sp_apply_job_to_targets** para definir os servidores de destino ou grupos de servidores de destino para o trabalho. Para remover trabalhos de servidores de destino ou grupos de servidores de destino, use **sp_remove_job_from_targets**.  
  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] gerencia trabalhos de forma fácil e com representação gráfica. Além disso, ele é recomendado para criar e gerenciar a infraestrutura de trabalhos.  
  
## <a name="permissions"></a>Permissões  
 Para executar esse procedimento armazenado, os usuários devem ser membros da função de servidor fixa **sysadmin** ou receber uma das funções de banco de dados fixas do agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a seguir, que residem no banco de dados **msdb** :  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 Para obter informações sobre as permissões específicas associadas a cada uma dessas funções de banco de dados fixas, consulte [SQL Server Agent funções de banco de dados fixas](../../ssms/agent/sql-server-agent-fixed-database-roles.md).  
  
 Somente os membros da função de servidor fixa **sysadmin** podem definir ou alterar o valor de **\@owner_login_name**. Se os usuários que não forem membros da função **sysadmin** definida ou alterarem o valor de **\@owner_login_name**, a execução desse procedimento armazenado falhará e um erro será retornado.  
  
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
  
### <a name="b-adding-a-job-with-pager-e-mail-and-net-send-information"></a>b. Adicionando um trabalho com informações de pager, email e net send  
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
  
## <a name="see-also"></a>Consulte Também  
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
  
  
