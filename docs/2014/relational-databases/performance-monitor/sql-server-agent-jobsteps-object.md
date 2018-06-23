---
title: SQL Server Agent, objeto JobSteps | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- JobSteps object
- SQLAgent:JobSteps
ms.assetid: 44f9983c-1753-4fe0-8475-973aa2460b3a
caps.latest.revision: 22
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 36fd1f3af30a3b9637df64ca5e118b6381e3bd06
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36121261"
---
# <a name="sql-server-agent-jobsteps-object"></a>SQL Server Agent, objeto JobSteps
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
  
## <a name="see-also"></a>Consulte também  
 [Gerenciar etapas de trabalho](../../ssms/agent/manage-job-steps.md)   
 [Usar objetos de desempenho](../../ssms/agent/use-performance-objects.md)   
 [Monitorar o uso de recursos &#40;Monitor do Sistema&#41;](monitor-resource-usage-system-monitor.md)  
  
  