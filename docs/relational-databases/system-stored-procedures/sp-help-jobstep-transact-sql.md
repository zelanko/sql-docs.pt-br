---
title: sp_help_jobstep (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
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
- sp_help_jobstep_TSQL
- sp_help_jobstep
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_jobstep
ms.assetid: 4a13b804-45f2-4f82-987f-42d9a57dd6db
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: bb316ee70ad1cf1f98898fd08edbb7cfb9622f56
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/03/2018
---
# <a name="sphelpjobstep-transact-sql"></a>sp_help_jobstep (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna informações das etapas em um trabalho usado pelo serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent para executar atividades automatizadas.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_help_jobstep { [ @job_id = ] 'job_id' | [ @job_name = ] 'job_name' }  
     [ , [ @step_id = ] step_id ]   
     [ , [ @step_name = ] 'step_name' ]   
     [ , [ @suffix = ] suffix ]   
```  
  
## <a name="arguments"></a>Argumentos  
 [ **@job_id =**] **'***job_id***'**  
 O número de identificação do trabalho para o qual as informações de trabalho devem ser retornadas. *job_id* é **uniqueidentifier**, com um padrão NULL.  
  
 [ **@job_name =**] **'***job_name***'**  
 O nome do trabalho. *job_name* é **sysname**, com um padrão NULL.  
  
> [!NOTE]  
>  O *job_id* ou *job_name* devem ser especificados, mas não é possível especificar ambos.  
  
 [  **@step_id =**] *step_id*  
 O número de identificação da etapa no trabalho. Se não for incluído, todas as etapas do trabalho serão incluídas. *step_id* é **int**, com um padrão NULL.  
  
 [  **@step_name =**] **'***step_name***'**  
 O nome da etapa no trabalho. *step_name* é **sysname**, com um padrão NULL.  
  
 [ **@suffix =**] *suffix*  
 Um sinalizador que indica se uma descrição de texto será anexada ao **sinalizadores** coluna na saída. *sufixo*é **bit**, com o padrão de **0**. Se *sufixo* é **1**, uma descrição será anexada.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**step_id**|**Int**|Identificador exclusivo da etapa.|  
|**step_name**|**sysname**|Nome da etapa no trabalho.|  
|**subsystem**|**nvarchar(40)**|Subsistema no qual o comando de etapa será executado.|  
|**command**|**nvarchar(max)**|Comando executado na etapa.|  
|**flags**|**Int**|Um bitmask de valores que controlam o comportamento da etapa.|  
|**cmdexec_success_code**|**Int**|Para uma **CmdExec** etapa, este é o código de saída do processo de um comando bem sucedido.|  
|**on_success_action**|**tinyint**|Ação a ser efetuada se a etapa tiver êxito:<br /><br /> **1** = sair do trabalho relatando êxito.<br /><br /> **2** = sair do trabalho relatando falha.<br /><br /> **3** = ir para a próxima etapa.<br /><br /> **4** = ir para a etapa.|  
|**on_success_step_id**|**Int**|Se **on_success_action** for 4, isto indicará a próxima etapa a ser executada.|  
|**on_fail_action**|**tinyint**|O que fazer se a etapa falhar. Os valores são os mesmos **on_success_action**.|  
|**on_fail_step_id**|**Int**|Se **on_fail_action** for 4, isto indicará a próxima etapa a ser executada.|  
|**server**|**sysname**|Reservado.|  
|**database_name**|**sysname**|Para uma etapa [!INCLUDE[tsql](../../includes/tsql-md.md)], este é o banco de dados no qual o comando é executado.|  
|**database_user_name**|**sysname**|Para uma etapa [!INCLUDE[tsql](../../includes/tsql-md.md)], este é o contexto de usuário do banco de dados no qual o comando é executado.|  
|**retry_attempts**|**Int**|Número máximo de vezes que o comando deve ser repetido (se for malsucedido).|  
|**retry_interval**|**Int**|Intervalo (em minutos) para quaisquer tentativas de repetição.|  
|**os_run_priority**|**Int**|Reservado.|  
|**output_file_name**|**nvarchar(200)**|Arquivo para o comando de saída deve ser gravada ([!INCLUDE[tsql](../../includes/tsql-md.md)], **CmdExec**, e **PowerShell** somente etapas).|  
|**last_run_outcome**|**Int**|Resultado da etapa na última vez em que foi executada:<br /><br /> **0** = falha<br /><br /> **1** = foi bem-sucedida<br /><br /> **2** = repetir<br /><br /> **3** = cancelada<br /><br /> **5** = desconhecido|  
|**last_run_duration**|**Int**|Duração (em segundos) da etapa na última vez em que foi executada.|  
|**last_run_retries**|**Int**|Número de vezes que o comando foi repetido da última vez em que a etapa foi executada.|  
|**last_run_date**|**Int**|Data em que a execução da etapa foi iniciada pela última vez.|  
|**last_run_time**|**Int**|Hora em que a execução da etapa foi iniciada pela última vez.|  
|**proxy_id**|**Int**|Proxy da etapa do trabalho.|  
  
## <a name="remarks"></a>Remarks  
 **sp_help_jobstep** está no **msdb** banco de dados.  
  
## <a name="permissions"></a>Permissões  
 Por padrão, os membros da função de servidor fixa **sysadmin** podem executar este procedimento armazenado. Deve ser concedida a outros usuários uma das seguintes funções de banco de dados fixas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent no banco de dados **msdb** :  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 Para obter detalhes sobre as permissões dessas funções, consulte [Funções de banco de dados fixas do SQL Server Agent](http://msdn.microsoft.com/library/719ce56b-d6b2-414a-88a8-f43b725ebc79).  
  
 Membros de **SQLAgentUserRole** só pode exibir as etapas de trabalho para trabalhos que possuem.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-return-information-for-all-steps-in-a-specific-job"></a>A. Retornar informações de todas as etapas em um trabalho específico  
 O exemplo a seguir retorna todas as etapas do trabalho nomeado `Weekly Sales Data Backup`.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_jobstep  
    @job_name = N'Weekly Sales Data Backup' ;  
GO  
```  
  
### <a name="b-return-information-about-a-specific-job-step"></a>B. Retornar informações sobre uma etapa de trabalho específica  
 O exemplo a seguir retorna informações sobre a primeira etapa de trabalho do trabalho nomeado `Weekly Sales Data Backup`.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_jobstep  
    @job_name = N'Weekly Sales Data Backup',  
    @step_id = 1 ;  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [sp_add_jobstep &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-jobstep-transact-sql.md)   
 [sp_delete_jobstep &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-jobstep-transact-sql.md)   
 [sp_help_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-job-transact-sql.md)   
 [sp_update_jobstep &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-update-jobstep-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
