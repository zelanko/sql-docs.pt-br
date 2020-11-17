---
title: Unir uma réplica secundária a um grupo de disponibilidade
description: Etapas para o ingresso de uma réplica secundária em um grupo de disponibilidade Always On usando o T-SQL (Transact-SQL), o PowerShell ou o SQL Server Management Studio.
ms.custom: seodec18
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: how-to
f1_keywords:
- sql13.swb.availabilitygroup.joinreplica.f1
helpviewer_keywords:
- Availability Groups [SQL Server], availability replicas
- Availability Groups [SQL Server], joining
- Availability Groups [SQL Server], configuring
ms.assetid: e5bd2489-097a-490e-8ea1-34fe48378ad1
author: cawrites
ms.author: chadam
ms.openlocfilehash: aa4ef43cd9c33fbbea2bc2bd3333ca85927d8ed5
ms.sourcegitcommit: 54cd97a33f417432aa26b948b3fc4b71a5e9162b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/13/2020
ms.locfileid: "94584199"
---
# <a name="join-a-secondary-replica-to-an-always-on-availability-group"></a>Ingressar uma réplica secundária em um grupo de disponibilidade Always On
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  Este tópico descreve como unir uma réplica secundária a um grupo de disponibilidade AlwaysOn usando o [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], o [!INCLUDE[tsql](../../../includes/tsql-md.md)]ou o PowerShell no [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]. Depois que uma réplica secundária é adicionada a um grupo de disponibilidade AlwaysOn, a réplica secundária deve ser unida ao grupo de disponibilidade. A operação para unir réplica deve ser executada na instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que está hospedando a réplica secundária.  

  
##  <a name="prerequisites"></a><a name="Prerequisites"></a> Pré-requisitos  
  
-   A réplica primária do grupo de disponibilidade deve estar online no momento.    
-   Você deve estar conectado à instância de servidor que hospeda uma réplica secundária que ainda não foi unida ao grupo de disponibilidade.    
-   A instância de servidor local deve ser capaz de se conectar ao ponto de extremidade de espelhamento de banco de dados da instância de servidor que está hospedando a réplica primária.  
  
> [!IMPORTANT]  
>  Se qualquer pré-requisito não for atendido, a operação de junção falhará. Após uma tentativa de junção com falha, talvez seja necessário conectar a instância do servidor que hospeda a réplica primária para remover e adicionar novamente a réplica secundária antes que seja possível uni-la ao grupo de disponibilidade. Para obter mais informações, veja [Remover uma réplica secundária de um grupo de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/remove-a-secondary-replica-from-an-availability-group-sql-server.md) e [Adicionar uma réplica secundária a um grupo de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/add-a-secondary-replica-to-an-availability-group-sql-server.md).  
  
##  <a name="permissions"></a><a name="Permissions"></a> Permissões  
 Requer a permissão ALTER AVAILABILITY GROUP no grupo de disponibilidade, a permissão CONTROL AVAILABILITY GROUP, a permissão ALTER ANY AVAILABILITY GROUP ou a permissão CONTROL SERVER.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
 **Para unir uma réplica de disponibilidade a um grupo de disponibilidade**  
  
1.  No Pesquisador de Objetos, conecte-se à instância do servidor que hospeda a réplica secundária e clique no nome do servidor para expandir a árvore de servidores.  
  
2.  Expanda os nós **Alta Disponibilidade AlwaysOn** e **Grupos de Disponibilidade**.  
  
3.  Selecione o grupo de disponibilidade da réplica secundária à qual você está conectado.  
  
4.  Clique com o botão direito do mouse na réplica secundária e clique em **Unir a Grupo de Disponibilidade**.  
  
5.  Isso abre a caixa de diálogo **Unir Réplica a Grupo de Disponibilidade** .  
  
6.  Para unir a réplica secundária ao grupo de disponibilidade, clique em **OK**.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Usando o Transact-SQL  
 **Para unir uma réplica de disponibilidade a um grupo de disponibilidade**  
  
1.  Conecte-se à instância de servidor que hospeda a réplica secundária.  
  
2.  Use a instrução [ALTER AVAILABILITY GROUP](../../../t-sql/statements/alter-availability-group-transact-sql.md) , da seguinte maneira:  
  
     ALTER AVAILABILITY GROUP *group_name* JOIN  
  
     em que *group_name* é o nome do grupo de disponibilidade.  
  
     O exemplo a seguir une a réplica secundária ao grupo de disponibilidade `MyAG`.  
  
    ```  
    ALTER AVAILABILITY GROUP MyAG JOIN;  
    ```  
  
    > [!NOTE]  
    >  Para ver esta instrução [!INCLUDE[tsql](../../../includes/tsql-md.md)] usada no contexto, veja [Criar um grupo de disponibilidade &#40;Transact-SQL&#41;](../../../database-engine/availability-groups/windows/create-an-availability-group-transact-sql.md).  
  
##  <a name="using-powershell"></a><a name="PowerShellProcedure"></a> Usando o PowerShell  
 **Para unir uma réplica de disponibilidade a um grupo de disponibilidade**  
  
 No provedor do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] PowerShell:  
  
1.  Altere o diretório (**cd**) para a instância de servidor que hospeda a réplica secundária.  
  
2.  Una a réplica secundária ao grupo de disponibilidade executando o cmdlet **Join-SqlAvailabilityGroup** com o nome do grupo de disponibilidade.  
  
     Por exemplo, o comando a seguir une a réplica secundária hospedada pela instância de servidor localizada no caminho especificado ao grupo de disponibilidade denominado `MyAg`.  Essa instância de servidor deve hospedar uma réplica secundária neste grupo de disponibilidade.  
  
    ```  
    Join-SqlAvailabilityGroup -Path SQLSERVER:\SQL\SecondaryServer\InstanceName -Name 'MyAg'  
    ```  
  
    > [!NOTE]  
    >  Para exibir a sintaxe de um cmdlet, use o cmdlet **Get-Help** no ambiente do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] PowerShell. Para obter mais informações, consulte [Get Help SQL Server PowerShell](../../../powershell/sql-server-powershell.md).  
  
 **Para configurar e usar o provedor do SQL Server PowerShell**  
  
-   [Provedor do SQL Server PowerShell](../../../powershell/sql-server-powershell-provider.md)  
  
##  <a name="follow-up-configure-secondary-databases"></a><a name="FollowUp"></a> Acompanhamento: Configurar bancos de dados secundários  
 Para cada banco de dados do grupo de disponibilidade, você precisa de um banco de dados secundário na instância de servidor que está hospedando a réplica secundária. Você pode configurar bancos de dados secundários antes ou depois que une uma réplica secundária a um grupo de disponibilidade, da seguinte maneira  
  
1.  Restaure o banco de dados e os backups de log recentes de cada banco de dados primário na instância de servidor que hospeda a réplica secundária, usando RESTORE WITH NORECOVERY em cada operação de restauração. Para obter mais informações, consulte [Preparar um banco de dados secundário manualmente para um grupo de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/manually-prepare-a-secondary-database-for-an-availability-group-sql-server.md).  
  
2.  Una cada banco de dados secundário ao grupo de disponibilidade. Para obter mais informações, consulte [Unir um banco de dados secundário a um grupo de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/join-a-secondary-database-to-an-availability-group-sql-server.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Criação e configuração de grupos de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/creation-and-configuration-of-availability-groups-sql-server.md)   
 [Visão geral dos grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Solucionar problemas de configuração de grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/troubleshoot-always-on-availability-groups-configuration-sql-server.md)  
  
