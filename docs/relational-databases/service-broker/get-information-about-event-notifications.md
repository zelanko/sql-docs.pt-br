---
title: Obter informações sobre notificações de eventos | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
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
ms.openlocfilehash: fefdced57d611d241dbb96b71a0b220139683243
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68083828"
---
# <a name="get-information-about-event-notifications"></a>Obter informações sobre notificações de eventos
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  As exibições de catálogo a seguir estão disponíveis para consultar metadados sobre notificações de eventos.  
  
 **Para obter informações sobre notificações de eventos em nível que não seja de servidor**  
  
-   [sys.event_notifications &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-event-notifications-transact-sql.md)  
  
> [!NOTE]  
>  Para exibir metadados sobre qualquer notificação de eventos no **sys.event_notifications** criada no nível do banco de dados, é necessário ter, no mínimo, o seguinte: a permissão CONTROL, ALTER, TAKE OWNERSHIP ou VIEW DEFINITION no banco de dados, ser o proprietário da notificação de eventos ou ter a permissão ALTER ANY DATABASE EVENT NOTIFICATION. Para notificações de eventos criadas em uma fila específica, é necessário ter, no mínimo, o seguinte: a permissão CONTROL, ALTER, TAKE OWNERSHIP ou VIEW DEFINITION sobre o objeto, ser o proprietário da notificação de eventos ou ter a permissão ALTER ANY DATABASE EVENT NOTIFICATION.  
  
 **Para obter informações sobre notificações de eventos em nível de servidor**  
  
-   [sys.server_event_notifications &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-event-notifications-transact-sql.md)  
  
> [!NOTE]  
>  É necessário ter, no mínimo, o seguinte: permissão CONTROL ou VIEW ANY DEFINITION no servidor, ser o logon ou o proprietário da notificação de eventos ou ter a permissão ALTER ANY EVENT NOTIFICATION para exibir metadados sobre qualquer notificação de eventos em **sys.server_event_notifications**.  
  
 **Para obter informações sobre todos os eventos que podem acionar notificações de eventos**  
  
-   [sys.event_notification_event_types &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-event-notification-event-types-transact-sql.md)  
  
> [!NOTE]  
>  Essa exibição de catálogo não retorna grupos de eventos.  
  
## <a name="see-also"></a>Consulte Também  
 [Notificações de eventos](../../relational-databases/service-broker/event-notifications.md)  
  
  
