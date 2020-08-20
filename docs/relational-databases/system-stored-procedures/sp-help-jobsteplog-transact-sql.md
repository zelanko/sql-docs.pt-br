---
description: sp_help_jobsteplog (Transact-SQL)
title: sp_help_jobsteplog (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_jobsteplog_TSQL
- sp_help_jobsteplog
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_jobsteplog
ms.assetid: 1a0be7b1-8f31-4b4c-aadb-586c0e00ed04
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 3c3659e9f82da6d735bb8d5c53d6a182d4fa14d9
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88464239"
---
# <a name="sp_help_jobsteplog-transact-sql"></a>sp_help_jobsteplog (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Retorna metadados sobre um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] log de etapa de trabalho do agente específico. **sp_help_jobsteplog** não retorna o log real.  

  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_help_jobsteplog { [ @job_id = ] 'job_id' | [ @job_name = ] 'job_name' }  
     [ , [ @step_id = ] step_id ]  
     [ , [ @step_name = ] 'step_name' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @job_id = ] 'job_id'` O número de identificação do trabalho para o qual retornar informações de log da etapa de trabalho. *job_id* é **int**, com um padrão de NULL.  
  
`[ @job_name = ] 'job_name'` O nome do trabalho. *job_name* é **sysname**, com um NULL padrão.  
  
> [!NOTE]  
>  *Job_id* ou *job_name* deve ser especificado, mas ambos não podem ser especificados.  
  
`[ @step_id = ] step_id` O número de identificação da etapa no trabalho. Se não for incluído, todas as etapas do trabalho serão incluídas. *step_id* é **int**, com um padrão de NULL.  
  
`[ @step_name = ] 'step_name'` O nome da etapa no trabalho. *step_name* é **sysname**, com um padrão de NULL.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**job_id**|**uniqueidentifier**|Identificador exclusivo do trabalho.|  
|**job_name**|**sysname**|Nome do trabalho.|  
|**step_id**|**int**|Identificador da etapa no trabalho. Por exemplo, se a etapa for a primeira etapa no trabalho, sua *step_id* será 1.|  
|**step_name**|**sysname**|Nome da etapa no trabalho.|  
|**step_uid**|**uniqueidentifier**|Identificador exclusivo da etapa (gerado pelo sistema) no trabalho.|  
|**date_created**|**datetime**|Data em que a etapa foi criada.|  
|**date_modified**|**datetime**|Data em que a etapa foi modificada pela última vez.|  
|**log_size**|**float**|Tamanho, em MB (megabytes), do log de etapas do trabalho.|  
|**Façam**|**nvarchar(max)**|Saída do log de etapas do trabalho.|  
  
## <a name="remarks"></a>Comentários  
 **sp_help_jobsteplog** está no banco de dados **msdb** .  
  
## <a name="permissions"></a>Permissões  
 Por padrão, os membros da função de servidor fixa **sysadmin** podem executar este procedimento armazenado. Deve ser concedida a outros usuários uma das seguintes funções de banco de dados fixas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent no banco de dados **msdb** :  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 Para obter detalhes sobre as permissões dessas funções, consulte [Funções de banco de dados fixas do SQL Server Agent](../../ssms/agent/sql-server-agent-fixed-database-roles.md).  
  
 Os membros de **SQLAgentUserRole** só podem exibir metadados de log de etapa de trabalho para as etapas de trabalho que eles possuem.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-returns-job-step-log-information-for-all-steps-in-a-specific-job"></a>a. Retorna informações do log de etapas de trabalho para todas as etapas em um trabalho específico  
 O exemplo a seguir retorna todas as informações do log de etapas de trabalho do trabalho nomeado `Weekly Sales Data Backup`.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_jobsteplog  
    @job_name = N'Weekly Sales Data Backup' ;  
GO  
```  
  
### <a name="b-return-job-step-log-information-about-a-specific-job-step"></a>B. Retorna informações do log de etapas de trabalho sobre uma etapa de trabalho específica  
 O exemplo a seguir retorna informações do log de etapas de trabalho sobre a primeira etapa do trabalho nomeado `Weekly Sales Data Backup`.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_jobsteplog  
    @job_name = N'Weekly Sales Data Backup',  
    @step_id = 1 ;  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [&#41;&#40;Transact-SQL de sp_add_jobstep ](../../relational-databases/system-stored-procedures/sp-add-jobstep-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_delete_jobstep ](../../relational-databases/system-stored-procedures/sp-delete-jobstep-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_help_jobstep ](../../relational-databases/system-stored-procedures/sp-help-jobstep-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_delete_jobstep ](../../relational-databases/system-stored-procedures/sp-delete-jobstep-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_delete_jobsteplog ](../../relational-databases/system-stored-procedures/sp-delete-jobsteplog-transact-sql.md)   
 [SQL Server Agent procedimentos armazenados &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sql-server-agent-stored-procedures-transact-sql.md)  
  
  
