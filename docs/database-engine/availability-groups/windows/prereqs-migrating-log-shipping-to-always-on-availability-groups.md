---
title: Pré-requisitos da migração do envio de logs para Grupos de Disponibilidade AlwaysOn | Microsoft Docs
ms.custom: ''
ms.date: 05/17/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: availability-groups
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- log shipping [SQL Server], AlwaysOn Availability Groups
- Availability Groups [SQL Server], interoperability
ms.assetid: 2738ce65-205e-4682-92d8-dc7e37c58b2b
caps.latest.revision: 24
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8216dade1acbfeee2761d980d27e9c2e1ce488d3
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="prereqs-migrating-log-shipping-to-always-on-availability-groups"></a>Pré-requisitos da migração do envio de logs para Grupos de Disponibilidade AlwaysOn
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Esse tópico descreve os pré-requisitos para converter um banco de dados primário para envio de logs junto com um ou mais de seus bancos de dados secundários para um banco de dados primário AlwaysOn e bancos de dados secundários.  
  
> [!NOTE]  
>  Você pode configurar qualquer banco de dados primário ou secundário (possivelmente legível) em um grupo de disponibilidade como um banco de dados primário de envio de logs.  
  
 **Neste tópico:**  
  
-   [Pré-requisitos do grupo de disponibilidade](#AGPrereqsRealAddress)  
  
-   [Pré-requisitos para envio de logs](#LogShipPrereqs)  
  
-   [Tarefas relacionadas](#RelatedTasks)  
  
-   [Conteúdo relacionado](#RelatedContent)  
  
##  <a name="AGPrereqsRealAddress"></a> Pré-requisitos do grupo de disponibilidade  
 Para permitir que trabalhos de backup sejam executados na réplica primária do grupo de disponibilidade, use as seguintes configurações de backup dos Grupos de Disponibilidade AlwaysOn:  
  
|Propriedade|Configuração|  
|--------------|-------------|  
|A preferência de backup automatizada do grupo de disponibilidade|Apenas na réplica primária|  
|Prioridade de backup da réplica primária.|>0|  
  
 **Para obter mais informações, consulte:**  
  
 [Exibir as propriedades do grupo de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/view-availability-group-properties-sql-server.md)  
  
 [Configurar backup em réplicas de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/configure-backup-on-availability-replicas-sql-server.md)  
  
##  <a name="LogShipPrereqs"></a> Pré-requisitos para envio de logs  
  
-   O banco de dados primário para envio de logs deve residir na instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que hospeda a réplica primária inicial/atual do grupo de disponibilidade.  
  
-   Para determinado banco de dados secundário para envio de log ser convertido em um banco de dados secundário AlwaysOn, ele deverá:  
  
    -   Usar o mesmo nome que o banco de dados primário.  
  
    -   Residir em uma instância de servidor que hospeda uma réplica secundária para o grupo de disponibilidade.  
  
 Quando o trabalho de backup estiver sendo executado no banco de dados primário, desabilite o trabalho de backup e, assim que o trabalho de restauração tiver sido executado em um determinado banco de dados secundário, desabilite o trabalho de restauração.  
  
 Depois que você criar todos os bancos de dados secundários para o grupo de disponibilidade, se você desejar executar backups em réplicas secundárias, precisará reconfigurar a preferência de backup automatizada do grupo de disponibilidade.  
  
 **Para obter mais informações, consulte:**  
  
 [Convertendo uma configuração para envio de logs para Grupo de Disponibilidade](https://blogs.msdn.microsoft.com/sqlalwayson/2012/01/09/converting-a-logshipping-configuration-to-availability-group/) (um blog do SQL Server)  
  
##  <a name="RelatedTasks"></a> Tarefas relacionadas  
 **Envio de logs**  
  
-   [Atualizando o envio de logs para o SQL Server 2016 &#40;Transact-SQL&#41;](../../../database-engine/log-shipping/upgrading-log-shipping-to-sql-server-2016-transact-sql.md)  
  
-   [Remover envio de log &#40;SQL Server&#41;](../../../database-engine/log-shipping/remove-log-shipping-sql-server.md)  
  
 **Grupos de Disponibilidade AlwaysOn**  
  
-   [Usar o Assistente de Grupo de Disponibilidade &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-availability-group-wizard-sql-server-management-studio.md)  
  
-   [Usar a caixa de diálogo Novo Grupo de Disponibilidade &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-new-availability-group-dialog-box-sql-server-management-studio.md)  
  
-   [Criar um grupo de disponibilidade &#40;Transact-SQL&#41;](../../../database-engine/availability-groups/windows/create-an-availability-group-transact-sql.md)  
  
-   [Criar um grupo de disponibilidade &#40;SQL Server PowerShell&#41;](../../../database-engine/availability-groups/windows/create-an-availability-group-sql-server-powershell.md)  
  
-   [Unir um banco de dados secundário a um grupo de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/join-a-secondary-database-to-an-availability-group-sql-server.md)  
  
-   [Configurar backup em réplicas de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/configure-backup-on-availability-replicas-sql-server.md)  
  
##  <a name="RelatedContent"></a> Conteúdo relacionado  
  
-   **Blogs:**  
  
     [Convertendo uma configuração para envio de logs para Grupo de Disponibilidade](https://blogs.msdn.microsoft.com/sqlalwayson/2012/01/09/converting-a-logshipping-configuration-to-availability-group/)  
  
     [Adicione um banco de dados primário de envio de logs e bancos de dados secundários a um grupo de disponibilidade existente](https://blogs.msdn.microsoft.com/sqlalwayson/2012/02/01/add-a-log-shipping-primary-database-and-secondary-databases-to-an-existing-availability-group/)  
  
     [Blogs da equipe do AlwaysOn do SQL Server: o blog oficial da equipe do AlwaysOn do SQL Server](https://blogs.msdn.microsoft.com/sqlalwayson/)  
  
     [Blogs dos engenheiros do CSS SQL Server](http://blogs.msdn.com/b/psssql/)  
  
-   **Whitepapers:**  
  
     [Guia de migração: Migrando para grupos de disponibilidade AlwaysOn de implantações anteriores que combinam espelhamento de banco de dados e envio de logs](http://msdn.microsoft.com/library/jj635217)  
  
     [White papers da Microsoft para SQL Server 2012](http://msdn.microsoft.com/library/hh403491.aspx)  
  
     [White papers da equipe de consultoria do cliente do SQL Server](http://sqlcat.com/)  
  
## <a name="see-also"></a>Consulte Também  
 [Sobre o envio de logs &#40;SQL Server&#41;](../../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [Visão geral dos grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Monitoramento de grupos de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/monitoring-of-availability-groups-sql-server.md)  
  
  
