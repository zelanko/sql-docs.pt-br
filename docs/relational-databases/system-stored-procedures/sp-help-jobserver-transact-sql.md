---
title: sp_help_jobserver (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_jobserver
- sp_help_jobserver_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_jobserver
ms.assetid: 57971787-f9f5-4199-9f64-c2b61a308906
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 155f56340925a1c2c2d6a095085203492f20f016
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85773854"
---
# <a name="sp_help_jobserver-transact-sql"></a>sp_help_jobserver (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  Retorna informações sobre o servidor para um determinado trabalho.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_help_jobserver  
     { [ @job_id = ] job_id   
     | [ @job_name = ] 'job_name' }  
     [ , [ @show_last_run_details = ] show_last_run_details ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @job_id = ] job_id`O número de identificação do trabalho para o qual retornar informações. *job_id* é **uniqueidentifier**, com um padrão de NULL.  
  
`[ @job_name = ] 'job_name'`O nome do trabalho para o qual retornar informações. *job_name* é **sysname**, com um padrão de NULL.  
  
> [!NOTE]  
>  *Job_id* ou *job_name* deve ser especificado, mas ambos não podem ser especificados.  
  
`[ @show_last_run_details = ] show_last_run_details`É se as informações de execução da última execução fazem parte do conjunto de resultados. *show_last_run_details* é **tinyint**, com um padrão de **0**. **0** não inclui informações da última execução e **1** faz.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**server_id**|**int**|Número de identificação do servidor de destino.|  
|**server_name**|**nvarchar(30)**|Nome do computador do servidor de destino.|  
|**enlist_date**|**datetime**|Data em que o servidor de destino foi inscrito no servidor mestre.|  
|**last_poll_date**|**datetime**|Data em que o servidor de destino fez a última sondagem no servidor mestre.|  
  
 Se **sp_help_jobserver** for executado com *show_last_run_details* definido como **1**, o conjunto de resultados terá essas colunas adicionais.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**last_run_date**|**int**|Data em que a execução do trabalho foi iniciada pela última vez nesse servidor de destino.|  
|**last_run_time**|**int**|Hora em que a execução do trabalho foi iniciada pela última vez nesse servidor.|  
|**last_run_duration**|**int**|Duração do trabalho na última vez em que foi executado nesse servidor de destino (em segundos).|  
|**last_outcome_message**|**nvarchar(1024)**|Descreve o último resultado do trabalho.|  
|**last_run_outcome**|**int**|Resultado do trabalho na última vez em que foi executado neste servidor:<br /><br /> **0** = falha<br /><br /> **1** = com êxito<br /><br /> **3** = cancelado<br /><br /> **5** = desconhecido|  
  
## <a name="permissions"></a>Permissões  
 Por padrão, os membros da função de servidor fixa **sysadmin** podem executar este procedimento armazenado. Deve ser concedida a outros usuários uma das seguintes funções de banco de dados fixas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent no banco de dados **msdb** :  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 Para obter detalhes sobre as permissões dessas funções, consulte [Funções de banco de dados fixas do SQL Server Agent](../../ssms/agent/sql-server-agent-fixed-database-roles.md).  
  
 Os membros de **SQLAgentUserRole** só podem exibir informações de trabalhos que possuem.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir retorna informações, incluindo as informações da última execução, sobre o trabalho `NightlyBackups`.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_jobserver  
    @job_name = N'NightlyBackups',  
    @show_last_run_details = 1 ;  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [&#41;&#40;Transact-SQL de sp_add_jobserver](../../relational-databases/system-stored-procedures/sp-add-jobserver-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_delete_jobserver](../../relational-databases/system-stored-procedures/sp-delete-jobserver-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
