---
title: sys. server_event_session_actions (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.server_event_session_actions
- server_event_session_actions_TSQL
- server_event_session_actions
- sys.server_event_session_actions_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.server_event_session_actions catalog view
- xe
ms.assetid: 1d8c604e-4361-4846-8661-14cfd1c44f63
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: dc3aa8a3dc8fd33e0e2b1a4b57968ad08f312f0d
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85664613"
---
# <a name="sysserver_event_session_actions-transact-sql"></a>sys.server_event_session_actions (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  Retorna uma linha para cada ação em cada evento de uma sessão de eventos.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|event_session_id|**int**|A identificação da sessão de evento. Não permite valor nulo.|  
|event_id|**int**|A ID do evento. Essa ID é exclusiva de um objeto da sessão de evento. Não permite valor nulo.|  
|name|**sysname**|O nome da ação. Permite valor nulo.|  
|pacote|**sysname**|O nome do pacote de eventos que contém um evento. Permite valor nulo.|  
|module|**sysname**|O nome do módulo que contém o evento. Permite valor nulo.|  
  
## <a name="permissions"></a>Permissões  
 , é necessário ter permissão VIEW SERVER STATE no servidor.  
  
## <a name="remarks"></a>Comentários  
 Essa exibição tem as cardinalidades de relação a seguir.  
  
||||  
|-|-|-|  
|De|Para|Relação|  
|sys.server_event_session_actions.event_session_id|sys.sys.server_event_sessions.event_session_id|Muitos para um|  
|sys.server_event_session_actions.event_id<br /><br /> sys.server_event_session_actions.event_session_id|sys.server_event_session_events.event_session_id<br /><br /> sys.server_event_session_events.event_id|Muitos para um|  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições de catálogo &#40;&#41;Transact-SQL](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Exibições de catálogo de eventos estendidos &#40;&#41;Transact-SQL](../../relational-databases/system-catalog-views/extended-events-catalog-views-transact-sql.md)   
 [Eventos estendidos](../../relational-databases/extended-events/extended-events.md)  
  
  
