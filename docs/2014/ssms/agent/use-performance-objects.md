---
title: Usar objetos de desempenho | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent, monitoring
- SQL Server Agent service, monitoring
- SQL Server Agent service, performance objects
- SQL Server Agent, performance objects
- performance objects [SQL Server Agent]
- monitoring [SQL Server], SQL Server Agent
- monitoring [SQL Server Agent]
- performance counters [SQL Server], SQL Server Agent
- counters [SQL Server], SQL Server Agent
ms.assetid: 830b843a-6b2a-4620-a51b-98358e9fc54b
author: stevestein
ms.author: sstein
ms.openlocfilehash: d7c1fe3f4a7d9a5fec901f84d8e913e49a4dbd1b
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85062101"
---
# <a name="use-performance-objects"></a>Usar objetos de desempenho
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] O Agent contém objetos de desempenho e contadores para monitorar o desempenho do serviço. Esses objetos de desempenho permitem-lhe usar o Monitor de Desempenho — uma ferramenta do Windows — para identificar o que o serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent está fazendo em segundo plano. Por exemplo, é possível identificar quantos trabalhos ativos o serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent executa atualmente, para determinar quais deles estão bloqueados.  
  
 Existem objetos de desempenho e contadores do serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent para cada instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instalada em um computador. Os objetos de desempenho são nomeados de acordo com a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que representam.  
  
 A tabela a seguir mostra como os objetos de desempenho do serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent são nomeados:  
  
|Tipo de instância|Nome do objeto|  
|-------------------|-----------------|  
|Padrão|**SQLAgent:** *objeto*:*contador*|  
|nomeado|**SQLAgent$**<br /> ***instance_name* :** *objeto*:*contador*|  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] contém os objetos de desempenho do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent a seguir.  
  
|Nome do objeto|Descrição|  
|-----------------|-----------------|  
|[SQLAgent:Jobs](../../relational-databases/performance-monitor/sql-server-agent-jobs-object.md)|Informações sobre o desempenho de trabalhos que foram iniciados, taxas de êxito e status atual|  
|[SQLAgent:JobSteps](../../relational-databases/performance-monitor/sql-server-agent-jobsteps-object.md)|Informações sobre o status de etapas de trabalho|  
|[SQLAgent:Alerts](../../relational-databases/performance-monitor/sql-server-agent-alerts-object.md)|Informações sobre o número de alertas e notificações|  
|[SQLAgent:Statistics](../../relational-databases/performance-monitor/sql-server-agent-statistics-object.md)|Informações gerais do desempenho|  
  
## <a name="see-also"></a>Consulte Também  
 [Monitorar e ajustar o desempenho](../../relational-databases/performance/monitor-and-tune-for-performance.md)   
 [Iniciar o Monitor do Sistema &#40;Windows&#41;](../../relational-databases/performance/start-system-monitor-windows.md)  
  
  
