---
title: Habilitar o recurso de grupo de disponibilidade para uma instância do SQL Server
description: Descreve como habilitar o recurso de grupo de disponibilidade Always On para uma instância do SQL Server.
ms.custom: seodec18
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: how-to
helpviewer_keywords:
- Availability Groups [SQL Server], server instance
- Availability Groups [SQL Server], about
ms.assetid: fad8db32-593e-49d5-989c-39eb8399c416
author: cawrites
ms.author: chadam
ms.openlocfilehash: f45626f82de0e1754ed34a515f9daeb68c54fbb8
ms.sourcegitcommit: 54cd97a33f417432aa26b948b3fc4b71a5e9162b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/13/2020
ms.locfileid: "94584528"
---
# <a name="enable-the-always-on-availability-group-feature-for-a-sql-server-instance"></a>Habilitar o recurso de grupo de disponibilidade Always On para uma instância do SQL Server
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]

  Este tópico contém informações sobre os requisitos de configuração de uma instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para dar suporte ao [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] no [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)].  
  
> [!IMPORTANT]  
>  Para obter informações básicas sobre os pré-requisitos e restrições do [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] em nós do WSFC (Cluster de Failover do Windows Server) e em instâncias do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], veja [Pré-requisitos, restrições e recomendações para grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md).  
   
##  <a name="terms-and-definitions"></a><a name="TermsAndDefinitions"></a> Termos e definições  
 [Grupos de disponibilidade AlwaysOn](../../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)  
 Uma solução de alta disponibilidade e de recuperação de desastres que fornece uma substituição em nível corporativo para o espelhamento de banco de dados. Um *grupo de disponibilidade* dá suporte a um ambiente de failover para um conjunto discreto de bancos de dados de usuário, conhecidos como *bancos de dados de disponibilidade*, que fazem failover juntos.  
  
 réplica de disponibilidade  
 Uma instanciação de um grupo de disponibilidade que é hospedado por uma instância específica do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e que mantém uma cópia local de cada banco de dados de disponibilidade pertencente ao grupo de disponibilidade. Existem dois tipos de réplica de disponibilidade: uma única *réplica primária* e uma a quatro *réplicas secundárias*. As instâncias do servidor que hospedam as réplicas de disponibilidade de um determinado grupo de disponibilidade residem em nós diferentes de um único cluster do WSFC (Windows Server Failover Clustering).  
  
 [ponto de extremidade de espelhamento de banco de dados](../../../database-engine/database-mirroring/the-database-mirroring-endpoint-sql-server.md)  
 Um ponto de extremidade é um objeto do SQL Server que permite que o SQL Server se comunique pela rede. Para participar do espelhamento de banco de dados e/ou do [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] , uma instância de servidor requer um ponto de extremidade especial dedicado. Todas as conexões de espelhamento e de grupo de disponibilidade em uma instância de servidor usam o mesmo ponto de extremidade de espelhamento do banco de dados. Esse ponto de extremidade é um ponto de extremidade com finalidade especial usado exclusivamente para essas conexões de outras instâncias de servidor.  
  
##  <a name="to-configure-a-server-instance-to-support-always-on-availability-groups"></a><a name="ConfigSI"></a> Para configurar uma instância de servidor para dar suporte a grupos de disponibilidade AlwaysOn  
 Para oferecer suporte ao [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)], uma instância de servidor deve residir em um nó no cluster de failover do WSFC que hospeda o grupo de disponibilidade, estar habilitada pelo [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] e possuir um ponto de extremidade de espelhamento de banco de dados.  
  
1.  Habilite o recurso Grupos de Disponibilidade AlwaysOn em cada instância de servidor que deve participar de um ou mais grupos de disponibilidade. Uma determinada instância de servidor pode hospedar uma única réplica de disponibilidade para um determinado grupo de disponibilidade.  
  
2.  Verifique se a instância de servidor tem um ponto de extremidade de espelhamento de banco de dados.  
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> Tarefas relacionadas  
 **Para habilitar os Grupos de Disponibilidade AlwaysOn**  
  
