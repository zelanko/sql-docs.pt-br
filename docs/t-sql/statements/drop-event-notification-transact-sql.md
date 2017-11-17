---
title: DROP EVENT NOTIFICATION (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DROP EVENT NOTIFICATION
- DROP_EVENT_NOTIFICATION_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- event notifications [SQL Server], removing
- deleting event notifications
- dropping event notifications
- DROP EVENT NOTIFICATION statement
- removing event notifications
ms.assetid: 0ffd8f47-4ea3-4238-9e73-c318df710cf7
caps.latest.revision: 33
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: ab32a9ffadce83635e8ef987607af913fe0f2472
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="drop-event-notification-transact-sql"></a>DROP EVENT NOTIFICATION (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Remove um disparador de notificação de eventos do banco de dados atual.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
DROP EVENT NOTIFICATION notification_name [ ,...n ]  
ON { SERVER | DATABASE | QUEUE queue_name }  
[ ; ]  
```  
  
## <a name="arguments"></a>Argumentos  
 *notification_name*  
 É o nome da notificação de eventos a ser removida. Podem ser especificadas várias notificações de eventos. Para ver uma lista de notificações de eventos atualmente criadas, use [event_notifications &#40; Transact-SQL &#41; ](../../relational-databases/system-catalog-views/sys-event-notifications-transact-sql.md).  
  
 SERVER  
 Indica que o escopo da notificação de eventos se aplica ao servidor atual. SERVER deverá ser especificado se ele foi especificado quando a notificação de eventos foi criada.  
  
 DATABASE  
 Indica que o escopo da notificação de eventos se aplica ao banco de dados atual. DATABASE deverá ser especificado se ele foi especificado quando a notificação de eventos foi criada.  
  
 FILA *nome_da_fila*  
 Indica o escopo da notificação de eventos se aplica à fila especificada pelo *nome_da_fila*. QUEUE deverá ser especificado se ele foi especificado quando a notificação de eventos foi criada. *nome_da_fila* é o nome da fila e também deve ser especificado.  
  
## <a name="remarks"></a>Comentários  
 Se uma notificação de eventos for acionada em uma transação e for descartada na mesma transação, a instância da notificação de eventos será enviada e depois descartada.  
  
## <a name="permissions"></a>Permissões  
 Para descartar uma notificação de eventos cujo escopo seja o nível do banco de dados, no mínimo, o usuário deverá ser o proprietário da notificação de eventos ou ter permissão ALTER ANY DATABASE EVENT NOTIFICATION no banco de dados atual.  
  
 Para descartar uma notificação de eventos cujo escopo seja o nível do servidor, no mínimo, o usuário deverá ser o proprietário da notificação de eventos ou ter permissão ALTER ANY DATABASE EVENT NOTIFICATION no servidor.  
  
 Para descartar uma notificação de eventos em uma fila específica, no mínimo, o usuário deverá ser o proprietário da notificação de eventos ou ter permissão ALTER na fila pai.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir cria uma notificação de eventos com escopo no banco de dados e depois a descarta:  
  
```tsql  
USE AdventureWorks2012;  
GO  
CREATE EVENT NOTIFICATION NotifyALTER_T1  
ON DATABASE  
FOR ALTER_TABLE  
TO SERVICE 'NotifyService',  
    '8140a771-3c4b-4479-8ac0-81008ab17984';  
GO  
DROP EVENT NOTIFICATION NotifyALTER_T1  
ON DATABASE;  
```  
  
## <a name="see-also"></a>Consulte também  
 [Criar notificação de eventos &#40; Transact-SQL &#41;](../../t-sql/statements/create-event-notification-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [event_notifications &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-event-notifications-transact-sql.md)   
 [Events &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-events-transact-sql.md)  
  
  

