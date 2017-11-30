---
title: sp_help_alert (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 08/09/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_help_alert
- sp_help_alert_TSQL
dev_langs: TSQL
helpviewer_keywords: sp_help_alert
ms.assetid: 850cef4e-6348-4439-8e79-fd1bca712091
caps.latest.revision: "25"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d574d40ff9c65f9a677fd0a4946428598b91476d
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/27/2017
---
# <a name="sphelpalert-transact-sql"></a>sp_help_alert (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Relata informações sobre os alertas definidos para o servidor.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_help_alert [ [ @alert_name = ] 'alert_name' ]   
     [ , [ @order_by = ] 'order_by' ]   
     [ , [ @alert_id = ] alert_id ]   
     [ , [ @category_name = ] 'category' ]   
     [ , [ @legacy_format = ] legacy_format ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@alert_name =**] **'***alert_name***'**  
 O nome do alerta. *alert_name* é **nvarchar (128)**. Se *alert_name* não é especificado, serão retornadas informações sobre todos os alertas.  
  
 [  **@order_by =**] **'***order_by***'**  
 A ordem de classificação a ser usada para produzir os resultados. *order_by*é **sysname**, com um padrão de N '*nome*'.  
  
 [  **@alert_id =**] *alert_id*  
 O número de identificação do alerta sobre o qual relatar informações. *alert_id*é **int**, com um padrão NULL.  
  
 [  **@category_name =**] **'***categoria***'**  
 A categoria do alerta. *categoria de* é **sysname**, com um padrão NULL.  
  
 [  **@legacy_format** =] *legacy_format*  
 Especifica se um conjunto de resultados legado deve ser produzido. *legacy_format* é **bit**, com um padrão de **0**. Quando *legacy_format* é **1**, **sp_help_alert** retorna o conjunto de resultados retornado por **sp_help_alert** no Microsoft SQL Server 2000.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Quando  **@legacy_format**  é **0**, **sp_help_alert** produz o seguinte conjunto de resultados.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**id**|**int**|Identificador inteiro exclusivo atribuído pelo sistema.|  
|**name**|**sysname**|Nome do alerta (por exemplo, demonstração: completo **msdb** log).|  
|**origem do evento**|**nvarchar (100)**|Origem do evento. Sempre será **MSSQLServer** para [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] versão 7.0|  
|**event_category_id**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**event_id**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**message_id**|**int**|Número de erro de mensagem que define o alerta. (Normalmente corresponde a um número de erro no **sysmessages** tabela). Se for usada gravidade para definir o alerta, **message_id** é **0** ou nulo.|  
|**severidade**|**int**|Nível de gravidade (de **9** por meio de **25**, **110**, **120**, **130**, ou **140**) que define o alerta.|  
|**habilitado**|**tinyint**|Status de alerta está habilitado no momento (**1**) ou não (**0**). Um alerta não habilitado não é enviado.|  
|**delay_between_responses**|**int**|Período de espera, em segundos, entre respostas ao alerta.|  
|**last_occurrence_date**|**int**|Data em que o alerta ocorreu pela última vez.|  
|**last_occurrence_time**|**int**|Hora em que o alerta ocorreu pela última vez.|  
|**last_response_date**|**int**|Data o alerta foi respondida pelo **SQLServerAgent** serviço.|  
|**last_response_time**|**int**|Tempo que o alerta foi respondida pelo **SQLServerAgent** serviço.|  
|**notification_message**|**nvarchar(512)**|Mensagem adicional opcional enviada ao operador como parte do email ou notificação de pager.|  
|**include_event_description**|**tinyint**|Define se a descrição do erro do SQL Server a partir do log de aplicativos do Microsoft Windows deve ser incluída como parte da mensagem de notificação.|  
|**database_name**|**sysname**|Banco de dados no qual o erro deve acontecer para que o alerta seja acionado. Se o nome de banco de dados for NULL, o alerta será acionado independentemente de onde o erro ocorreu.|  
|**event_description_keyword**|**nvarchar (100)**|Descrição do erro do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no log de aplicativos do Windows que deve ser como a sequência de caracteres fornecida.|  
|**occurrence_count**|**int**|Número de vezes que o alerta ocorreu.|  
|**count_reset_date**|**int**|Data de **occurrence_count** foi redefinido pela última vez.|  
|**count_reset_time**|**int**|Tempo de **occurrence_count** foi redefinido pela última vez.|  
|**job_id**|**uniqueidentifier**|Número de identificação do trabalho a ser executado em resposta a um alerta.|  
|**job_name**|**sysname**|Nome do trabalho a ser executado em resposta a um alerta.|  
|**has_notification**|**int**|Diferente de zero se um ou mais operadores forem notificados para este alerta. O valor é um ou mais dos seguintes valores (ORed junto):<br /><br /> **1**= tem notificação de email<br /><br /> **2**= tem notificação de pager<br /><br /> **4**= tem **net send** notificação.|  
|**sinalizadores**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**performance_condition**|**nvarchar(512)**|Se **tipo** é **2**, esta coluna mostra a definição da condição de desempenho; caso contrário, a coluna será NULL.|  
|**category_name**|**sysname**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)] sempre será '[Uncategorized]' para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 7.0.|  
|**wmi_namespace**|**sysname**|Se **tipo** é **3**, esta coluna mostra o namespace do evento WMI.|  
|**wmi_query**|**nvarchar(512)**|Se **tipo** é **3**, esta coluna mostra a consulta para o evento WMI.|  
|**tipo**|**int**|Tipo do evento:<br /><br /> **1**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] alerta de evento<br /><br /> **2**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] alerta de desempenho<br /><br /> **3** = alerta de eventos WMI|  
  
 Quando  **@legacy_format**  é **1**, **sp_help_alert** produz o seguinte conjunto de resultados.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**id**|**int**|Identificador inteiro exclusivo atribuído pelo sistema.|  
