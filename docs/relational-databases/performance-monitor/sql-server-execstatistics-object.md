---
title: SQL Server, objeto ExecStatistics | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: performance-monitor
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQLServer:ExecStatistics
- ExecStatistics object
ms.assetid: 4f8557a8-345f-4622-a8a5-763a0388ad94
caps.latest.revision: "14"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 837b52d5d457a4466a46d08df918e25616d14bff
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/18/2018
---
# <a name="sql-server-execstatistics-object"></a>SQL Server, objeto ExecStatistics
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] O objeto **SQLServer:ExecStatistics** do Microsoft SQL Server oferece contadores para o monitoramento de diversas execuções.  
  
 Esta tabela descreve os contadores **Exec Statistics** do SQL Server.  
  
|Contadores Exec Statistics do SQL Server|Description|  
|-----------------------------------------|-----------------|  
|**Consulta Distribuída**|Estatísticas referentes à execução de consultas distribuídas.|  
|**Chamadas DTC**|Estatísticas referentes à execução de chamadas DTC.|  
|**Procedimentos Estendidos**|Estatísticas referentes à execução de procedimentos estendidos.|  
|**Chamadas OLEDB**|Estatísticas referentes à execução de chamadas OLEDB.|  
  
 Cada contador no objeto contém as seguintes instâncias:  
  
|Item|Description|  
|----------|-----------------|  
|**Tempo médio de execução (ms)**|Tempo médio de execução do tipo de execução selecionado.|  
|**Tempo de execução cumulativo (ms) por segundo**|Tempo de execução agregado, por segundo, do tipo de execução selecionado.|  
|**Execuções em andamento**|Número de execuções em andamento do tipo de execução selecionado.|  
|**Execuções iniciadas por segundo**|Número de execuções iniciadas por segundo, do tipo de execução selecionado.|  
  
## <a name="see-also"></a>Consulte Também  
 [Monitorar o uso de recursos &#40;Monitor do Sistema&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
  
  
