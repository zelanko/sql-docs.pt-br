---
description: Agendar rastreamentos
title: Agendar rastreamentos | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
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
ms.openlocfilehash: 1f86e9cf97c82ead3059d846f9709aa7a0c87d99
ms.sourcegitcommit: 04cf7905fa32e0a9a44575a6f9641d9a2e5ac0f8
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/07/2020
ms.locfileid: "91810803"
---
# <a name="schedule-traces"></a>Agendar rastreamentos
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  Há dois modos de agendar rastreamentos no Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Você pode:  
  
-   Habilitar uma hora de parada do rastreamento.  
  
-   Usar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent para agendar um rastreamento.  
  
## <a name="specifying-a-stop-time"></a>Especificando uma hora de parada  
 Você poderá especificar uma hora de parada do rastreamento se usar procedimentos armazenados [!INCLUDE[tsql](../../includes/tsql-md.md)] ou o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]. A hora de parada deve ser definida quando o rastreamento é originalmente configurado.  
  
## <a name="scheduling-traces-by-using-sql-server-agent"></a>Agendando rastreamentos usando o SQL Server Agent  
 A melhor maneira de agendar rastreamentos é usar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent para iniciar o rastreamento e especificar uma hora de parada, por meio do procedimento armazenado [!INCLUDE[tsql](../../includes/tsql-md.md)]**sp_trace_setstatus**ou do [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)].  
  
 **Para definir um filtro de hora de término para um rastreamento**  
  
 [Filtrar eventos com base na hora de término do evento &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/filter-events-based-on-the-event-end-time-sql-server-profiler.md)  
  
 [sp_trace_setstatus &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setstatus-transact-sql.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Tarefas de administração automatizadas &#40;SQL Server Agent&#41;](../../ssms/agent/automated-administration-tasks-sql-server-agent.md)  
  
