---
title: sys.database_event_session_events (banco de dados do SQL Azure) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.component: system-catalog-views
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- Azure SQL Database
ms.assetid: f4c9eb0a-173c-4c66-8dd8-6f7176b2657f
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 9287bfe2f99e4bebc7a57b9ac527c04ada95bf9b
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
ms.locfileid: "33178362"
---
# <a name="sysdatabaseeventsessionevents-azure-sql-database"></a>sys.database_event_session_events (banco de dados do SQL Azure)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Retorna uma linha para cada evento em uma sessão de evento.  
  
||  
|-|  
|**Aplica-se a**: [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] V12 e versões posteriores.|  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|event_session_id|**Int**|A identificação da sessão de evento. Não permite valor nulo.|  
|event_id|**Int**|A ID do evento. Essa ID é exclusiva dentro de um objeto de sessão de evento. Não permite valor nulo.|  
|nome|**sysname**|O nome do evento. Não permite valor nulo.|  
|pacote|**sysname**|O nome do pacote de eventos que contém um evento. Não permite valor nulo.|  
|Módulo|**sysname**|O nome do módulo que contém o evento. Não permite valor nulo.|  
|predicate|**nvarchar(3000)**|A expressão de predicado que é aplicada ao evento. Permite valor nulo.|  
|predicate_xml|**nvarchar(3000)**|A expressão de predicado XML que é aplicada ao evento. Permite valor nulo.|  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão VIEW DATABASE STATE no servidor.  
  
## <a name="remarks"></a>Remarks  
 Essa exibição tem as cardinalidades de relação a seguir.  
  
||||  
|-|-|-|  
|De|Para|Relação|  
|sys.database_event_session_events.event_session_id|sys.database_event_sessions.event_session_id|Muitos para um|  
  
## <a name="see-also"></a>Consulte também  
 [Eventos estendidos](../../relational-databases/extended-events/extended-events.md)  
  
  
