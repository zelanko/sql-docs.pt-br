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
manager: craigg
ms.openlocfilehash: 24cd1864fc31524dcd661cd9eb108d8cb4fa1b77
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47846716"
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
 O nome do alerta a ser atualizado. *nome da* está **sysname**, sem padrão.  
  
 [  **@new_name =**] **'***new_name***'**  
 Um nome novo para o alerta. O nome deve ser exclusivo. *new_name* está **sysname**, com um padrão NULL.  
  
 [  **@enabled =**] *habilitado*  
 Especifica se o alerta está habilitado (**1**) ou não habilitado (**0**). *habilitada* está **tinyint**, com um padrão NULL. Um alerta deve estar habilitado para ser disparado.  
  
 [  **@message_id =**] *message_id*  
 Uma mensagem nova ou número de erro para a definição alerta. Normalmente, *message_id* corresponde a um número de erro no **sysmessages** tabela. *message_id* está **int**, com um padrão NULL. Uma mensagem ID pode ser usada somente se for a configuração de nível de severidade do alerta **0**.  
  
 [  **@severity =**] *gravidade*  
 Um novo nível de gravidade (de **1** por meio **25**) para a definição de alerta. Qualquer [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mensagem enviada para o log de aplicativo do Windows com a gravidade especificada ativará o alerta. *gravidade* está **int**, com um padrão NULL. Um nível de severidade pode ser usado somente se a configuração de ID de mensagem para o alerta for **0**.  
  
 [  **@delay_between_responses =**] *delay_between_responses*  
 O novo período de espera, em segundos, entre respostas ao alerta. *delay_between_responses* está **int**, com um padrão NULL.  
  
 [  **@notification_message =**] **'***notification_message***'**  
 O texto revisado de uma mensagem adicional enviada ao operador como parte de email, **net send**, ou notificação de pager. *notification_message* está **nvarchar(512)**, com um padrão NULL.  
  
 [  **@include_event_description_in =**] *include_event_description_in*  
 Especifica se a descrição do erro do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a partir do log de aplicativo do Windows deve ser incluída na mensagem de notificação. *include_event_description_in* está **tinyint**, com um padrão de NULL, e pode ser um ou mais destes valores.  
  
|Valor|Description|  
|-----------|-----------------|  
|**0**|None|  
|**1**|Email|  
|**2**|Pager|  
|**4**|**net send**|  
|**7**|Todos|  
  
 [  **@database_name =**] **'***banco de dados***'**  
 O nome do banco de dados no qual o erro deve ocorrer para que o alerta seja acionado. *banco de dados* é **sysname.** Os nomes entre colchetes ([ ]) não são permitidos. O valor padrão é NULL.  
  
 [  **@event_description_keyword =**] **'***event_description_keyword***'**  
 Uma cadeia de caracteres que deve ser localizada na descrição do erro no log de mensagens de erro. Os caracteres correspondentes ao padrão da expressão LIKE do [!INCLUDE[tsql](../../includes/tsql-md.md)] podem ser usados. *event_description_keyword* está **nvarchar(100)**, com um padrão NULL. Esse parâmetro é útil para filtrar nomes de objeto (por exemplo, **% customer_table %**).  
  
 [  **@job_id =**] *job_id*  
 O número de identificação do trabalho. *job_id* está **uniqueidentifier**, com um padrão NULL. Se *job_id* for especificado, *job_name* deverão ser omitidos.  
  
 [  **@job_name =**] **'***job_name***'**  
 O nome do trabalho executado em resposta a esse alerta. *job_name* está **sysname**, com um padrão NULL. Se *job_name* for especificado, *job_id* deverão ser omitidos.  
  
 [  **@occurrence_count =** ] *occurrence_count*  
 Redefine o número de vezes em que o alerta ocorreu. *occurrence_count* está **int**, com um padrão de NULL e pode ser definido somente como **0**.  
  
 [  **@count_reset_date =**] *count_reset_date*  
 Redefine a data em que a contagem de ocorrências foi redefinida pela última vez. *count_reset_date* está **int**, com um padrão NULL.  
  
 [  **@count_reset_time =**] *count_reset_time*  
 Redefine a hora em que a contagem de ocorrências foi redefinida pela última vez. *count_reset_time* está **int**, com um padrão NULL.  
  
 [  **@last_occurrence_date =**] *last_occurrence_date*  
 Redefine a data em que o alerta ocorreu pela última vez. *last_occurrence_date* está **int**, com um padrão de NULL e pode ser definido somente como **0**.  
  
 [  **@last_occurrence_time =**] *last_occurrence_time*  
 Redefine a hora em que o alerta ocorreu pela última vez. *last_occurrence_time* está **int**, com um padrão de NULL e pode ser definido somente como **0**.  
  
 [  **@last_response_date =**] *last_response_date*  
 Redefine a data em que o alerta foi respondido pela última vez pelo serviço SQLServerAgent. *last_response_date* está **int**, com um padrão de NULL e pode ser definido somente como **0**.  
  
 [  **@last_response_time =**] *last_response_time*  
 Redefine a hora em que o alerta foi respondido pela última vez pelo serviço SQLServerAgent. *last_response_time* está **int**, com um padrão de NULL e pode ser definido somente como **0**.  
  
 [  **@raise_snmp_trap =**] *raise_snmp_trap*  
 Reservado.  
  
 [  **@performance_condition =**] **'***performance_condition***'**  
 Um valor expressado no formato **'***itemcomparatorvalue***'**. *performance_condition* está **nvarchar(512)**, com um padrão de NULL e consiste nestes elementos.  
  
|Elemento Format|Description|  
|--------------------|-----------------|  
|*Item*|Um objeto de desempenho, contador de desempenho ou instância nomeada do contador|  
|*Comparador*|Um destes operadores: **>**, **<**, **=**|  
|*Value*|Valor numérico do contador|  
  
 [  **@category_name =**] **'***categoria***'**  
 O nome da categoria do alerta. *categoria* está **sysname** com um padrão NULL.  
  
 [ **@wmi_namespace**=] **'***wmi_namespace***'**  
 O namespace WMI para consulta de eventos. *wmi_namespace* está **sysname**, com um padrão NULL.  
  
 [ **@wmi_query**= ] **'***wmi_query***'**  
 A consulta que especifica o evento WMI do alerta. *wmi_query* está **nvarchar(512)**, com um padrão NULL.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 Somente **sysmessages** gravados para o [!INCLUDE[msCoName](../../includes/msconame-md.md)] log de aplicativo do Windows pode disparar um alerta.  
  
 **sp_update_alert** altera somente as configurações de alerta para o qual parâmetro valores são fornecidos. Se um parâmetro for omitido, a configuração atual será retida.  
  
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
  
  
