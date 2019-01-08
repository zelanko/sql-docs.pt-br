---
title: Pré-requisitos para migrar de envio de logs para grupos de disponibilidade AlwaysOn (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- log shipping [SQL Server], AlwaysOn Availability Groups
- Availability Groups [SQL Server], interoperability
ms.assetid: 2738ce65-205e-4682-92d8-dc7e37c58b2b
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 865e8d720e9977f582ac5ae8a0e75d995fc82629
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/13/2018
ms.locfileid: "53364388"
---
# <a name="prerequisites-for-migrating-from-log-shipping-to-alwayson-availability-groups-sql-server"></a>Pré-requisitos para migrar de envio de logs para grupos de disponibilidade AlwaysOn (SQL Server)
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
  
 [Exibir as propriedades do grupo de disponibilidade &#40;SQL Server&#41;](view-availability-group-properties-sql-server.md)  
  
 [Configurar backup em réplicas de disponibilidade &#40;SQL Server&#41;](configure-backup-on-availability-replicas-sql-server.md)  
  
##  <a name="LogShipPrereqs"></a> Pré-requisitos para envio de logs  
  
-   O banco de dados primário para envio de logs deve residir na instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que hospeda a réplica primária inicial/atual do grupo de disponibilidade.  
  
-   Para um determinado banco de dados secundário para envio de log ser convertido em um banco de dados secundário AlwaysOn, ele deverá:  
  
    -   Usar o mesmo nome que o banco de dados primário.  
  
    -   Residir em uma instância de servidor que hospeda uma réplica secundária para o grupo de disponibilidade.  
  
 Quando o trabalho de backup estiver sendo executado no banco de dados primário, desabilite o trabalho de backup e, assim que o trabalho de restauração tiver sido executado em um determinado banco de dados secundário, desabilite o trabalho de restauração.  
  
 Depois que você criar todos os bancos de dados secundários para o grupo de disponibilidade, se você desejar executar backups em réplicas secundárias, precisará reconfigurar a preferência de backup automatizada do grupo de disponibilidade.  
  
 **Para obter mais informações, consulte:**  
  
 [Convertendo uma configuração para envio de logs para Grupo de Disponibilidade](https://blogs.msdn.com/b/sqlalwayson/archive/2012/01/09/converting-a-logshipping-configuration-to-availability-group.aspx) (um blog do SQL Server)  
  
##  <a name="RelatedTasks"></a> Tarefas relacionadas  
 **Envio de logs**  
  
-   [Atualizar o envio de logs para o SQL Server 2014 &#40;Transact-SQL&#41;](../../log-shipping/upgrading-log-shipping-to-sql-server-2016-transact-sql.md)  
  
-   [Remover envio de log &#40;SQL Server&#41;](../../log-shipping/remove-log-shipping-sql-server.md)  
  
 **Grupos de disponibilidade AlwaysOn**  
  
-   [Usar o Assistente de Grupo de Disponibilidade &#40;SQL Server Management Studio&#41;](use-the-availability-group-wizard-sql-server-management-studio.md)  
  
-   [Usar a caixa de diálogo Novo Grupo de Disponibilidade &#40;SQL Server Management Studio&#41;](use-the-new-availability-group-dialog-box-sql-server-management-studio.md)  
  
-   [Criar um grupo de disponibilidade &#40;Transact-SQL&#41;](create-an-availability-group-transact-sql.md)  
  
-   [Criar um grupo de disponibilidade &#40;SQL Server PowerShell&#41;](../../../powershell/sql-server-powershell.md)  
  
-   [Unir um banco de dados secundário a um grupo de disponibilidade &#40;SQL Server&#41;](join-a-secondary-database-to-an-availability-group-sql-server.md)  
  
-   [Configurar backup em réplicas de disponibilidade &#40;SQL Server&#41;](configure-backup-on-availability-replicas-sql-server.md)  
  
##  <a name="RelatedContent"></a> Conteúdo relacionado  
  
-   **Blogs:**  
  
     [Convertendo uma configuração para envio de logs para Grupo de Disponibilidade](https://blogs.msdn.com/b/sqlalwayson/archive/2012/01/09/converting-a-logshipping-configuration-to-availability-group.aspx)  
  
     [Adicione um banco de dados primário de envio de logs e bancos de dados secundários a um grupo de disponibilidade existente](https://blogs.msdn.com/b/sqlalwayson/archive/2012/02/01/use-log-shipping-to-prepare-secondary-databases-for-an-existing-availability-group.aspx)  
  
     [Blogs da equipe do AlwaysOn do SQL Server: O Team Blog oficial do SQL Server AlwaysOn](https://blogs.msdn.com/b/sqlalwayson/)  
  
     [Blogs dos engenheiros do CSS SQL Server](https://blogs.msdn.com/b/psssql/)  
  
-   **Whitepapers:**  
  
     [Guia de migração: Migrando para grupos de disponibilidade AlwaysOn de implantações anteriores que combinam espelhamento de banco de dados e envio de logs](https://msdn.microsoft.com/library/jj635217)  
  
     [White papers da Microsoft para SQL Server 2012](https://msdn.microsoft.com/library/hh403491.aspx)  
  
     [White papers da equipe de consultoria do cliente do SQL Server](http://sqlcat.com/)  
  
## <a name="see-also"></a>Consulte também  
 [Sobre o envio de logs &#40;SQL Server&#41;](../../log-shipping/about-log-shipping-sql-server.md)   
 [Visão geral dos grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [Monitoramento de grupos de disponibilidade &#40;SQL Server&#41;](monitoring-of-availability-groups-sql-server.md)  
  
  
