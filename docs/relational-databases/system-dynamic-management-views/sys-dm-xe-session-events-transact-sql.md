---
title: sys.dm_xe_session_events (Transact-SQL) | Microsoft Docs
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
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: ada8092471c107766881d1cd8b8700b612207ee2
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47665489"
---
# <a name="sysdmxesessionevents-transact-sql"></a>sys.dm_xe_session_events (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna informações sobre os eventos da sessão. Eventos são pontos de execução discretos. Predicados poderão ser se aplicados a eventos para fazer com que parem de acionar caso o evento não contiver a informação exigida.  
   
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|event_session_address|**varbinary(8)**|O endereço da memória da sessão de evento. Não permite valor nulo.|  
|event_name|**nvarchar(60)**|O nome do evento ao qual uma ação está associada. Não permite valor nulo.|  
|event_package_guid|**uniqueidentifier**|A GUID para o pacote que contém o evento. Não permite valor nulo.|  
|event_predicate|**nvarchar(2048)**|Uma representação XML da árvore de predicado que é aplicada ao evento. Permite valor nulo.|  
  
## <a name="permissions"></a>Permissões  
 , é necessário ter permissão VIEW SERVER STATE no servidor.  
  
### <a name="relationship-cardinalities"></a>Cardinalidades de relações  
  
|De|Para|Relação|  
|----------|--------|------------------|  
|sys.dm_xe_session_events.event_session_address|sys.dm_xe_sessions.address|Muitos para um|  
|sys.dm_xe_session_events.event_package_guid, sys.dm_xe_session_events.event_name|sys.dm_xe_objects.name, sys.dm_xe_objects.package_guid|Muitos para um|  
  
## <a name="see-also"></a>Consulte também  
 [Exibições e funções de gerenciamento dinâmico &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)  
  
  

