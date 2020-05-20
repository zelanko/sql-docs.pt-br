---
title: sp_help_jobstep (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_jobstep_TSQL
- sp_help_jobstep
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_jobstep
ms.assetid: 4a13b804-45f2-4f82-987f-42d9a57dd6db
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 55fcc73b489a781601a2a6c5bbe139ee449cd60d
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82827556"
---
# <a name="sp_help_jobstep-transact-sql"></a>sp_help_jobstep (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna informações das etapas em um trabalho usado pelo serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent para executar atividades automatizadas.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_help_jobstep { [ @job_id = ] 'job_id' | [ @job_name = ] 'job_name' }  
     [ , [ @step_id = ] step_id ]   
     [ , [ @step_name = ] 'step_name' ]   
     [ , [ @suffix = ] suffix ]   
```  
  
## <a name="arguments"></a>Argumentos  
`[ @job_id = ] 'job_id'`O número de identificação do trabalho para o qual retornar informações do trabalho. *job_id* é **uniqueidentifier**, com um padrão de NULL.  
  
`[ @job_name = ] 'job_name'`O nome do trabalho. *job_name* é **sysname**, com um NULL padrão.  
  
> [!NOTE]  
>  *Job_id* ou *job_name* deve ser especificado, mas ambos não podem ser especificados.  
  
`[ @step_id = ] step_id`O número de identificação da etapa no trabalho. Se não for incluído, todas as etapas do trabalho serão incluídas. *step_id* é **int**, com um padrão de NULL.  
  
`[ @step_name = ] 'step_name'`O nome da etapa no trabalho. *step_name* é **sysname**, com um padrão de NULL.  
  
`[ @suffix = ] suffix`Um sinalizador que indica se uma descrição de texto é anexada à coluna **flags** na saída. o *sufixo*é **bit**, com o padrão **0**. Se o *sufixo* for **1**, uma descrição será anexada.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**step_id**|**int**|Identificador exclusivo da etapa.|  
|**step_name**|**sysname**|Nome da etapa no trabalho.|  
|**subsistema**|**nvarchar(40)**|Subsistema no qual o comando de etapa será executado.|  
|**linha**|**nvarchar(max)**|Comando executado na etapa.|  
|**sinalizadores**|**int**|Um bitmask de valores que controlam o comportamento da etapa.|  
|**cmdexec_success_code**|**int**|Para uma etapa de **CmdExec** , esse é o código de saída do processo de um comando bem-sucedido.|  
|**on_success_action**|**tinyint**|Ação a ser efetuada se a etapa tiver êxito:<br /><br /> **1** = sair do trabalho relatando êxito.<br /><br /> **2** = sair do trabalho relatando falha.<br /><br /> **3** = vá para a próxima etapa.<br /><br /> **4** = ir para a etapa.|  
|**on_success_step_id**|**int**|Se **on_success_action** for 4, isso indicará a próxima etapa a ser executada.|  
|**on_fail_action**|**tinyint**|O que fazer se a etapa falhar. Os valores são os mesmos que **on_success_action**.|  
|**on_fail_step_id**|**int**|Se **on_fail_action** for 4, isso indicará a próxima etapa a ser executada.|  
|**servidor**|**sysname**|Reservado.|  
|**database_name**|**sysname**|Para uma etapa [!INCLUDE[tsql](../../includes/tsql-md.md)], este é o banco de dados no qual o comando é executado.|  
|**database_user_name**|**sysname**|Para uma etapa [!INCLUDE[tsql](../../includes/tsql-md.md)], este é o contexto de usuário do banco de dados no qual o comando é executado.|  
|**retry_attempts**|**int**|Número máximo de vezes que o comando deve ser repetido (se for malsucedido).|  
|**retry_interval**|**int**|Intervalo (em minutos) para quaisquer tentativas de repetição.|  
|**os_run_priority**|**int**|Reservado.|  
|**output_file_name**|**nvarchar(200)**|Arquivo no qual a saída de comando deve ser gravada ( [!INCLUDE[tsql](../../includes/tsql-md.md)] , **CmdExec**e etapas do **PowerShell** somente).|  
|**last_run_outcome**|**int**|Resultado da etapa na última vez em que foi executada:<br /><br /> **0** = falha<br /><br /> **1** = com êxito<br /><br /> **2** = repetir<br /><br /> **3** = cancelado<br /><br /> **5** = desconhecido|  
|**last_run_duration**|**int**|Duração (hhmmss) da etapa na última vez que foi executada.|  
|**last_run_retries**|**int**|Número de vezes que o comando foi repetido da última vez em que a etapa foi executada.|  
|**last_run_date**|**int**|Data em que a execução da etapa foi iniciada pela última vez.|  
|**last_run_time**|**int**|Hora em que a execução da etapa foi iniciada pela última vez.|  
|**proxy_id**|**int**|Proxy da etapa do trabalho.|  
  
## <a name="remarks"></a>Comentários  
 **sp_help_jobstep** está no banco de dados **msdb** .  
  
## <a name="permissions"></a>Permissões  
 Por padrão, os membros da função de servidor fixa **sysadmin** podem executar este procedimento armazenado. Deve ser concedida a outros usuários uma das seguintes funções de banco de dados fixas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent no banco de dados **msdb** :  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 Para obter detalhes sobre as permissões dessas funções, consulte [Funções de banco de dados fixas do SQL Server Agent](../../ssms/agent/sql-server-agent-fixed-database-roles.md).  
  
 Os membros de **SQLAgentUserRole** só podem exibir etapas de trabalho para os trabalhos que eles possuem.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-return-information-for-all-steps-in-a-specific-job"></a>a. Retornar informações de todas as etapas em um trabalho específico  
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
  
## <a name="see-also"></a>Consulte Também  
 [&#41;&#40;Transact-SQL de sp_add_jobstep](../../relational-databases/system-stored-procedures/sp-add-jobstep-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_delete_jobstep](../../relational-databases/system-stored-procedures/sp-delete-jobstep-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_help_job](../../relational-databases/system-stored-procedures/sp-help-job-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_update_jobstep](../../relational-databases/system-stored-procedures/sp-update-jobstep-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
