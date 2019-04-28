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
manager: craigg
ms.openlocfilehash: 509dd27a784fd14b5aefc811065b265f37c3f6c3
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62660768"
---
# <a name="sphelpjob-transact-sql"></a>sp_help_job (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna informações sobre trabalhos usados pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent para executar atividades automatizadas no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
`[ @job_id = ] job_id` O número de identificação do trabalho. *job_id* está **uniqueidentifier**, com um padrão NULL.  
  
`[ @job_name = ] 'job_name'` O nome do trabalho. *job_name* está **sysname**, com um padrão NULL.  
  
> [!NOTE]  
>  Para exibir um trabalho específico, ou *job_id* ou *job_name* deve ser especificado.  Omitir ambas *job_id* e *job_name* para retornar informações sobre todos os trabalhos.
  
`[ @job_aspect = ] 'job_aspect'` O atributo de trabalho para exibir. *job_aspect* está **varchar(9)**, com um padrão de NULL, e pode ser um destes valores.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**ALL**|Informações de aspecto do trabalho|  
|**JOB**|Informações do trabalho|  
|**AGENDAS**|Informações da agenda|  
|**STEPS**|Informações de etapa do trabalho|  
|**DESTINOS**|Informações de destino|  
  
`[ @job_type = ] 'job_type'` O tipo de trabalhos a serem incluídos no relatório. *job_type* está **varchar(12)**, com um padrão NULL. *job_type* pode ser **LOCAL** ou **MULTISSERVIDOR**.  
  
`[ @owner_login_name = ] 'login_name'` O nome de logon do proprietário do trabalho. *login_name* está **sysname**, com um padrão NULL.  
  
`[ @subsystem = ] 'subsystem'` O nome do subsistema. *subsistema* está **nvarchar(40)**, com um padrão NULL.  
  
`[ @category_name = ] 'category'` O nome da categoria. *categoria* está **sysname**, com um padrão NULL.  
  
`[ @enabled = ] enabled` Um número que indica se as informações são mostradas para habilitado trabalhos ou desabilitados. *habilitada* está **tinyint**, com um padrão NULL. **1** indica trabalhos habilitados, e **0** indica trabalhos desabilitados.  
  
`[ @execution_status = ] status` O status de execução para os trabalhos. *status* está **int**, com um padrão de NULL, e pode ser um destes valores.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**0**|Retorna somente os trabalhos que não estão ociosos ou suspensos.|  
|**1**|Em execução.|  
|**2**|Esperando por thread.|  
|**3**|Entre repetições.|  
|**4**|Ocioso.|  
|**5**|Suspenso.|  
|**7**|Executando ações de conclusão.|  
  
`[ @date_comparator = ] 'date_comparison'` O operador de comparação a ser usado em comparações de *date_created* e *date_modified*. *date_comparison* está **char(1)** e pode ser =, \<, ou >.  
  
`[ @date_created = ] date_created` A data em que o trabalho foi criado. *Date_Created*está **datetime**, com um padrão NULL.  
  
`[ @date_last_modified = ] date_modified` A data em que o trabalho foi modificado pela última vez. *date_modified* está **datetime**, com um padrão NULL.  
  
