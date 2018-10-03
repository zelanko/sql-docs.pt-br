---
title: sp_help_notification (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_notification
- sp_help_notification_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_notification
ms.assetid: 0273457f-9d2a-4a6f-9a16-6a6bf281cba0
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 3ccc926844f6d3c054a69cb51f3156dc8e186a98
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47833574"
---
# <a name="sphelpnotification-transact-sql"></a>sp_help_notification (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Informa uma lista de alertas para determinado operador ou uma lista de operadores para um determinado alerta.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_help_notification  
     [ @object_type = ] 'object_type' ,  
     [ @name = ] 'name' ,  
     [ @enum_type = ] 'enum_type' ,   
     [ @notification_method = ] notification_method   
     [ , [ @target_name = ] 'target_name' ]   
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@object_type =**] **'***object_type***'**  
 O tipo de informação a ser retornado. *object_type*está **char(9)**, sem padrão. *object_type* pode ser ALERTS, que lista os alertas atribuídos ao nome de operador fornecido *,* ou OPERATORS, que lista os operadores responsáveis pelo nome de alerta fornecido *.*  
  
 [  **@name =**] **'***nome***'**  
 Um nome de operador (se *object_type* for OPERATORS) ou um nome de alerta (se *object_type* for ALERTS). *nome da* está **sysname**, sem padrão.  
  
 [  **@enum_type =**] **'***enum_type***'**  
 O *object_type*informações que são retornadas. *enum_type* é ACTUAL na maioria dos casos. *enum_type*está **char(10)**, sem padrão e pode ser um destes valores.  
  
|Valor|Description|  
|-----------|-----------------|  
|ACTUAL|Lista apenas os *object_types* associado *nome*.|  
|ALL|Lista todos os*object_types* incluindo aqueles que não estão associados *nome*.|  
|TARGET|Lista apenas os *object_types* correspondência fornecido *target_name*, independentemente da associação com*nome*.|  
  
 [  **@notification_method =**] *notification_method*  
 Um valor numérico que determina as colunas de método de notificação que devem ser retornadas. *notification_method* está **tinyint**, e pode ser um dos valores a seguir.  
  
|Valor|Description|  
|-----------|-----------------|  
|**1**|Email: retorna apenas o **use_email** coluna.|  
|**2**|Pager: retorna apenas o **use_pager** coluna.|  
|**4**|NetSend: retorna apenas o **use_netsend** coluna.|  
|**7**|Tudo: retorna todas as colunas.|  
  
 [  **@target_name =**] **'***target_name***'**  
 Um nome de alerta a ser pesquisado (se *object_type* for ALERTS) ou um nome de operador a ser pesquisado (se *object_type* for OPERATORS). *target_name* é necessária somente se *enum_type* é o destino. *target_name* está **sysname**, com um padrão NULL.  
  
## <a name="return-code-valves"></a>Valores de código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Se *object_type* é **alertas**, o conjunto de resultados listará todos os alertas para um determinado operador.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**alert_id**|**int**|Número de identificador de alerta.|  
|**alert_name**|**sysname**|Nome do alerta.|  
|**use_email**|**int**|Email é usado para notificar o operador:<br /><br /> **1** = Sim<br /><br /> **0** = Não|  
|**use_pager**|**int**|Pager é usado para notificar o operador:<br /><br /> **1** = Sim<br /><br /> **0** = Não|  
|**use_netsend**|**int**|Pop-up de rede é usado para notificar o operador:<br /><br /> **1** = Sim<br /><br /> **0** = Não|  
|**has_email**|**int**|Número de notificações de email enviadas para esse alerta.|  
|**has_pager**|**int**|Número de notificações de pager enviadas para esse alerta.|  
|**has_netsend**|**int**|Número de **net send** notificações enviadas para esse alerta.|  
  
 Se **object_type** é **OPERADORES**, o conjunto de resultados listará todos os operadores para um determinado alerta.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**operator_id**|**int**|Número de identificação do operador.|  
|**operator_name**|**sysname**|Nome do operador.|  
|**use_email**|**int**|O email é usado para enviar uma notificação ao operador:<br /><br /> **1** = Sim<br /><br /> **0** = Não|  
|**use_pager**|**int**|O pager é usado para enviar uma notificação ao operador:<br /><br /> **1** = Sim<br /><br /> **0** = Não|  
|**use_netsend**|**int**|É um pop-up de rede usado para notificar o operador:<br /><br /> **1** = Sim<br /><br /> **0** = Não|  
|**has_email**|**int**|O operador tem um endereço de email:<br /><br /> **1** = Sim<br /><br /> **0** = Não|  
|**has_pager**|**int**|O operador tem um endereço de pager:<br /><br /> **1** = Sim<br /><br /> **0** = Não|  
|**has_netsend**|**int**|O operador tem uma notificação net send configurada.<br /><br /> **1** = Sim<br /><br /> **0** = Não|  
  
## <a name="remarks"></a>Comentários  
 Esse procedimento armazenado deve ser executado a partir de **msdb** banco de dados.  
  
## <a name="permissions"></a>Permissões  
 Para executar este procedimento armazenado, o usuário deve ser um membro da função de servidor fixa **sysadmin** .  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-listing-alerts-for-a-specific-operator"></a>A. Listando alertas para um operador específico  
 O exemplo a seguir retorna todos os alertas para os quais o operador `François Ajenstat` recebe qualquer tipo de notificação.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_notification   
    @object_type = N'ALERTS',  
    @name = N'François Ajenstat',  
    @enum_type = N'ACTUAL',  
    @notification_method = 7 ;  
GO  
```  
  
### <a name="b-listing-operators-for-a-specific-alert"></a>B. Listando operadores para um alerta específico  
 O exemplo a seguir retorna todos os operadores que recebem qualquer tipo de notificação para o alerta `Test Alert`.  
  
```  
USE msdb ;  
GO  
  
EXEC sp_help_notification  
    @object_type = N'OPERATORS',  
    @name = N'Test Alert',  
    @enum_type = N'ACTUAL',  
    @notification_method = 7 ;  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [sp_add_notification &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-notification-transact-sql.md)   
 [sp_delete_notification &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-notification-transact-sql.md)   
 [sp_update_notification &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-update-notification-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
