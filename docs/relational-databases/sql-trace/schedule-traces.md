---
title: "Agendar rastreamentos | Microsoft Docs"
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
  - "filtros [SQL Server], eventos"
  - "rastreamentos [SQL Server]"
  - "rastreamentos [SQL Server], parando"
  - "eventos [SQL Server], filtros"
  - "agendando rastreamentos [SQL Server]"
  - "rastreamentos [SQL Server], agendando"
  - "parando rastreamentos"
ms.assetid: 620b79db-924b-4502-8af3-39efcfca245d
caps.latest.revision: 24
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 24
---
# Agendar rastreamentos
  Há dois modos de agendar rastreamentos no Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Você pode:  
  
-   Habilitar uma hora de parada do rastreamento.  
  
-   Usar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent para agendar um rastreamento.  
  
## Especificando uma hora de parada  
 Você poderá especificar uma hora de parada do rastreamento se usar procedimentos armazenados [!INCLUDE[tsql](../../includes/tsql-md.md)] ou o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]. A hora de parada deve ser definida quando o rastreamento é originalmente configurado.  
  
## Agendando rastreamentos usando o SQL Server Agent  
 A melhor maneira de agendar rastreamentos é usar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent para iniciar o rastreamento e especificar uma hora de parada, por meio do procedimento armazenado [!INCLUDE[tsql](../../includes/tsql-md.md)] **sp_trace_setstatus** ou do [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)].  
  
 **Para definir um filtro de hora de término para um rastreamento**  
  
 [Filtrar eventos com base na hora de término do evento &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/filter-events-based-on-the-event-end-time-sql-server-profiler.md)  
  
 [sp_trace_setstatus &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setstatus-transact-sql.md)  
  
## Consulte também  
 [Tarefas de administração automatizadas &#40;SQL Server Agent&#41;](../../ssms/agent/automated-administration-tasks-sql-server-agent.md)  
  
  