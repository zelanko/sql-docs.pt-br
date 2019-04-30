---
title: SQL Server Agent, objeto Alertas | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Alerts object
- SQLAgent:Alerts
ms.assetid: e5e37f74-ee88-46d0-ad8f-71fd1b1fa64a
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: d88041f61c2f84e510c637b71f0ebb1bbb2a97cd
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63250932"
---
# <a name="sql-server-agent-alerts-object"></a>SQL Server Agent, objeto Alerts
  O objeto de desempenho **Alerts** do SQL Server Agent contém contadores de desempenho que relatam informações sobre alertas do SQL Server Agent. A tabela a seguir lista os contadores contidos nesse objeto.  
  
 A tabela abaixo contém os contadores de **SQLAgent:Alerts** .  
  
|Nome|Descrição|  
|----------|-----------------|  
|**Alertas ativados**|Este contador informa o total de alertas que o Microsoft SQL Agent ativou desde que foi reiniciado pela última vez.|  
|**Alertas ativados/minuto**|Este contador informa o número de alertas que o SQL Server Agent ativou no último minuto.|  
  
> [!NOTE]  
>  Para usar este objeto do SQL Server Agent, os usuários devem ser membros da função de servidor fixa **sysadmin** .  
  
## <a name="see-also"></a>Consulte também  
 [Alerts](../../ssms/agent/alerts.md)   
 [Usar objetos de desempenho](../../ssms/agent/use-performance-objects.md)   
 [Monitorar o uso de recursos &#40;Monitor do Sistema&#41;](monitor-resource-usage-system-monitor.md)  
  
  
