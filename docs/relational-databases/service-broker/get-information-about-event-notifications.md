---
description: Obter informações sobre notificações de eventos
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
ms.openlocfilehash: bd3467841761b31d96e12bbc21c4d4a765406589
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88464867"
---
# <a name="get-information-about-event-notifications"></a>Obter informações sobre notificações de eventos
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  As exibições de catálogo a seguir estão disponíveis para consultar metadados sobre notificações de eventos.  
  
 **Para obter informações sobre notificações de eventos em nível que não seja de servidor**  
  
-   [sys.event_notifications &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-event-notifications-transact-sql.md)  
  
> [!NOTE]  
>  Para exibir metadados sobre qualquer notificação de eventos em **sys.event_notifications** criada no nível do banco de dados, é necessário ter, no mínimo, o seguinte: permissão CONTROL, ALTER, TAKE OWNERSHIP ou VIEW DEFINITION no banco de dados, permissão ALTER ANY DATABASE EVENT NOTIFICATION ou ser o proprietário da notificação de eventos. Para notificações de eventos criadas em uma fila específica, é necessário ter, no mínimo, o seguinte: permissão CONTROL, ALTER, TAKE OWNERSHIP ou VIEW DEFINITION no objeto, permissão ALTER ANY DATABASE EVENT NOTIFICATION ou ser o proprietário da notificação de eventos.  
  
 **Para obter informações sobre notificações de eventos em nível de servidor**  
  
-   [sys.server_event_notifications &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-event-notifications-transact-sql.md)  
  
> [!NOTE]  
>  É necessário ter, no mínimo, o seguinte: permissão CONTROL ou VIEW ANY DEFINITION no servidor, permissão ALTER ANY EVENT NOTIFICATION ou ser o logon ou proprietário da notificação de eventos para poder exibir metadados sobre qualquer notificação de eventos em **sys.server_event_notifications**.  
  
 **Para obter informações sobre todos os eventos que podem acionar notificações de eventos**  
  
-   [sys.event_notification_event_types &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-event-notification-event-types-transact-sql.md)  
  
> [!NOTE]  
>  Essa exibição de catálogo não retorna grupos de eventos.  
  
## <a name="see-also"></a>Consulte Também  
 [Notificações de eventos](../../relational-databases/service-broker/event-notifications.md)  
  
  