`[ @description = ] 'description_pattern'` A descrição do trabalho. *description_pattern* está **nvarchar(512)**, com um padrão NULL. *description_pattern* pode incluir os caracteres de curinga do SQL Server para correspondência de padrões.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Se nenhum argumento for especificado, **sp_help_job** retorna este conjunto de resultados.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**job_id**|**uniqueidentifier**|A ID exclusiva do trabalho.|  
|**originating_server**|**nvarchar(30)**|Nome do servidor do qual o trabalho originou.|  
|**name**|**sysname**|Nome do trabalho.|  
|**enabled**|**tinyint**|Indica se o trabalho está habilitado para ser executado.|  
|**description**|**nvarchar(512)**|Descrição do trabalho.|  
|**start_step_id**|**int**|ID da etapa do trabalho em que a execução deve começar.|  
|**category**|**sysname**|Categoria do trabalho.|  
|**owner**|**sysname**|Proprietário do trabalho.|  
|**notify_level_eventlog**|**int**|**Bitmask** que indica sob quais circunstâncias um evento de notificação deve ser registrado no log de aplicativo do Microsoft Windows. Pode ser um destes valores:<br /><br /> **0** = nunca<br /><br /> **1** = quando um trabalho for bem-sucedido<br /><br /> **2** = quando o trabalho falhar<br /><br /> **3** = sempre que o trabalho for concluído (independentemente do resultado do trabalho)|  
|**notify_level_email**|**int**|**Bitmask** que indica sob quais circunstâncias um email de notificação deve ser enviado quando um trabalho é concluído. Os valores possíveis são os mesmos para **notify_level_eventlog**.|  
|**notify_level_netsend**|**int**|**Bitmask** que indica sob quais circunstâncias uma mensagem de rede deve ser enviada quando um trabalho é concluído. Os valores possíveis são os mesmos para **notify_level_eventlog**.|  
|**notify_level_page**|**int**|**Bitmask** que indica sob quais circunstâncias uma página deve ser enviada quando um trabalho é concluído. Os valores possíveis são os mesmos para **notify_level_eventlog**.|  
|**notify_email_operator**|**sysname**|Nome de email do operador a ser notificado.|  
|**notify_netsend_operator**|**sysname**|Nome do computador ou usuário usado ao enviar mensagens de rede.|  
|**notify_page_operator**|**sysname**|Nome do computador ou usuário usado ao enviar uma página.|  
|**delete_level**|**int**|**Bitmask** que indica sob quais circunstâncias o trabalho deve ser excluído quando um trabalho é concluído. Os valores possíveis são os mesmos para **notify_level_eventlog**.|  
|**date_created**|**datetime**|Data em que o trabalho foi criado.|  
|**date_modified**|**datetime**|Data em que o trabalho foi modificado pela última vez.|  
|**version_number**|**int**|Versão do trabalho (atualizada automaticamente sempre que o trabalho é modificado).|  
|**last_run_date**|**int**|Data da última execução do trabalho.|  
|**last_run_time**|**int**|Hora da última execução do trabalho.|  
|**last_run_outcome**|**int**|Resultado do trabalho na última vez em que foi executado:<br /><br /> **0** = falha<br /><br /> **1** = foi bem-sucedida<br /><br /> **3** = cancelada<br /><br /> **5** = desconhecido|  
|**next_run_date**|**int**|Próxima data em que o trabalho foi agendado para ser executado.|  
|**next_run_time**|**int**|Próxima hora em que o trabalho foi agendado para ser executado.|  
|**next_run_schedule_id**|**int**|Número de identificação do próximo agendamento de execução.|  
|**current_execution_status**|**int**|Status de execução atual.|  
|**current_execution_step**|**sysname**|Etapa de execução atual no trabalho.|  
|**current_retry_attempt**|**int**|Se o trabalho estiver em execução e a etapa foi repetida, esta é a tentativa de repetição atual.|  
|**has_step**|**int**|Número de etapas que o trabalho possui.|  
|**has_schedule**|**int**|Número de agendamentos que o trabalho possui.|  
|**has_target**|**int**|Número de servidores de destino que o trabalho possui.|  
|**type**|**int**|Tipo do trabalho.<br /><br /> 1 = Trabalho local.<br /><br /> **2** = trabalho multisservidor.<br /><br /> **0** = trabalho não tem nenhum servidor de destino.|  
  
 Se *job_id* ou *job_name* for especificado, **sp_help_job** retorna esses conjuntos de resultados adicionais para etapas de trabalho, agendas de trabalho e servidores de destino do trabalho.  
  
 Este é o conjunto de resultados para etapas de trabalho.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**step_id**|**int**|Identificador exclusivo (para este trabalho) da etapa.|  
