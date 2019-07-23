---
title: Monitoramento de desempenho e atividade de servidor | Microsoft Docs
ms.custom: ''
ms.date: 11/27/2018
ms.prod: sql
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
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: 073095217dc08f2f11605f8b0e7b5da11035e34a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68113353"
---
# <a name="server-performance-and-activity-monitoring"></a>Monitoramento de desempenho e atividade de servidor
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  A meta do monitoramento de bancos de dados é avaliar o desempenho do servidor. Um monitoramento eficaz envolve a criação de instantâneos periódicos do desempenho atual para isolar processos que estão ocasionando problemas, e a coleta contínua de dados para o controle das tendências de desempenho. [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e o sistema operacional [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows fornecem utilitários que permitem exibir a condição atual do banco de dados e controlar o desempenho à medida que as condições vão mudando.  
  
 A seção a seguir contém tópicos que descrevem como usar as ferramentas de monitoramento de desempenho e atividade do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e do Windows. Ela contém os seguintes tópicos:  
  
## <a name="to-perform-monitoring-tasks-with-windows-tools"></a>Para executar tarefas de monitoramento com ferramentas do Windows 
  
-   [Iniciar o Monitor do Sistema &#40;Windows&#41;](../../relational-databases/performance/start-system-monitor-windows.md)  
  
-   [Exibir o log de aplicativos do Windows &#40;Windows&#41;](../../relational-databases/performance/view-the-windows-application-log-windows-10.md)  
  
## <a name="to-create-sql-server-database-alerts-with-windows-tools"></a>Para criar alertas de banco de dados do SQL Server com ferramentas do Windows  
  
-   [Configurar um alerta de banco de dados do SQL Server &#40;Windows&#41;](../../relational-databases/performance/set-up-a-sql-server-database-alert-windows.md)  

## <a name="to-perform-monitoring-tasks-with-extended-events"></a>Para executar tarefas de monitoramento com os Eventos Estendidos  
 
 -   [Eventos estendidos](../../relational-databases/extended-events/extended-events.md)
 
 -   [Início rápido: eventos estendidos no SQL Server](../../relational-databases/extended-events/quick-start-extended-events-in-sql-server.md)
 
 -   [Gerenciar sessões de evento no Pesquisador de Objetos](../../relational-databases/extended-events/manage-event-sessions-in-the-object-explorer.md)
 
 -   [Alterar uma sessão de Eventos Estendidos](../../relational-databases/extended-events/alter-an-extended-events-session.md)
 
 -   [Converter um script existente de Rastreamento do SQL em uma sessão de Eventos Estendidos](../../relational-databases/extended-events/convert-an-existing-sql-trace-script-to-an-extended-events-session.md)
 
 -   [Exibir os Eventos Estendidos equivalentes às classes de rastreamento de eventos do SQL](../../relational-databases/extended-events/view-the-extended-events-equivalents-to-sql-trace-event-classes.md)
   
## <a name="to-perform-monitoring-tasks-with-sql-server-management-studio"></a>Para realizar tarefas de monitoramento com o SQL Server Management Studio  
  
-   [Exibir o log de erros do SQL Server &#40;SQL Server Management Studio&#41;](../../relational-databases/performance/view-the-sql-server-error-log-sql-server-management-studio.md)  
  
-   [Abrir o Monitor de Atividade &#40;SQL Server Management Studio&#41;](../../relational-databases/performance-monitor/open-activity-monitor-sql-server-management-studio.md)  

-   [Monitorando o desempenho com o Repositório de Consultas](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)

## <a name="to-perform-monitoring-tasks-with-sql-trace-and-sql-server-profiler"></a>Para realizar tarefas de monitoramento com o Rastreamento do SQL e o SQL Server Profiler

> [!IMPORTANT]
> As próximas seções descrevem métodos de uso do Rastreamento do SQL e [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)].  
> Rastreamento do SQL e [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] estão preteridos. O namespace *Microsoft.SqlServer.Management.Trace* que contém os objetos Trace e Replay do Microsoft SQL Server também foi preterido.   
> [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
> Em vez disso, use Eventos Estendidos. Para obter mais informações sobre [Eventos Estendidos](../../relational-databases/extended-events/extended-events.md), confira [Início rápido: eventos estendidos no SQL Server](../../relational-databases/extended-events/quick-start-extended-events-in-sql-server.md) e no [SSMS XEvent Profiler](../../relational-databases/extended-events/use-the-ssms-xe-profiler.md).

> [!NOTE] 
> [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] para as cargas de trabalho do Analysis Services NÃO está preterido e o suporte a ele continuará.

### <a name="to-perform-monitoring-tasks-with-sql-trace-by-using-transact-sql-stored-procedures"></a>Para realizar tarefas de monitoramento com o Rastreamento do SQL, usando procedimentos armazenados Transact-SQL  
  
-   [Criar um rastreamento &#40;Transact-SQL&#41;](../../relational-databases/sql-trace/create-a-trace-transact-sql.md)  
  
-   [Definir um filtro de rastreamento &#40;Transact-SQL&#41;](../../relational-databases/sql-trace/set-a-trace-filter-transact-sql.md)  
  
-   [Modificar um rastreamento existente &#40;Transact-SQL&#41;](../../relational-databases/sql-trace/modify-an-existing-trace-transact-sql.md)  
  
-   [Exibir um rastreamento salvo &#40;Transact-SQL&#41;](../../relational-databases/sql-trace/view-a-saved-trace-transact-sql.md)  
  
-   [Exibir informações de filtro &#40;Transact-SQL&#41;](../../relational-databases/sql-trace/view-filter-information-transact-sql.md)  
  
-   [Excluir um rastreamento &#40;Transact-SQL&#41;](../../relational-databases/sql-trace/delete-a-trace-transact-sql.md)  
  
### <a name="to-create-and-modify-traces-by-using-sql-server-profiler"></a>Para criar e modificar rastreamentos usando o SQL Server Profiler  
  
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
  
### <a name="to-start-pause-and-stop-traces-by-using-sql-server-profiler"></a>Para iniciar, pausar e parar rastreamentos usando o SQL Server Profiler  
  
-   [Iniciar um rastreamento automaticamente após a conexão com um servidor &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/start-a-trace-automatically-after-connecting-to-a-server-sql-server-profiler.md)  
  
-   [Pausar um rastreamento &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/pause-a-trace-sql-server-profiler.md)  
  
-   [Interromper um rastreamento &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/stop-a-trace-sql-server-profiler.md)  
  
-   [Executar um rastreamento que foi pausado ou interrompido &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/run-a-trace-after-it-has-been-paused-or-stopped-sql-server-profiler.md)  
  
### <a name="to-open-traces-and-configure-how-traces-are-displayed-by-using-sql-server-profiler"></a>Para abrir rastreamentos e configurar a forma como serão exibidos usando o SQL Server Profiler  
  
-   [Abrir um arquivo de rastreamento &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/open-a-trace-file-sql-server-profiler.md)  
  
-   [Abrir uma tabela de rastreamento &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/open-a-trace-table-sql-server-profiler.md)  
  
-   [Limpar uma janela de rastreamento &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/clear-a-trace-window-sql-server-profiler.md)  
  
-   [Fechar uma janela de rastreamento &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/close-a-trace-window-sql-server-profiler.md)  
  
-   [Definir padrões de definição de rastreamento &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/set-trace-definition-defaults-sql-server-profiler.md)  
  
-   [Definir padrões de exibição de rastreamento &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/set-trace-display-defaults-sql-server-profiler.md)  
  
### <a name="to-replay-traces-by-using-sql-server-profiler"></a>Para repetir rastreamentos usando o SQL Server Profiler  
  
-   [Reproduzir um arquivo de rastreamento &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/replay-a-trace-file-sql-server-profiler.md)  
  
-   [Reproduzir uma tabela de rastreamento &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/replay-a-trace-table-sql-server-profiler.md)  
  
-   [Reproduzir um único evento de cada vez &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/replay-a-single-event-at-a-time-sql-server-profiler.md)  
  
-   [Reproduzir em um ponto de interrupção &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/replay-to-a-breakpoint-sql-server-profiler.md)  
  
-   [Reproduzir para um cursor &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/replay-to-a-cursor-sql-server-profiler.md)  
  
-   [Reproduzir um script Transact-SQL &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/replay-a-transact-sql-script-sql-server-profiler.md)  
  
### <a name="to-create-modify-and-use-trace-templates-by-using-sql-server-profiler"></a>Para criar, modificar e usar modelos de rastreamento usando o SQL Server Profiler  
  
-   [Criar um modelo de rastreamento &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/create-a-trace-template-sql-server-profiler.md)  
  
-   [Modificar um modelo de rastreamento &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/modify-a-trace-template-sql-server-profiler.md)  
  
-   [Derivar um modelo de um rastreamento em execução &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/derive-a-template-from-a-running-trace-sql-server-profiler.md)  
  
-   [Derivar um modelo de um arquivo ou uma tabela de rastreamento &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/derive-a-template-from-a-trace-file-or-trace-table-sql-server-profiler.md)  
  
-   [Exportar um modelo de rastreamento &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/export-a-trace-template-sql-server-profiler.md)  
  
-   [Importar um modelo de rastreamento &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/import-a-trace-template-sql-server-profiler.md)  
  
### <a name="to-use-sql-server-profiler-traces-to-collect-and-monitor-server-performance"></a>Para usar rastreamentos do SQL Server Profiler para coletar e monitorar o desempenho do servidor  
  
-   [Localizar um valor ou coluna de dados durante um rastreamento &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/find-a-value-or-data-column-while-tracing-sql-server-profiler.md)  
  
-   [Salvar gráficos de deadlock &#40;SQL Server Profiler&#41;](../../relational-databases/performance/save-deadlock-graphs-sql-server-profiler.md)  
  
-   [Salvar eventos Showplan XMLL separadamente &#40;SQL Server Profiler&#41;](../../relational-databases/performance/save-showplan-xml-events-separately-sql-server-profiler.md)  
  
-   [Salvar eventos Showplan XML Statistics Profile separadamente &#40;SQL Server Profiler&#41;](../../relational-databases/performance/save-showplan-xml-statistics-profile-events-separately-sql-server-profiler.md)  
  
-   [Extrair um script de um rastreamento &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/extract-a-script-from-a-trace-sql-server-profiler.md)  
  
-   [Correlacionar um rastreamento com dados do log de desempenho do Windows &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/correlate-a-trace-with-windows-performance-log-data-sql-server-profiler.md)  
  
  
