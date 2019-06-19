---
title: Monitoramento de desempenho e atividade de servidor | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- activity monitoring [SQL Server]
- traces [SQL Server], how-to topics
- monitoring server performance [SQL Server], activity monitoring
- stored procedures [SQL Server], traces
- performance [SQL Server], servers
- servers [SQL Server], performance
- SQL Server Profiler, how-to topics
- SQL Server Management Studio [SQL Server], monitoring system
- Profiler [SQL Server Profiler], how-to topics
ms.assetid: f9abe48d-d6e9-4c38-a355-fc5eb5a95a25
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 7289c18fac421bbdb5ccc0e00a3bea60b7a22d9e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63150612"
---
# <a name="server-performance-and-activity-monitoring"></a>Monitoramento de desempenho e atividade de servidor
  A meta do monitoramento de bancos de dados é avaliar o desempenho do servidor. Um monitoramento eficaz envolve a criação de instantâneos periódicos do desempenho atual para isolar processos que estão ocasionando problemas, e a coleta contínua de dados para o controle das tendências de desempenho. [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e o sistema operacional [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows fornecem utilitários que permitem exibir a condição atual do banco de dados e controlar o desempenho à medida que as condições vão mudando.  
  
 A seção a seguir contém tópicos que descrevem como usar as ferramentas de monitoramento de desempenho e atividade do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e do Windows. Ela contém os seguintes tópicos:  
  
## <a name="in-this-section"></a>Nesta seção  
 **Para executar tarefas de monitoramento com ferramentas do Windows**  
  
-   [Iniciar o Monitor do Sistema &#40;Windows&#41;](start-system-monitor-windows.md)  
  
-   [Exibir o log de aplicativos do Windows &#40;Windows&#41;](view-the-windows-application-log-windows-10.md)  
  
 **Para criar alertas de banco de dados do SQL Server com ferramentas do Windows**  
  
-   [Configurar um alerta de banco de dados do SQL Server &#40;Windows&#41;](set-up-a-sql-server-database-alert-windows.md)  
  
 **Para realizar tarefas de monitoramento com o SQL Server Management Studio**  
  
-   [Exibir o log de erros do SQL Server &#40;SQL Server Management Studio&#41;](../../ssms/sql-server-management-studio-ssms.md)  
  
-   [Abrir o Monitor de Atividade &#40;SQL Server Management Studio&#41;](../performance-monitor/open-activity-monitor-sql-server-management-studio.md)  
  
 **Para realizar tarefas de monitoramento com o Rastreamento do SQL, usando procedimentos armazenados Transact-SQL**  
  
-   [Criar um rastreamento &#40;Transact-SQL&#41;](../sql-trace/create-a-trace-transact-sql.md)  
  
-   [Definir um filtro de rastreamento &#40;Transact-SQL&#41;](../../ssms/agent/set-sql-server-alias-for-sql-server-agent-service-ssms.md)  
  
-   [Modificar um rastreamento existente &#40;Transact-SQL&#41;](../sql-trace/modify-an-existing-trace-transact-sql.md)  
  
-   [Exibir um rastreamento salvo &#40;Transact-SQL&#41;](../sql-trace/view-a-saved-trace-transact-sql.md)  
  
-   [Exibir informações de filtro &#40;Transact-SQL&#41;](../sql-trace/view-filter-information-transact-sql.md)  
  
-   [Excluir um rastreamento &#40;Transact-SQL&#41;](../sql-trace/delete-a-trace-transact-sql.md)  
  
 **Para criar e modificar rastreamentos usando o SQL Server Profiler**  
  
-   [Criar um rastreamento &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/create-a-trace-sql-server-profiler.md)  
  
-   [Definir opções de rastreamento globais &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/set-global-trace-options-sql-server-profiler.md)  
  
-   [Especificar eventos e colunas de dados para um arquivo de rastreamento &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/specify-events-and-data-columns-for-a-trace-file-sql-server-profiler.md)  
  
-   [Criar um script Transact-SQL para executar um rastreamento &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/create-a-transact-sql-script-for-running-a-trace-sql-server-profiler.md)  
  
-   [Salvar resultados de rastreamento em um arquivo &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/save-trace-results-to-a-file-sql-server-profiler.md)  
  
-   [Definir um tamanho máximo para um arquivo de rastreamento &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/set-a-maximum-file-size-for-a-trace-file-sql-server-profiler.md)  
  
-   [Salvar resultados de rastreamento em uma tabela &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/save-trace-results-to-a-table-sql-server-profiler.md)  
  
-   [Definir um tamanho máximo para uma tabela de rastreamento &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/set-a-maximum-table-size-for-a-trace-table-sql-server-profiler.md)  
  
-   [Filtrar eventos em um rastreamento &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/filter-events-in-a-trace-sql-server-profiler.md)  
  
-   [Exibir informações de filtro &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/view-filter-information-sql-server-profiler.md)  
  
-   [Modificar um filtro &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/modify-a-filter-sql-server-profiler.md)  
  
-   [Filtrar eventos com base na hora de início do evento &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/filter-events-based-on-the-event-start-time-sql-server-profiler.md)  
  
-   [Filtrar eventos com base na hora de término do evento &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/filter-events-based-on-the-event-end-time-sql-server-profiler.md)  
  
-   [Filtrar SPIDs &#40;IDs de processo de servidor&#41; em um rastreamento &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/filter-server-process-ids-spids-in-a-trace-sql-server-profiler.md)  
  
-   [Organizar colunas exibidas em um rastreamento &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/organize-columns-displayed-in-a-trace-sql-server-profiler.md)  
  
 **Para iniciar, pausar e parar rastreamentos usando o SQL Server Profiler**  
  
-   [Iniciar um rastreamento automaticamente após a conexão com um servidor &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/start-a-trace-automatically-after-connecting-to-a-server-sql-server-profiler.md)  
  
-   [Pausar um rastreamento &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/pause-a-trace-sql-server-profiler.md)  
  
-   [Interromper um rastreamento &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/stop-a-trace-sql-server-profiler.md)  
  
-   [Executar um rastreamento que foi pausado ou interrompido &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/run-a-trace-after-it-has-been-paused-or-stopped-sql-server-profiler.md)  
  
 **Para abrir rastreamentos e configurar a forma como serão exibidos usando o SQL Server Profiler**  
  
-   [Abrir um arquivo de rastreamento &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/open-a-trace-file-sql-server-profiler.md)  
  
-   [Abrir uma tabela de rastreamento &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/open-a-trace-table-sql-server-profiler.md)  
  
-   [Limpar uma janela de rastreamento &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/clear-a-trace-window-sql-server-profiler.md)  
  
-   [Fechar uma janela de rastreamento &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/close-a-trace-window-sql-server-profiler.md)  
  
-   [Definir padrões de definição de rastreamento &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/set-trace-definition-defaults-sql-server-profiler.md)  
  
-   [Definir padrões de exibição de rastreamento &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/set-trace-display-defaults-sql-server-profiler.md)  
  
 **Para repetir rastreamentos usando o SQL Server Profiler**  
  
-   [Reproduzir um arquivo de rastreamento &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/replay-a-trace-file-sql-server-profiler.md)  
  
-   [Reproduzir uma tabela de rastreamento &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/replay-a-trace-table-sql-server-profiler.md)  
  
-   [Reproduzir um único evento de cada vez &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/replay-a-single-event-at-a-time-sql-server-profiler.md)  
  
-   [Reproduzir em um ponto de interrupção &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/replay-to-a-breakpoint-sql-server-profiler.md)  
  
-   [Reproduzir para um cursor &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/replay-to-a-cursor-sql-server-profiler.md)  
  
-   [Reproduzir um script Transact-SQL &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/replay-a-transact-sql-script-sql-server-profiler.md)  
  
 **Para criar, modificar e usar modelos de rastreamento usando o SQL Server Profiler**  
  
-   [Criar um modelo de rastreamento &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/create-a-trace-template-sql-server-profiler.md)  
  
-   [Modificar um modelo de rastreamento &#40;SQL Server Profiler&#41;](../../database-engine/modify-a-trace-template-sql-server-profiler.md)  
  
-   [Derivar um modelo de um rastreamento em execução &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/derive-a-template-from-a-running-trace-sql-server-profiler.md)  
  
-   [Derivar um modelo de um arquivo ou uma tabela de rastreamento &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/derive-a-template-from-a-trace-file-or-trace-table-sql-server-profiler.md)  
  
-   [Exportar um modelo de rastreamento &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/export-a-trace-template-sql-server-profiler.md)  
  
-   [Importar um modelo de rastreamento &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/import-a-trace-template-sql-server-profiler.md)  
  
 **Para usar rastreamentos do SQL Server Profiler para coletar e monitorar o desempenho do servidor**  
  
-   [Localizar um valor ou coluna de dados durante um rastreamento &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/find-a-value-or-data-column-while-tracing-sql-server-profiler.md)  
  
-   [Salvar gráficos de deadlock &#40;SQL Server Profiler&#41;](save-deadlock-graphs-sql-server-profiler.md)  
  
-   [Salvar eventos Showplan XMLL separadamente &#40;SQL Server Profiler&#41;](save-showplan-xml-events-separately-sql-server-profiler.md)  
  
-   [Salvar eventos Showplan XML Statistics Profile separadamente &#40;SQL Server Profiler&#41;](save-showplan-xml-statistics-profile-events-separately-sql-server-profiler.md)  
  
-   [Extrair um script de um rastreamento &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/extract-a-script-from-a-trace-sql-server-profiler.md)  
  
-   [Correlacionar um rastreamento com dados do log de desempenho do Windows &#40;SQL Server Profiler&#41;](../../database-engine/correlate-a-trace-with-windows-performance-log-data-sql-server-profiler.md)  
  
  
