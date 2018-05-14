---
title: SQL Server Agent, objeto JobSteps | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
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
- JobSteps object
- SQLAgent:JobSteps
ms.assetid: 44f9983c-1753-4fe0-8475-973aa2460b3a
caps.latest.revision: 23
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 21835671518515b1efe02698a0f01f4dcd051179
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="sql-server-agent-jobsteps-object"></a>SQL Server Agent, objeto JobSteps
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  O objeto de desempenho [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] JobSteps **do** Agent contém contadores de desempenho que relatam informações sobre etapas de trabalho do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. A tabela a seguir lista os contadores contidos nesse objeto.  
  
 A tabela abaixo contém os contadores de **SQLAgent:JobSteps** .  
  
|Nome|Description|  
|----------|-----------------|  
|**Etapas ativas**|Este contador informa o número de etapas de trabalho atualmente em execução.|  
|**Etapas em fila**|Este contador informa o número de etapas de trabalho que estão prontas para execução pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent, mas que ainda não foram iniciadas.|  
|**Total de repetições de etapas**|Este contador informa o total de vezes que o [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] repetiu uma etapa de trabalho desde a última reinicialização do servidor.|  
  
 Cada contador no objeto contém as seguintes instâncias:  
  
|Instância|Description|  
|--------------|-----------------|  
|**_Total**|Informações de todas as etapas de trabalho.|  
|**ActiveScripting**|Informações de etapas de trabalho que usam o subsistema **ActiveScripting** .|  
|**ANALYSISCOMMAND**|Informações de etapas de trabalho que usam o subsistema ANALYSISCOMMAND.|  
|**ANALYSISQUERY**|Informações de etapas de trabalho que usam o subsistema ANALYSISQUERY.|  
|**CmdExec**|Informações de etapas de trabalho que usam o subsistema **CmdExec** .|  
|**Distribuição**|Informações de etapas de trabalho que usam o subsistema **Distribution** .|  
|**Dts**|Informações de etapas de trabalho que usam o subsistema [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .|  
|**LogReader**|Informações de etapas de trabalho que usam o subsistema **LogReader** .|  
|**Mesclagem**|Informações de etapas de trabalho que usam o subsistema **Merge** .|  
|**PowerShell**|Informações de etapas de trabalho que usam o subsistema **PowerShell** .|  
|**QueueReader**|Informações de etapas de trabalho que usam o subsistema **QueueReader** .|  
|**Instantâneo**|Informações de etapas de trabalho que usam o subsistema **Snapshot** .|  
|**TSQL**|Informações de etapas de trabalho que executam [!INCLUDE[tsql](../../includes/tsql-md.md)].|  
  
## <a name="see-also"></a>Consulte Também  
 [Gerenciar etapas de trabalho](http://msdn.microsoft.com/library/51352afc-a0a4-428b-8985-f9e58bb57c31)   
 [Usar objetos de desempenho](http://msdn.microsoft.com/library/830b843a-6b2a-4620-a51b-98358e9fc54b)   
 [Monitorar o uso de recursos &#40;Monitor do Sistema&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
  
  
