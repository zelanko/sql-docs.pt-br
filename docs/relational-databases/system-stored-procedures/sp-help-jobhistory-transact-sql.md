---
title: sp_help_jobhistory (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_jobhistory_TSQL
- sp_help_jobhistory
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_jobhistory
ms.assetid: a944d44e-411b-4735-8ce4-73888d4262d7
author: stevestein
ms.author: sstein
ms.openlocfilehash: 10033b2525ba28e79bd31a73bd9e71a7cca15e42
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68054933"
---
# <a name="sp_help_jobhistory-transact-sql"></a>sp_help_jobhistory (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Fornece informações sobre os trabalhos para servidores no domínio de administração multisservidor.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
`[ @job_id = ] job_id`O número de identificação do trabalho. *job_id* é **uniqueidentifier**, com um padrão de NULL.  
  
`[ @job_name = ] 'job_name'`O nome do trabalho. *job_name* é **sysname**, com um padrão de NULL.  
  
`[ @step_id = ] step_id`O número de identificação da etapa. *step_id* é **int**, com um padrão de NULL.  
  
`[ @sql_message_id = ] sql_message_id`O número de identificação da mensagem de erro retornada por Microsoft SQL Server ao executar o trabalho. *sql_message_id* é **int**, com um padrão de NULL.  
  
`[ @sql_severity = ] sql_severity`O nível de severidade da mensagem de erro retornada por SQL Server ao executar o trabalho. *sql_severity* é **int**, com um padrão de NULL.  
  
`[ @start_run_date = ] start_run_date`A data em que o trabalho foi iniciado. *start_run_date*é **int**, com um padrão de NULL. *start_run_date* deve ser inserido no formato AAAAMMDD, em que yyyy é um ano de quatro caracteres, mm é um nome de mês de dois caracteres e DD é um nome de dia de dois caracteres.  
  
`[ @end_run_date = ] end_run_date`A data em que o trabalho foi concluído. *end_run_date* é **int**, com um padrão de NULL. *end_run_date*deve ser inserido no formato AAAAMMDD, em que yyyy é um ano de quatro dígitos, mm é um nome de mês de dois caracteres e DD é um nome de dia de dois caracteres.  
  
`[ @start_run_time = ] start_run_time`A hora em que o trabalho foi iniciado. *start_run_time* é **int**, com um padrão de NULL. *start_run_time*deve ser inserido no formato HHMMSS, em que HH é uma hora de dois caracteres do dia, mm é um minuto de dois caracteres do dia e SS é um segundo de dois caracteres do dia.  
  
`[ @end_run_time = ] end_run_time`A hora em que o trabalho concluiu sua execução. *end_run_time* é **int**, com um padrão de NULL. *end_run_time*deve ser inserido no formato HHMMSS, em que HH é uma hora de dois caracteres do dia, mm é um minuto de dois caracteres do dia e SS é um segundo de dois caracteres do dia.  
  
`[ @minimum_run_duration = ] minimum_run_duration`O período mínimo de tempo para a conclusão do trabalho. *minimum_run_duration* é **int**, com um padrão de NULL. *minimum_run_duration*deve ser inserido no formato HHMMSS, em que HH é uma hora de dois caracteres do dia, mm é um minuto de dois caracteres do dia e SS é um segundo de dois caracteres do dia.  
  
`[ @run_status = ] run_status`O status de execução do trabalho. *run_status* é **int**, com um padrão de NULL, e pode ser um desses valores.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**0**|Failed (Falha)|  
|**1**|Teve êxito|  
|**2**|Repetir (somente a etapa)|  
|**3**|Canceled|  
|**4**|Mensagem em andamento|  
|**5**|Unknown|  
  
`[ @minimum_retries = ] minimum_retries`O número mínimo de vezes que um trabalho deve ser executado novamente. *minimum_retries* é **int**, com um padrão de NULL.  
  
`[ @oldest_first = ] oldest_first`Deve apresentar a saída com os trabalhos mais antigos primeiro. *Oldest_First* é **int**, com um padrão de **0**, que apresenta os trabalhos mais recentes primeiro. **1** apresenta os trabalhos mais antigos primeiro.  
  
`[ @server = ] 'server'`O nome do servidor no qual o trabalho foi executado. o *servidor* é **nvarchar (30)**, com um padrão de NULL.  
  
`[ @mode = ] 'mode'`É se SQL Server imprime todas as colunas no conjunto de resultados (**completo**) ou um resumo das colunas. o *modo* é **varchar (7)**, com um padrão de **Resumo**.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 A lista de colunas real depende do valor de *Mode*. O conjunto de colunas mais abrangente é mostrado abaixo e é retornado quando o *modo* está cheio.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**instance_id**|**int**|Número de identificação de entrada de histórico.|  
|**job_id**|**uniqueidentifier**|Número de identificação do trabalho.|  
|**job_name**|**sysname**|Nome do trabalho.|  
|**step_id**|**int**|Número de identificação da etapa (será **0** para um histórico de trabalhos).|  
|**step_name**|**sysname**|Nome da etapa (será o NULL para um histórico de trabalho).|  
|**sql_message_id**|**int**|Para uma etapa do [!INCLUDE[tsql](../../includes/tsql-md.md)], o número de erro mais recente do [!INCLUDE[tsql](../../includes/tsql-md.md)] encontrado ao executar o comando.|  
|**sql_severity**|**int**|Para uma etapa do [!INCLUDE[tsql](../../includes/tsql-md.md)], a severidade de erro mais alta do [!INCLUDE[tsql](../../includes/tsql-md.md)] encontrada ao executar o comando.|  
|**message**|**nvarchar(1024)**|Mensagem de histórico de trabalho ou de etapa.|  
|**run_status**|**int**|Resultado do trabalho ou da etapa.|  
|**run_date**|**int**|Data em que o trabalho ou a etapa começaram a ser executados.|  
|**run_time**|**int**|Hora em que o trabalho ou a etapa começaram a ser executados.|  
|**run_duration**|**int**|Tempo decorrido na execução do trabalho ou da etapa no formato HHMMSS.|  
|**operator_emailed**|**nvarchar (20)**|Operador que foi enviado por email relativo a esse trabalho (é NULL para o histórico de etapas).|  
|**operator_netsent**|**nvarchar (20)**|Operador ao qual foi enviada uma mensagem de rede em relação a esse trabalho (é NULL para o histórico de etapas).|  
|**operator_paged**|**nvarchar (20)**|Operador que foi informado por pager em relação a esse trabalho (é NULL para o histórico de etapas).|  
|**retries_attempted**|**int**|Número de vezes que a etapa foi repetida (sempre 0 para um histórico de trabalhos).|  
|**servidor**|**nvarchar(30)**|Servidor no qual a etapa ou o trabalho são executados. É sempre (**local**).|  
  
## <a name="remarks"></a>Comentários  
 **sp_help_jobhistory** retorna um relatório com o histórico dos trabalhos agendados especificados. Se nenhum parâmetro for especificado, o relatório conterá o histórico para todos os trabalhos agendados.  
  
## <a name="permissions"></a>Permissões  
 Por padrão, os membros da função de servidor fixa **sysadmin** podem executar este procedimento armazenado. Deve ser concedida a outros usuários uma das seguintes funções de banco de dados fixas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent no banco de dados **msdb** :  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 Para obter detalhes sobre as permissões dessas funções, consulte [Funções de banco de dados fixas do SQL Server Agent](../../ssms/agent/sql-server-agent-fixed-database-roles.md).  
  
 Os membros da função de banco de dados **SQLAgentUserRole** só podem exibir o histórico de trabalhos que eles possuem.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-listing-all-job-information-for-a-job"></a>a. Listando todas as informações de um trabalho  
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
  
## <a name="see-also"></a>Consulte Também  
 [&#41;&#40;Transact-SQL de sp_purge_jobhistory](../../relational-databases/system-stored-procedures/sp-purge-jobhistory-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
