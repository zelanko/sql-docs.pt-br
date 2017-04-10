---
title: "Repetir um &#250;nico evento de cada vez (SQL Server Profiler) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "eventos [SQL Server], repetindo um único evento de cada vez"
  - "rastreamentos [SQL Server], reproduzindo"
  - "repetindo rastreamentos"
ms.assetid: 220fb192-9636-41a2-b15c-62af6cab8fff
caps.latest.revision: 21
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 21
---
# Repetir um &#250;nico evento de cada vez (SQL Server Profiler)
  Este tópico descreve como repetir um evento de cada vez em um arquivo ou tabela de rastreamento de repetição usando o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)].  
  
### Para repetir um único evento de cada vez  
  
1.  Abra o arquivo ou tabela de rastreamento que deseja repetir. Para obter mais informações, consulte [Abrir um arquivo de rastreamento &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/open-a-trace-file-sql-server-profiler.md) ou [Abrir uma tabela de rastreamento &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/open-a-trace-table-sql-server-profiler.md).  
  
     Certifique-se de que o arquivo ou tabela de rastreamento aberto contém as classes de evento necessárias para a repetição. Para obter mais informações, consulte [Replay Requirements](../../tools/sql-server-profiler/replay-requirements.md).  
  
2.  No menu **Repetir** , clique em **Etapa**e conecte-se à instância de servidor em que deseja repetir o rastreamento.  
  
3.  Na caixa de diálogo **Configuração de Repetição** , verifique as definições e clique em **OK**. Para obter mais informações sobre como especificar configurações na caixa de diálogo **Configuração de Reprodução**, consulte [Repetir um arquivo de rastreamento &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/replay-a-trace-file-sql-server-profiler.md) ou [Repetir uma tabela de rastreamento &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/replay-a-trace-table-sql-server-profiler.md).  
  
4.  Para repetir o primeiro evento, clique em **OK** na caixa de diálogo **Configuração de Repetição** .  
  
5.  Para repetir eventos subsequentes, no menu **Repetir** , clique em **Etapa**ou pressione F10. Continue clicando em **Etapa** ou pressionando F10 para cada evento.  
  
## Consulte também  
 [Repetir rastreamentos](../../tools/sql-server-profiler/replay-traces.md)   
 [SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md)  
  
  