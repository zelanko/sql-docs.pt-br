---
title: DROP EVENT NOTIFICATION (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 852662f66b3989cfec15392218346d792be8b835
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66270218"
---
# <a name="drop-event-notification-transact-sql"></a>DROP EVENT NOTIFICATION (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Remove um disparador de notificação de eventos do banco de dados atual.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
DROP EVENT NOTIFICATION notification_name [ ,...n ]  
ON { SERVER | DATABASE | QUEUE queue_name }  
[ ; ]  
```  
  
## <a name="arguments"></a>Argumentos  
 *notification_name*  
 É o nome da notificação de eventos a ser removida. Podem ser especificadas várias notificações de eventos. Para ver uma lista de notificações de eventos atualmente criadas, use [event_notifications &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-event-notifications-transact-sql.md).  
  
 SERVER  
 Indica que o escopo da notificação de eventos se aplica ao servidor atual. SERVER deverá ser especificado se ele foi especificado quando a notificação de eventos foi criada.  
  
 DATABASE  
 Indica que o escopo da notificação de eventos se aplica ao banco de dados atual. DATABASE deverá ser especificado se ele foi especificado quando a notificação de eventos foi criada.  
  
 QUEUE *queue_name*  
 Indica que o escopo da notificação de eventos se aplica à fila especificada por *queue_name*. QUEUE deverá ser especificado se ele foi especificado quando a notificação de eventos foi criada. *queue_name* é o nome da fila e também deve ser especificado.  
  
## <a name="remarks"></a>Remarks  
 Se uma notificação de eventos for acionada em uma transação e for descartada na mesma transação, a instância da notificação de eventos será enviada e depois descartada.  
  
## <a name="permissions"></a>Permissões  
 Para descartar uma notificação de eventos cujo escopo seja o nível do banco de dados, no mínimo, o usuário deverá ser o proprietário da notificação de eventos ou ter permissão ALTER ANY DATABASE EVENT NOTIFICATION no banco de dados atual.  
  
 Para descartar uma notificação de eventos cujo escopo seja o nível do servidor, no mínimo, o usuário deverá ser o proprietário da notificação de eventos ou ter permissão ALTER ANY DATABASE EVENT NOTIFICATION no servidor.  
  
 Para descartar uma notificação de eventos em uma fila específica, no mínimo, o usuário deverá ser o proprietário da notificação de eventos ou ter permissão ALTER na fila pai.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir cria uma notificação de eventos com escopo no banco de dados e depois a descarta:  
  
```sql  
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
  
## <a name="see-also"></a>Consulte Também  
 [CREATE EVENT NOTIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/create-event-notification-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [sys.event_notifications &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-event-notifications-transact-sql.md)   
 [sys.events &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-events-transact-sql.md)  
  
  
