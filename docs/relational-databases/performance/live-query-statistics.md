---
title: Estatísticas de consulta dinâmica | Microsoft Docs
ms.custom: ''
ms.date: 11/21/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- query statistics [SQL Server] live query stats
- live query statistics
- debugging [SQL Server], live query stats
- statistics [SQL Server], live query statistics
- query profiling
- lightweight query profiling
- lightweight profiling
ms.assetid: 07f8f594-75b4-4591-8c29-d63811d7753e
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: 82634dc8169fa266e6fb1c92ec9a14129e40e947
ms.sourcegitcommit: 2d4067fc7f2157d10a526dcaa5d67948581ee49e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/28/2020
ms.locfileid: "78180083"
---
# <a name="live-query-statistics"></a>Estatísticas de Consulta ao Vivo
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] fornece a capacidade de exibir o plano de execução ao vivo de uma consulta ativa. Esse plano de consulta dinâmica fornece informações em tempo real sobre o processo de execução da consulta, conforme os controles fluem de um [operador de plano de consulta](../../relational-databases/showplan-logical-and-physical-operators-reference.md) para outro. O plano de consulta ao vivo exibe o progresso geral da consulta e as estatísticas de tempo de execução do nível de operador, como o número de linhas produzido, tempo decorrido, progresso do operador, etc. Como esses dados estão disponíveis em tempo real sem a necessidade de aguardar a conclusão da consulta, essas estatísticas de execução são extremamente úteis para depurar problemas de desempenho de consulta. Este recurso está disponível do [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] em diante; no entanto, ele pode funcionar com o [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)].  

> [!NOTE]
> Internamente, estatísticas de consulta em tempo real aproveitam o DMV [sys.dm_exec_query_profiles](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-profiles-transact-sql.md).
  
**Aplica-se a:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (começando com [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]) e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
> [!WARNING]  
> Este recurso é usado principalmente para a solução de problemas. O uso desse recurso pode diminuir moderadamente o desempenho geral da consulta, especialmente em [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]. Para obter mais informações, confira [Infraestrutura de Criação de Perfil de Consulta](../../relational-databases/performance/query-profiling-infrastructure.md).  
> Esse recurso pode ser usado com o [Depurador Transact-SQL](../../relational-databases/scripting/configure-firewall-rules-before-running-the-tsql-debugger.md).  
  
## <a name="to-view-live-query-statistics-for-one-query"></a>Para exibir estatísticas de consulta em tempo real para uma consulta 
  
1.  Para exibir o plano de execução de consulta ao vivo, no menu Ferramentas, clique no ícone **Incluir Estatísticas de Consulta em Tempo Real**.  
  
     ![Botão de Estatísticas de Consultas Dinâmicas na barra de ferramentas](../../relational-databases/performance/media/livequerystatstoolbar.png "Botão de Estatísticas de Consultas Dinâmicas na barra de ferramentas")  
  
     Também é possível acessar o plano de execução de consulta dinâmica clicando com o botão direito do mouse em uma consulta selecionada no [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] e, em seguida, clicando em **Incluir Estatísticas de Consulta Dinâmica**.  
  
     ![Botão de Estatísticas de Consultas Dinâmicas no menu pop-up](../../relational-databases/performance/media/livequerystatsmenu.png "Botão de Estatísticas de Consultas Dinâmicas no menu pop-up")  
  
2.  Agora execute a consulta. O plano de consulta dinâmico exibe o progresso geral da consulta e as estatísticas de tempo de execução (por exemplo, tempo decorrido, progresso, etc.) dos operadores do plano de consulta. As informações de andamento da consulta e as estatísticas de execução são atualizadas periodicamente enquanto a execução da consulta está em andamento. Use essas informações para entender o processo de execução geral da consulta e depurar consultas de longa execução, consultas executadas indefinidamente, consultas que causam estouro de tempdb e problemas de tempo limite.  
  
     ![Botão de Estatísticas de Consultas Dinâmicas no plano de execução](../../relational-databases/performance/media/livequerystatsplan.png "Botão de Estatísticas de Consultas Dinâmicas no plano de execução")  
  
## <a name="to-view-live-query-statistics-for-any-query"></a>Para exibir estatísticas de consulta em tempo real para qualquer consulta 

O plano de execução em tempo real também pode ser acessado pelo **[Monitor de Atividades](../../relational-databases/performance-monitor/activity-monitor.md)** clicando com o botão direito do mouse em qualquer consulta na tabela **Processos** ou **Consultas Dispendiosas Ativas**.  
  
 ![Botão de Estatísticas de Consultas Dinâmicas no Monitor de Atividade](../../relational-databases/performance/media/livequerystatsactmon.png "Botão de Estatísticas de Consultas Dinâmicas no Monitor de Atividade")  
  
## <a name="remarks"></a>Comentários  
 A infraestrutura do perfil de estatísticas deve ser habilitada antes que as estatísticas de consulta ao vivo possam capturar informações sobre o andamento das consultas. Dependendo da versão, a sobrecarga pode ser significativa. Para obter mais informações sobre essa sobrecarga, confira [Infraestrutura de criação de perfil de consulta](../../relational-databases/performance/query-profiling-infrastructure.md).
  
## <a name="permissions"></a>Permissões  
Requer permissão `SHOWPLAN` no nível de banco de dados para preencher a página de resultados de **Estatísticas de consulta em tempo real** e requer as permissões necessárias para executar a consulta.
No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], é necessária a permissão `VIEW SERVER STATE` de nível de servidor para ver as estatísticas dinâmicas.  
Nas camadas Premium do [!INCLUDE[ssSDS](../../includes/sssds-md.md)], é necessária a permissão `VIEW DATABASE STATE` no banco de dados para ver as estatísticas dinâmicas. Nas camadas Standard e Basic do [!INCLUDE[ssSDS](../../includes/sssds-md.md)], é necessária a conta de **administrador do servidor** ou uma conta de **administrador do Azure Active Directory** para ver as estatísticas dinâmicas.
  
## <a name="see-also"></a>Consulte Também  
 [Monitorar e ajustar o desempenho](../../relational-databases/performance/monitor-and-tune-for-performance.md)     
 [Ferramentas para monitoramento e ajuste de desempenho](../../relational-databases/performance/performance-monitoring-and-tuning-tools.md)     
 [Abrir o Monitor de Atividade &#40;SQL Server Management Studio&#41;](../../relational-databases/performance-monitor/open-activity-monitor-sql-server-management-studio.md)     
 [Monitor de atividade](../../relational-databases/performance-monitor/activity-monitor.md)     
 [Monitorando o desempenho com o repositório de consultas](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)     
 [sys.dm_exec_query_statistics_xml](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-statistics-xml-transact-sql.md)     
 [sys.dm_exec_query_profiles](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-profiles-transact-sql.md)     
 [Sinalizadores de rastreamento](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)    
 [Referência de operadores físicos e lógicos de plano de execução](../../relational-databases/showplan-logical-and-physical-operators-reference.md)     
 [Infraestrutura de Criação de Perfil de Consulta](../../relational-databases/performance/query-profiling-infrastructure.md)   
