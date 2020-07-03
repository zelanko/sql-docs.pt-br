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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: b9fad9d93a1c0d4781f792fedfe3fe7649e17c98
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85891736"
---
# <a name="sp_help_notification-transact-sql"></a>sp_help_notification (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Informa uma lista de alertas para determinado operador ou uma lista de operadores para um determinado alerta.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
`[ @object_type = ] 'object_type'`O tipo de informações a serem retornadas. *object_type*é **Char (9)**, sem padrão. *object_type* pode ser alertas, que lista os alertas atribuídos ao nome do operador fornecido *,* ou operadores, que lista os operadores responsáveis pelo nome do alerta fornecido *.*  
  
`[ @name = ] 'name'`Um nome de operador (se *object_type* é operadores) ou um nome de alerta (se *object_type* for alertas). o *nome* é **sysname**, sem padrão.  
  
`[ @enum_type = ] 'enum_type'`As informações de *object_type*retornadas. *enum_type* é real na maioria dos casos. *enum_type*é **Char (10)**, sem padrão, e pode ser um desses valores.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|ACTUAL|Lista somente os *object_types* associados ao *nome*.|  
|ALL|Lista todos os*object_types* incluindo aqueles que não estão associados ao *nome*.|  
|TARGET|Lista somente o *object_types* correspondente ao *target_name*fornecido, independentemente da associação com o*nome*.|  
  
`[ @notification_method = ] notification_method`Um valor numérico que determina as colunas de método de notificação a serem retornadas. *notification_method* é **tinyint**e pode ser um dos valores a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**1**|Email: retorna apenas a coluna **use_email** .|  
|**2**|Pager: retorna apenas a coluna **use_pager** .|  
|**4**|Netsend: retorna apenas a coluna **use_netsend** .|  
|**7**|Tudo: retorna todas as colunas.|  
  
`[ @target_name = ] 'target_name'`Um nome de alerta a ser pesquisado (se *object_type* é alertas) ou um nome de operador para pesquisar (se *object_type* forem operadores). *target_name* será necessário somente se *ENUM_TYPE* for o destino. *target_name* é **sysname**, com um padrão de NULL.  
  
## <a name="return-code-valves"></a>Valores de código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Se *object_type* for **alertas**, o conjunto de resultados listará todos os alertas de um determinado operador.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**alert_id**|**int**|Número de identificador de alerta.|  
|**alert_name**|**sysname**|Nome do alerta.|  
|**use_email**|**int**|Email é usado para notificar o operador:<br /><br /> **1** = Sim<br /><br /> **0** = não|  
|**use_pager**|**int**|Pager é usado para notificar o operador:<br /><br /> **1** = Sim<br /><br /> **0** = não|  
|**use_netsend**|**int**|Pop-up de rede é usado para notificar o operador:<br /><br /> **1** = Sim<br /><br /> **0** = não|  
|**has_email**|**int**|Número de notificações de email enviadas para esse alerta.|  
|**has_pager**|**int**|Número de notificações de pager enviadas para esse alerta.|  
|**has_netsend**|**int**|Número de notificações do **net send** enviadas para este alerta.|  
  
 Se **object_type** for **Operators**, o conjunto de resultados listará todos os operadores de um determinado alerta.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**operator_id**|**int**|Número de identificação do operador.|  
|**operator_name**|**sysname**|Nome do operador.|  
|**use_email**|**int**|O email é usado para enviar uma notificação ao operador:<br /><br /> **1** = Sim<br /><br /> **0** = não|  
|**use_pager**|**int**|O pager é usado para enviar uma notificação ao operador:<br /><br /> **1** = Sim<br /><br /> **0** = não|  
|**use_netsend**|**int**|É um pop-up de rede usado para notificar o operador:<br /><br /> **1** = Sim<br /><br /> **0** = não|  
|**has_email**|**int**|O operador tem um endereço de email:<br /><br /> **1** = Sim<br /><br /> **0** = não|  
|**has_pager**|**int**|O operador tem um endereço de pager:<br /><br /> **1** = Sim<br /><br /> **0** = não|  
|**has_netsend**|**int**|O operador tem uma notificação net send configurada.<br /><br /> **1** = Sim<br /><br /> **0** = não|  
  
## <a name="remarks"></a>Comentários  
 Esse procedimento armazenado deve ser executado do banco de dados **msdb** .  
  
## <a name="permissions"></a>Permissões  
 Para executar este procedimento armazenado, o usuário deve ser um membro da função de servidor fixa **sysadmin** .  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-listing-alerts-for-a-specific-operator"></a>a. Listando alertas para um operador específico  
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
  
## <a name="see-also"></a>Consulte Também  
 [&#41;&#40;Transact-SQL de sp_add_notification](../../relational-databases/system-stored-procedures/sp-add-notification-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_delete_notification](../../relational-databases/system-stored-procedures/sp-delete-notification-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_update_notification](../../relational-databases/system-stored-procedures/sp-update-notification-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