|**name**|**sysname**|Nome do alerta (por exemplo, demonstração: completo **msdb** log).|  
|**origem do evento**|**nvarchar (100)**|Origem do evento. Sempre será **MSSQLServer** para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] versão 7.0|  
|**event_category_id**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**event_id**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**message_id**|**int**|Número de erro de mensagem que define o alerta. (Normalmente corresponde a um número de erro no **sysmessages** tabela). Se for usada gravidade para definir o alerta, **message_id** é **0** ou nulo.|  
|**severidade**|**int**|Nível de gravidade (de **9** por meio de **25**, **110**, **120**, **130**, ou 1**40**) que define o alerta.|  
|**habilitado**|**tinyint**|Status de alerta está habilitado no momento (**1**) ou não (**0**). Um alerta não habilitado não é enviado.|  
|**delay_between_responses**|**int**|Período de espera, em segundos, entre respostas ao alerta.|  
|**last_occurrence_date**|**int**|Data em que o alerta ocorreu pela última vez.|  
|**last_occurrence_time**|**int**|Hora em que o alerta ocorreu pela última vez.|  
|**last_response_date**|**int**|Data o alerta foi respondida pelo **SQLServerAgent** serviço.|  
|**last_response_time**|**int**|Tempo que o alerta foi respondida pelo **SQLServerAgent** serviço.|  
|**notification_message**|**nvarchar(512)**|Mensagem adicional opcional enviada ao operador como parte do email ou notificação de pager.|  
|**include_event_description**|**tinyint**|Define se a descrição do erro do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a partir do log de aplicativos do Windows deve ser incluída como parte da mensagem de notificação.|  
|**database_name**|**sysname**|Banco de dados no qual o erro deve acontecer para que o alerta seja acionado. Se o nome de banco de dados for NULL, o alerta será acionado independentemente de onde o erro ocorreu.|  
|**event_description_keyword**|**nvarchar (100)**|Descrição do erro do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no log de aplicativos do Windows que deve ser como a sequência de caracteres fornecida.|  
|**occurrence_count**|**int**|Número de vezes que o alerta ocorreu.|  
|**count_reset_date**|**int**|Data de **occurrence_count** foi redefinido pela última vez.|  
|**count_reset_time**|**int**|Tempo de **occurrence_count** foi redefinido pela última vez.|  
|**job_id**|**uniqueidentifier**|Número de identificação do trabalho.|  
|**job_name**|**sysname**|Um trabalho sob demanda a ser executado em resposta a um alerta.|  
|**has_notification**|**int**|Diferente de zero se um ou mais operadores forem notificados para este alerta. O valor é um ou mais dos seguintes (unidos por OR):<br /><br /> **1**= tem notificação de email<br /><br /> **2**= tem notificação de pager<br /><br /> **4**= tem **net send** notificação.|  
|**sinalizadores**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)].|  
|**performance_condition**|**nvarchar(512)**|Se **tipo** é **2**, esta coluna mostra a definição da condição de desempenho. Se **tipo** é **3**, esta coluna mostra a consulta para o evento WMI. Caso contrário, a coluna será NULL.|  
|**category_name**|**sysname**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]Sempre será '**[Uncategorized]**' para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 7.0.|  
|**tipo**|**int**|Tipo de alerta:<br /><br /> **1**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] alerta de evento<br /><br /> **2**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] alerta de desempenho<br /><br /> **3** = alerta de eventos WMI|  
  
## <a name="remarks"></a>Comentários  
 **sp_help_alert** deve ser executado a partir de **msdb** banco de dados.  
  
## <a name="permissions"></a>Permissões  
 Por padrão, os membros da função de servidor fixa **sysadmin** podem executar este procedimento armazenado. Deve ser concedida a outros usuários a função de banco de dados fixa **SQLAgentOperatorRole** no banco de dados **msdb** .  
  
 Para obter detalhes sobre **SQLAgentOperatorRole**, consulte [funções de banco de dados fixa do SQL Server Agent](http://msdn.microsoft.com/library/719ce56b-d6b2-414a-88a8-f43b725ebc79).  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir relata informações sobre o alerta `Demo: Sev. 25 Errors`.  
  
```  
USE msdb ;  
GO  
  
EXEC sp_help_alert @alert_name = 'Demo: Sev. 25 Errors';  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [sp_add_alert &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-alert-transact-sql.md)   
 [sp_update_alert &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-update-alert-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
