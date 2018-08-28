---
title: SQL Server Agent, objeto Alertas | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: performance-monitor
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Alerts object
- SQLAgent:Alerts
ms.assetid: e5e37f74-ee88-46d0-ad8f-71fd1b1fa64a
caps.latest.revision: 24
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: d310d463d0cb20135b1318f6ffd27c0b602f33e4
ms.sourcegitcommit: 79d4dc820767f7836720ce26a61097ba5a5f23f2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/16/2018
ms.locfileid: "40412692"
---
# <a name="sql-server-agent-alerts-object"></a>SQL Server Agent, objeto Alerts
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  O objeto de desempenho **Alerts** do SQL Server Agent contém contadores de desempenho que relatam informações sobre alertas do SQL Server Agent. A tabela a seguir lista os contadores contidos nesse objeto.  
  
 A tabela abaixo contém os contadores de **SQLAgent:Alerts** .  
  
|Nome|Descrição|  
|----------|-----------------|  
|**Alertas ativados**|Este contador informa o total de alertas que o Microsoft SQL Agent ativou desde que foi reiniciado pela última vez.|  
|**Alertas ativados/minuto**|Este contador informa o número de alertas que o SQL Server Agent ativou no último minuto.|  
  
> [!NOTE]  
>  Para usar este objeto do SQL Server Agent, os usuários devem ser membros da função de servidor fixa **sysadmin** .  
  
## <a name="see-also"></a>Consulte Também  
 [Alerts](../../ssms/agent/alerts.md)   
 [Usar objetos de desempenho](../../ssms/agent/use-performance-objects.md)   
 [Monitorar o uso de recursos &#40;Monitor do Sistema&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
  
  
