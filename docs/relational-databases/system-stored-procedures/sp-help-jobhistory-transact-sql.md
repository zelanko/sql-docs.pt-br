---
title: sp_help_jobhistory (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_help_jobhistory_TSQL
- sp_help_jobhistory
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_jobhistory
ms.assetid: a944d44e-411b-4735-8ce4-73888d4262d7
caps.latest.revision: 33
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b903b6e0494e94da555750cb94a3c4cd0c0c41c9
ms.sourcegitcommit: 79d4dc820767f7836720ce26a61097ba5a5f23f2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/16/2018
ms.locfileid: "40393366"
---
# <a name="sphelpjobhistory-transact-sql"></a>sp_help_jobhistory (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Fornece informações sobre os trabalhos para servidores no domínio de administração multisservidor.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_help_jobhistory [ [ @job_id = ] job_id ]   
     [ , [ @job_name = ] 'job_name' ]   
     [ , [ @step_id = ] step_id ]   
     [ , [ @sql_message_id = ] sql_message_id ]   
     [ , [ @sql_severity = ] sql_severity ]   
     [ , [ @start_run_date = ] start_run_date ]   
     [ , [ @end_run_date = ] end_run_date ]   
     [ , [ @start_run_time = ] start_run_time ]   
     [ , [ @end_run_time = ] end_run_time ]   
     [ , [ @minimum_run_duration = ] minimum_run_duration ]   
     [ , [ @run_status = ] run_status ]   
     [ , [ @minimum_retries = ] minimum_retries ]   
     [ , [ @oldest_first = ] oldest_first ]   
     [ , [ @server = ] 'server' ]   
     [ , [ @mode = ] 'mode' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [ **@job_id=** ] *job_id*  
 O número de identificação do trabalho. *job_id* está **uniqueidentifier**, com um padrão NULL.  
  
 [ **@job_name=** ] **'***job_name***'**  
 O nome do trabalho. *job_name* está **sysname**, com um padrão NULL.  
  
 [  **@step_id=** ] *step_id*  
 O número de identificação da etapa. *step_id* está **int**, com um padrão NULL.  
  
 [  **@sql_message_id=** ] *sql_message_id*  
 O número de identificação da mensagem de erro retornada pelo Microsoft SQL Server ao executar o trabalho. *sql_message_id* está **int**, com um padrão NULL.  
  
 [ **@sql_severity=** ] *sql_severity*  
 O nível de severidade da mensagem de erro retornada pelo Microsoft SQL Server ao executar o trabalho. *sql_severity* está **int**, com um padrão NULL.  
  
 [ **@start_run_date=** ] *start_run_date*  
 A data em que o trabalho foi iniciado. *start_run_date*está **int**, com um padrão NULL. *start_run_date* deve ser inserida no formato AAAAMMDD, em que AAAA é um ano de quatro caracteres, MM é um nome de mês de dois caracteres e DD é o nome de um dia de dois caracteres.  
  
 [ **@end_run_date=** ] *end_run_date*  
 A data em que o trabalho foi concluído. *end_run_date* está **int**, com um padrão NULL. *end_run_date*deve ser inserida no formato AAAAMMDD, em que AAAA é um ano de quatro dígitos, MM é um nome de mês de dois caracteres e DD é o nome de um dia de dois caracteres.  
  
 [ **@start_run_time=** ] *start_run_time*  
 A hora em que o trabalho foi iniciado. *start_run_time* está **int**, com um padrão NULL. *start_run_time*deve ser inserida no formato HHMMSS, onde HH é uma hora do dia de dois caracteres, MM é um minuto de dois caracteres do dia e SS é um segundo do dia de dois caracteres.  
  
 [  **@end_run_time=** ] *end_run_time*  
 A hora em que a execução do trabalho foi concluída. *end_run_time* está **int**, com um padrão NULL. *end_run_time*deve ser inserida no formato HHMMSS, onde HH é uma hora do dia de dois caracteres, MM é um minuto de dois caracteres do dia e SS é um segundo do dia de dois caracteres.  
  
 [ **@minimum_run_duration=** ] *minimum_run_duration*  
 O período de tempo mínimo para a conclusão do trabalho. *minimum_run_duration* está **int**, com um padrão NULL. *minimum_run_duration*deve ser inserida no formato HHMMSS, onde HH é uma hora do dia de dois caracteres, MM é um minuto de dois caracteres do dia e SS é um segundo do dia de dois caracteres.  
  
 [ **@run_status=** ] *run_status*  
 O status da execução do trabalho. *run_status* está **int**, com um padrão de NULL, e pode ser um destes valores.  
  
|Valor|Description|  
|-----------|-----------------|  
|**0**|Falhou|  
|**1**|Teve êxito|  
|**2**|Repetir (somente a etapa)|  
|**3**|Canceled|  
|**4**|Mensagem em andamento|  
|**5**|Unknown (desconhecido)|  
  
 [  **@minimum_retries=** ] *minimum_retries*  
 O número mínimo de horas para repetir a execução de um trabalho. *minimum_retries* está **int**, com um padrão NULL.  
  
 [ **@oldest_first=** ] *oldest_first*  
 Define se a saída deve ser apresentada com os trabalhos mais antigos primeiro. *oldest_first* está **int**, com um padrão de **0**, que apresenta os trabalhos mais recentes primeiro. **1** apresenta os trabalhos mais antigos primeiro.  
  
 [  **@server=** ] **'***server***'**  
 O nome do servidor no qual o trabalho foi executado. *servidor* está **nvarchar (30)**, com um padrão NULL.  
  
 [  **@mode=** ] **'***modo***'**  
 Especifica se o SQL Server imprime todas as colunas no conjunto de resultados (**completo**) ou um resumo das colunas. *modo* está **varchar(7)**, com um padrão de **resumo**.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 A lista de colunas real depende do valor de *modo*. O conjunto mais abrangente de colunas é mostrado abaixo e é retornado quando *modo* é FULL.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**instance_id**|**int**|Número de identificação de entrada de histórico.|  
|**job_id**|**uniqueidentifier**|Número de identificação do trabalho.|  
|**job_name**|**sysname**|Nome do trabalho.|  
|**step_id**|**int**|Número de identificação da etapa (será **0** um histórico de trabalhos).|  
|**step_name**|**sysname**|Nome da etapa (será o NULL para um histórico de trabalho).|  
|**sql_message_id**|**int**|Para uma etapa do [!INCLUDE[tsql](../../includes/tsql-md.md)], o número de erro mais recente do [!INCLUDE[tsql](../../includes/tsql-md.md)] encontrado ao executar o comando.|  
|**sql_severity**|**int**|Para uma etapa do [!INCLUDE[tsql](../../includes/tsql-md.md)], a severidade de erro mais alta do [!INCLUDE[tsql](../../includes/tsql-md.md)] encontrada ao executar o comando.|  
|**message**|**nvarchar(1024)**|Mensagem de histórico de trabalho ou de etapa.|  
|**run_status**|**int**|Resultado do trabalho ou da etapa.|  
|**run_date**|**int**|Data em que o trabalho ou a etapa começaram a ser executados.|  
|**run_time**|**int**|Hora em que o trabalho ou a etapa começaram a ser executados.|  
|**run_duration**|**int**|Tempo decorrido na execução do trabalho ou da etapa no formato HHMMSS.|  
|**operator_emailed**|**nvarchar(20)**|Operador que foi enviado por email relativo a esse trabalho (é NULL para o histórico de etapas).|  
|**operator_netsent**|**nvarchar(20)**|Operador ao qual foi enviada uma mensagem de rede em relação a esse trabalho (é NULL para o histórico de etapas).|  
|**operator_paged**|**nvarchar(20)**|Operador que foi informado por pager em relação a esse trabalho (é NULL para o histórico de etapas).|  
|**retries_attempted**|**int**|Número de vezes que a etapa foi repetida (sempre 0 para um histórico de trabalhos).|  
|**server**|**nvarchar(30)**|Servidor no qual a etapa ou o trabalho são executados. É sempre (**local**).|  
  
## <a name="remarks"></a>Remarks  
 **sp_help_jobhistory** retorna um relatório com o histórico de trabalhos agendados especificados. Se nenhum parâmetro for especificado, o relatório conterá o histórico para todos os trabalhos agendados.  
  
## <a name="permissions"></a>Permissões  
 Por padrão, os membros da função de servidor fixa **sysadmin** podem executar este procedimento armazenado. Deve ser concedida a outros usuários uma das seguintes funções de banco de dados fixas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent no banco de dados **msdb** :  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 Para obter detalhes sobre as permissões dessas funções, consulte [Funções de banco de dados fixas do SQL Server Agent](../../ssms/agent/sql-server-agent-fixed-database-roles.md).  
  
 Os membros de **SQLAgentUserRole** função de banco de dados só pode exibir o histórico de trabalhos que eles possuem.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-listing-all-job-information-for-a-job"></a>A. Listando todas as informações de um trabalho  
 O exemplo a seguir lista todas as informações de trabalho para o trabalho `NightlyBackups`.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_jobhistory   
    @job_name = N'NightlyBackups' ;  
GO  
```  
  
### <a name="b-listing-information-for-jobs-that-match-certain-conditions"></a>B. Listando informações de trabalhos que correspondam a determinadas condições  
 O exemplo a seguir imprime todas as colunas e todas as informações de trabalho para quaisquer trabalhos e etapas de trabalho que falharam com uma mensagem de erro de `50100` (uma mensagem de erro definida pelo usuário) e uma severidade de `20`.  
  
```  
USE msdb  
GO  
  
EXEC dbo.sp_help_jobhistory  
    @sql_message_id = 50100,  
    @sql_severity = 20,  
    @run_status = 0,  
    @mode = N'FULL' ;  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [sp_purge_jobhistory &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-purge-jobhistory-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
