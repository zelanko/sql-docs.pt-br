---
description: sys.server_events (Transact-SQL)
title: sys. server_events (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
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
author: markingmyname
ms.author: maghan
ms.openlocfilehash: f451456320e7248f48be5a9b7233f1a6cf5b2968
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89551363"
---
# <a name="sysserver_events-transact-sql"></a>sys.server_events (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Contém uma linha para cada evento ao qual é acionada uma notificação de eventos do nível de servidor ou um gatilho DDL do nível de servidor. As colunas **object_id** e **tipo** identificam exclusivamente o evento de servidor.  

  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|ID da notificação de eventos no nível de servidor ou gatilho DDL no nível de servidor a serem acionados.|  
|**tipo**|**int**|Tipo do evento que provoca o acionamento da notificação de eventos ou do gatilho DDL.|  
|**type_desc**|**nvarchar(60)**|Descrição do evento que provoca o acionamento do gatilho DDL ou da notificação de eventos.|  
|**event_group_type**|**int**|Grupo de eventos no qual o gatilho ou a notificação de eventos são criados, ou NULL quando não é criado em um grupo de eventos.|  
|**event_group_type_desc**|**nvarchar(60)**|Descrição do grupo de eventos no qual o gatilho ou a notificação de eventos são criados, ou NULL quando não for criado em um grupo de eventos.|  
  
## <a name="permissions"></a>Permissões  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições de catálogo de objeto&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [Exibições de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
