---
title: "Correlacionar um rastreamento com os dados de log de desempenho do Windows | Microsoft Docs"
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
  - "correlacionando rastreamento com dados de log"
  - "logs [SQL Server], rastreamentos"
  - "Profiler [SQL Server Profiler], correlacionando rastreamento com dados de log"
  - "rastreamentos [SQL Server], logs"
  - "SQL Server Profiler, correlacionando rastreamento com dados de log"
ms.assetid: 1e4412c8-d27c-4aae-9b35-214128d1d00a
caps.latest.revision: 10
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 10
---
# Correlacionar um rastreamento com os dados de log de desempenho do Windows
  Usando o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)], você pode abrir um log de desempenho do Microsoft Windows, escolher os contadores que deseja correlacionar com um rastreamento e exibir os contadores de desempenho selecionados junto com o rastreamento na interface gráfica do usuário do [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]. Quando você seleciona um evento na janela de rastreamento, uma barra vermelha vertical no painel da janela de dados do Monitor do Sistema do [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] indica os dados do log de desempenho que se correlacionam com o evento de rastreamento selecionado.  
  
 Para correlacionar um rastreamento com contadores de desempenho, abra um arquivo ou tabela de rastreamento que contenha as colunas de dados **StartTime** e **EndTime** e clique em **Importar Dados de Desempenho** no menu **Arquivo** do [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]. Em seguida, você pode abrir um log de desempenho e selecionar os objetos e contadores do Monitor do Sistema que deseja correlacionar com o rastreamento.  
  
## Consulte também  
 [Correlacionar um rastreamento com dados do log de desempenho do Windows &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/correlate-a-trace-with-windows-performance-log-data-sql-server-profiler.md)  
  
  