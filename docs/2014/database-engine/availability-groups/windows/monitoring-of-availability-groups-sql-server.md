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
manager: craigg
ms.openlocfilehash: 1793032a72ae1dd150caa5ddd1739f7f5620bce1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62790187"
---
# <a name="monitoring-of-availability-groups-sql-server"></a>Monitoramento de grupos de disponibilidade (SQL Server)
  Para monitorar as propriedades e o estado de um grupo de disponibilidade AlwaysOn, você pode usar as seguintes ferramentas.  
  
|Ferramenta|Descrição breve|Links|  
|----------|-----------------------|-----------|  
|Pacote de monitoramento do System Center para SQL Server|O pacote de Monitoramento para SQL Server (SQLMP) é a solução indicada para monitorar grupos de disponibilidade, réplica de disponibilidade e bancos de dados de disponibilidade para administradores de TI. Os recursos de monitoramento que são de particular relevância para o [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] incluem o seguinte:<br /><br /> Capacidade de descoberta automática de grupos de disponibilidade, réplicas de disponibilidade e banco de dados de disponibilidade dentre centenas de computadores. Isto permite que você mantenha o controle de seu inventário de [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] .<br /><br /> Alertas e tickets totalmente capazes do System Center Operations Manager (SCOM). Estes recursos fornecem um conhecimento detalhado que permite uma resolução mais rápida para um problema.<br /><br /> Uma extensão personalizada para o monitoramento de integridade AlwaysOn usando um gerenciamento baseado em políticas (PBM).<br /><br /> Acúmulos de integridade de bancos de dados de disponibilidade para réplicas de disponibilidade.<br /><br /> Tarefas personalizadas que gerenciam o [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] do console do System Center Operations Manager.|Para baixar o pacote de monitoramento (SQLServerMP.msi) e o *Guia do Pacote de Gerenciamento do SQL Server para System Center Operations Manager* (SQLServerMPGuide.doc), consulte:<br /><br /> [Pacote de monitoramento do System Center para SQL Server](https://www.microsoft.com/download/details.aspx?displaylang=en&id=10631)|  
|[!INCLUDE[tsql](../../../includes/tsql-md.md)]|[!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] e as exibições de gerenciamento dinâmico fornecem informações preciosas sobre seus grupos de disponibilidade e suas réplicas, bancos de dados, ouvintes e ambiente de cluster WSFC.|[Monitorar grupos de disponibilidade &#40;Transact-SQL&#41;](monitor-availability-groups-transact-sql.md)|  
|[!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]|O painel **Detalhes do Pesquisador de Objetos** exibe informações básicas sobre os grupos de disponibilidade hospedados na instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] à qual você está conectado.<br /><br /> Dica: Use esse painel para selecionar vários grupos de disponibilidade, réplicas ou bancos de dados e executar tarefas administrativas rotineiras nos objetos selecionados; Por exemplo, remover várias réplicas de disponibilidade ou bancos de dados de um grupo de disponibilidade.|[Usar os detalhes do Pesquisador de Objetos para monitorar grupos de disponibilidade &#40;SQL Server Management Studio&#41;](use-object-explorer-details-to-monitor-availability-groups.md)|  
|[!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]|As caixas de diálogo de**Propriedades** permitem que você exiba as propriedades dos grupos de disponibilidade, réplicas ou ouvintes e, em alguns casos, alterar os seus valores.|[Exibir as propriedades do grupo de disponibilidade &#40;SQL Server&#41;](view-availability-group-properties-sql-server.md)<br /><br /> [Exibir as propriedades da réplica de disponibilidade &#40;SQL Server&#41;](view-availability-replica-properties-sql-server.md)<br /><br /> [Exibir propriedades do ouvinte do grupo de disponibilidade &#40;SQL Server&#41;](view-availability-group-listener-properties-sql-server.md)|  
|Monitor do Sistema|O objeto de desempenho **SQLServer:Availability Replica** contém contadores de desempenho que relatam informações sobre réplicas de disponibilidade.|[SQL Server, Réplica de Disponibilidade](../../../relational-databases/performance-monitor/sql-server-availability-replica.md)|  
|Monitor do Sistema|O objeto de desempenho **SQLServer:Database Replica** contém contadores de desempenho que relatam informações sobre os bancos de dados secundários em uma determinada réplica secundária.<br /><br /> O objeto **SQLServer:Databases** no SQL Server contém contadores de desempenho que monitoram atividades do log de transações, entre outras coisas. Os contadores a seguir são particularmente relevantes para monitorar a atividade de log de transações em bancos de dados de disponibilidade: **Tempo de Gravação de Liberação de Log (ms)** , **Liberações de Log/s**, **Perdas no Cache do Pool de Logs/s**, **Leituras de Disco do Pool de Logs/s** e **Solicitações do Pool de Logs/s**.|[SQL Server, Réplica de banco de dados](../../../relational-databases/performance-monitor/sql-server-database-replica.md) e [SQL Server, objeto Databases](../../../relational-databases/performance-monitor/sql-server-databases-object.md)|  
  
##  <a name="RelatedContent"></a> Conteúdo relacionado  
  
-   **Blogs:**  
  
     [O modelo de integridade AlwaysOn parte 1 – arquitetura do modelo de integridade](https://blogs.msdn.com/b/sqlalwayson/archive/2012/02/09/overview-of-the-alwayson-manageability-health-model.aspx)  
  
     [O modelo de integridade AlwaysOn parte 2 – Extending the Health Model](https://blogs.msdn.com/b/sqlalwayson/archive/2012/02/13/extending-the-alwayson-health-model.aspx)  
  
     [Monitorando a integridade do AlwaysOn com o PowerShell - parte 1: Basic cmdlet overview](https://blogs.msdn.com/b/sqlalwayson/archive/2012/02/13/monitoring-alwayson-health-with-powershell-part-1.aspx) (Monitoramento de integridade do Always On com o PowerShell, parte 1: visão geral básica de cmdlet)  
  
     [Monitorando a integridade do AlwaysOn com o PowerShell - parte 2: Advanced cmdlet usage](https://blogs.msdn.com/b/sqlalwayson/archive/2012/02/13/monitoring-alwayson-health-with-powershell-part-2.aspx) (Monitoramento de integridade do Always On com o PowerShell, parte 2: uso avançado de cmdlet)  
  
     [Monitorando a integridade do AlwaysOn com o PowerShell - parte 3: A simple monitoring application](https://blogs.msdn.com/b/sqlalwayson/archive/2012/02/15/monitoring-alwayson-health-with-powershell-part-3.aspx) (Monitoramento de integridade do Always On com o PowerShell, parte 3: um aplicativo de monitoramento simples)  
  
     [Monitorando a integridade do AlwaysOn com o PowerShell - parte 4: Integration with SQL Server Agent](https://blogs.msdn.com/b/sqlalwayson/archive/2012/02/15/the-always-on-health-model-part-4.aspx) (Monitoramento de integridade do Always On com o PowerShell, parte 4: integração ao SQL Server Agent)  
  
     [Blogs da equipe do AlwaysOn do SQL Server: O Team Blog oficial do SQL Server AlwaysOn](https://blogs.msdn.com/b/sqlalwayson/)  
  
     [Blogs dos engenheiros do CSS SQL Server](https://blogs.msdn.com/b/psssql/)  
  
-   **White papers:**  
  
     [White papers da Microsoft para SQL Server 2012](https://msdn.microsoft.com/library/hh403491.aspx)  
  
     [White papers da equipe de consultoria do cliente do SQL Server](http://sqlcat.com/)  
  
## <a name="see-also"></a>Consulte também  
 [Exibições do catálogo de grupos de disponibilidade AlwaysOn &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/always-on-availability-groups-catalog-views-transact-sql)   
 [Grupos de disponibilidade AlwaysOn, funções e exibições de gerenciamento dinâmico &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/always-on-availability-groups-dynamic-management-views-functions)   
 [Política de failover flexível para failover automático de um grupo de disponibilidade &#40;SQL Server&#41;](flexible-automatic-failover-policy-availability-group.md)   
 [Visão geral dos grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [Reparo automático de página &#40;para grupos de disponibilidade e espelhamento de banco de dados&#41;](../../../sql-server/failover-clusters/automatic-page-repair-availability-groups-database-mirroring.md)   
 [Usar o Painel AlwaysOn &#40;SQL Server Management Studio&#41;](use-the-always-on-dashboard-sql-server-management-studio.md)  
  
  
