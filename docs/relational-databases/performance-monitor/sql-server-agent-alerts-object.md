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
ms.openlocfilehash: ea269c45f065e03f5583e62ca98f0084e2fb4772
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32951271"
---
# <a name="sql-server-agent-alerts-object"></a>SQL Server Agent, objeto Alerts
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  O objeto de desempenho **Alerts** do SQL Server Agent contém contadores de desempenho que relatam informações sobre alertas do SQL Server Agent. A tabela a seguir lista os contadores contidos nesse objeto.  
  
 A tabela abaixo contém os contadores de **SQLAgent:Alerts** .  
  
|Nome|Description|  
|----------|-----------------|  
|**Alertas ativados**|Este contador informa o total de alertas que o Microsoft SQL Agent ativou desde que foi reiniciado pela última vez.|  
|**Alertas ativados/minuto**|Este contador informa o número de alertas que o SQL Server Agent ativou no último minuto.|  
  
> [!NOTE]  
>  Para usar este objeto do SQL Server Agent, os usuários devem ser membros da função de servidor fixa **sysadmin** .  
  
## <a name="see-also"></a>Consulte Também  
 [Alerts](http://msdn.microsoft.com/library/3f57d0f0-4781-46ec-82cd-b751dc5affef)   
 [Usar objetos de desempenho](http://msdn.microsoft.com/library/830b843a-6b2a-4620-a51b-98358e9fc54b)   
 [Monitorar o uso de recursos &#40;Monitor do Sistema&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
  
  
