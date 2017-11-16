---
title: Ferramentas para monitoramento e ajuste de desempenho | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- tools [SQL Server], monitoring performance
- monitoring server performance [SQL Server], tools
- monitoring performance [SQL Server], tools
- database performance [SQL Server], tools
- tuning databases [SQL Server], tools
- database monitoring [SQL Server], tools
- performance [SQL Server], monitoring tools
- server performance [SQL Server], tools
ms.assetid: 31529dfe-68e7-49f7-b3c2-39fcecf33a95
caps.latest.revision: "37"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: d7063b1fdbcec713bea65b0e5e68f0ea40a683fd
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="performance-monitoring-and-tuning-tools"></a>Ferramentas para monitoramento e ajuste de desempenho
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fornece um conjunto abrangente de ferramentas para monitorar eventos no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e ajustar o design do banco de dados físico. A escolha da ferramenta depende do tipo de monitoramento ou de ajuste a ser feito e dos eventos em particular a monitorar.  
  
 A seguir, encontra-se as ferramentas de monitoramento e ajuste do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] :  
  
|Ferramenta|Descrição|  
|----------|-----------------|  
|[sp_trace_setfilter &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setfilter-transact-sql.md)|[!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] rastreia eventos de processos do mecanismo, como o início de um lote ou de uma transação, o que lhe permite monitorar a atividade de servidor e de banco de dados (por exemplo, deadlocks, erros fatais e atividade de logon). Você pode capturar dados do [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] em uma tabela do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou em um arquivo para análise posterior, bem como reproduzir passo a passo os eventos capturados no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para determinar o que aconteceu exatamente.|  
|[SQL Server Distributed Replay](../../tools/distributed-replay/sql-server-distributed-replay.md)|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] O Distributed Replay pode usar vários computadores para reproduzir dados de rastreamento com uma simulação de uma carga de trabalho de missão crítica.|  
|[Monitorar o uso de recursos &#40;Monitor do Sistema&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)|O Monitor do Sistema rastreia, principalmente, o uso de recursos, como o número de solicitações de páginas do gerenciador de buffers em uso, o que permite monitorar o desempenho e a atividade do servidor por meio de objetos e contadores ou de contadores definidos pelo usuário para monitorar eventos. O Monitor do Sistema (Monitor de Desempenho, no Microsoft Windows NT 4.0) coleta contagens e taxas, e não dados, acerca dos eventos (por exemplo, uso de memória, número de transações ativas, números de bloqueios ou atividade de CPU). Você pode definir limites em contadores específicos para gerar alertas que notificam operadores.<br /><br /> O Monitor do Sistema funciona nos sistemas operacionais Microsoft Windows Server e Windows. Pode monitorar (remota ou localmente) uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no Windows NT 4.0 ou posterior.<br /><br /> A principal diferença entre o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] e o Monitor do Sistema é que o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] monitora eventos do Mecanismo de Banco de Dados, enquanto que o Monitor do Sistema monitora o uso de recursos associado a processos de servidor.|  
|[Abrir o Monitor de Atividade &#40;SQL Server Management Studio&#41;](../../relational-databases/performance-monitor/open-activity-monitor-sql-server-management-studio.md)|O Monitor de Atividade no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] é útil para exibições ad hoc da atividade atual, além disso, exibe graficamente informações sobre:<br /><br /> Processos em execução em uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> Processos bloqueados.<br /><br /> Bloqueios.<br /><br /> Atividade de usuário.|  
|[Estatísticas de consulta dinâmica](../../relational-databases/performance/live-query-statistics.md)|Exibe estatísticas em tempo real sobre as etapas de execução da consulta. Como esses dados estão disponíveis durante a execução da consulta, essas estatísticas de execução são extremamente úteis para depurar problemas de desempenho de consulta.|  
|[Rastreamento do SQL](../../relational-databases/sql-trace/sql-trace.md)|[!INCLUDE[tsql](../../includes/tsql-md.md)] que criam, filtram e definem rastreamentos:<br /><br /> [sp_trace_create &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-create-transact-sql.md)<br /><br /> [sp_trace_generateevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-generateevent-transact-sql.md)<br /><br /> [sp_trace_setevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)<br /><br /> [sp_trace_setfilter &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setfilter-transact-sql.md)<br /><br /> [sp_trace_setstatus &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setstatus-transact-sql.md)|  
|Logs de erros|O log de eventos dos aplicativos Windows fornece um panorama dos eventos que ocorrem nos sistemas operacionais Windows Server e Windows como um todo, bem como dos eventos no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent e em pesquisas de texto completo. Ele contém informações sobre eventos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que não se encontram em nenhum outro lugar. Você pode usar as informações do log de erros para solucionar problemas relacionados ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|[Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)|Os seguintes procedimentos armazenados do sistema do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] constituem uma excelente alternativa para muitas tarefas de monitoramento:<br /><br /> [sp_who &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-who-transact-sql.md):<br />                    Fornece informações retratando usuários e processos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] atuais, inclusive a instrução executada atualmente e se está bloqueada.<br /><br /> [sp_lock &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-lock-transact-sql.md):<br />                    Fornece informações retratando bloqueios, inclusive a ID de objeto, ID de índice, tipo de bloqueio e tipo ou recurso ao qual se aplica o bloqueio.<br /><br /> [sp_spaceused &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-spaceused-transact-sql.md): <br />                    Exibe uma estimativa da quantidade atual de espaço em disco utilizada por uma tabela (ou pelo banco de dados inteiro).<br /><br /> [sp_monitor &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-monitor-transact-sql.md):<br />                    Exibe estatísticas, incluindo o uso da CPU, uso de E/S e a quantidade de tempo ocioso desde a última execução de **sp_monitor** .|  
|[DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)|Instruções DBCC (Database Console Command) lhe permitem examinar as estatísticas de desempenho e a consistência lógica e física de um banco de dados.|  
|[Funções internas &#40;Transact-SQL&#41;](~/t-sql/functions/functions.md)|Funções internas exibem estatísticas que retratam a atividade do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] desde o momento em que o servidor foi iniciado; essas estatísticas são armazenadas em contadores predefinidos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Por exemplo, **@@CPU_BUSY** contém o tempo durante o qual a CPU executa o código do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]; **@@CONNECTIONS** contém o número de conexões ou tentativas de conexão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e **@@PACKET_ERRORS** contém o número de pacotes de rede que ocorrem em conexões do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|[Sinalizadores de rastreamento &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)|Sinalizadores de rastreamento exibem informações sobre uma atividade específica no servidor e são usados para diagnosticar problemas ou questões de desempenho (por exemplo, cadeias de deadlock).|  
|[Orientador de Otimização do Mecanismo de Banco de Dados](../../relational-databases/performance/database-engine-tuning-advisor.md)|O Orientador de Otimização do Mecanismo de Banco de Dados analisa os efeitos sobre o desempenho das instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] executadas em relação ao banco de dados que se deseja ajustar O Orientador de Otimização do Mecanismo de Banco de Dados dá recomendações sobre adição, remoção ou modificações de índices, exibições e partições.|  
  
