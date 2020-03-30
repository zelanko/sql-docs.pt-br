---
title: Monitorar os componentes do SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 11/27/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
ms.assetid: e8f1b16b-ea40-4e12-886c-967ebda4e6e4
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: 252162be51d79224ac786ff44ae2620f4f189f81
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "68046747"
---
# <a name="monitor-sql-server-components"></a>Monitorar componentes do SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Monitorar é importante porque o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fornece serviço em um ambiente dinâmico. Os dados mudam no aplicativo. O tipo de acesso de que os usuários precisam muda. O modo de conexão dos usuários muda. Os tipos de aplicativos que acessam o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] podem até mudar, mas o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gerencia automaticamente os recursos em nível de sistema, como a memória e o espaço em disco, a fim de minimizar a necessidade de ajustes manuais abrangentes em nível de sistema. O monitoramento permite aos administradores identificar tendências de desempenho para determinar se são necessárias alterações.  
  
Para monitorar qualquer componente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] com eficiência:  
  
1.  Determine suas metas de monitoramento.  
2.  Selecione a ferramenta apropriada.    
3.  Identifique os componentes a monitorar.  
4.  Selecione a métrica para esses componentes.  
5.  Monitore o servidor.  
6.  Analise os dados.  
  
Cada uma destas etapas é discutida a seguir.  
  
## <a name="determine-your-monitoring-goals"></a>Determine suas metas de monitoramento  
Para monitorar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] com eficiência, você deve identificar claramente o motivo do monitoramento. Podem ser motivos:  
  
-   Estabelecer uma linha de base de desempenho.  
-   Identificar alterações de desempenho no decorrer do tempo.  
-   Diagnosticar problemas de desempenho específicos.  
-   Identificar componentes ou processos a otimizar.  
-   Comparar o efeito de aplicativos cliente diferentes sobre o desempenho.  
-   Auditar a atividade de usuário.  
-   Testar um servidor sob cargas diferentes.  
-   Testar a arquitetura de banco de dados.  
-   Testar as agendas de manutenção.  
-   Testar os planos de backup e restauração.  
-   Determinar quando modificar sua configuração de hardware.  
  
## <a name="select-the-appropriate-tool"></a>Selecione a ferramenta apropriada  
Depois de determinar o motivo do monitoramento, selecione as ferramentas apropriadas para esse tipo de monitoramento. O sistema operacional Windows e o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fornecem um conjunto completo de ferramentas para monitorar servidores em ambientes com grande volume de transações. Essas ferramentas revelam claramente a condição de uma instância do Mecanismo de Banco de Dados do SQL Server ou de uma instância do SQL Server Analysis Services.  
  
O Windows fornece as seguintes ferramentas para monitorar aplicativos em execução em um servidor:  
  
-   O [Monitor do Sistema](../../relational-databases/performance/start-system-monitor-windows.md), que permite coletar e exibir dados em tempo real sobre atividades como uso de memória, disco e processador.  
-   Logs e alertas de desempenho  
-   Gerenciador de Tarefas  
  
