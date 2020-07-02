---
title: sys. dm_xe_session_events (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_xe_session_events
- sys.dm_xe_session_events_TSQL
- dm_xe_session_events
- dm_xe_session_events_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_xe_session_events dynamic management view
- extended events [SQL Server], views
ms.assetid: 4f027b31-4e03-43a6-849d-1ba9d8d34ae8
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 69cff79a8d9ef8de3bf6b38bb28884b2c0ade999
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85648346"
---
# <a name="sysdm_xe_session_events-transact-sql"></a>sys.dm_xe_session_events (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  Retorna informações sobre os eventos da sessão. Eventos são pontos de execução discretos. Predicados poderão ser se aplicados a eventos para fazer com que parem de acionar caso o evento não contiver a informação exigida.  
   
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|event_session_address|**varbinary (8)**|O endereço da memória da sessão de evento. Não permite valor nulo.|  
|event_name|**nvarchar(256)**|O nome do evento ao qual uma ação está associada. Não permite valor nulo.|  
|event_package_guid|**uniqueidentifier**|A GUID para o pacote que contém o evento. Não permite valor nulo.|  
|event_predicate|**nvarchar (3072)**|Uma representação XML da árvore de predicado que é aplicada ao evento. Permite valor nulo.|  
  
## <a name="permissions"></a>Permissões  
 , é necessário ter permissão VIEW SERVER STATE no servidor.  
  
### <a name="relationship-cardinalities"></a>Cardinalidades de relações  
  
|De|Para|Relação|  
|----------|--------|------------------|  
|sys.dm_xe_session_events.event_session_address|sys.dm_xe_sessions.address|Muitos para um|  
|sys. dm_xe_session_events. event_package_guid,<br /><br /> sys. dm_xe_session_events. event_name|sys.dm_xe_objects.name,<br /><br /> sys.dm_xe_objects.package_guid|Muitos para um|  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições e funções de gerenciamento dinâmico &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)  
  
  

