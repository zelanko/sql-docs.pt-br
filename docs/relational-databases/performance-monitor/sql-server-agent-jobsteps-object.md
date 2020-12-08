---
title: SQL Server Agent, objeto JobSteps | Microsoft Docs
description: Saiba mais sobre o objeto de desempenho JobSteps do SQL Server Agent, que contém contadores de desempenho que relatam informações sobre as etapas dos trabalhos do SQL Server Agent.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- JobSteps object
- SQLAgent:JobSteps
ms.assetid: 44f9983c-1753-4fe0-8475-973aa2460b3a
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.openlocfilehash: 18c4c7db9fcd23581162eb4da4d763bfc1efbb3c
ms.sourcegitcommit: 0e0cd9347c029e0c7c9f3fe6d39985a6d3af967d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/02/2020
ms.locfileid: "96505923"
---
# <a name="sql-server-agent-jobsteps-object"></a>SQL Server Agent, objeto JobSteps
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  O objeto de desempenho [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] JobSteps **do** Agent contém contadores de desempenho que relatam informações sobre etapas de trabalho do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. A tabela a seguir lista os contadores contidos nesse objeto.  
  
 A tabela abaixo contém os contadores de **SQLAgent:JobSteps** .  
  
|Nome|Descrição|  
|----------|-----------------|  
|**Etapas ativas**|Este contador informa o número de etapas de trabalho atualmente em execução.|  
|**Etapas em fila**|Este contador informa o número de etapas de trabalho que estão prontas para execução pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent, mas que ainda não foram iniciadas.|  
|**Total de repetições de etapas**|Esse contador informa o número total de vezes que o [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] repetiu uma etapa de trabalho desde a última reinicialização do servidor.|  
  
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
  
## <a name="see-also"></a>Consulte Também  
 [Gerenciar etapas de trabalho](../../ssms/agent/manage-job-steps.md)   
 [Usar objetos de desempenho](../../ssms/agent/use-performance-objects.md)   
 [Monitorar o uso de recursos &#40;Monitor do Sistema&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
  
  
