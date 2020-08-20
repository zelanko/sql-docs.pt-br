---
description: sp_add_notification (Transact-SQL)
title: sp_add_notification (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_add_notification_TSQL
- sp_add_notification
dev_langs:
- TSQL
helpviewer_keywords:
- sp_add_notification
ms.assetid: 0525e0a2-ed0b-4e69-8a4c-a9e3e3622fbd
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 0c009cd32cf3fdd92fbb638a00d5f1f4a024a1b8
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88493522"
---
# <a name="sp_add_notification-transact-sql"></a>sp_add_notification (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Configura uma notificação para um alerta.  
  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_add_notification [ @alert_name = ] 'alert' ,   
    [ @operator_name = ] 'operator' ,   
    [ @notification_method = ] notification_method  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @alert_name = ] 'alert'` O alerta para esta notificação. o *alerta* é **sysname**, sem padrão.  
  
`[ @operator_name = ] 'operator'` O operador a ser notificado quando o alerta ocorrer. o *operador* é **sysname**, sem padrão.  
  
`[ @notification_method = ] notification_method` O método pelo qual o operador é notificado. *notification_method* é **tinyint**, sem padrão. *notification_method* pode ser um ou mais desses valores combinados com um operador lógico **or** .  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**1**|Email|  
|**2**|Pager|  
|**4**|**net send**|  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Nenhum  
  
## <a name="remarks"></a>Comentários  
 **sp_add_notification** deve ser executado do banco de dados **msdb** .  
  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] fornece um modo fácil e gráfico para gerenciar o sistema de alertas inteiro. Usar o [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] é o modo recomendado de configuração de sua infraestrutura de alerta.  
  
 Para enviar uma notificação em resposta a um alerta, primeiro você deve configurar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent para enviar email.  
  
 Se ocorrer uma falha ao enviar uma mensagem de email ou uma notificação de pager, a falha será relatada no log de erros do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros da função de servidor fixa **sysadmin** podem executar **sp_add_notification**.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir adiciona uma notificação de email para o alerta especificado (`Test Alert`).  
  
> **Observação:** Este exemplo supõe que `Test Alert` já existe e que `François Ajenstat` é um nome de operador válido.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_add_notification  
 @alert_name = N'Test Alert',  
 @operator_name = N'François Ajenstat',  
 @notification_method = 1 ;  
GO  
```  
  
## <a name="see-also"></a>Confira também  
 [&#41;&#40;Transact-SQL de sp_delete_notification ](../../relational-databases/system-stored-procedures/sp-delete-notification-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_help_notification ](../../relational-databases/system-stored-procedures/sp-help-notification-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_update_notification ](../../relational-databases/system-stored-procedures/sp-update-notification-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_add_operator ](../../relational-databases/system-stored-procedures/sp-add-operator-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
