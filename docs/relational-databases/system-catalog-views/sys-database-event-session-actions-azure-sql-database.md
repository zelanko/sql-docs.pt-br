---
title: sys. database_event_session_actions (banco de dados SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
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
ms.assetid: 32494df1-7ab7-4b88-a858-6b1021d67433
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: d9bea94e4e51b18fb345543d74cd079ccf21bdb8
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43077706"
---
# <a name="sysdatabaseeventsessionactions-azure-sql-database"></a>sys.database_event_session_actions (Banco de Dados SQL do Azure)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Retorna uma linha para cada ação em cada evento de uma sessão de eventos.  
  
||  
|-|  
|**Aplica-se ao**: [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] V12 e versões posteriores.|  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|event_session_id|**int**|A identificação da sessão de evento. Não permite valor nulo.|  
|event_id|**int**|A ID do evento. Essa ID é exclusiva de um objeto da sessão de evento. Não permite valor nulo.|  
|nome|**sysname**|O nome da ação. Permite valor nulo.|  
|pacote|**sysname**|O nome do pacote de eventos que contém um evento. Permite valor nulo.|  
|módulo|**sysname**|O nome do módulo que contém o evento. Permite valor nulo.|  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão VIEW DATABASE STATE no servidor.  
  
## <a name="remarks"></a>Remarks  
 Essa exibição tem as cardinalidades de relação a seguir.  
  
||||  
|-|-|-|  
|De|Para|Relação|  
|sys.database_event_session_actions.event_session_id|sys.sys.database_event_sessions.event_session_id|Muitos para um|  
|sys.database_event_session_actions.event_id<br /><br /> sys.database_event_session_actions.event_session_id|sys.database_event_session_events.event_session_id<br /><br /> sys.database_event_session_events.event_id|Muitos para um|  
  
  
