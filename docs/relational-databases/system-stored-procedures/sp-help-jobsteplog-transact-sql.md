---
title: sp_help_jobsteplog (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 08/09/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_help_jobsteplog_TSQL
- sp_help_jobsteplog
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_jobsteplog
ms.assetid: 1a0be7b1-8f31-4b4c-aadb-586c0e00ed04
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c337559b68f6fae23e284f2c151a498af53ae88e
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/03/2018
---
# <a name="sphelpjobsteplog-transact-sql"></a>sp_help_jobsteplog (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna metadados sobre um determinado [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] log de etapa de trabalho do Agent. **sp_help_jobsteplog** não retorna o log real.  

  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_help_jobsteplog { [ @job_id = ] 'job_id' | [ @job_name = ] 'job_name' }  
     [ , [ @step_id = ] step_id ]  
     [ , [ @step_name = ] 'step_name' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [ **@job_id =**] **'***job_id***'**  
 O número de identificação do trabalho para o qual as informações do log de etapas de trabalho serão retornadas. *job_id* é **int**, com um padrão NULL.  
  
 [ **@job_name =**] **'***job_name***'**  
 O nome do trabalho. *job_name* é **sysname**, com um padrão NULL.  
  
> [!NOTE]  
>  O *job_id* ou *job_name* devem ser especificados, mas não é possível especificar ambos.  
  
 [  **@step_id =**] *step_id*  
 O número de identificação da etapa no trabalho. Se não for incluído, todas as etapas do trabalho serão incluídas. *step_id* é **int**, com um padrão NULL.  
  
 [  **@step_name =**] **'***step_name***'**  
 O nome da etapa no trabalho. *step_name* é **sysname**, com um padrão NULL.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**job_id**|**uniqueidentifier**|Identificador exclusivo do trabalho.|  
|**job_name**|**sysname**|Nome do trabalho.|  
|**step_id**|**Int**|Identificador da etapa no trabalho. Por exemplo, se a etapa é a primeira etapa no trabalho, seu *step_id* é 1.|  
|**step_name**|**sysname**|Nome da etapa no trabalho.|  
|**step_uid**|**uniqueidentifier**|Identificador exclusivo da etapa (gerado pelo sistema) no trabalho.|  
|**date_created**|**datetime**|Data em que a etapa foi criada.|  
|**date_modified**|**datetime**|Data em que a etapa foi modificada pela última vez.|  
|**log_size**|**float**|Tamanho, em MB (megabytes), do log de etapas do trabalho.|  
|**log**|**nvarchar(max)**|Saída do log de etapas do trabalho.|  
  
## <a name="remarks"></a>Remarks  
 **sp_help_jobsteplog** está no **msdb** banco de dados.  
  
## <a name="permissions"></a>Permissões  
 Por padrão, os membros da função de servidor fixa **sysadmin** podem executar este procedimento armazenado. Deve ser concedida a outros usuários uma das seguintes funções de banco de dados fixas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent no banco de dados **msdb** :  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 Para obter detalhes sobre as permissões dessas funções, consulte [Funções de banco de dados fixas do SQL Server Agent](http://msdn.microsoft.com/library/719ce56b-d6b2-414a-88a8-f43b725ebc79).  
  
 Membros de **SQLAgentUserRole** só pode exibir metadados de log de etapa de trabalho para etapas de trabalho que eles possuem.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-returns-job-step-log-information-for-all-steps-in-a-specific-job"></a>A. Retorna informações do log de etapas de trabalho para todas as etapas em um trabalho específico  
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
  
## <a name="see-also"></a>Consulte também  
 [sp_add_jobstep &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-jobstep-transact-sql.md)   
 [sp_delete_jobstep &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-jobstep-transact-sql.md)   
 [sp_help_jobstep &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-jobstep-transact-sql.md)   
 [sp_delete_jobstep &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-jobstep-transact-sql.md)   
 [sp_delete_jobsteplog &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-jobsteplog-transact-sql.md)   
 [Agente do SQL Server armazenados procedimentos &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sql-server-agent-stored-procedures-transact-sql.md)  
  
  
