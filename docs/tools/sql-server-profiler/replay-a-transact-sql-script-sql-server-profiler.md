---
title: "Repetir um script Transact-SQL (SQL Server Profiler) | Microsoft Docs"
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
  - "rastreamentos [SQL Server], reproduzindo"
  - "scripts [SQL Server], rastreamentos"
  - "repetindo rastreamentos"
ms.assetid: 9c0eb222-e6e3-4bc1-a25f-a41e962d361b
caps.latest.revision: 24
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 24
---
# Repetir um script Transact-SQL (SQL Server Profiler)
  Ao testar possíveis soluções para um problema de desempenho, use o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] para repetir scripts [!INCLUDE[tsql](../../includes/tsql-md.md)] e compare o desempenho antes e depois das alterações.  
  
### Para repetir um script Transact-SQL   
  
1.  No menu **Arquivo** , aponte para **Abrir**e clique em **Arquivo de Script**.  
  
2.  Selecione o arquivo de script [!INCLUDE[tsql](../../includes/tsql-md.md)] que deseja abrir. Certifique-se de que o script [!INCLUDE[tsql](../../includes/tsql-md.md)] contenha os eventos necessários para a repetição. Para obter mais informações, consulte [Replay Requirements](../../tools/sql-server-profiler/replay-requirements.md).  
  
3.  No menu **Repetir** , clique em **Iniciar**e conecte-se ao servidor em que deseja repetir o script.  
  
4.  Na caixa de diálogo **Configuração de Repetição** , verifique as definições e clique em **OK**.  
  
## Consulte também  
 [Repetir rastreamentos](../../tools/sql-server-profiler/replay-traces.md)   
 [SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md)  
  
  