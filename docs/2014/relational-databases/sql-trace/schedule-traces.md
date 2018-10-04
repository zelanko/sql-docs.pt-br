---
title: Agendar rastreamentos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- filters [SQL Server], events
- traces [SQL Server]
- traces [SQL Server], stopping
- events [SQL Server], filters
- scheduling traces [SQL Server]
- traces [SQL Server], scheduling
- stopping traces
ms.assetid: 620b79db-924b-4502-8af3-39efcfca245d
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 0c680ea7b2fc8360fce0ff81f0d22f1816107f49
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48157236"
---
# <a name="schedule-traces"></a>Agendar rastreamentos
  Há dois modos de agendar rastreamentos no Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Você pode:  
  
-   Habilitar uma hora de parada do rastreamento.  
  
-   Usar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent para agendar um rastreamento.  
  
## <a name="specifying-a-stop-time"></a>Especificando uma hora de parada  
 Você poderá especificar uma hora de parada do rastreamento se usar procedimentos armazenados [!INCLUDE[tsql](../../includes/tsql-md.md)] ou o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]. A hora de parada deve ser definida quando o rastreamento é originalmente configurado.  
  
## <a name="scheduling-traces-by-using-sql-server-agent"></a>Agendando rastreamentos usando o SQL Server Agent  
 A melhor maneira de agendar rastreamentos é usar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent para iniciar o rastreamento e especificar uma hora de parada, por meio do procedimento armazenado [!INCLUDE[tsql](../../includes/tsql-md.md)] **sp_trace_setstatus**ou do [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)].  
  
 **Para definir um filtro de hora de término para um rastreamento**  
  
 [Filtrar eventos com base na hora de término do evento &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/filter-events-based-on-the-event-end-time-sql-server-profiler.md)  
  
 [sp_trace_setstatus &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setstatus-transact-sql)  
  
## <a name="see-also"></a>Consulte também  
 [Tarefas de administração automatizadas &#40;SQL Server Agent&#41;](../../ssms/agent/sql-server-agent.md)  
  
  
