---
title: Tipos de espera de Grupos de Disponibilidade Always On (SQL Server) | Microsoft Docs
ms.custom: ag-guide
ms.date: 06/13/2017
ms.prod: sql-server-2016
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: afa8caff-f325-48d9-a8ef-a30beab60389
caps.latest.revision: 6
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 6b74bcf7846c296a7d3d9f1e559712da9f46fc68
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="always-on-availability-groups-wait-types"></a>Tipos de espera de Grupos de Disponibilidade Always On
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Ao solucionar problemas de latência de Grupos de Disponibilidade Always On, as estatísticas de espera podem ser monitoradas para acúmulo, usando os tipos de espera de disponibilidade específicos de grupos na DMV (exibição de gerenciamento dinâmico) [sys.dm_os_wait_stats &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md).  
  
 Para obter informações gerais sobre como usar estatísticas de espera, veja [Espera e filas do SQL Server 2005](https://technet.microsoft.com/library/cc966413.aspx). Esse documento foi escrito para o SQL Server 2005, mas as informações podem ser aplicadas a versões mais recentes do SQL Server.  
  
## <a name="query-for-availability-groups-wait-types"></a>Consultar tipos de espera de grupos de disponibilidade  
 Use a consulta T-SQL abaixo para recuperar todas as estatísticas de espera com os tipos de espera de grupos de disponibilidade:  
  
```sql  
SELECT * FROM sys.dm_os_wait_stats   
WHERE wait_type LIKE '%hadr%'  
ORDER BY wait_time_ms DESC  
```  
  
 Para monitorar as estatísticas de espera, capturando eventos estendidos, use o seguinte comando T-SQL.  
  
```sql
CREATE EVENT SESSION [alwayson] ON SERVER   
ADD EVENT sqlos.wait_info(  
    WHERE ([wait_type]=(758) OR [wait_type]=(776) OR [wait_type]=(853) OR [wait_type]=(833)))  
WITH (MAX_MEMORY=4096 KB,EVENT_RETENTION_MODE=ALLOW_SINGLE_EVENT_LOSS,MAX_DISPATCH_LATENCY=30 SECONDS,  
MAX_EVENT_SIZE=0 KB,MEMORY_PARTITION_MODE=NONE,TRACK_CAUSALITY=OFF,STARTUP_STATE=OFF)  
GO  
```  
  
 Você pode exibir o mapeamento de chave-valor do tipo de espera executando a seguinte consulta:  
  
```sql
SELECT * FROM sys.dm_xe_map_values   
WHERE name='wait_types' AND map_value LIKE '%hadr%'   
ORDER BY map_key ASC  
```  
  
## <a name="next-steps"></a>Próximas etapas  
 [Tipos de esperas](~/relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md#WaitTypes)  
  
  