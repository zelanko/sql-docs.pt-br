---
title: sp_update_notification (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_update_notification_TSQL
- sp_update_notification
dev_langs:
- TSQL
helpviewer_keywords:
- sp_updatenotification
ms.assetid: 3e1c3d40-8c24-46ce-a68e-ce6c6a237fda
author: stevestein
ms.author: sstein
ms.openlocfilehash: 35cfa3aeda8e296cd1a85a0e8a098aaddac90954
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68084861"
---
# <a name="sp_update_notification-transact-sql"></a>sp_update_notification (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Atualiza o método de uma notificação de alerta.  

  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_update_notification  
          [@alert_name =] 'alert' ,  
     [@operator_name =] 'operator' ,  
     [@notification_method =] notification  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @alert_name = ] 'alert'`O nome do alerta associado a esta notificação. o *alerta* é **sysname**, sem padrão.  
  
`[ @operator_name = ] 'operator'`O operador que será notificado quando o alerta ocorrer. o *operador* é **sysname**, sem padrão.  
  
`[ @notification_method = ] notification`O método pelo qual o operador é notificado. a *notificação*é **tinyint**, sem padrão, e pode ser um ou mais desses valores.  
  
|Valor|DESCRIÇÃO|  
|-----------|-----------------|  
|**1**|Email|  
|**2**|Pager|  
|**quatro**|**net send**|  
|**7**|Todos os métodos|  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_update_notification** deve ser executado do banco de dados **msdb** .  
  
 Você pode atualizar uma notificação para um operador que não tem as informações de endereço necessárias usando o *notification_method*especificado. Se ocorrer uma falha ao enviar uma mensagem de email ou uma notificação de pager, a falha será relatada no log de erros do Microsoft SQL Server Agent.  
  
## <a name="permissions"></a>Permissões  
 Para executar esse procedimento armazenado, os usuários devem receber a função de servidor fixa **sysadmin** .  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir modifica o método de notificação para notificações enviadas `François Ajenstat`para o para `Test Alert`o alerta.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_update_notification  
   @alert_name = N'Test Alert',  
   @operator_name = N'François Ajenstat',  
   @notification_method = 7;  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [&#41;&#40;Transact-SQL de sp_add_notification](../../relational-databases/system-stored-procedures/sp-add-notification-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_delete_notification](../../relational-databases/system-stored-procedures/sp-delete-notification-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_help_notification](../../relational-databases/system-stored-procedures/sp-help-notification-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