|**step_name**|**sysname**|Nome da etapa.|  
|**subsystem**|**nvarchar(40)**|Subsistema no qual o comando de etapa será executado.|  
|**command**|**nvarchar(3200)**|Comando que será executado.|  
|**flags**|**nvarchar(4000)**|**Bitmask** de valores que controlam o comportamento da etapa.|  
|**cmdexec_success_code**|**int**|Para um **CmdExec** etapa, isso é o código de saída do processo de um comando bem sucedido.|  
|**on_success_action**|**nvarchar(4000)**|O que fazer se a etapa tiver êxito:<br /><br /> **1** = sair com êxito.<br /><br /> **2** = sair com falha.<br /><br /> **3** = ir para a próxima etapa.<br /><br /> **4** = ir para a etapa.|  
|**on_success_step_id**|**int**|Se **on_success_action** é **4**, isso indica que a próxima etapa a ser executada.|  
|**on_fail_action**|**nvarchar(4000)**|Ação a ser executada se a etapa falhar. Os valores são os mesmos para **on_success_action**.|  
|**on_fail_step_id**|**int**|Se **on_fail_action** é **4**, isso indica que a próxima etapa a ser executada.|  
|**server**|**sysname**|Reservado.|  
|**database_name**|**sysname**|Para uma etapa [!INCLUDE[tsql](../../includes/tsql-md.md)], este é o banco de dados no qual o comando será executado.|  
|**database_user_name**|**sysname**|Para uma etapa [!INCLUDE[tsql](../../includes/tsql-md.md)], este é o contexto de usuário do banco de dados no qual o comando é executado.|  
|**retry_attempts**|**int**|Número máximo de vezes que o comando deve ser repetido (se for malsucedido) antes que a etapa seja considerada com falha.|  
|**retry_interval**|**int**|Intervalo (em minutos) entre quaisquer tentativas de repetição.|  
|**os_run_priority**|**varchar(4000)**|Reservado.|  
|**output_file_name**|**varchar(200)**|Arquivo de saída para o qual comando deve ser gravada ([!INCLUDE[tsql](../../includes/tsql-md.md)] e **CmdExec** somente etapas).|  
|**last_run_outcome**|**int**|Resultado da etapa na última vez em que foi executada:<br /><br /> **0** = falha<br /><br /> **1** = foi bem-sucedida<br /><br /> **3** = cancelada<br /><br /> **5** = desconhecido|  
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
|**enabled**|**int**|Se a agenda está ativa (**1**) ou não (**0**).|  
|**freq_type**|**int**|Valor que indica quando o trabalho será executado:<br /><br /> **1** = uma vez<br /><br /> **4** = diariamente<br /><br /> **8** = semanalmente<br /><br /> **16** = mensalmente<br /><br /> **32** = mensalmente, relativo a **freq_interval**<br /><br /> **64** = executar quando **SQLServerAgent** inicia o serviço.|  
|**freq_interval**|**int**|Dias quando o trabalho é executado. O valor depende do valor de **freq_type**. Para obter mais informações, consulte [sp_add_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)|  
|**freq_subday_type**|**Int**|Unidades para **freq_subday_interval**. Para obter mais informações, consulte [sp_add_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)|  
|**freq_subday_interval**|**int**|Número de **freq_subday_type** períodos ocorrer entre cada execução do trabalho. Para obter mais informações, consulte [sp_add_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)|  
|**freq_relative_interval**|**int**|Agendada a ocorrência do trabalho do **freq_interval** em cada mês. Para obter mais informações, consulte [sp_add_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)|  
|**freq_recurrence_factor**|**int**|Número de meses entre a execução agendada do trabalho.|  
|**active_start_date**|**int**|Data em que a execução do trabalho será iniciada.|  
|**active_end_date**|**int**|Data em que a execução do trabalho será finalizada.|  
|**active_start_time**|**int**|Hora de começar a execução do trabalho em **active_start_date.**|  
|**active_end_time**|**int**|Tempo para terminar a execução do trabalho no **active_end_date**.|  
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
|**last_run_outcome**|**tinyint**|Resultado do trabalho na última vez em que foi executado neste servidor:<br /><br /> **0** = falha<br /><br /> **1** = foi bem-sucedida<br /><br /> **3** = cancelada<br /><br /> **5** = desconhecido|  
|**last_outcome_message**|**nvarchar(1024)**|Mensagem de resultado do trabalho na última vez em que foi executado neste servidor de destino.|  
  
## <a name="permissions"></a>Permissões  
 Por padrão, os membros da função de servidor fixa **sysadmin** podem executar este procedimento armazenado. Deve ser concedida a outros usuários uma das seguintes funções de banco de dados fixas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent no banco de dados **msdb** :  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 Para obter detalhes sobre as permissões dessas funções, consulte [Funções de banco de dados fixas do SQL Server Agent](../../ssms/agent/sql-server-agent-fixed-database-roles.md).  
  
 Os membros **SQLAgentUserRole** só podem exibir os trabalhos que possuem. Os membros **sysadmin**, **SQLAgentReaderRole**, e **SQLAgentOperatorRole** pode exibir todos os trabalhos locais e multisservidor.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-list-information-for-all-jobs"></a>A. Listar informações de todos os trabalhos  
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
  
## <a name="see-also"></a>Consulte também  
 [sp_add_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-job-transact-sql.md)   
 [sp_delete_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-job-transact-sql.md)   
 [sp_update_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-update-job-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
