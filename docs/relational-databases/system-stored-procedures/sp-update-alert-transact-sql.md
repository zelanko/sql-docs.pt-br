---
title: sp_update_alert (Transact-SQL) | Microsoft Docs
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
- sp_update_alert_TSQL
- sp_update_alert
dev_langs:
- TSQL
helpviewer_keywords:
- sp_update_alert
ms.assetid: 4bbaeaab-8aca-4c9e-abc1-82ce73090bd3
caps.latest.revision: 34
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: a7715e354208953dc62e4a161a44f195babf92f3
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
---
# <a name="spupdatealert-transact-sql"></a>sp_update_alert (Transact-SQL)
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
 [  **@name =**] **'***nome***'**  
 O nome do alerta a ser atualizado. *nome* é **sysname**, sem padrão.  
  
 [  **@new_name =**] **'***novo_nome***'**  
 Um nome novo para o alerta. O nome deve ser exclusivo. *Novo_nome* é **sysname**, com um padrão NULL.  
  
 [  **@enabled =**] *habilitado*  
 Especifica se o alerta está habilitado (**1**) ou não habilitado (**0**). *habilitado* é **tinyint**, com um padrão NULL. Um alerta deve estar habilitado para ser disparado.  
  
 [  **@message_id =**] *message_id*  
 Uma mensagem nova ou número de erro para a definição alerta. Normalmente, *message_id* corresponde a um número de erro no **sysmessages** tabela. *message_id* é **int**, com um padrão NULL. Uma mensagem ID pode ser usada somente se a configuração de nível de severidade do alerta é **0**.  
  
 [  **@severity =**] *severidade*  
 Um novo nível de gravidade (de **1** por meio de **25**) para a definição de alerta. Qualquer [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mensagem enviada ao log de aplicativos do Windows com a gravidade especificada ativará o alerta. *severidade* é **int**, com um padrão NULL. Um nível de severidade pode ser usado somente se a configuração de ID de mensagem para o alerta é **0**.  
  
 [  **@delay_between_responses =**] *delay_between_responses*  
 O novo período de espera, em segundos, entre respostas ao alerta. *delay_between_responses* é **int**, com um padrão NULL.  
  
 [  **@notification_message =**] **'***notification_message***'**  
 O texto revisado de uma mensagem adicional enviada ao operador como parte do email, **net send**, ou uma notificação de pager. *notification_message* é **nvarchar (512)**, com um padrão NULL.  
  
 [  **@include_event_description_in =**] *include_event_description_in*  
 Especifica se a descrição do erro do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a partir do log de aplicativo do Windows deve ser incluída na mensagem de notificação. *include_event_description_in* é **tinyint**, com um padrão NULL, e pode ser um ou mais desses valores.  
  
|Value|Descrição|  
|-----------|-----------------|  
|**0**|Nenhuma|  
|**1**|Email|  
|**2**|Pager|  
|**4**|**net send**|  
|**7**|Todos|  
  
 [  **@database_name =**] **'***banco de dados***'**  
 O nome do banco de dados no qual o erro deve ocorrer para que o alerta seja acionado. *banco de dados* é **sysname.** Os nomes entre colchetes ([ ]) não são permitidos. O valor padrão é NULL.  
  
 [  **@event_description_keyword =**] **'***event_description_keyword***'**  
 Uma cadeia de caracteres que deve ser localizada na descrição do erro no log de mensagens de erro. Os caracteres correspondentes ao padrão da expressão LIKE do [!INCLUDE[tsql](../../includes/tsql-md.md)] podem ser usados. *event_description_keyword* é **nvarchar (100)**, com um padrão NULL. Esse parâmetro é útil para filtrar nomes de objeto (por exemplo, **% customer_table %**).  
  
 [  **@job_id =**] *job_id*  
 O número de identificação do trabalho. *job_id* é **uniqueidentifier**, com um padrão NULL. Se *job_id* for especificado, *job_name* deve ser omitido.  
  
 [  **@job_name =**] **'***job_name***'**  
 O nome do trabalho executado em resposta a esse alerta. *job_name* é **sysname**, com um padrão NULL. Se *job_name* for especificado, *job_id* deve ser omitido.  
  
 [  **@occurrence_count =** ] *occurrence_count*  
 Redefine o número de vezes em que o alerta ocorreu. *occurrence_count* é **int**, com um padrão NULL e pode ser definido somente como **0**.  
  
 [  **@count_reset_date =**] *count_reset_date*  
 Redefine a data em que a contagem de ocorrências foi redefinida pela última vez. *count_reset_date* é **int**, com um padrão NULL.  
  
 [  **@count_reset_time =**] *count_reset_time*  
 Redefine a hora em que a contagem de ocorrências foi redefinida pela última vez. *count_reset_time* é **int**, com um padrão NULL.  
  
 [  **@last_occurrence_date =**] *last_occurrence_date*  
 Redefine a data em que o alerta ocorreu pela última vez. *last_occurrence_date* é **int**, com um padrão NULL e pode ser definido somente como **0**.  
  
 [  **@last_occurrence_time =**] *last_occurrence_time*  
 Redefine a hora em que o alerta ocorreu pela última vez. *last_occurrence_time* é **int**, com um padrão NULL e pode ser definido somente como **0**.  
  
 [  **@last_response_date =**] *last_response_date*  
 Redefine a data em que o alerta foi respondido pela última vez pelo serviço SQLServerAgent. *last_response_date* é **int**, com um padrão NULL e pode ser definido somente como **0**.  
  
 [  **@last_response_time =**] *last_response_time*  
 Redefine a hora em que o alerta foi respondido pela última vez pelo serviço SQLServerAgent. *last_response_time* é **int**, com um padrão NULL e pode ser definido somente como **0**.  
  
 [  **@raise_snmp_trap =**] *raise_snmp_trap*  
 Reservado.  
  
 [  **@performance_condition =**] **'***performance_condition***'**  
 Um valor expressado no formato **'***itemcomparatorvalue***'**. *performance_condition* é **nvarchar (512)**, com um padrão NULL e consiste nestes elementos.  
  
|Elemento Format|Description|  
|--------------------|-----------------|  
|*Item*|Um objeto de desempenho, contador de desempenho ou instância nomeada do contador|  
|*Comparador*|Um destes operadores: **>**, **<**, **=**|  
|*Value*|Valor numérico do contador|  
  
 [  **@category_name =**] **'***categoria***'**  
 O nome da categoria do alerta. *categoria de* é **sysname** com um padrão NULL.  
  
 [ **@wmi_namespace**=] **'***wmi_namespace***'**  
 O namespace WMI para consulta de eventos. *wmi_namespace* é **sysname**, com um padrão NULL.  
  
 [ **@wmi_query**= ] **'***wmi_query***'**  
 A consulta que especifica o evento WMI do alerta. *wmi_query* é **nvarchar (512)**, com um padrão NULL.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Remarks  
 Somente **sysmessages** gravados para o [!INCLUDE[msCoName](../../includes/msconame-md.md)] log de aplicativo do Windows pode disparar um alerta.  
  
 **sp_update_alert** altera somente as configurações de alerta para quais valores são fornecidos. Se um parâmetro for omitido, a configuração atual será retida.  
  
## <a name="permissions"></a>Permissões  
 Para executar esse procedimento armazenado, os usuários devem ser um membro do **sysadmin** função de servidor fixa.  
  
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
  
  
