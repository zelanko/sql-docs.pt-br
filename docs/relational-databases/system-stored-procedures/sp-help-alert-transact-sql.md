---
title: sp_help_alert (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_alert
- sp_help_alert_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_alert
ms.assetid: 850cef4e-6348-4439-8e79-fd1bca712091
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: cca6c1730343a038b24e17d6aaa0156cb99c13b1
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85901532"
---
# <a name="sp_help_alert-transact-sql"></a>sp_help_alert (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Relata informações sobre os alertas definidos para o servidor.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_help_alert [ [ @alert_name = ] 'alert_name' ]   
     [ , [ @order_by = ] 'order_by' ]   
     [ , [ @alert_id = ] alert_id ]   
     [ , [ @category_name = ] 'category' ]   
     [ , [ @legacy_format = ] legacy_format ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @alert_name = ] 'alert_name'`O nome do alerta. *alert_name* é **nvarchar (128)**. Se *alert_name* não for especificado, serão retornadas informações sobre todos os alertas.  
  
`[ @order_by = ] 'order_by'`A ordem de classificação a ser usada para produzir os resultados. *order_by*é **sysname**, com um padrão de N '*Name*'.  
  
`[ @alert_id = ] alert_id`O número de identificação do alerta sobre o qual relatar informações. *alert_id*é **int**, com um padrão de NULL.  
  
`[ @category_name = ] 'category'`A categoria do alerta. a *categoria* é **sysname**, com um padrão de NULL.  
  
`[ @legacy_format = ] legacy_format`É se um conjunto de resultados herdado deve ser produzido. *legacy_format* é **bit**, com um padrão de **0**. Quando *legacy_format* é **1**, **sp_help_alert** retorna o conjunto de resultados retornado por **sp_help_alert** no Microsoft SQL Server 2000.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Quando ** \@ legacy_format** é **0**, **sp_help_alert** produz o seguinte conjunto de resultados.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**id**|**int**|Identificador inteiro exclusivo atribuído pelo sistema.|  
|**name**|**sysname**|Nome do alerta (por exemplo, demonstração: log **msdb** completo).|  
|**event_source**|**nvarchar (100)**|Origem do evento. Ele sempre será **MSSQLSERVER** para a [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] versão 7,0|  
|**event_category_id**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**event_id**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**message_id**|**int**|Número de erro de mensagem que define o alerta. (Geralmente corresponde a um número de erro na tabela **sysmessages** ). Se a severidade for usada para definir o alerta, **message_id** será **0** ou NULL.|  
|**severity**|**int**|Nível de severidade (de **9** a **25**, **110**, **120**, **130**ou **140**) que define o alerta.|  
|**habilitado**|**tinyint**|Status de se o alerta está habilitado no momento (**1**) ou não (**0**). Um alerta não habilitado não é enviado.|  
|**delay_between_responses**|**int**|Período de espera, em segundos, entre respostas ao alerta.|  
|**last_occurrence_date**|**int**|Data em que o alerta ocorreu pela última vez.|  
|**last_occurrence_time**|**int**|Hora em que o alerta ocorreu pela última vez.|  
|**last_response_date**|**int**|Data em que o alerta foi respondido pela última vez pelo serviço **SQLSERVERAGENT** .|  
|**last_response_time**|**int**|Hora em que o alerta foi respondido pela última vez pelo serviço **SQLSERVERAGENT** .|  
|**notification_message**|**nvarchar(512)**|Mensagem adicional opcional enviada ao operador como parte do email ou notificação de pager.|  
|**include_event_description**|**tinyint**|Define se a descrição do erro do SQL Server a partir do log de aplicativos do Microsoft Windows deve ser incluída como parte da mensagem de notificação.|  
|**database_name**|**sysname**|Banco de dados no qual o erro deve acontecer para que o alerta seja acionado. Se o nome de banco de dados for NULL, o alerta será acionado independentemente de onde o erro ocorreu.|  
|**event_description_keyword**|**nvarchar (100)**|Descrição do erro do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no log de aplicativos do Windows que deve ser como a sequência de caracteres fornecida.|  
|**occurrence_count**|**int**|Número de vezes que o alerta ocorreu.|  
|**count_reset_date**|**int**|Data em que a **occurrence_count** foi redefinida pela última vez.|  
|**count_reset_time**|**int**|Hora em que a **occurrence_count** foi redefinida pela última vez.|  
|**job_id**|**uniqueidentifier**|Número de identificação do trabalho a ser executado em resposta a um alerta.|  
|**job_name**|**sysname**|Nome do trabalho a ser executado em resposta a um alerta.|  
|**has_notification**|**int**|Diferente de zero se um ou mais operadores forem notificados para este alerta. O valor é um ou mais dos seguintes valores (or ligad):<br /><br /> **1**= tem notificação por email<br /><br /> **2**= tem notificação por pager<br /><br /> **4**= tem notificação **net send** .|  
|**sinalizadores**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**performance_condition**|**nvarchar(512)**|Se o **tipo** for **2**, essa coluna mostrará a definição da condição de desempenho; caso contrário, a coluna será nula.|  
|**category_name**|**sysname**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)] sempre será '[Uncategorized]' para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 7.0.|  
|**wmi_namespace**|**sysname**|Se **Type** for **3**, essa coluna mostrará o namespace para o evento WMI.|  
|**wmi_query**|**nvarchar(512)**|Se **Type** for **3**, essa coluna mostrará a consulta para o evento WMI.|  
|**type**|**int**|Tipo do evento:<br /><br /> **1**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] alerta de evento<br /><br /> **2**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] alerta de desempenho<br /><br /> **3** = alerta de evento WMI|  
  
 Quando ** \@ legacy_format** é **1**, **sp_help_alert** produz o seguinte conjunto de resultados.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**id**|**int**|Identificador inteiro exclusivo atribuído pelo sistema.|  
|**name**|**sysname**|Nome do alerta (por exemplo, demonstração: log **msdb** completo).|  
|**event_source**|**nvarchar (100)**|Origem do evento. Ele sempre será **MSSQLSERVER** para a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] versão 7,0|  
|**event_category_id**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**event_id**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**message_id**|**int**|Número de erro de mensagem que define o alerta. (Geralmente corresponde a um número de erro na tabela **sysmessages** ). Se a severidade for usada para definir o alerta, **message_id** será **0** ou NULL.|  
|**severity**|**int**|Nível de severidade (de **9** a **25**, **110**, **120**, **130**ou 1**40**) que define o alerta.|  
|**habilitado**|**tinyint**|Status de se o alerta está habilitado no momento (**1**) ou não (**0**). Um alerta não habilitado não é enviado.|  
|**delay_between_responses**|**int**|Período de espera, em segundos, entre respostas ao alerta.|  
|**last_occurrence_date**|**int**|Data em que o alerta ocorreu pela última vez.|  
|**last_occurrence_time**|**int**|Hora em que o alerta ocorreu pela última vez.|  
|**last_response_date**|**int**|Data em que o alerta foi respondido pela última vez pelo serviço **SQLSERVERAGENT** .|  
|**last_response_time**|**int**|Hora em que o alerta foi respondido pela última vez pelo serviço **SQLSERVERAGENT** .|  
|**notification_message**|**nvarchar(512)**|Mensagem adicional opcional enviada ao operador como parte do email ou notificação de pager.|  
|**include_event_description**|**tinyint**|Define se a descrição do erro do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a partir do log de aplicativos do Windows deve ser incluída como parte da mensagem de notificação.|  
|**database_name**|**sysname**|Banco de dados no qual o erro deve acontecer para que o alerta seja acionado. Se o nome de banco de dados for NULL, o alerta será acionado independentemente de onde o erro ocorreu.|  
|**event_description_keyword**|**nvarchar (100)**|Descrição do erro do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no log de aplicativos do Windows que deve ser como a sequência de caracteres fornecida.|  
|**occurrence_count**|**int**|Número de vezes que o alerta ocorreu.|  
|**count_reset_date**|**int**|Data em que a **occurrence_count** foi redefinida pela última vez.|  
|**count_reset_time**|**int**|Hora em que a **occurrence_count** foi redefinida pela última vez.|  
|**job_id**|**uniqueidentifier**|Número de identificação do trabalho.|  
|**job_name**|**sysname**|Um trabalho sob demanda a ser executado em resposta a um alerta.|  
|**has_notification**|**int**|Diferente de zero se um ou mais operadores forem notificados para este alerta. O valor é um ou mais dos seguintes (unidos por OR):<br /><br /> **1**= tem notificação por email<br /><br /> **2**= tem notificação por pager<br /><br /> **4**= tem notificação **net send** .|  
|**sinalizadores**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)].|  
|**performance_condition**|**nvarchar(512)**|Se o **tipo** for **2**, essa coluna mostrará a definição da condição de desempenho. Se **Type** for **3**, essa coluna mostrará a consulta para o evento WMI. Caso contrário, a coluna será NULL.|  
|**category_name**|**sysname**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]Será sempre '**[Não categorizado]**' para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 7,0.|  
|**type**|**int**|Tipo de alerta:<br /><br /> **1**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] alerta de evento<br /><br /> **2**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] alerta de desempenho<br /><br /> **3** = alerta de evento WMI|  
  
## <a name="remarks"></a>Comentários  
 **sp_help_alert** deve ser executado do banco de dados **msdb** .  
  
## <a name="permissions"></a>Permissões  
 Por padrão, os membros da função de servidor fixa **sysadmin** podem executar este procedimento armazenado. Deve ser concedida a outros usuários a função de banco de dados fixa **SQLAgentOperatorRole** no banco de dados **msdb** .  
  
 Para obter detalhes sobre **SQLAgentOperatorRole**, consulte [SQL Server Agent funções de banco de dados fixas](../../ssms/agent/sql-server-agent-fixed-database-roles.md).  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir relata informações sobre o alerta `Demo: Sev. 25 Errors`.  
  
```  
USE msdb ;  
GO  
  
EXEC sp_help_alert @alert_name = 'Demo: Sev. 25 Errors';  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [&#41;&#40;Transact-SQL de sp_add_alert](../../relational-databases/system-stored-procedures/sp-add-alert-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_update_alert](../../relational-databases/system-stored-procedures/sp-update-alert-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
