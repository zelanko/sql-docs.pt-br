---
title: "Estatísticas de consulta dinâmica | Microsoft Docs"
ms.custom: SQL2016_New_Updated
ms.date: 10/28/2015
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- query statistics [SQL Server] live query stats
- live query statistics
- debugging [SQL Server], live query stats
- statistics [SQL Server], live query statistics
ms.assetid: 07f8f594-75b4-4591-8c29-d63811d7753e
caps.latest.revision: "16"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 5381ceb39baa1e81001d9d80c9171545038a09b2
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="live-query-statistics"></a>Estatísticas de Consulta ao Vivo
  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] fornece a capacidade de exibir o plano de execução ao vivo de uma consulta ativa. Esse plano de consulta ao vivo fornece visões em tempo real sobre o processo de execução da consulta, conforme os controles são transmitidos de um operador de plano de consulta para outro. O plano de consulta ao vivo exibe o progresso geral da consulta e as estatísticas de tempo de execução do nível de operador, como o número de linhas produzido, tempo decorrido, progresso do operador, etc. Como esses dados estão disponíveis em tempo real sem a necessidade de aguardar a conclusão da consulta, essas estatísticas de execução são extremamente úteis para depurar problemas de desempenho de consulta. Este recurso está disponível do [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] em diante; no entanto, ele pode funcionar com o [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)].  
  
**Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] até a [versão atual](http://go.microsoft.com/fwlink/p/?LinkId=299658)).  
  
> [!WARNING]  
>  Este recurso é usado principalmente para a solução de problemas. O uso desse recurso pode diminuir moderadamente o desempenho geral da consulta. Esse recurso pode ser usado com o [Depurador Transact-SQL](../../relational-databases/scripting/configure-firewall-rules-before-running-the-tsql-debugger.md).  
  
#### <a name="to-view-live-query-statistics"></a>Para exibir estatísticas de consulta ao vivo  
  
1.  Para exibir o plano de execução de consulta ao vivo, no menu Ferramentas, clique no ícone **Estatísticas de Consulta ao Vivo** .  
  
     ![Botão Estatísticas de Consulta Dinâmica na barra de ferramentas](../../relational-databases/performance/media/livequerystatstoolbar.png "Botão Estatísticas de Consulta Dinâmica na barra de ferramentas")  
  
     Exiba também o acesso ao plano de execução de consulta dinâmica clicando com o botão direito do mouse em uma consulta selecionada no [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] e, em seguida, clique em **Incluir Estatísticas de Consulta Dinâmica**.  
  
     ![Botão Estatísticas de Consulta Dinâmica no menu pop-up](../../relational-databases/performance/media/livequerystatsmenu.png "Botão Estatísticas de Consulta Dinâmica no menu pop-up")  
  
2.  Agora execute a consulta. O plano de consulta dinâmico exibe o progresso geral da consulta e as estatísticas de tempo de execução (por exemplo, tempo decorrido, progresso, etc.) dos operadores do plano de consulta. As informações de andamento da consulta e as estatísticas de execução são atualizadas periodicamente enquanto a execução da consulta está em andamento. Use essas informações para entender o processo de execução geral da consulta e depurar consultas de longa execução, consultas executadas indefinidamente, consultas que causam estouro de tempdb e problemas de tempo limite.  
  
     ![Botão Estatísticas de Consulta Dinâmica no plano de execução](../../relational-databases/performance/media/livequerystatsplan.png "Botão Estatísticas de Consulta Dinâmica no plano de execução")  
  
 O plano de execução ao vivo também pode ser acessado pelo **Monitor de Atividades** clicando com o botão direito nas consultas, na tabela **Consultas Dispendiosas Ativas** .  
  
 ![Botão Estatísticas de Consulta Dinâmica no Monitor de Atividade](../../relational-databases/performance/media/livequerystatsactmon.png "Botão Estatísticas de Consulta Dinâmica no Monitor de Atividade")  
  
## <a name="remarks"></a>Comentários  
 A infraestrutura do perfil de estatísticas deve ser habilitada antes que as estatísticas de consulta ao vivo possam capturar informações sobre o andamento das consultas. A especificação de **Incluir Estatísticas de Consulta ao Vivo** no [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] habilita a infraestrutura de estatísticas para a sessão de consulta atual. 
 
Até o [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], há duas outras maneiras de habilitar a infraestrutura de estatísticas que pode ser usada para exibir as estatísticas de consultas dinâmicas em outras sessões (por exemplo, no Monitor de Atividade):  
  
-   Execute `SET STATISTICS XML ON;` ou `SET STATISTICS PROFILE ON;` na sessão de destino.  
  
 ou  
  
-   Habilitar o evento estendido **query_post_execution_showplan** . Esta é uma configuração ampla de servidor que permite estatísticas de consulta ao vivo em todas as sessões. Para habilitar eventos estendidos, consulte [Monitor System Activity Using Extended Events](../../relational-databases/extended-events/monitor-system-activity-using-extended-events.md).  

Do [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1 em diante, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] inclui uma versão leve da infraestrutura do perfil de estatísticas. Há duas maneiras de habilitar a infraestrutura de estatísticas leve que pode ser usada para exibir as estatísticas de consultas dinâmicas em outras sessões (por exemplo, no Monitor de Atividade):

-   Use o sinalizador de rastreamento global 7412.  
  
 ou  
  
-   Habilite o evento estendido **query_thread_profile** . Esta é uma configuração ampla de servidor que permite estatísticas de consulta ao vivo em todas as sessões. Para habilitar eventos estendidos, consulte [Monitor System Activity Using Extended Events](../../relational-databases/extended-events/monitor-system-activity-using-extended-events.md).
  
 > [!NOTE]
 > Não há suporte para procedimentos armazenados nativamente compilados.  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão **SHOWPLAN** do nível de banco de dados para preencher a página de resultados **Estatísticas de Consulta ao Vivo** , a permissão de nível de servidor **VIEW SERVER STATE** para ver as estatísticas ao vivo e exige as permissões necessárias para executar a consulta.  
  
## <a name="see-also"></a>Consulte também  
 [Monitorar e ajustar o desempenho](../../relational-databases/performance/monitor-and-tune-for-performance.md)   
 [Ferramentas para monitoramento e ajuste de desempenho](../../relational-databases/performance/performance-monitoring-and-tuning-tools.md)   
 [Abrir o Monitor de Atividade &#40;SQL Server Management Studio&#41;](../../relational-databases/performance-monitor/open-activity-monitor-sql-server-management-studio.md)   
 [Monitor de atividade](../../relational-databases/performance-monitor/activity-monitor.md)   
 [Monitorando o desempenho usando o Repositório de Consultas](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)   
 [sys.dm_exec_query_statistics_xml](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-statistics-xml-transact-sql.md)   
 [sys.dm_exec_query_profiles](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-profiles-transact-sql.md)   
 [Sinalizadores de rastreamento](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)
