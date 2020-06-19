---
title: Monitoramento de grupos de disponibilidade (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- Availability Groups [SQL Server], troubleshooting
ms.assetid: 1d5e3291-0d0a-45a1-88e5-1fc242d17210
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: da41c6d629ffb57749ae9c13e715f535e98aa3da
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84936696"
---
# <a name="monitoring-of-availability-groups-sql-server"></a>Monitoramento de grupos de disponibilidade (SQL Server)
  Para monitorar as propriedades e o estado de um grupo de disponibilidade AlwaysOn, você pode usar as seguintes ferramentas.  
  
|Ferramenta|Breve descrição|Links|  
|----------|-----------------------|-----------|  
|Pacote de monitoramento do System Center para SQL Server|O pacote de Monitoramento para SQL Server (SQLMP) é a solução indicada para monitorar grupos de disponibilidade, réplica de disponibilidade e bancos de dados de disponibilidade para administradores de TI. Os recursos de monitoramento que são de particular relevância para o [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] incluem o seguinte:<br /><br /> Capacidade de descoberta automática de grupos de disponibilidade, réplicas de disponibilidade e banco de dados de disponibilidade dentre centenas de computadores. Isto permite que você mantenha o controle de seu inventário de [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] .<br /><br /> Alertas e tickets totalmente capazes do System Center Operations Manager (SCOM). Estes recursos fornecem um conhecimento detalhado que permite uma resolução mais rápida para um problema.<br /><br /> Uma extensão personalizada para o monitoramento de integridade AlwaysOn usando um gerenciamento baseado em políticas (PBM).<br /><br /> Acúmulos de integridade de bancos de dados de disponibilidade para réplicas de disponibilidade.<br /><br /> Tarefas personalizadas que gerenciam o [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] do console do System Center Operations Manager.|Para baixar o pacote de monitoramento (SQLServerMP.msi) e o *Guia do Pacote de Gerenciamento do SQL Server para System Center Operations Manager* (SQLServerMPGuide.doc), consulte:<br /><br /> [Pacote de monitoramento do System Center para SQL Server](https://www.microsoft.com/download/details.aspx?displaylang=en&id=10631)|  
|[!INCLUDE[tsql](../../../includes/tsql-md.md)]|[!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] e as exibições de gerenciamento dinâmico fornecem informações preciosas sobre seus grupos de disponibilidade e suas réplicas, bancos de dados, ouvintes e ambiente de cluster WSFC.|[Monitorar grupos de disponibilidade &#40;Transact-SQL&#41;](monitor-availability-groups-transact-sql.md)|  
|[!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]|O painel **Detalhes do Pesquisador de Objetos** exibe informações básicas sobre os grupos de disponibilidade hospedados na instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] à qual você está conectado.<br /><br /> Dica: use esse painel para selecionar vários grupos de disponibilidade, réplicas ou bancos de dados e executar tarefas administrativas rotineiras nos objetos selecionados; por exemplo, remover várias réplicas ou bancos de dados de disponibilidade de um grupo de disponibilidade.|[Usar os detalhes do Pesquisador de Objetos para monitorar grupos de disponibilidade &#40;SQL Server Management Studio&#41;](use-object-explorer-details-to-monitor-availability-groups.md)|  
|[!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]|As caixas de diálogo de**Propriedades** permitem que você exiba as propriedades dos grupos de disponibilidade, réplicas ou ouvintes e, em alguns casos, alterar os seus valores.|[Exibir as propriedades do grupo de disponibilidade &#40;SQL Server&#41;](view-availability-group-properties-sql-server.md)<br /><br /> [Exibir as propriedades da réplica de disponibilidade &#40;SQL Server&#41;](view-availability-replica-properties-sql-server.md)<br /><br /> [Exibir propriedades do ouvinte do grupo de disponibilidade &#40;SQL Server&#41;](view-availability-group-listener-properties-sql-server.md)|  
|Monitor do Sistema|O objeto de desempenho **SQLServer:Availability Replica** contém contadores de desempenho que relatam informações sobre réplicas de disponibilidade.|[SQL Server, Réplica de Disponibilidade](../../../relational-databases/performance-monitor/sql-server-availability-replica.md)|  
|Monitor do Sistema|O objeto de desempenho **SQLServer:Database Replica** contém contadores de desempenho que relatam informações sobre os bancos de dados secundários em uma determinada réplica secundária.<br /><br /> O objeto **SQLServer:Databases** no SQL Server contém contadores de desempenho que monitoram atividades do log de transações, entre outras coisas. Os contadores a seguir são particularmente relevantes para o monitoramento de atividades do log de transações em bancos de dados de disponibilidade: **Tempo de Gravação de Liberação de Log (ms)**, **Liberações de log/s**, **Erros de Cache do Pool de Logs/s**, **Leituras de Disco do Pool de Logs/s**e **Solicitações do Pool de Logs/s**.|[SQL Server, Réplica de banco de dados](../../../relational-databases/performance-monitor/sql-server-database-replica.md) e [SQL Server, objeto Databases](../../../relational-databases/performance-monitor/sql-server-databases-object.md)|  
  
##  <a name="related-content"></a><a name="RelatedContent"></a> Conteúdo relacionado  
  
-   **Blogs:**  
  
     [O modelo de integridade AlwaysOn Parte 1 -- Arquitetura do modelo de integridade](https://docs.microsoft.com/archive/blogs/sqlalwayson/the-alwayson-health-model-part-1-health-model-architecture)  
  
     [O modelo de integridade AlwaysOn Parte 2 -- Estendendo o modelo de integridade](https://docs.microsoft.com/archive/blogs/sqlalwayson/the-alwayson-health-model-part-2-extending-the-health-model)  
  
     [Monitorando a integridade do AlwaysOn com o PowerShell - parte 1: Visão geral básica de cmdlet](https://docs.microsoft.com/archive/blogs/sqlalwayson/monitoring-alwayson-health-with-powershell-part-1-basic-cmdlet-overview)  
  
     [Monitorando a integridade do AlwaysOn com o PowerShell - parte 2: Uso avançado de cmdlet](https://docs.microsoft.com/archive/blogs/sqlalwayson/monitoring-alwayson-health-with-powershell-part-2-advanced-cmdlet-usage)  
  
     [Monitorando a integridade do AlwaysOn com o PowerShell - parte 3: Um simples aplicativo de monitoramento](https://docs.microsoft.com/archive/blogs/sqlalwayson/monitoring-alwayson-health-with-powershell-part-3-a-simple-monitoring-application)  
  
     [Monitorando a integridade do AlwaysOn com o PowerShell - parte 4: Integração com o SQL Server Agent](https://docs.microsoft.com/archive/blogs/sqlalwayson/monitoring-alwayson-health-with-powershell-part-4-integration-with-sql-server-agent)  
  
     [Blogs da equipe do SQL Server AlwaysOn: o blog oficial da equipe do SQL Server AlwaysOn](https://docs.microsoft.com/archive/blogs/sqlalwayson/)  
  
     [Blogs dos engenheiros do CSS SQL Server](https://blogs.msdn.com/b/psssql/)  
  
-   **Whitepapers:**  
  
     [White papers da Microsoft para SQL Server 2012](https://msdn.microsoft.com/library/hh403491.aspx)  
  
     [White papers da equipe de consultoria do cliente do SQL Server](http://sqlcat.com/)  
  
## <a name="see-also"></a>Consulte Também  
 [Grupos de Disponibilidade AlwaysOn exibições de catálogo &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/always-on-availability-groups-catalog-views-transact-sql)   
 [Grupos de Disponibilidade AlwaysOn exibições e funções de gerenciamento dinâmico &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/always-on-availability-groups-dynamic-management-views-functions)   
 [Política de failover flexível para failover automático de um grupo de disponibilidade &#40;SQL Server&#41;](flexible-automatic-failover-policy-availability-group.md)   
 [Visão geral do Grupos de Disponibilidade AlwaysOn &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [&#40;de reparo automático de página para grupos de disponibilidade e espelhamento de banco de dados&#41;](../../../sql-server/failover-clusters/automatic-page-repair-availability-groups-database-mirroring.md)   
 [Usar o Painel AlwaysOn &#40;SQL Server Management Studio&#41;](use-the-always-on-dashboard-sql-server-management-studio.md)  
  
  
