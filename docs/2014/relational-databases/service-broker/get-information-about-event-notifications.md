---
title: Obter informações sobre notificações de eventos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- event notifications [SQL Server], metadata
- status information [SQL Server], event notifications
- metadata [SQL Server], event notifications
ms.assetid: 8bc10867-66d6-4f57-ac32-a6c29f3327cd
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 9786faaf44724b1a2452bd5304b63deb2c9ea54e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63015305"
---
# <a name="get-information-about-event-notifications"></a>Obter informações sobre notificações de eventos
  As exibições de catálogo a seguir estão disponíveis para consultar metadados sobre notificações de eventos.  
  
 **Para obter informações sobre notificações de eventos em nível que não seja de servidor**  
  
-   [sys.event_notifications &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-event-notifications-transact-sql)  
  
> [!NOTE]  
>  Para exibir metadados sobre qualquer notificação de evento em **event_notifications** criados no banco de dados do nível, no mínimo deve ter o seguinte: CONTROLAR, ALTER, TAKE OWNERSHIP ou exibir permissão DEFINITION no banco de dados, ser o proprietário da notificação de eventos ou ter a permissão ALTER ANY DATABASE EVENT NOTIFICATION. As notificações de eventos criadas em uma fila específica, no mínimo você deve ter o seguinte: CONTROLAR, ALTER, TAKE OWNERSHIP ou exibir permissão DEFINITION no objeto, ser o proprietário da notificação de eventos ou ter a permissão ALTER ANY DATABASE EVENT NOTIFICATION.  
  
 **Para obter informações sobre notificações de eventos em nível de servidor**  
  
-   [sys.server_event_notifications &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-server-event-notifications-transact-sql)  
  
> [!NOTE]  
>  No mínimo, você deve ter o seguinte: CONTROLAR ou exibir qualquer permissão DEFINITION no servidor, ser o logon ou proprietário da notificação de eventos ou ter a permissão ALTER ANY EVENT NOTIFICATION para exibir metadados sobre qualquer notificação de evento em **server_event_notifications**.  
  
 **Para obter informações sobre todos os eventos que podem acionar notificações de eventos**  
  
-   [sys.event_notification_event_types &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-event-notification-event-types-transact-sql)  
  
> [!NOTE]  
>  Essa exibição de catálogo não retorna grupos de eventos.  
  
## <a name="see-also"></a>Consulte também  
 [Notificações de eventos](event-notifications.md)  
  
  
