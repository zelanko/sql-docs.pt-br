---
description: sysmail_delete_log_sp (Transact-SQL)
title: sysmail_delete_log_sp (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysmail_delete_log_sp_TSQL
- sysmail_delete_log_sp
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_delete_log_sp
ms.assetid: e94b37a1-70ad-46a5-86c0-721892156f7c
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: ae70fc03530ac80596ead5fe6e2e1927e323c5c8
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88473360"
---
# <a name="sysmail_delete_log_sp-transact-sql"></a>sysmail_delete_log_sp (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Exclui eventos do log do Database Mail. Exclui todos os eventos no log ou os eventos que atendem a critérios de data ou de tipo.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sysmail_delete_log_sp  [ [ @logged_before = ] 'logged_before' ]  
    [, [ @event_type = ] 'event_type' ]  
  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @logged_before = ] 'logged_before'` Exclui entradas até a data e a hora especificadas pelo argumento *logged_before* . *logged_before* é **DateTime** com NULL como padrão. NULL indica todas as datas.  
  
`[ @event_type = ] 'event_type'` Exclui entradas de log do tipo especificado como o *event_type*. *event_type* é **varchar (15)** sem padrão. As entradas válidas são **êxito**, **aviso**, **erro**e **informativo**. NULL indica todos os tipos de evento.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 Use o procedimento armazenado **sysmail_delete_log_sp** para excluir permanentemente as entradas do log de Database Mail. Um argumento opcional permite excluir somente os registros mais antigos fornecendo uma data e hora. Os eventos mais antigos que o argumento serão excluídos. Um argumento opcional permite excluir somente eventos de um determinado tipo, especificado como o argumento de **event_type** .  
  
 A exclusão de entradas no log do Database Mail não exclui as entradas de emails das tabelas do Database Mail. Use [sysmail_delete_mailitems_sp](../../relational-databases/system-stored-procedures/sysmail-delete-mailitems-sp-transact-sql.md) para excluir emails das tabelas de Database Mail.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros da função de servidor fixa **sysadmin** podem acessar esse procedimento.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-deleting-all-events"></a>a. Excluindo todos os eventos  
 O exemplo a seguir exclui todos os eventos no log do Database Mail.  
  
```  
EXECUTE msdb.dbo.sysmail_delete_log_sp ;  
GO  
```  
  
### <a name="b-deleting-the-oldest-events"></a>B. Excluindo os eventos mais antigos  
 O exemplo a seguir exclui os eventos no log do Database Mail anteriores a 9 de outubro de 2005.  
  
```  
EXECUTE msdb.dbo.sysmail_delete_log_sp  
    @logged_before = 'October 9, 2005' ;  
GO  
```  
  
### <a name="c-deleting-all-events-of-a-certain-type"></a>C. Excluindo todos os eventos de um determinado tipo  
 O exemplo a seguir exclui todas as mensagens de êxito no log do Database Mail.  
  
```  
EXECUTE msdb.dbo.sysmail_delete_log_sp  
    @event_type = 'success' ;  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [&#41;&#40;Transact-SQL de sysmail_event_log ](../../relational-databases/system-catalog-views/sysmail-event-log-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sysmail_delete_mailitems_sp ](../../relational-databases/system-stored-procedures/sysmail-delete-mailitems-sp-transact-sql.md)   
 [Criar um trabalho do SQL Server Agent para arquivar mensagens e logs de eventos do Database Mail](../../relational-databases/database-mail/create-a-sql-server-agent-job-to-archive-database-mail-messages-and-event-logs.md)  
  
  