## <a name="choosing-a-monitoring-tool"></a>Escolhendo uma ferramenta de monitoramento  
 A escolha de uma ferramenta de monitoramento depende do evento ou da atividade a ser monitorada.  
  
|Evento ou atividade|SQL Server Profiler|Distributed Replay|Monitor do Sistema|Monitor de Atividade|Transact-SQL|Logs de erros|  
|-----------------------|-------------------------|------------------------|--------------------|----------------------|-------------------|----------------|  
|Análise de tendência|Sim||Sim||||  
|Reprodução dos eventos capturados|Sim (de um único computador)|Sim (de vários computadores)|||||  
|Monitoramento ad hoc|Sim|||Sim|Sim|Sim|  
|Geração de alertas|||Sim||||  
|Interface gráfica|Sim||Sim|Sim||Sim|  
|Uso em aplicativo personalizado|Sim*||||Sim||  
  
 *Usando procedimentos armazenados do sistema [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] .  
  
## <a name="windows-monitoring-tools"></a>Ferramentas de monitoramento do Windows  
 Os sistemas operacionais Windows e Windows Server 2003 também fornecem as seguintes ferramentas de monitoramento.  
  
|Ferramenta|Descrição|  
|----------|-----------------|  
|Gerenciador de Tarefas|Mostra uma sinopse dos processos e aplicativos em execução no sistema.|  
|Agente do monitor da rede|Monitora o tráfego da rede.|  
  
 Para obter mais informações sobre ferramentas dos sistemas operacionais Windows ou Windows Server, consulte a documentação do Windows.  
  
  
