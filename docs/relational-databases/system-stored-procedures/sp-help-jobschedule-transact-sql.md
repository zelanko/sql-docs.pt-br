---
description: sp_help_jobschedule (Transact-SQL)
title: sp_help_jobschedule (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_jobschedule
- sp_help_jobschedule_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_jobschedule
ms.assetid: 2cded902-9272-4667-ac4b-a4f95a9f008e
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 5d74890ab154700159fcf6ca086f88cd2ac57409
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89538815"
---
# <a name="sp_help_jobschedule-transact-sql"></a>sp_help_jobschedule (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Retorna informações sobre o agendamento de trabalhos usado pelo [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para executar atividades automatizadas.  
 
 
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_help_jobschedule { [ @job_id = ] job_id | [ @job_name = ] 'job_name' }  
     [ , [ @schedule_name = ] 'schedule_name' ]  
     [ , [ @schedule_id = ] schedule_id ]  
     [ , [ @include_description = ] include_description ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @job_id = ] job_id` O número de identificação do trabalho. *job_id*é **uniqueidentifier**, com um padrão de NULL.  
  
`[ @job_name = ] 'job_name'` O nome do trabalho. *job_name*é **sysname**, com um padrão de NULL.  
  
> [!NOTE]
> *Job_id* ou *job_name* deve ser especificado, mas ambos não podem ser especificados.

`[ @schedule_name = ] 'schedule_name'` O nome do item de agenda para o trabalho. *schedule_name*é **sysname**, com um padrão de NULL.  
  
`[ @schedule_id = ] schedule_id` O número de identificação do item de agendamento para o trabalho. *schedule_id*é **int**, com um padrão de NULL.  
  
`[ @include_description = ] include_description` Especifica se a descrição do agendamento deve ser incluída no conjunto de resultados. *include_description* é **bit**, com um padrão de **0**. Quando *include_description* é **0**, a descrição da agenda não é incluída no conjunto de resultados. Quando *include_description* é **1**, a descrição da agenda é incluída no conjunto de resultados.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**schedule_id**|**int**|Número do identificador de agenda.|  
|**schedule_name**|**sysname**|Nome da agenda.|  
|**habilitado**|**int**|Se a agenda está habilitada (**1**) ou não habilitada (**0**).|  
|**freq_type**|**int**|Valor que indica quando o trabalho deve ser executado.<br /><br /> **1** = uma vez<br /><br /> **4** = diariamente<br /><br /> **8** = semanalmente<br /><br /> **16** = mensalmente<br /><br /> **32** = mensalmente, em relação ao **freq_interval**<br /><br /> **64** = executar quando o serviço **SQLSERVERAGENT** for iniciado.|  
|**freq_interval**|**int**|Dias em que o trabalho é executado. O valor depende do valor de **freq_type**. Para obter mais informações, consulte [sp_add_schedule &#40;&#41;Transact-SQL ](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md).|  
|**freq_subday_type**|**int**|Unidades para **freq_subday_interval**. Para obter mais informações, consulte [sp_add_schedule &#40;&#41;Transact-SQL ](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md).|  
|**freq_subday_interval**|**int**|Número de períodos de **freq_subday_type** a ocorrer entre cada execução do trabalho. Para obter mais informações, consulte [sp_add_schedule &#40;&#41;Transact-SQL ](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md).|  
|**freq_relative_interval**|**int**|A ocorrência do trabalho agendado do **freq_interval** em cada mês. Para obter mais informações, consulte [sp_add_schedule &#40;&#41;Transact-SQL ](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md).|  
|**freq_recurrence_factor**|**int**|Número de meses entre a execução agendada do trabalho.|  
|**active_start_date**|**int**|Data em que a agenda foi ativada.|  
|**active_end_date**|**int**|Data de término da agenda.|  
|**active_start_time**|**int**|Hora do dia em que a agenda é iniciada.|  
|**active_end_time**|**int**|Hora do dia em que a agenda é encerrada.|  
|**date_created**|**datetime**|Data em que a agenda foi criada.|  
|**schedule_description**|**nvarchar(4000)**|Uma descrição em inglês da agenda que é derivada de valores em ** agendas demsdb.dbo.sys**. Quando *include_description* é **0**, essa coluna contém texto informando que a descrição não foi solicitada.|  
|**next_run_date**|**int**|Próxima data em que a agenda fará com que o trabalho seja executado.|  
|**next_run_time**|**int**|Próxima hora em que a agenda fará com que o trabalho seja executado.|  
|**schedule_uid**|**uniqueidentifier**|Identificador da agenda.|  
|**job_count**|**int**|Contagem de trabalhos retornados.|  
  
> **Observação: sp_help_jobschedule** retorna valores da **dbo.sysJobSchedules** e **dbo.sysagenda** tabelas do sistema no **msdb**. **sysjobschedules** atualiza a cada 20 minutos. Isso pode afetar os valores que são retornados por esse procedimento armazenado.  
  
## <a name="remarks"></a>Comentários  
 Os parâmetros de **sp_help_jobschedule** podem ser usados somente em determinadas combinações. Se *schedule_id* for especificado, nem *job_id* nem *job_name* poderão ser especificados. Caso contrário, os parâmetros *job_id* ou *job_name* podem ser usados com *schedule_name*.  
  
## <a name="permissions"></a>Permissões  
 Exige associação à função de servidor fixa **sysadmin** . Deve ser concedida a outros usuários uma das seguintes funções de banco de dados fixas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent no banco de dados **msdb** :  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 Para obter detalhes sobre as permissões dessas funções, consulte [Funções de banco de dados fixas do SQL Server Agent](../../ssms/agent/sql-server-agent-fixed-database-roles.md).  
  
 Os membros de **SQLAgentUserRole** só podem exibir as propriedades de agendas de trabalho que possuem.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-returning-the-job-schedule-for-a-specific-job"></a>a. Retornando a agenda de trabalho para um trabalho específico  
 O exemplo a seguir retorna todas as informações de agendamento do trabalho chamado `BackupDatabase`.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_jobschedule  
    @job_name = N'BackupDatabase' ;  
GO  
```  
  
### <a name="b-returning-the-job-schedule-for-a-specific-schedule"></a>B. Retornando a agenda de trabalho de uma agenda específica  
 O exemplo a seguir retorna as informações da agenda chamada `NightlyJobs` e do trabalho chamado `RunReports`.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_jobschedule   
    @job_name = N'RunReports',  
    @schedule_name = N'NightlyJobs' ;  
GO  
```  
  
### <a name="c-returning-the-job-schedule-and-schedule-description-for-a-specific-schedule"></a>C. Retornando a agenda de trabalho e a descrição de uma agenda específica  
 O exemplo a seguir retorna as informações da agenda chamada `NightlyJobs` e do trabalho chamado `RunReports`. O conjunto de resultados retornado inclui uma descrição da agenda.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_jobschedule  
    @job_name = N'RunReports',  
    @schedule_name = N'NightlyJobs',  
    @include_description = 1 ;  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [&#41;&#40;Transact-SQL de sp_add_schedule ](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_delete_schedule ](../../relational-databases/system-stored-procedures/sp-delete-schedule-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_update_schedule ](../../relational-databases/system-stored-procedures/sp-update-schedule-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
