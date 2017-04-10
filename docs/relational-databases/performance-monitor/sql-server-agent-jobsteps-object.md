---
title: "SQL Server Agent, objeto JobSteps | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "objeto JobSteps"
  - "SQLAgent:JobSteps"
ms.assetid: 44f9983c-1753-4fe0-8475-973aa2460b3a
caps.latest.revision: 23
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 23
---
# SQL Server Agent, objeto JobSteps
  O objeto de desempenho [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] JobSteps **do** Agent contém contadores de desempenho que relatam informações sobre etapas de trabalho do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. A tabela a seguir lista os contadores contidos nesse objeto.  
  
 A tabela abaixo contém os contadores de **SQLAgent:JobSteps** .  
  
|Nome|Descrição|  
|----------|-----------------|  
|**Etapas ativas**|Este contador informa o número de etapas de trabalho atualmente em execução.|  
|**Etapas em fila**|Este contador informa o número de etapas de trabalho que estão prontas para execução pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent, mas que ainda não foram iniciadas.|  
|**Total de repetições de etapas**|Este contador informa o total de vezes que o [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] repetiu uma etapa de trabalho desde a última reinicialização do servidor.|  
  
 Cada contador no objeto contém as seguintes instâncias:  
  
|Instância|Descrição|  
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
  
## Consulte também  
 [Gerenciar etapas de trabalho](../../ssms/agent/manage-job-steps.md)   
 [Usar objetos de desempenho](../../ssms/agent/use-performance-objects.md)   
 [Monitorar o uso de recursos &#40;Monitor do Sistema&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
  
  