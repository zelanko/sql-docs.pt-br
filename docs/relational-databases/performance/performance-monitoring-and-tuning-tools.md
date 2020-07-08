---
title: Ferramentas para monitoramento e ajuste de desempenho | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
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
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: 30cc668487299677bb2874300d660d09d1dedd22
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85635452"
---
# <a name="performance-monitoring-and-tuning-tools"></a>Ferramentas para monitoramento e ajuste de desempenho
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  O [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fornece um conjunto abrangente de ferramentas para monitorar eventos no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e ajustar o design do banco de dados físico. A escolha da ferramenta depende do tipo de monitoramento ou de ajuste a ser feito e dos eventos em particular a monitorar.  
  
 A seguir, encontra-se as ferramentas de monitoramento e ajuste do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] :  
  
|Ferramenta|DESCRIÇÃO|  
|----------|-----------------|  
|[Funções internas &#40;Transact-SQL&#41;](~/t-sql/functions/functions.md)|Funções internas exibem estatísticas que retratam a atividade do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] desde o momento em que o servidor foi iniciado; essas estatísticas são armazenadas em contadores predefinidos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Por exemplo, **\@\@CPU_BUSY** contém o tempo de execução do código do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pela CPU; **\@\@CONNECTIONS** contém o número de conexões ou tentativas de conexão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e **\@\@PACKET_ERRORS** contém o número de pacotes de rede ocorridos em conexões do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|[DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)|Instruções DBCC (Database Console Command) lhe permitem examinar as estatísticas de desempenho e a consistência lógica e física de um banco de dados.|  
|[Orientador de Otimização do Mecanismo de Banco de Dados (DTA)](../../relational-databases/performance/database-engine-tuning-advisor.md)|O Orientador de Otimização do Mecanismo de Banco de Dados analisa os efeitos sobre o desempenho das instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] executadas em relação ao banco de dados que se deseja ajustar O Orientador de Otimização do Mecanismo de Banco de Dados dá recomendações sobre adição, remoção ou modificações de índices, exibições e partições.|  
|[DEA (Assistente para Experimentos de Banco de Dados)](https://www.microsoft.com/download/details.aspx?id=54090)|O DEA (Assistente para Experimentos de Banco de Dados) é uma nova solução de teste A/B para o SQL Server. Ela ajudará na avaliação de uma versão de destino do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] para uma determinada carga de trabalho. Ao atualizar de versões do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] anteriores (começando com [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]) para qualquer versão mais recente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], DEA poderá fornecer as métricas de análise comparativa.|
|Logs de erros|O log de eventos dos aplicativos Windows fornece um panorama dos eventos que ocorrem nos sistemas operacionais Windows Server e Windows como um todo, bem como dos eventos no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent e em pesquisas de texto completo. Ele contém informações sobre eventos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que não se encontram em nenhum outro lugar. Você pode usar as informações do log de erros para solucionar problemas relacionados ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|[Eventos estendidos](../../relational-databases/extended-events/extended-events.md)|Eventos Estendidos são um sistema de monitoramento de desempenho de peso leve que usa poucos recursos de desempenho. Os Eventos Estendidos fornecem três interfaces gráficas do usuário (Assistente de Nova Sessão, Nova Sessão e XE Profiler) para criar, modificar, exibir e analisar os dados da sessão.|  
|[Funções e exibições de gerenciamento dinâmico relacionadas à execução &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)|DMVs relacionadas à execução permitem a você verificar informações relacionadas à execução.|
|[Estatísticas de Consulta Dinâmica (LQS)](../../relational-databases/performance/live-query-statistics.md)|Exibe estatísticas em tempo real sobre as etapas de execução da consulta. Como esses dados estão disponíveis durante a execução da consulta, essas estatísticas de execução são extremamente úteis para depurar problemas de desempenho de consulta.|  
|[Monitorar o uso de recursos &#40;Monitor do Sistema&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)|O Monitor do Sistema rastreia, principalmente, o uso de recursos, como o número de solicitações de páginas do gerenciador de buffers em uso, o que permite monitorar o desempenho e a atividade do servidor por meio de objetos e contadores ou de contadores definidos pelo usuário para monitorar eventos. O Monitor do Sistema (Monitor de Desempenho, no Microsoft Windows NT 4.0) coleta contagens e taxas, e não dados, acerca dos eventos (por exemplo, uso de memória, número de transações ativas, números de bloqueios ou atividade de CPU). Você pode definir limites em contadores específicos para gerar alertas que notificam operadores.<br /><br /> O Monitor do Sistema funciona nos sistemas operacionais Microsoft Windows Server e Windows. Pode monitorar (remota ou localmente) uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no Windows NT 4.0 ou posterior.<br /><br /> A principal diferença entre o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] e o Monitor do Sistema é que o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] monitora eventos do Mecanismo de Banco de Dados, enquanto que o Monitor do Sistema monitora o uso de recursos associado a processos de servidor.|  
|[Abrir o Monitor de Atividade &#40;SQL Server Management Studio&#41;](../../relational-databases/performance-monitor/open-activity-monitor-sql-server-management-studio.md)|O Monitor de Atividade no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] é útil para exibições ad hoc da atividade atual, além disso, exibe graficamente informações sobre:<br /><br />– Processos em execução em uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]<br />– Processos bloqueados<br />– Bloqueios<br />– Atividade de usuário|  
|[Painel de Desempenho](../../relational-databases/performance/performance-dashboard.md)|O Painel de Desempenho no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ajuda a identificar rapidamente se há qualquer gargalo de desempenho atual em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|[Assistente de Ajuste de Consulta (QTA)](../../relational-databases/performance/upgrade-dbcompat-using-qta.md)|O recurso QTA (Assistente de Ajuste de Consulta) orientará os usuários pelo fluxo de trabalho recomendado para manter a estabilidade do desempenho durante as atualizações para as versões do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mais recentes, conforme documentado na seção *Manter a estabilidade do desempenho durante a atualização para o SQL Server mais recente* dos [Cenários de uso do Repositório de Consultas](../../relational-databases/performance/query-store-usage-scenarios.md#CEUpgrade). |  
|[Repositório de Consultas](../..//relational-databases/performance/monitoring-performance-by-using-the-query-store.md)|O recurso Repositório de Consultas fornece informações sobre escolha e desempenho do plano de consulta. Ele simplifica a solução de problemas, ajudando você a identificar rapidamente diferenças de desempenho causadas por alterações nos planos de consulta. O Repositório de Consultas captura automaticamente um histórico das consultas, dos planos e das estatísticas de runtime e os mantém para sua análise. Ele separa os dados por janelas por hora, permitindo que você veja os padrões de uso do banco de dados e entenda quando as alterações aos planos de consulta ocorreram no servidor.|
|[Rastreamento do SQL](../../relational-databases/sql-trace/sql-trace.md)|[!INCLUDE[tsql](../../includes/tsql-md.md)] que criam, filtram e definem rastreamentos:<br /><br /> [sp_trace_create &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-create-transact-sql.md)<br />[sp_trace_generateevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-generateevent-transact-sql.md)<br />[sp_trace_setevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)<br />[sp_trace_setfilter &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setfilter-transact-sql.md)<br />[sp_trace_setstatus &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setstatus-transact-sql.md)|  
|[SQL Server Distributed Replay](../../tools/distributed-replay/sql-server-distributed-replay.md)|O [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay pode usar vários computadores para reproduzir dados de rastreamento com uma simulação de uma carga de trabalho de missão crítica.|  
|[sp_trace_setfilter &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setfilter-transact-sql.md)|[!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] rastreia eventos de processos do mecanismo, como o início de um lote ou de uma transação, o que lhe permite monitorar a atividade de servidor e de banco de dados (por exemplo, deadlocks, erros fatais e atividade de logon). Você pode capturar dados do [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] em uma tabela do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou em um arquivo para análise posterior, bem como reproduzir passo a passo os eventos capturados no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para determinar o que aconteceu exatamente.|  
|[Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)|Os seguintes procedimentos armazenados do sistema do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] constituem uma excelente alternativa para muitas tarefas de monitoramento:<br /><br /> [sp_who &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-who-transact-sql.md):<br />                    Fornece informações retratando usuários e processos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] atuais, inclusive a instrução executada atualmente e se está bloqueada.<br /><br /> [sp_lock &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-lock-transact-sql.md):<br />                    Fornece informações retratando bloqueios, inclusive a ID de objeto, ID de índice, tipo de bloqueio e tipo ou recurso ao qual se aplica o bloqueio.<br /><br /> [sp_spaceused &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-spaceused-transact-sql.md): <br />                    Exibe uma estimativa da quantidade atual de espaço em disco utilizada por uma tabela (ou pelo banco de dados inteiro).<br /><br /> [sp_monitor &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-monitor-transact-sql.md):<br />                    Exibe estatísticas, incluindo o uso da CPU, uso de E/S e a quantidade de tempo ocioso desde a última execução de **sp_monitor** .|  
|[Sinalizadores de rastreamento &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)|Sinalizadores de rastreamento exibem informações sobre uma atividade específica no servidor e são usados para diagnosticar problemas ou questões de desempenho (por exemplo, cadeias de deadlock).|  
  
## <a name="choosing-a-monitoring-tool"></a>Escolhendo uma ferramenta de monitoramento  
 A escolha de uma ferramenta de monitoramento depende do evento ou da atividade a ser monitorada.  
  
|Evento ou atividade|Eventos estendidos|SQL Server Profiler|Distributed Replay|Monitor do Sistema|Monitor de Atividade|Transact-SQL|Logs de erros|Painel de Desempenho|  
|-----------------------|-----------------------|-------------------------|------------------------|--------------------|----------------------|-------------------|----------------|----------------|   
|Análise de tendência|Sim|Sim||Sim|||||  
|Reprodução dos eventos capturados||Sim (de um único computador)|Sim (de vários computadores)||||||  
|Monitoramento ad hoc|Sim<sup>1</sup>|Sim|||Sim|Sim|Sim|Sim|  
|Geração de alertas||||Sim|||||  
|Interface gráfica|Sim|Sim||Sim|Sim||Sim|Sim|  
|Uso em aplicativo personalizado|Sim|Sim<sup>2</sup>||||Sim|||  
  
 <sup>1</sup> Usando o [SQL Server Management Studio XEvent Profiler](../../relational-databases/extended-events/use-the-ssms-xe-profiler.md)    
 <sup>2</sup> Usando procedimentos armazenados do sistema [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)].  
  
## <a name="windows-monitoring-tools"></a>Ferramentas de monitoramento do Windows  
 Os sistemas operacionais Windows e Windows Server 2003 também fornecem as seguintes ferramentas de monitoramento.  
  
|Ferramenta|DESCRIÇÃO|  
|----------|-----------------|  
|Gerenciador de Tarefas|Mostra uma sinopse dos processos e aplicativos em execução no sistema.|  
|Agente do monitor da rede|Monitora o tráfego da rede.|  
  
 Para obter mais informações sobre ferramentas dos sistemas operacionais Windows ou Windows Server, consulte a documentação do Windows.  
  
  
