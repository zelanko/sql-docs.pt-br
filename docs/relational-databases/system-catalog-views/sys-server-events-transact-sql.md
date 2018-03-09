---
title: server_events (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- server_events_TSQL
- sys.server_events_TSQL
- server_events
- sys.server_events
dev_langs:
- TSQL
helpviewer_keywords:
- sys.server_events catalog view
ms.assetid: 996f6c9b-6426-4847-95d9-6b77541422be
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: bbacdd3b1f3943906be711c64f2368c4a5e7a779
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="sysserverevents-transact-sql"></a>sys.server_events (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contém uma linha para cada evento ao qual é acionada uma notificação de eventos do nível de servidor ou um gatilho DDL do nível de servidor. As colunas **object_id** e **tipo** identificar exclusivamente o evento de servidor.  

  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|ID da notificação de eventos no nível de servidor ou gatilho DDL no nível de servidor a serem acionados.|  
|**tipo**|**int**|Tipo do evento que provoca o acionamento da notificação de eventos ou do gatilho DDL.|  
|**type_desc**|**nvarchar (60)**|Descrição do evento que provoca o acionamento do gatilho DDL ou da notificação de eventos.|  
|**event_group_type**|**int**|Grupo de eventos no qual o gatilho ou a notificação de eventos são criados, ou NULL quando não é criado em um grupo de eventos.|  
|**event_group_type_desc**|**nvarchar (60)**|Descrição do grupo de eventos no qual o gatilho ou a notificação de eventos são criados, ou NULL quando não for criado em um grupo de eventos.|  
  
## <a name="permissions"></a>Permissões  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte também  
 [Exibições de catálogo de objeto &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [Exibições de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
