---
title: Modelos e permissões do SQL Server Profiler | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Profiler [SQL Server Profiler], about SQL Server Profiler
- SQL Server Profiler, about SQL Server Profiler
ms.assetid: 6d00378a-5d74-463b-9ed6-a2685306a9d2
caps.latest.revision: 33
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: cb7943b3117882365c0e33e8aa78e6a6e70e675d
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36122954"
---
# <a name="sql-server-profiler-templates-and-permissions"></a>Modelos e permissões do SQL Server Profiler
  [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] mostra como o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] resolve consultas internamente. Isso permite que os administradores saibam exatamente quais instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] ou Expressões Multidimensionais são enviadas ao servidor e como este acessa o banco de dados ou cubo para retornar conjuntos de resultados.  
  
 Usando o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)], você pode fazer este procedimento:  
  
-   Criar um rastreamento baseado em um modelo reutilizável  
  
-   Observar os resultados do rastreamento enquanto ele é executado  
  
-   Armazenar os resultados do rastreamento em uma tabela  
  
-   Iniciar, interromper, pausar e modificar os resultados do rastreamento, conforme a necessidade  
  
-   Repetir os resultados do rastreamento  
  
 Use o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] para monitorar apenas os eventos que lhe interessam. Se os rastreamentos estiverem se tornando grandes demais, você poderá filtrá-los de acordo com as informações desejadas, de modo que apenas um subconjunto dos dados do evento seja coletado. O monitoramento de muitos eventos causa sobrecarga no servidor e no processo de monitoramento, além de aumentar muito a tabela ou arquivo de rastreamento, especialmente se o monitoramento se estender por um longo período de tempo.  
  
> [!NOTE]  
>  Os valores de coluna de rastreamento maiores que 1 GB retornam um erro e são truncados na saída do rastreamento.  
  
## <a name="in-this-section"></a>Nesta seção  
  
|Tópico|Description|  
|-----------|-----------------|  
|[Modelos do SQL Server Profiler](sql-server-profiler-templates.md)|Contém informações sobre os modelos de rastreamento predefinidos que acompanham o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)].|  
|[Permissões necessárias para executar o SQL Server Profiler](permissions-required-to-run-sql-server-profiler.md)|Contém informações sobre as permissões exigidas para executar o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)].|  
|[Salvar rastreamentos e modelos de rastreamento](save-traces-and-trace-templates.md)|Contém informações sobre como salvar a saída do rastreamento e como salvar as definições de rastreamento em um modelo.|  
|[Modificar modelos de rastreamento](modify-trace-templates.md)|Contém informações sobre como modificar modelos de rastreamento usando o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] ou [!INCLUDE[tsql](../../includes/tsql-md.md)].|  
|[Iniciar um rastreamento](start-a-trace.md)|Contém informações sobre o que acontece quando um rastreamento é iniciado, pausado ou interrompido.|  
|[Correlacionar um rastreamento com os dados de log de desempenho do Windows](correlate-a-trace-with-windows-performance-log-data.md)|Contém informações sobre como correlacionar os dados do log de desempenho do Windows com um rastreamento, usando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Profiler.|  
|[Exibir e analisar rastreamentos com o SQL Server Profiler](view-and-analyze-traces-with-sql-server-profiler.md)|Contém informações sobre como usar rastreamentos para solucionar problemas de dados, como exibir nomes de objeto em um rastreamento e como localizar eventos em um rastreamento.|  
|[Analisar deadlocks com o SQL Server Profiler](analyze-deadlocks-with-sql-server-profiler.md)|Contém informações sobre como usar o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] para identificar a causa de um deadlock.|  
|[Analisar consultas com resultados do Plano de Execução no SQL Server Profiler](analyze-queries-with-showplan-results-in-sql-server-profiler.md)|Contém informações sobre como usar o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] para coletar e exibir resultados do Plano de Execução e suas estatísticas.|  
|[Filtrar rastreamentos com o SQL Server Profiler](filter-traces-with-sql-server-profiler.md)|Contém informações sobre como definir filtros em colunas de dados para filtrar a saída do rastreamento, usando o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)].|  
|[Reproduzir rastreamentos](replay-traces.md)|Contém informações que explicam o que significa repetir um rastreamento e o que é necessário para isso.|  
  
## <a name="see-also"></a>Consulte também  
 [SQL Server Profiler](sql-server-profiler.md)   
 [Iniciar o SQL Server Profiler](start-sql-server-profiler.md)  
  
  