Para obter mais informações sobre ferramentas do Windows Server ou do Windows, consulte a documentação do Windows.  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fornece as seguintes ferramentas para monitorar componentes do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
-   [Eventos estendidos](../../relational-databases/extended-events/extended-events.md)
-   [Rastreamento do SQL](../../relational-databases/sql-trace/sql-trace.md)  
-   [SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md)  
-   [Distributed Replay Utility](../../tools/distributed-replay/sql-server-distributed-replay.md)  
-   [Monitor de Atividade](../../relational-databases/performance-monitor/activity-monitor.md)  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] Plano de execução gráfico  
-   [Procedimentos Armazenados do sistema](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)
-   [DBCC (Comandos de console de banco de dados)](../../t-sql/database-console-commands/dbcc-transact-sql.md)  
-   [Exibições e funções de gerenciamento dinâmico](../../relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
-   [Funções](../../t-sql/functions/functions.md)   
-   [Sinalizadores de rastreamento](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)   

> [!IMPORTANT]
> Rastreamento do SQL e [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] estão preteridos. O namespace *Microsoft.SqlServer.Management.Trace* que contém os objetos Trace e Replay do Microsoft SQL Server também foi preterido. 
> [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 
> Em vez disso, use Eventos Estendidos. Para obter mais informações sobre [eventos estendidos](../../relational-databases/extended-events/extended-events.md), confira [Início rápido: eventos estendidos no SQL Server](../../relational-databases/extended-events/quick-start-extended-events-in-sql-server.md) e [SSMS XEvent Profiler](../../relational-databases/extended-events/use-the-ssms-xe-profiler.md).

> [!NOTE]
> [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] para as cargas de trabalho do Analysis Services NÃO está preterido e o suporte a ele continuará.

Para obter mais informações sobre os ferramentas de monitoramento do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , veja [Ferramentas para monitoramento e ajuste de desempenho](../../relational-databases/performance/performance-monitoring-and-tuning-tools.md).  
  
## <a name="identify-the-components-to-monitor"></a>Identifique os componentes a monitorar  
A terceira etapa para monitorar uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é identificar os componentes a monitorar. Por exemplo, se estiver usando o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] para rastrear um servidor, você poderá definir que o rastreamento colete dados sobre eventos específicos. Também é possível excluir eventos que não se aplicam à situação.  
  
## <a name="select-metrics-for-monitored-components"></a>Selecione a métrica para os componentes monitorados  
Tendo identificado os componentes a monitorar, determine a métrica para esses componentes. Por exemplo, após selecionar os eventos a serem considerados por um rastreamento, você pode optar por incluir apenas dados específicos sobre os eventos. Limitar o rastreamento aos dados relevantes minimiza os recursos de sistema necessários para realizá-lo.  
  
## <a name="monitor-the-server"></a>Monitore o servidor  
Para monitorar o servidor, execute a ferramenta de monitoramento que você configurou para reunir dados. Por exemplo, após definir um rastreamento, você pode executá-lo para reunir dados sobre os eventos ocorridos no servidor.  

## <a name="analyze-the-data"></a>Analise os dados  
Terminado o rastreamento, analise os dados para ver se a meta do monitoramento foi atingida. Em caso negativo, modifique os componentes ou a métrica utilizada para monitorar o servidor.  
  
Segue, abaixo, uma descrição do processo da captura de dados de eventos e sua disposição para uso.  
  
1.  Aplique filtros para limitar os dados de eventos coletados.  
  
    Limitar os dados de eventos permite que o sistema se concentre nos eventos pertinentes ao cenário de monitoramento. Por exemplo, se desejar monitorar consultas lentas, você pode usar um filtro para monitorar apenas as consultas emitidas pelo aplicativo que levam mais de 30 segundos na execução contra um banco de dados em particular. 
    
    Para obter mais informações sobre filtragem de rastreamentos de Eventos Estendidos, confira [Início Rápido: Eventos Estendidos no SQL Server](../../relational-databases/extended-events/quick-start-extended-events-in-sql-server.md#demo-of-ssms-integration). 
    
    Para obter mais informações sobre filtragem de Rastreamento do SQL, confira [Definir um filtro de rastreamento &#40;Transact-SQL&#41;](../../relational-databases/sql-trace/set-a-trace-filter-transact-sql.md) e [Filtrar eventos em um rastreamento &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/filter-events-in-a-trace-sql-server-profiler.md).  
  
2.  Monitore (capture) os eventos.  
  
    Assim que é habilitado, o monitoramento ativo captura dados do aplicativo, da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ou do sistema operacional especificado. Por exemplo, quando a atividade do disco é monitorada por meio do Monitor do Sistema, o monitoramento captura dados de eventos, como leituras e gravações de disco, e os exibe na tela. Para obter mais informações, veja [Monitorar o uso de recursos &#40;Monitor do Sistema&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md).  
  
3.  Salve os dados de eventos capturados.  
  
    Salvar dados de eventos capturados permite analisá-lo mais tarde. Os dados de eventos capturados são salvos em um arquivo que pode ser carregado de volta na ferramenta que os criou originalmente para análise. É importante salvar os dados de eventos capturados ao criar uma linha de base de desempenho. Os dados de linha de base de desempenho são salvos e utilizados para comparar dados de eventos capturados recentemente e determinar se o desempenho é o ideal.
    
    Eventos Estendidos permitem que dados de eventos sejam salvos em um arquivo de evento, contador de eventos, histograma e buffer de anéis. Para obter mais informações, confira [Destinos para Eventos Estendidos no SQL Server](../../relational-databases/extended-events/targets-for-extended-events-in-sql-server.md).
    
    Dados de evento de Rastreamento do SQL podem, inclusive, ser reproduzidos usando o Distributed Replay Utility ou [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] permite salvar dados de evento em um arquivo ou tabela [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter mais informações, veja [Modelos e permissões do SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler-templates-and-permissions.md).  
  
4.  Crie modelos de rastreamento que contenham as configurações especificadas para capturar os eventos.  
  
    Os modelos de rastreamento contêm especificações sobre os próprios eventos, dados de eventos e filtros utilizados para capturar dados. Esses modelos podem ser usados para monitorar um conjunto de eventos específicos mais tarde sem ter que redefinir os eventos, dados de eventos ou filtros. Por exemplo, se desejar monitorar com frequência o número de deadlocks e os usuários envolvidos neles, você poderá criar um modelo com a definição desses eventos, dados de eventos e filtros de eventos, salvá-lo e reaplicar o filtro na próxima vez em que quiser monitorar deadlocks.
    
    Uma definição de sessão de Evento Estendido é um modelo que pode ser inserido no script e usado novamente. Para criar e gerenciar sessões, confira [Gerenciar Sessões de Evento no Pesquisador de Objetos](../../relational-databases/extended-events/manage-event-sessions-in-the-object-explorer.md). O XEvent Profiler [!INCLUDE[ssManStudio](../../includes/ssManStudio-md.md)] já fornece modelos que estão prontos para uso. Para obter mais informações, confira [Usar o SSMS XEvent Profiler](../../relational-databases/extended-events/use-the-ssms-xe-profiler.md).
       
    [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] usa modelos de rastreamento para esse propósito. Para obter mais informações, veja [Definir padrões de definição de rastreamento &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/set-trace-definition-defaults-sql-server-profiler.md) e [Criar um modelo de rastreamento &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/create-a-trace-template-sql-server-profiler.md).  
    
    > [!TIP]
    > Uma definição de rastreamento do SQL pode ser convertida em uma sessão de Eventos Estendidos. Para obter mais informações, confira [Converter um script existente de rastreamento SQL em uma sessão de Eventos Estendidos](../../relational-databases/extended-events/convert-an-existing-sql-trace-script-to-an-extended-events-session.md).
  
5.  Analise os dados de eventos capturados.  
  
     Para a análise, os dados de eventos capturados são carregados no aplicativo que os capturou. 
     
     Por exemplo, um rastreamento capturado de Evento Estendido pode ser recarregado em [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para exibição e análise. Para obter mais informações, consulte [Exibição avançada de dados de destino dos Eventos Estendidos no SQL Server](../../relational-databases/extended-events/advanced-viewing-of-target-data-from-extended-events-in-sql-server.md).

     Dados de rastreamento do SQL podem ser recarregados no [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] para exibição e análise. Para obter mais informações, veja [Exibir e analisar rastreamentos com o SQL Server Profiler](../../tools/sql-server-profiler/view-and-analyze-traces-with-sql-server-profiler.md).  
  
     Analisar dados de eventos requer determinar o que está acontecendo e por quê. Essas informações lhe permitem fazer alterações que possam melhorar o desempenho, como adicionar mais memória, alterar índices, corrigir problemas de código com instruções ou procedimentos armazenados do [!INCLUDE[tsql](../../includes/tsql-md.md)] e assim por diante, segundo o tipo de análise realizada. Por exemplo, você pode usar o Orientador de Otimização do [!INCLUDE[ssDE](../../includes/ssde-md.md)] para analisar um rastreamento capturado de Eventos Estendidos ou [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] e fazer recomendações de índice de acordo com os resultados.  
  
6.  Reproduza dados de evento capturados (opcional).  
  
     A reprodução de eventos permite estabelecer uma cópia de teste do ambiente de banco de dados do qual os dados foram capturados e repetir os eventos capturados conforme ocorreram originalmente no sistema real. Esse recurso está disponível somente com o Distributed Replay Utility ou o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]. É possível reproduzir os eventos na mesma velocidade em que ocorreram originalmente, o mais rápido possível (para estressar o sistema) ou, mais provavelmente, uma etapa por vez (para analisar o sistema após a ocorrência de cada evento). Analisando os eventos exatos em um ambiente de teste, é possível prevenir danos ao sistema de produção. Para obter mais informações, veja [Reproduzir rastreamentos](../../tools/sql-server-profiler/replay-traces.md).  
  
  