-   [Habilitar e desabilitar Grupos de Disponibilidade AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/enable-and-disable-always-on-availability-groups-sql-server.md)  
  
 **Para determinar se um ponto de extremidade de espelhamento de banco de dados existe**  
  
-   [sys.database_mirroring_endpoints &#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-database-mirroring-endpoints-transact-sql.md)  
  
 **Para criar um ponto de extremidade de espelhamento de banco de dados**  
  
-   [Criar um ponto de extremidade de espelhamento de banco de dados para grupos de disponibilidade AlwaysOn &#40;SQL Server PowerShell&#41;](../../../database-engine/availability-groups/windows/database-mirroring-always-on-availability-groups-powershell.md)  
  
-   [Criar um ponto de extremidade de espelhamento de banco de dados para a Autenticação do Windows &#40;SQL Server&#41;](../../../database-engine/database-mirroring/create-a-database-mirroring-endpoint-for-windows-authentication-transact-sql.md)  
  
-   [Permitir que um ponto de extremidade de espelhamento de banco de dados use certificados para conexões de saída &#40;Transact-SQL&#41;](../../../database-engine/database-mirroring/database-mirroring-use-certificates-for-outbound-connections.md)  
  
##  <a name="related-content"></a><a name="RelatedContent"></a> Conteúdo relacionado  
  
-   **Blogs:**  
  
     [Série de aprendizado do AlwaysOn – HADRON: uso do pool de trabalho para bancos de dados habilitados para HADRON](/archive/blogs/psssql/alwayson-hadron-learning-series-worker-pool-usage-for-hadron-enabled-databases)  
  
     [Blogs da equipe do AlwaysOn do SQL Server: o blog oficial da equipe do AlwaysOn do SQL Server](/archive/blogs/sqlalwayson/)  
  
     [Blogs dos engenheiros do CSS SQL Server](/archive/blogs/psssql/)  
  
-   **Vídeos:**  
  
     [Microsoft SQL Server codinome “Denali” Série AlwaysOn, Parte 1: Introduzindo a próxima geração de solução de alta disponibilidade](https://channel9.msdn.com/Events/TechEd/NorthAmerica/2011/DBI302)  
  
     [Microsoft SQL Server codinome “Denali” Série AlwaysOn, Parte 2: Criando uma solução de alta disponibilidade de missão crítica usando AlwaysOn](https://channel9.msdn.com/Events/TechEd/NorthAmerica/2011/DBI404)  
  
-   **Whitepapers:**  
  
     [Guia de soluções AlwaysOn do Microsoft SQL Server para alta disponibilidade e recuperação de desastre](/previous-versions/sql/sql-server-2012/hh781257(v=msdn.10))  
  
     [White papers da Microsoft para SQL Server 2012](https://social.technet.microsoft.com/wiki/contents/articles/13146.white-paper-gallery-for-sql-server.aspx#[Category]SQLServer2012)  
  
     [White papers da equipe de consultoria do cliente do SQL Server](https://techcommunity.microsoft.com/t5/DataCAT/bg-p/DataCAT/)  
  
## <a name="see-also"></a>Consulte Também  
 [Visão geral dos grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Pré-requisitos, restrições e recomendações para grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md)   
 [O ponto de extremidade de espelhamento de banco de dados &#40;SQL Server&#41;](../../../database-engine/database-mirroring/the-database-mirroring-endpoint-sql-server.md)   
 [Grupos de Disponibilidade AlwaysOn: Interoperabilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/always-on-availability-groups-interoperability-sql-server.md)   
 [Clustering de failover e Grupos de Disponibilidade AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/failover-clustering-and-always-on-availability-groups-sql-server.md)   
 [WSFC &#40;Windows Server Failover Clustering&#41; com o SQL Server](../../../sql-server/failover-clusters/windows/windows-server-failover-clustering-wsfc-with-sql-server.md)   
 [Instâncias do cluster de failover AlwaysOn &#40;SQL Server&#41;](../../../sql-server/failover-clusters/windows/always-on-failover-cluster-instances-sql-server.md)  
  
