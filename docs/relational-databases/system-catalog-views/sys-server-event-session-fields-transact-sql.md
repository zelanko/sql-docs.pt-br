---
description: sys.server_event_session_fields (Transact-SQL)
title: sys. server_event_session_fields (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- server_event_session_fields
- server_event_session_fields_TSQL
- sys.server_event_session_fields
- sys.server_event_session_fields_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.server_event_session_fields catalog view
- xe
ms.assetid: 7109f9fb-8a1f-432c-92d1-6f8af3e96af1
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 18849b0e5a3911022e90a6f9a768fbbb7e921729
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89551376"
---
# <a name="sysserver_event_session_fields-transact-sql"></a>sys.server_event_session_fields (Transact-SQL)
[!INCLUDE[sqlserver](../../includes/applies-to-version/sqlserver.md)]

  Retorna uma linha para cada coluna personalizável explicitamente definida em eventos e destinos.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|event_session_id|**int**|A identificação da sessão de evento. Não permite valor nulo.|  
|object_id|**int**|A ID do objeto ao qual este campo é associado. Não permite valor nulo.|  
|name|**sysname**|O nome do campo. Não permite valor nulo.|  
|value|**sql_variant**|O valor do campo. Não permite valor nulo.|  
  
## <a name="permissions"></a>Permissões  
 , é necessário ter permissão VIEW SERVER STATE no servidor.  
  
## <a name="remarks"></a>Comentários  
 Essa exibição tem as cardinalidades de relação a seguir.  
  
| De | Para | Relação |
| ---- | -- | ------------ |
|sys.server_event_session_actions.event_session_id|sys. server_event_sessions. event_session_id|Muitos para um|  
|sys.server_event_session_actions.event_id<br /><br /> sys.server_event_session_actions.object_id<br /><br /> sys.server_event_session_actions.event_session_id|sys.server_event_session_events.event_session_id<br /><br /> sys.server_event_session_events.event_id|Muitos para um|  
|sys.server_event_session_actions.event_session_id<br /><br /> sys.server_event_session_actions.object_id|sys.server_event_session_targets.event_session_id<br /><br /> sys.server_event_session_targets.target_id|Muitos para um|  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Exibições de catálogo de eventos estendidos &#40;&#41;Transact-SQL ](../../relational-databases/system-catalog-views/extended-events-catalog-views-transact-sql.md)   
 [Eventos estendidos](../../relational-databases/extended-events/extended-events.md)  
  
  
