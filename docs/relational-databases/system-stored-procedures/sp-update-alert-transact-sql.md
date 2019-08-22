---
title: sp_update_alert (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_update_alert_TSQL
- sp_update_alert
dev_langs:
- TSQL
helpviewer_keywords:
- sp_update_alert
ms.assetid: 4bbaeaab-8aca-4c9e-abc1-82ce73090bd3
author: stevestein
ms.author: sstein
ms.openlocfilehash: 2856f89264994b9f1812653450d94e2cb2e2b0c2
ms.sourcegitcommit: cbbb210c0315f9e2be2b9cd68db888ac53429814
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/21/2019
ms.locfileid: "69890841"
---
# <a name="sp_update_alert-transact-sql"></a>sp_update_alert (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Atualiza as configurações de um alerta existente.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_update_alert   
     [ @name =] 'name'   
     [ , [ @new_name =] 'new_name']   
     [ , [ @enabled =] enabled]   
     [ , [ @message_id =] message_id]   
     [ , [ @severity =] severity]   
     [ , [ @delay_between_responses =] delay_between_responses]   
     [ , [ @notification_message =] 'notification_message']   
     [ , [ @include_event_description_in =] include_event_description_in]   
     [ , [ @database_name =] 'database']   
     [ , [ @event_description_keyword =] 'event_description_keyword']   
     [ , [ @job_id =] job_id | [@job_name =] 'job_name']   
     [ , [ @occurrence_count = ] occurrence_count]   
     [ , [ @count_reset_date =] count_reset_date]   
     [ , [ @count_reset_time =] count_reset_time]   
     [ , [ @last_occurrence_date =] last_occurrence_date]   
     [ , [ @last_occurrence_time =] last_occurrence_time]   
     [ , [ @last_response_date =] last_response_date]   
     [ , [ @last_response_time =] last_response _time]  
     [ , [ @raise_snmp_trap =] raise_snmp_trap]  
     [ , [ @performance_condition =] 'performance_condition' ]   
     [ , [ @category_name =] 'category']  
     [ , [ @wmi_namespace = ] 'wmi_namespace' ]  
     [ , [ @wmi_query = ] 'wmi_query' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @name = ] 'name'`O nome do alerta a ser atualizado. o *nome* é **sysname**, sem padrão.  
  
`[ @new_name = ] 'new_name'`Um novo nome para o alerta. O nome deve ser exclusivo. *new_name* é **sysname**, com um padrão de NULL.  
  
`[ @enabled = ] enabled`Especifica se o alerta está habilitado (**1**) ou não está habilitado (**0**). *habilitado* é **tinyint**, com um padrão de NULL. Um alerta deve estar habilitado para ser disparado.  
  
`[ @message_id = ] message_id`Uma nova mensagem ou número de erro para a definição de alerta. Normalmente, *message_id* corresponde a um número de erro na tabela **sysmessages** . *message_id* é **int**, com um padrão de NULL. Uma ID de mensagem poderá ser usada somente se a configuração de nível de severidade do alerta for **0**.  
  
`[ @severity = ] severity`Um novo nível de severidade (de **1** a **25**) para a definição de alerta. [!INCLUDE[msCoName](../../includes/msconame-md.md)] Qualquer[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mensagem enviada ao log de aplicativos do Windows com a severidade especificada ativará o alerta. a *severidade* é **int**, com um padrão de NULL. Um nível de severidade só poderá ser usado se a configuração da ID da mensagem para o alerta for **0**.  
  
`[ @delay_between_responses = ] delay_between_responses`O novo período de espera, em segundos, entre as respostas para o alerta. *delay_between_responses* é **int**, com um padrão de NULL.  
  
`[ @notification_message = ] 'notification_message'`O texto revisado de uma mensagem adicional enviada ao operador como parte da notificação por email, **net send**ou pager. *notification_message* é **nvarchar (512)** , com um padrão de NULL.  
  
`[ @include_event_description_in = ] include_event_description_in`Especifica se a descrição do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] erro do log de aplicativos do Windows deve ser incluída na mensagem de notificação. *include_event_description_in* é **tinyint**, com um padrão de NULL, e pode ser um ou mais desses valores.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**0**|Nenhum|  
|**1**|Email|  
|**2**|Pager|  
|**4**|**net send**|  
|**7**|Todas|  
  
`[ @database_name = ] 'database'`O nome do banco de dados no qual o erro deve ocorrer para que o alerta seja acionado. o *banco de dados* é **sysname.** Os nomes entre colchetes ([ ]) não são permitidos. O valor padrão é NULL.  
  
`[ @event_description_keyword = ] 'event_description_keyword'`Uma sequência de caracteres que deve ser encontrada na descrição do erro no log de mensagens de erro. Os caracteres correspondentes ao padrão da expressão LIKE do [!INCLUDE[tsql](../../includes/tsql-md.md)] podem ser usados. *event_description_keyword* é **nvarchar (100)** , com um padrão de NULL. Esse parâmetro é útil para filtrar nomes de objetos (por exemplo, **% customer_table%** ).  
  
`[ @job_id = ] job_id`O número de identificação do trabalho. *job_id* é **uniqueidentifier**, com um padrão de NULL. Se *job_id* for especificado, *job_name* deverá ser omitido.  
  
`[ @job_name = ] 'job_name'`O nome do trabalho que é executado em resposta a este alerta. *job_name* é **sysname**, com um padrão de NULL. Se *job_name* for especificado, *job_id* deverá ser omitido.  
  
`[ @occurrence_count = ] occurrence_count`Redefine o número de vezes que o alerta ocorreu. *occurrence_count* é **int**, com um padrão de NULL, e só pode ser definido como **0**.  
  
`[ @count_reset_date = ] count_reset_date`Redefine a data em que a contagem de ocorrências foi redefinida pela última vez. *count_reset_date* é **int**, com um padrão de NULL.  
  
`[ @count_reset_time = ] count_reset_time`Redefine a hora em que a contagem de ocorrências foi redefinida pela última vez. *count_reset_time* é **int**, com um padrão de NULL.  
  
`[ @last_occurrence_date = ] last_occurrence_date`Redefine a data em que o alerta ocorreu pela última vez. *last_occurrence_date* é **int**, com um padrão de NULL, e só pode ser definido como **0**.  
  
`[ @last_occurrence_time = ] last_occurrence_time`Redefine a hora em que o alerta ocorreu pela última vez. *last_occurrence_time* é **int**, com um padrão de NULL, e só pode ser definido como **0**.  
  
`[ @last_response_date = ] last_response_date`Redefine a data em que o alerta foi respondido pela última vez pelo serviço SQLServerAgent. *last_response_date* é **int**, com um padrão de NULL, e só pode ser definido como **0**.  
  
`[ @last_response_time = ] last_response_time`Redefine a hora em que o alerta foi respondido pela última vez pelo serviço SQLServerAgent. *last_response_time* é **int**, com um padrão de NULL, e só pode ser definido como **0**.  
  
`[ @raise_snmp_trap = ] raise_snmp_trap`Reservado.  
  
`[ @performance_condition = ] 'performance_condition'`Um valor expresso no formato **'** comparador **'** . *performance_condition* é **nvarchar (512)** , com um padrão de NULL, e consiste nesses elementos.  
  
|Elemento Format|Descrição|  
|--------------------|-----------------|  
|*Item*|Um objeto de desempenho, contador de desempenho ou instância nomeada do contador|  
|*Comparador*|Um destes operadores: **>** ,, **<** **=**|  
|*Valor*|Valor numérico do contador|  
  
`[ @category_name = ] 'category'`O nome da categoria de alerta. a *categoria* é **sysname** com um padrão de NULL.  
  
`[ @wmi_namespace = ] 'wmi_namespace'`O namespace WMI para consultar eventos. *wmi_namespace* é **sysname**, com um padrão de NULL.  
  
`[ @wmi_query = ] 'wmi_query'`A consulta que especifica o evento WMI para o alerta. *wmi_query* é **nvarchar (512)** , com um padrão de NULL.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 Somente **sysmessages** gravadas no [!INCLUDE[msCoName](../../includes/msconame-md.md)] log de aplicativos do Windows podem disparar um alerta.  
  
 **sp_update_alert** altera apenas as configurações de alerta para as quais os valores de parâmetro são fornecidos. Se um parâmetro for omitido, a configuração atual será retida.  
  
## <a name="permissions"></a>Permissões  
 Para executar esse procedimento armazenado, os usuários devem ser membros da função de servidor fixa **sysadmin** .  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir altera a configuração habilitada de `Test Alert` para `0`.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_update_alert  
    @name = N'Test Alert',  
    @enabled = 0 ;  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [sp_add_alert &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-alert-transact-sql.md)   
 [sp_help_alert &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-alert-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
