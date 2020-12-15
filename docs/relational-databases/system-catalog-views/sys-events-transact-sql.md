---
description: sys.events (Transact-SQL)
title: sys. Events (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.events_TSQL
- sys.events
- events_TSQL
- events
dev_langs:
- TSQL
helpviewer_keywords:
- sys.events catalog view
ms.assetid: f245a97a-80fc-43fb-a6e4-139420c9a47a
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 3383217a22167b5255f748792952949396138fe4
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97413047"
---
# <a name="sysevents-transact-sql"></a>sys.events (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  Contém uma linha para cada evento para qual um gatilho ou uma notificação de eventos são disparados. Esses eventos representam os tipos de evento que são especificados quando a notificação de evento ou gatilho é criada usando [CREATE TRIGGER](../../t-sql/statements/create-trigger-transact-sql.md) ou [CREATE EVENT NOTIFICATION](../../t-sql/statements/create-event-notification-transact-sql.md).  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|ID do gatilho ou da notificação de eventos. Esse valor, juntamente com o **tipo**, identifica exclusivamente a linha.|  
|**tipo**|**int**|Evento que faz o gatilho ser disparado.|  
|**type_desc**|**nvarchar(60)**|Descrição do evento que faz o gatilho ser disparado.|  
|**is_trigger_event**|**bit**|1 = Evento de gatilho.<br /><br /> 0 = Evento de notificação.|  
|**event_group_type**|**int**|Grupo de eventos no qual o gatilho ou a notificação de eventos são criados, ou NULL quando não é criado em um grupo de eventos.|  
|**event_group_type_desc**|**nvarchar(60)**|Descrição do grupo de eventos no qual o gatilho ou a notificação de eventos são criados, ou NULL quando não é criado em um grupo de eventos.|  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições de catálogo de objeto&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [Exibições de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
