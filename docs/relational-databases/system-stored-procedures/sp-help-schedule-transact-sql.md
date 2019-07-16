---
title: sp_help_schedule (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_schedule
- sp_help_schedule_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_schedule
ms.assetid: b2fc4ce1-0a8e-44d2-b206-7dc7b258d8c9
author: stevestein
ms.author: sstein
ms.openlocfilehash: f5a68160c8aee1bcb399513051e1f4cc35cea970
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68085210"
---
# <a name="sphelpschedule-transact-sql"></a>sp_help_schedule (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Lista informações sobre agendas.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_help_schedule   
     [ @schedule_id = ] id ,  
     [ @schedule_name = ] 'schedule_name'   
     [ , [ @attached_schedules_only = ] attached_schedules_only ]  
     [ , [ @include_description = ] include_description ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @schedule_id = ] id` O identificador da agenda à lista. *schedule_name* está **int**, sem padrão. Qualquer um dos *schedule_id* ou *schedule_name* pode ser especificado.  
  
`[ @schedule_name = ] 'schedule_name'` O nome da agenda à lista. *schedule_name* está **sysname**, sem padrão. Qualquer um dos *schedule_id* ou *schedule_name* pode ser especificado.  
  
`[ @attached_schedules_only = ] attached_schedules_only ]` Especifica se deve mostrar apenas agendas que um trabalho anexado. *attached_schedules_only* está **bit**, com um padrão de **0**. Quando *attached_schedules_only* é **0**, todas as agendas são mostradas. Quando *attached_schedules_only* é **1**, o conjunto de resultados contém apenas as agendas que estão anexadas a um trabalho.  
  
`[ @include_description = ] include_description` Especifica se devem ser incluídas descrições no conjunto de resultados. *include_description* está **bit**, com um padrão de **0**. Quando *include_description* é **0**, o *schedule_description* coluna do conjunto de resultados contém um espaço reservado. Quando *include_description* é **1**, a descrição da agenda será incluída no conjunto de resultados.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Este procedimento retorna o seguinte conjunto de resultados:  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**schedule_id**|**int**|Número do identificador de agenda.|  
|**schedule_uid**|**uniqueidentifier**|Identificador da agenda.|  
|**schedule_name**|**sysname**|Nome da agenda.|  
|**habilitado**|**int**|Se a agenda foi habilitada (**1**) ou não habilitado (**0**).|  
|**freq_type**|**int**|Valor que indica quando o trabalho a ser executado.<br /><br /> **1** = uma vez<br /><br /> **4** = diariamente<br /><br /> **8** = semanalmente<br /><br /> **16** = mensalmente<br /><br /> **32** = mensalmente, relativo a **freq_interval**<br /><br /> **64** = executar quando o serviço SQLServerAgent é iniciado.|  
|**freq_interval**|**int**|Dias quando o trabalho é executado. O valor depende do valor de **freq_type**. Para obter mais informações, consulte [sp_add_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md).|  
|**freq_subday_type**|**int**|Unidades para **freq_subday_interval**. Para obter mais informações, consulte [sp_add_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md).|  
|**freq_subday_interval**|**int**|Número de **freq_subday_type** períodos ocorrer entre cada execução do trabalho. Para obter mais informações, consulte [sp_add_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md).|  
|**freq_relative_interval**|**int**|Agendada a ocorrência do trabalho do **freq_interval** em cada mês. Para obter mais informações, consulte [sp_add_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md).|  
|**freq_recurrence_factor**|**int**|Número de meses entre a execução agendada do trabalho.|  
|**active_start_date**|**int**|Data em que a agenda foi ativada.|  
|**active_end_date**|**int**|Data de término da agenda.|  
|**active_start_time**|**int**|Hora do dia em que a agenda é iniciada.|  
|**active_end_time**|**int**|Hora do dia em que a agenda é encerrada.|  
|**date_created**|**datetime**|Data em que a agenda foi criada.|  
|**schedule_description**|**nvarchar(4000)**|Uma descrição em inglês da agenda (se solicitado).|  
|**job_count**|**int**|Retorna o número de trabalhos que referenciam essa agenda.|  
  
## <a name="remarks"></a>Comentários  
 Quando nenhum parâmetro for fornecido, **sp_help_schedule** lista informações para todas as agendas na instância.  
  
## <a name="permissions"></a>Permissões  
 Por padrão, os membros da função de servidor fixa **sysadmin** podem executar este procedimento armazenado. Deve ser concedida a outros usuários uma das seguintes funções de banco de dados fixas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent no banco de dados **msdb** :  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 Para obter detalhes sobre as permissões dessas funções, consulte [Funções de banco de dados fixas do SQL Server Agent](../../ssms/agent/sql-server-agent-fixed-database-roles.md).  
  
 Os membros **SQLAgentUserRole** só podem exibir as agendas que eles possuem.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-listing-information-for-all-schedules-in-the-instance"></a>A. Listando informações para todas as agendas da instância  
 O exemplo a seguir lista as informações para todas as agendas na instância.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_schedule ;  
GO  
```  
  
### <a name="b-listing-information-for-a-specific-schedule"></a>B. Listando informações de uma agenda específica  
 O exemplo a seguir lista as informações para a agenda chamada `NightlyJobs`.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_schedule  
    @schedule_name = N'NightlyJobs' ;  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [sp_add_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)   
 [sp_attach_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-attach-schedule-transact-sql.md)   
 [sp_delete_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-schedule-transact-sql.md)   
 [sp_detach_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-detach-schedule-transact-sql.md)  
  
  
