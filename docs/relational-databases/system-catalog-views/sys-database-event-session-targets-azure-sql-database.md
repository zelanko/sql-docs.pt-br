---
title: sys. database_event_session_targets (banco de dados SQL) | Microsoft Docs
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
ms.assetid: 38d775ee-1fe1-4820-88c6-02b2f875a66b
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 3d1b59b0a9cc78dafb9b5847cb065fd981ec2495
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43075759"
---
# <a name="sysdatabaseeventsessiontargets-azure-sql-database"></a>sys.database_event_session_targets (Banco de Dados SQL do Azure)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Retorna uma linha para cada destino de evento em uma sessão de evento.  
  
||  
|-|  
|**Aplica-se ao**: [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] V12 e versões posteriores.|  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|event_session_id|**int**|A identificação da sessão de evento. Não permite valor nulo.|  
|target_id|**int**|A identificação do destino. Essa identificação é exclusiva dentro de um objeto de sessão de evento. Não permite valor nulo.|  
|nome|**sysname**|O nome do destino de evento. Não permite valor nulo.|  
|pacote|**sysname**|O nome do pacote de eventos que contém um destino de evento. Não permite valor nulo.|  
|módulo|**sysname**|O nome do módulo que contém um destino de evento. Não permite valor nulo.|  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão VIEW DATABASE STATE no servidor.  
  
## <a name="remarks"></a>Remarks  
 Essa exibição tem as cardinalidades de relação a seguir.  
  
||||  
|-|-|-|  
|De|Para|Relação|  
|sys.database_event_session_targets.event_session_id|sys.database_event_sessions.event_session_id|Muitos para um|  
  
## <a name="see-also"></a>Consulte também  
 [Eventos estendidos](../../relational-databases/extended-events/extended-events.md)  
  
  
