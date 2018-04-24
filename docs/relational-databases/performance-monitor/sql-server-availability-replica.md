---
title: SQL Server, Réplica de Disponibilidade | Microsoft Docs
ms.custom: ''
ms.date: 08/25/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: performance-monitor
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- performance counters [SQL Server], AlwaysOn Availability Groups
- SQLServer:Availability Replica
- Availability Groups [SQL Server], performance counters
ms.assetid: e402f996-c1fb-484a-b804-45c49972f2e0
caps.latest.revision: 25
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 7aad317c244b13d80c48188f921b1e75e24655aa
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="sql-server-availability-replica"></a>SQL Server, Réplica de Disponibilidade
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  O objeto de desempenho **SQLServer:Availability Replica** contém contadores de desempenho que relatam informações sobre as réplicas de disponibilidade em grupos de disponibilidade AlwaysOn no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Todos os contadores de desempenho de réplica de disponibilidade aplicam-se às réplicas primária e secundárias, com contadores de envio/recebimento refletindo a réplica local. Para a maior parte, a réplica primária envia a maioria dos dados e as réplicas secundárias recebem os dados. Porém, as réplicas secundárias enviam ACKs e algum outro tráfego em segundo plano para as réplicas primárias. Observe que, em uma determinada réplica de disponibilidade, alguns contadores mostrarão um valor igual a zero, dependendo da função atual, primária ou secundária, da réplica local.  
  
|Nome do contador|Description|  
|------------------|-----------------|  
|**Bytes Recebidos da Réplica/s**|O número de bytes recebidos da réplica de disponibilidade por segundo. Pings e atualizações de status gerarão tráfego de rede mesmo em bancos de dados sem atualizações de usuário.|  
|**Bytes Enviados à Réplica/s**|O número de bytes enviados à réplica de disponibilidade remota por segundo. Na réplica primária, esse é o número de bytes enviados à réplica secundária. Na réplica secundária, esse é o número de bytes enviados à réplica primária.|  
|**Bytes Enviados ao Transporte/s**|O número real de bytes enviados por segundo pela rede à réplica de disponibilidade remota. Na réplica primária, esse é o número de bytes enviados à réplica secundária. Na réplica secundária, esse é o número de bytes enviados à réplica primária.|  
|**Tempo de Controle de Fluxo (ms/s)**|Tempo em milissegundos que as mensagens do fluxo de log aguardaram pelo controle de fluxo de envio no último segundo.|  
|**Controle de Fluxo/s**|Número de vezes que o controle de fluxo foi iniciado no último segundo. **Tempo de Controle de Fluxo (ms/s)** dividido por **Controle de Fluxo/s** corresponde ao tempo médio por espera.|  
|**Recebimentos da Réplica/s**|Número de mensagens AlwaysOn recebidas da réplica de disponibilidade por segundo.|  
|**Mensagens Reenviadas/s**|Número de mensagens AlwaysOn reenviadas no último segundo.|  
|**Envios à Réplica/s**|Número de mensagens AlwaysOn enviadas a essa réplica de disponibilidade por segundo.|  
|**Envios ao Transporte/s**|O número real de mensagens AlwaysOn enviadas por segundo pela rede à réplica de disponibilidade remota. Na réplica primária, esse é o número de mensagens enviadas à réplica secundária. Na réplica secundária, esse é o número de mensagens enviadas à réplica primária.|  
  
## <a name="see-also"></a>Consulte Também  
 [Monitorar o uso de recursos &#40;Monitor do Sistema&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)   
 [SQL Server, Réplica de banco de dados](../../relational-databases/performance-monitor/sql-server-database-replica.md)   
 [Grupos de Disponibilidade AlwaysOn (SQL Server)](../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)  
  
  
