---
title: SQL Server, Réplica de Disponibilidade | Microsoft Docs
description: Saiba mais sobre o objeto de desempenho SSQLServer:Availability Replica, que contém contadores de desempenho sobre as réplicas de disponibilidade nos grupos de disponibilidade Always On.
ms.custom: ''
ms.date: 08/25/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- performance counters [SQL Server], AlwaysOn Availability Groups
- SQLServer:Availability Replica
- Availability Groups [SQL Server], performance counters
ms.assetid: e402f996-c1fb-484a-b804-45c49972f2e0
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.openlocfilehash: eb320ec65adf1a08df69954f133571c50de3eef8
ms.sourcegitcommit: 0e0cd9347c029e0c7c9f3fe6d39985a6d3af967d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/02/2020
ms.locfileid: "96505886"
---
# <a name="sql-server-availability-replica"></a>SQL Server, Réplica de Disponibilidade

 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  O objeto de desempenho **SQLServer:Availability Replica** contém contadores de desempenho que relatam informações sobre as réplicas de disponibilidade em grupos de disponibilidade AlwaysOn no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Todos os contadores de desempenho de réplica de disponibilidade aplicam-se às réplicas primária e secundárias, com contadores de envio/recebimento refletindo a réplica local. Para a maior parte, a réplica primária envia a maioria dos dados e as réplicas secundárias recebem os dados. Porém, as réplicas secundárias enviam ACKs e algum outro tráfego em segundo plano para as réplicas primárias. Observe que, em uma determinada réplica de disponibilidade, alguns contadores mostrarão um valor igual a zero, dependendo da função atual, primária ou secundária, da réplica local.  
  
|Nome do contador|Descrição|  
|------------------|-----------------|  
|**Bytes Recebidos da Réplica/s**|**No SQL Server 2012 e 2014:** número real de bytes (compactados) recebidos da réplica de disponibilidade por segundo (síncrona ou assíncrona). Pings e atualizações de status gerarão tráfego de rede mesmo em bancos de dados sem atualizações de usuário. <BR/> <BR/> **SQL Server 2016 e posteriores:** número real de bytes recebidos (compactados para assincronia, descompactados para sincronia) da réplica de disponibilidade por segundo.|  
|**Bytes Enviados à Réplica/s**|**No SQL Server 2012 e 2014:** número real de bytes (compactados) enviados por segundo pela rede para a réplica de disponibilidade remota (síncrona ou assíncrona). Por padrão, a compactação tem tanto a réplica síncrona quanto a assíncrona habilitadas. <BR/> <BR/> **No SQL Server 2016 e posterior:** O número de bytes enviados à réplica de disponibilidade remota por segundo. Antes da compactação da réplica assíncrona. (Número real de bytes da réplica síncrona sem compactação)|  
|**Bytes Enviados ao Transporte/s**|**No SQL Server 2012 e 2014:** número real de bytes enviados por segundo (compactados) pela rede para a réplica de disponibilidade remota (síncrona ou assíncrona). Por padrão, a compactação tem tanto a réplica síncrona quanto a assíncrona habilitadas. <BR/> <BR/> **No SQL Server 2016 e posterior:** número de bytes enviados para a réplica de disponibilidade remota por segundo Antes da compactação da réplica assíncrona. (Número real de bytes da réplica síncrona sem compactação)|  
|**Tempo de Controle de Fluxo (ms/s)**|Tempo em milissegundos que as mensagens do fluxo de log aguardaram pelo controle de fluxo de envio no último segundo.|  
|**Controle de Fluxo/s**|Número de vezes que o controle de fluxo foi iniciado no último segundo. **Tempo de Controle de Fluxo (ms/s)** dividido por **Controle de Fluxo/s** corresponde ao tempo médio por espera.|  
|**Recebimentos da Réplica/s**|Número de mensagens Always On recebidas da réplica por segundo.|  
|**Mensagens Reenviadas/s**|Número de mensagens AlwaysOn reenviadas no último segundo.|  
|**Envios à Réplica/s**|Número de mensagens AlwaysOn enviadas a essa réplica de disponibilidade por segundo.|  
|**Envios ao Transporte/s**|O número real de mensagens AlwaysOn enviadas por segundo pela rede à réplica de disponibilidade remota. Na réplica primária, esse é o número de mensagens enviadas à réplica secundária. Na réplica secundária, esse é o número de mensagens enviadas à réplica primária.|  
  
## <a name="see-also"></a>Consulte Também 
 
 [Monitorar o uso de recursos &#40;Monitor do Sistema&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)   
 [SQL Server, Réplica de banco de dados](../../relational-databases/performance-monitor/sql-server-database-replica.md)   
 [Grupos de Disponibilidade AlwaysOn (SQL Server)](../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)  
  
  
