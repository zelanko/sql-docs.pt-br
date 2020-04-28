---
title: sp_help_job (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/02/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_job_TSQL
- sp_help_job
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_job
ms.assetid: 8a8b6104-e0e4-4d07-a2c3-f4243ee0d6fa
author: stevestein
ms.author: sstein
ms.openlocfilehash: 29870a0ffb3d2c3b1872acbb40266aef0d16b62c
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "75546558"
---
# <a name="sp_help_job-transact-sql"></a>sp_help_job (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna informações sobre trabalhos usados pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent para executar atividades automatizadas no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_help_job { [ @job_id = ] job_id  
[ @job_name = ] 'job_name' }   
     [ , [ @job_aspect = ] 'job_aspect' ]   
     [ , [ @job_type = ] 'job_type' ]   
     [ , [ @owner_login_name = ] 'login_name' ]   
     [ , [ @subsystem = ] 'subsystem' ]   
     [ , [ @category_name = ] 'category' ]   
     [ , [ @enabled = ] enabled ]   
     [ , [ @execution_status = ] status ]   
     [ , [ @date_comparator = ] 'date_comparison' ]   
     [ , [ @date_created = ] date_created ]   
     [ , [ @date_last_modified = ] date_modified ]   
     [ , [ @description = ] 'description_pattern' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @job_id = ] job_id`O número de identificação do trabalho. *job_id* é **uniqueidentifier**, com um padrão de NULL.  
  
`[ @job_name = ] 'job_name'`O nome do trabalho. *job_name* é **sysname**, com um padrão de NULL.  
  
> [!NOTE]  
>  Para exibir um trabalho específico, *job_id* ou *job_name* deve ser especificado.  Omita *job_id* e *job_name* para retornar informações sobre todos os trabalhos.
  
`[ @job_aspect = ] 'job_aspect'`O atributo de trabalho a ser exibido. *job_aspect* é **varchar (9)**, com um padrão de NULL, e pode ser um desses valores.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**ALL**|Informações de aspecto do trabalho|  
|**TRABALHO**|Informações do trabalho|  
|**AGENDAMENTO**|Informações da agenda|  
|**TAREFAS**|Informações de etapa do trabalho|  
|**AOS**|Informações de destino|  
  
`[ @job_type = ] 'job_type'`O tipo de trabalho a ser incluído no relatório. *job_type* é **varchar (12)**, com um padrão de NULL. *job_type* pode ser **local** ou **vários servidores**.  
  
`[ @owner_login_name = ] 'login_name'`O nome de logon do proprietário do trabalho. *login_name* é **sysname**, com um padrão de NULL.  
  
`[ @subsystem = ] 'subsystem'`O nome do subsistema. *subsistema* é **nvarchar (40)**, com um padrão de NULL.  
  
`[ @category_name = ] 'category'`O nome da categoria. a *categoria* é **sysname**, com um padrão de NULL.  
  
`[ @enabled = ] enabled`Um número que indica se as informações são mostradas para trabalhos habilitados ou desabilitados. *habilitado* é **tinyint**, com um padrão de NULL. **1** indica trabalhos habilitados e **0** indica trabalhos desabilitados.  
  
`[ @execution_status = ] status`O status de execução para os trabalhos. o *status* é **int**, com um padrão de NULL, e pode ser um desses valores.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**0**|Retorna somente os trabalhos que não estão ociosos ou suspensos.|  
|**1**|Em execução.|  
|**2**|Esperando por thread.|  
|**3**|Entre repetições.|  
|**4**|Ocioso.|  
|**5**|Suspenso.|  
|**7**|Executando ações de conclusão.|  
  
`[ @date_comparator = ] 'date_comparison'`O operador de comparação a ser usado em comparações de *Date_Created* e *date_modified*. *date_comparison* é **Char (1)** e pode ser =, \<ou >.  
  
`[ @date_created = ] date_created`A data em que o trabalho foi criado. *Date_Created*é **DateTime**, com um padrão de NULL.  
  
`[ @date_last_modified = ] date_modified`A data em que o trabalho foi modificado pela última vez. *date_modified* é **DateTime**, com um padrão de NULL.  
  
`[ @description = ] 'description_pattern'`A descrição do trabalho. *description_pattern* é **nvarchar (512)**, com um padrão de NULL. *description_pattern* pode incluir os caracteres curinga SQL Server para correspondência de padrões.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Se nenhum argumento for especificado, **sp_help_job** retornará esse conjunto de resultados.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**job_id**|**uniqueidentifier**|A ID exclusiva do trabalho.|  
|**originating_server**|**nvarchar(30)**|Nome do servidor do qual o trabalho originou.|  
|**name**|**sysname**|Nome do trabalho.|  
|**habilitado**|**tinyint**|Indica se o trabalho está habilitado para ser executado.|  
|**ndescrição**|**nvarchar(512)**|Descrição do trabalho.|  
|**start_step_id**|**int**|ID da etapa do trabalho em que a execução deve começar.|  
|**category**|**sysname**|Categoria do trabalho.|  
|**proprietário**|**sysname**|Proprietário do trabalho.|  
|**notify_level_eventlog**|**int**|**Bitmask** que indica em quais circunstâncias um evento de notificação deve ser registrado no log de aplicativos do Microsoft Windows. Pode ser um destes valores:<br /><br /> **0** = nunca<br /><br /> **1** = quando um trabalho é executado com sucesso<br /><br /> **2** = quando o trabalho falha<br /><br /> **3** = sempre que o trabalho for concluído (independentemente do resultado do trabalho)|  
|**notify_level_email**|**int**|**Bitmask** que indica em quais circunstâncias um email de notificação deve ser enviado quando um trabalho é concluído. Os valores possíveis são os mesmos para **notify_level_eventlog**.|  
|**notify_level_netsend**|**int**|**Bitmask** que indica em quais circunstâncias uma mensagem de rede deve ser enviada quando um trabalho é concluído. Os valores possíveis são os mesmos para **notify_level_eventlog**.|  
|**notify_level_page**|**int**|**Bitmask** que indica em que circunstâncias uma página deve ser enviada quando um trabalho é concluído. Os valores possíveis são os mesmos para **notify_level_eventlog**.|  
|**notify_email_operator**|**sysname**|Nome de email do operador a ser notificado.|  
|**notify_netsend_operator**|**sysname**|Nome do computador ou usuário usado ao enviar mensagens de rede.|  
|**notify_page_operator**|**sysname**|Nome do computador ou usuário usado ao enviar uma página.|  
|**delete_level**|**int**|**Bitmask** que indica em quais circunstâncias o trabalho deve ser excluído quando um trabalho é concluído. Os valores possíveis são os mesmos para **notify_level_eventlog**.|  
|**date_created**|**datetime**|Data em que o trabalho foi criado.|  
|**date_modified**|**datetime**|Data em que o trabalho foi modificado pela última vez.|  
|**version_number**|**int**|Versão do trabalho (atualizada automaticamente sempre que o trabalho é modificado).|  
|**last_run_date**|**int**|Data da última execução do trabalho.|  
|**last_run_time**|**int**|Hora da última execução do trabalho.|  
|**last_run_outcome**|**int**|Resultado do trabalho na última vez em que foi executado:<br /><br /> **0** = falha<br /><br /> **1** = com êxito<br /><br /> **3** = cancelado<br /><br /> **5** = desconhecido|  
|**next_run_date**|**int**|Próxima data em que o trabalho foi agendado para ser executado.|  
|**next_run_time**|**int**|Próxima hora em que o trabalho foi agendado para ser executado.|  
|**next_run_schedule_id**|**int**|Número de identificação do próximo agendamento de execução.|  
|**current_execution_status**|**int**|Status de execução atual:<br /><br /> **1** = executando<br /><br /> **2** = aguardando o thread<br /><br /> **3** = entre repetições<br /><br /> **4** = ocioso<br /><br /> **5** = suspenso<br /><br /> **6** = obsoleto<br /><br /> **7** = PerformingCompletionActions|  
|**current_execution_step**|**sysname**|Etapa de execução atual no trabalho.|  
|**current_retry_attempt**|**int**|Se o trabalho estiver em execução e a etapa foi repetida, esta é a tentativa de repetição atual.|  
|**has_step**|**int**|Número de etapas que o trabalho possui.|  
|**has_schedule**|**int**|Número de agendamentos que o trabalho possui.|  
|**has_target**|**int**|Número de servidores de destino que o trabalho possui.|  
|**type**|**int**|Tipo do trabalho.<br /><br /> 1 = Trabalho local.<br /><br /> **2** = trabalho multisservidor.<br /><br /> **0** = o trabalho não tem servidores de destino.|  
  
 Se *job_id* ou *job_name* for especificado, **sp_help_job** retornará esses conjuntos de resultados adicionais para etapas de trabalho, agendas de trabalho e servidores de destino de trabalho.  
  
 Este é o conjunto de resultados para etapas de trabalho.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**step_id**|**int**|Identificador exclusivo (para este trabalho) da etapa.|  
|**step_name**|**sysname**|Nome da etapa.|  
|**subsistema**|**nvarchar(40)**|Subsistema no qual o comando de etapa será executado.|  
|**linha**|**nvarchar (3200)**|Comando que será executado.|  
|**sinalizadores**|**nvarchar(4000)**|**Bitmask** de valores que controlam o comportamento da etapa.|  
|**cmdexec_success_code**|**int**|Para uma etapa de **CmdExec** , esse é o código de saída do processo de um comando bem-sucedido.|  
|**on_success_action**|**nvarchar(4000)**|O que fazer se a etapa tiver êxito:<br /><br /> **1** = encerrar com êxito.<br /><br /> **2** = encerrar com falha.<br /><br /> **3** = ir para a próxima etapa.<br /><br /> **4** = ir para a etapa.|  
|**on_success_step_id**|**int**|Se **on_success_action** for **4**, isso indicará a próxima etapa a ser executada.|  
|**on_fail_action**|**nvarchar(4000)**|Ação a ser executada se a etapa falhar. Os valores são os mesmos para **on_success_action**.|  
|**on_fail_step_id**|**int**|Se **on_fail_action** for **4**, isso indicará a próxima etapa a ser executada.|  
|**servidor**|**sysname**|Reservado.|  
|**database_name**|**sysname**|Para uma etapa [!INCLUDE[tsql](../../includes/tsql-md.md)], este é o banco de dados no qual o comando será executado.|  
|**database_user_name**|**sysname**|Para uma etapa [!INCLUDE[tsql](../../includes/tsql-md.md)], este é o contexto de usuário do banco de dados no qual o comando é executado.|  
|**retry_attempts**|**int**|Número máximo de vezes que o comando deve ser repetido (se for malsucedido) antes que a etapa seja considerada com falha.|  
|**retry_interval**|**int**|Intervalo (em minutos) entre quaisquer tentativas de repetição.|  
|**os_run_priority**|**varchar (4000)**|Reservado.|  
|**output_file_name**|**varchar (200)**|Arquivo no qual a saída de comando deve ser[!INCLUDE[tsql](../../includes/tsql-md.md)] gravada (e somente etapas de **CmdExec** ).|  
|**last_run_outcome**|**int**|Resultado da etapa na última vez em que foi executada:<br /><br /> **0** = falha<br /><br /> **1** = com êxito<br /><br /> **3** = cancelado<br /><br /> **5** = desconhecido|  
|**last_run_duration**|**int**|Duração (em segundos) da etapa na última vez em que foi executada.|  
|**last_run_retries**|**int**|Número de vezes que o comando foi repetido da última vez em que a etapa foi executada.|  
|**last_run_date**|**int**|Data em que a execução da etapa foi iniciada pela última vez.|  
|**last_run_time**|**int**|Hora em que a execução da etapa foi iniciada pela última vez.|  
|**proxy_id**|**int**|Proxy da etapa do trabalho.|  
  
 Este é o conjunto de resultados para agendas de trabalho.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**schedule_id**|**int**|Identificador da agenda (exclusivo em todos os trabalhos).|  
|**schedule_name**|**sysname**|Nome da agenda (exclusivo somente para este trabalho).|  
|**habilitado**|**int**|Se a agenda está ativa (**1**) ou não (**0**).|  
|**freq_type**|**int**|Valor que indica quando o trabalho será executado:<br /><br /> **1** = uma vez<br /><br /> **4** = diariamente<br /><br /> **8** = semanalmente<br /><br /> **16** = mensalmente<br /><br /> **32** = mensalmente, em relação ao **freq_interval**<br /><br /> **64** = executar quando o serviço **SQLSERVERAGENT** for iniciado.|  
|**freq_interval**|**int**|Dias em que o trabalho é executado. O valor depende do valor de **freq_type**. Para obter mais informações, consulte [sp_add_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)|  
|**freq_subday_type**|**Int**|Unidades para **freq_subday_interval**. Para obter mais informações, consulte [sp_add_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)|  
|**freq_subday_interval**|**int**|Número de períodos de **freq_subday_type** a ocorrer entre cada execução do trabalho. Para obter mais informações, consulte [sp_add_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)|  
|**freq_relative_interval**|**int**|A ocorrência do trabalho agendado do **freq_interval** em cada mês. Para obter mais informações, consulte [sp_add_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)|  
|**freq_recurrence_factor**|**int**|Número de meses entre a execução agendada do trabalho.|  
|**active_start_date**|**int**|Data em que a execução do trabalho será iniciada.|  
|**active_end_date**|**int**|Data em que a execução do trabalho será finalizada.|  
|**active_start_time**|**int**|Tempo para iniciar a execução do trabalho em **active_start_date.**|  
|**active_end_time**|**int**|Tempo para concluir a execução do trabalho em **active_end_date**.|  
|**date_created**|**datetime**|Data em que a agenda foi criada.|  
|**schedule_description**|**nvarchar(4000)**|Uma descrição em inglês da agenda (se solicitado).|  
|**next_run_date**|**int**|Próxima data em que a agenda fará com que o trabalho seja executado.|  
|**next_run_time**|**int**|Próxima hora em que a agenda fará com que o trabalho seja executado.|  
|**schedule_uid**|**uniqueidentifier**|Identificador da agenda.|  
|**job_count**|**int**|Retorna o número de trabalhos que fazem referência a esta agenda.|  
  
 Este é o conjunto de resultados para servidores de destino de trabalho.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**server_id**|**int**|Identificador do servidor de destino.|  
|**server_name**|**nvarchar(30)**|Nome do computador do servidor de destino.|  
|**enlist_date**|**datetime**|Data em que o servidor de destino foi inscrito no servidor mestre.|  
|**last_poll_date**|**datetime**|Data em que o servidor de destino fez a última sondagem no servidor mestre.|  
|**last_run_date**|**int**|Data em que a execução do trabalho foi iniciada pela última vez nesse servidor de destino.|  
|**last_run_time**|**int**|Hora em que a execução do trabalho foi iniciada pela última vez nesse servidor de destino.|  
|**last_run_duration**|**int**|Duração do trabalho na última vez em que foi executado neste servidor de destino.|  
|**last_run_outcome**|**tinyint**|Resultado do trabalho na última vez em que foi executado neste servidor:<br /><br /> **0** = falha<br /><br /> **1** = com êxito<br /><br /> **3** = cancelado<br /><br /> **5** = desconhecido|  
|**last_outcome_message**|**nvarchar(1024)**|Mensagem de resultado do trabalho na última vez em que foi executado neste servidor de destino.|  
  
## <a name="permissions"></a>Permissões  
 Por padrão, os membros da função de servidor fixa **sysadmin** podem executar este procedimento armazenado. Deve ser concedida a outros usuários uma das seguintes funções de banco de dados fixas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent no banco de dados **msdb** :  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 Para obter detalhes sobre as permissões dessas funções, consulte [Funções de banco de dados fixas do SQL Server Agent](../../ssms/agent/sql-server-agent-fixed-database-roles.md).  
  
 Os membros de **SQLAgentUserRole** só podem exibir os trabalhos que eles possuem. Os membros de **sysadmin**, **SQLAgentReaderRole**e **SQLAgentOperatorRole** podem exibir todos os trabalhos locais e multisservidor.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-list-information-for-all-jobs"></a>a. Listar informações de todos os trabalhos  
 O exemplo a seguir executa o procedimento `sp_help_job` sem parâmetros para retornar as informações de todos os trabalhos atualmente definidos no banco de dados `msdb`.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_job ;  
GO  
```  
  
### <a name="b-listing-information-for-jobs-matching-a-specific-criteria"></a>B. Listando informações de trabalhos que correspondam a critérios específicos  
 O exemplo a seguir lista informações dos trabalhos multisservidor pertencentes a `françoisa` em que o trabalho está habilitado e em execução.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_job   
   @job_type = N'MULTI-SERVER',  
   @owner_login_name = N'françoisa',  
   @enabled = 1,  
   @execution_status = 1 ;  
GO  
```  
  
### <a name="c-listing-all-aspects-of-information-for-a-job"></a>C. Listando todos os aspectos de informações de um trabalho  
 O exemplo a seguir lista todos os aspectos das informações do trabalho `NightlyBackups`.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_job  
    @job_name = N'NightlyBackups',  
    @job_aspect = N'ALL' ;  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [&#41;&#40;Transact-SQL de sp_add_job](../../relational-databases/system-stored-procedures/sp-add-job-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_delete_job](../../relational-databases/system-stored-procedures/sp-delete-job-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_update_job](../../relational-databases/system-stored-procedures/sp-update-job-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
