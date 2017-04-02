---
title: "Iniciar um rastreamento | Microsoft Docs"
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
  - "SQL Server Profiler, parando rastreamentos"
  - "pausando rastreamentos"
  - "Profiler [SQL Server Profiler], parando rastreamentos"
  - "Profiler [SQL Server Profiler], iniciando rastreamentos"
  - "rastreamentos [SQL Server], iniciando"
  - "SQL Server Profiler, pausando rastreamentos"
  - "rastreamentos [SQL Server], parando"
  - "Profiler [SQL Server Profiler], pausando rastreamentos"
  - "rastreamentos [SQL Server], pausando"
  - "SQL Server Profiler, iniciando rastreamentos"
  - "parando rastreamentos"
  - "iniciando rastreamentos"
ms.assetid: aeeb38eb-229a-4c8b-ad66-57e9ce45fb6a
caps.latest.revision: 24
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 24
---
# Iniciar um rastreamento
  Após definir um novo rastreamento ou criar um modelo usando o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)], você pode iniciar, pausar ou interromper a captura de dados usando a nova definição ou modelo de rastreamento.  
  
## Iniciando um rastreamento  
 Quando se inicia um rastreamento e a origem definida é uma instância do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] ou do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cria uma fila que fornece um local de guarda temporária para os eventos de servidor capturados.  
  
 Quando o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] é utilizado para acessar o Rastreamento do SQL, uma nova janela de rastreamento é aberta (se já não houver uma) quando o rastreamento é iniciado e os dados são capturados imediatamente.  
  
 Quando se usam procedimentos armazenados [!INCLUDE[tsql](../../includes/tsql-md.md)] do sistema para acessar o Rastreamento do SQL, é necessário iniciar um rastreamento toda vez que uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é iniciada para a captura de dados. Depois que um rastreamento é iniciado, só é possível modificar seu nome.  
  
> [!NOTE]  
>  Ao trabalhar com rastreamentos existentes, você pode exibir as propriedades, mas não pode modificá-las. Para modificar as propriedades, interrompa ou pause o rastreamento.  
  
## Consulte também  
 [Iniciar um rastreamento automaticamente após a conexão com um servidor &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/start-a-trace-automatically-after-connecting-to-a-server-sql-server-profiler.md)   
 [Pausar um rastreamento &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/pause-a-trace-sql-server-profiler.md)   
 [Interromper um rastreamento &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/stop-a-trace-sql-server-profiler.md)   
 [Limpar uma janela de rastreamento &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/clear-a-trace-window-sql-server-profiler.md)   
 [Executar um rastreamento que foi pausado ou interrompido &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/run-a-trace-after-it-has-been-paused-or-stopped-sql-server-profiler.md)  
  
  