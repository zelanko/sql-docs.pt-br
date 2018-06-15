---
title: Obter informações sobre notificações de eventos | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: service-broker
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- event notifications [SQL Server], metadata
- status information [SQL Server], event notifications
- metadata [SQL Server], event notifications
ms.assetid: 8bc10867-66d6-4f57-ac32-a6c29f3327cd
caps.latest.revision: 22
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e1e48620ea775cc4ae729ff9e85e4c82fa27fb0d
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32967901"
---
# <a name="get-information-about-event-notifications"></a>Obter informações sobre notificações de eventos
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
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
  
  
