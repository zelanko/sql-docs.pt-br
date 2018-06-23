---
title: Criação e configuração de grupos de disponibilidade (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Availability Groups [SQL Server], deploying
- Availability Groups [SQL Server], configuring
- Availability Groups [SQL Server], creating
ms.assetid: 7f89fab8-6ee2-4273-9de0-e594bfb9407f
caps.latest.revision: 27
author: rothja
ms.author: jroth
manager: jhubbard
ms.openlocfilehash: e7d93c8a1b85d663c5c1590b76c4bf98f5050b3c
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36116662"
---
# <a name="creation-and-configuration-of-availability-groups-sql-server"></a>Criação e configuração de grupos de disponibilidade (SQL Server)
  Os tópicos desta seção explicam como implantar uma implementação do [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] em instâncias do [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] que residem nos diferentes nós WSFC (Windows Server Failover Clustering) em um único cluster de failover WSFC.  
  
 Antes de criar seu primeiro grupo de disponibilidade, é altamente recomendável que você se familiarize com as informações nos seguintes tópicos:  
  
 [Pré-requisitos, restrições e recomendações para grupos de disponibilidade do AlwaysOn &#40;do SQL Server&#41;](prereqs-restrictions-recommendations-always-on-availability.md)  
 Este tópico descreve os pré-requisitos, as restrições e recomendações para computadores; nós WSFC; instâncias do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]; grupos de disponibilidade, réplicas e bancos de dados. Este tópico também contém informações sobre considerações de segurança.  
  
 [Introdução aos grupos de disponibilidade do AlwaysOn &#40;do SQL Server&#41;](getting-started-with-always-on-availability-groups-sql-server.md)  
 Contém informações sobre as etapas de configuração de uma instância de servidor, criação de um grupo de disponibilidade, configuração do grupo de disponibilidade para conexões de cliente, gerenciamento de grupos de disponibilidade e monitoramento de grupos de disponibilidade.  
  
 
  
##  <a name="RelatedTasks"></a> Tarefas relacionadas  
 **Para configurar uma instância de servidor para [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]**  
  
-   [Habilitar e desabilitar grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](enable-and-disable-always-on-availability-groups-sql-server.md)  
  
-   [Criar um banco de dados do ponto de extremidade de espelhamento para grupos de disponibilidade do AlwaysOn &#40;do SQL Server PowerShell&#41;](database-mirroring-always-on-availability-groups-powershell.md)  
  
-   [Criar um ponto de extremidade de espelhamento de banco de dados para a Autenticação do Windows &#40;SQL Server&#41;](../../database-mirroring/create-a-database-mirroring-endpoint-for-windows-authentication-transact-sql.md)  
  
-   [Permitir que um ponto de extremidade de espelhamento de banco de dados use certificados para conexões de saída &#40;Transact-SQL&#41;](../../database-mirroring/database-mirroring-use-certificates-for-outbound-connections.md)  
  
 **Para começar a configurar grupos de disponibilidade AlwaysOn**  
  
-   [Introdução aos grupos de disponibilidade do AlwaysOn &#40;do SQL Server&#41;](getting-started-with-always-on-availability-groups-sql-server.md)  
  
 **Para criar e configurar um novo grupo de disponibilidade**  
  
-   [Usar o Assistente de Grupo de Disponibilidade &#40;SQL Server Management Studio&#41;](use-the-availability-group-wizard-sql-server-management-studio.md)  
  
-   [Criar um grupo de disponibilidade &#40;Transact-SQL&#41;](create-an-availability-group-transact-sql.md)  
  
-   [Criar um grupo de disponibilidade &#40;SQL Server PowerShell&#41;](../../../powershell/sql-server-powershell.md)  
  
-   [Usar a caixa de diálogo Novo Grupo de Disponibilidade &#40;SQL Server Management Studio&#41;](use-the-new-availability-group-dialog-box-sql-server-management-studio.md)  
  
-   [Especificar a URL do ponto de extremidade ao adicionar ou modificar uma réplica de disponibilidade &#40;SQL Server&#41;](specify-endpoint-url-adding-or-modifying-availability-replica.md)  
  
-   [Criar ou configurar um ouvinte do grupo de disponibilidade &#40;SQL Server&#41;](create-or-configure-an-availability-group-listener-sql-server.md)  
  
-   [Configurar a política de Failover flexível para controlar condições de Failover automático (grupos de disponibilidade AlwaysOn)](configure-flexible-automatic-failover-policy.md)  
  
-   [Configurar backup em réplicas de disponibilidade &#40;SQL Server&#41;](configure-backup-on-availability-replicas-sql-server.md)  
  
-   [Configurar o acesso somente leitura em uma réplica de disponibilidade &#40;SQL Server&#41;](configure-read-only-access-on-an-availability-replica-sql-server.md)  
  
-   [Configurar o roteamento somente leitura para um grupo de disponibilidade &#40;SQL Server&#41;](configure-read-only-routing-for-an-availability-group-sql-server.md)  
  
-   [Unir uma réplica secundária a um grupo de disponibilidade &#40;SQL Server&#41;](join-a-secondary-replica-to-an-availability-group-sql-server.md)  
  
-   [Iniciar movimentação de dados em um banco de dados secundário AlwaysOn &#40;do SQL Server&#41;](start-data-movement-on-an-always-on-secondary-database-sql-server.md)  
  
-   [Preparar um banco de dados secundário manualmente para um grupo de disponibilidade &#40;SQL Server&#41;](manually-prepare-a-secondary-database-for-an-availability-group-sql-server.md)  
  
-   [Unir um banco de dados secundário a um grupo de disponibilidade &#40;SQL Server&#41;](join-a-secondary-database-to-an-availability-group-sql-server.md)  
  
-   [Gerenciamento de logons e trabalhos para os bancos de dados de um grupo de disponibilidade &#40;SQL Server&#41;](../../logins-and-jobs-for-availability-group-databases.md)  
  
 **Para solucionar problemas**  
  
-   [Solucionar problemas de grupos de configuração de disponibilidade AlwaysOn (SQL Server) excluído](troubleshoot-always-on-availability-groups-configuration-sql-server.md)  
  
-   [Solucionar problemas de uma falha na operação adicionar arquivo &#40;grupos de disponibilidade AlwaysOn&#41;](troubleshoot-a-failed-add-file-operation-always-on-availability-groups.md)  
  
##  <a name="RelatedContent"></a> Conteúdo relacionado  
  
-   **Blogs:**  
  
     [Aprendizado do AlwaysON - HADRON série: Bancos de dados habilitados do uso do Pool de trabalho para HADRON](http://blogs.msdn.com/b/psssql/archive/2012/05/17/alwayson-hadron-learning-series-worker-pool-usage-for-hadron-enabled-databases.aspx)  
  
     [Blogs da equipe do AlwaysOn do SQL Server: O SQL Server AlwaysOn Team Blog oficial](http://blogs.msdn.com/b/sqlalwayson/)  
  
     [Blogs dos engenheiros do CSS SQL Server](http://blogs.msdn.com/b/psssql/)  
  
-   **Vídeos:**  
  
     [Microsoft SQL Server codinome "Denali" série de AlwaysOn, parte 1: Introduzindo a próxima geração de solução de alta disponibilidade](http://channel9.msdn.com/Events/TechEd/NorthAmerica/2011/DBI302)  
  
     [Microsoft SQL Server codinome "Denali" série de AlwaysOn, parte 2: Criando uma solução de alta disponibilidade de missão crítica usando AlwaysOn](http://channel9.msdn.com/Events/TechEd/NorthAmerica/2011/DBI404)  
  
-   **Whitepapers:**  
  
     [Guia de soluções do Microsoft SQL Server AlwaysOn para alta disponibilidade e recuperação de desastres](http://go.microsoft.com/fwlink/?LinkId=227600)  
  
     [White papers da Microsoft para SQL Server 2012](http://msdn.microsoft.com/library/hh403491.aspx)  
  
     [White papers da equipe de consultoria do cliente do SQL Server](http://sqlcat.com/)  
  
## <a name="see-also"></a>Consulte também  
 [Visão geral dos grupos de disponibilidade do AlwaysOn &#40;do SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [Administração de um grupo de disponibilidade &#40;SQL Server&#41;](administration-of-an-availability-group-sql-server.md)   
 [Políticas AlwaysOn para problemas operacionais com grupos de disponibilidade do AlwaysOn (SQL Server)](always-on-policies-for-operational-issues-always-on-availability.md)   
 [Monitoramento de grupos de disponibilidade &#40;SQL Server&#41;](monitoring-of-availability-groups-sql-server.md)   
 [Grupos de disponibilidade do AlwaysOn: Interoperabilidade (SQL Server)](always-on-availability-groups-interoperability-sql-server.md)  
  
  