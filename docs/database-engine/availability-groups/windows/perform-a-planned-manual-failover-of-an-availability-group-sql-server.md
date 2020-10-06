---
title: Executar um failover manual planejado de um grupo de disponibilidade
description: Este tópico descreve como executar um failover manual planejado de um grupo de disponibilidade Always On.
ms.custom: seodec18
ms.date: 10/25/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql13.swb.availabilitygroup.manualfailover.f1
helpviewer_keywords:
- Availability Groups [SQL Server], failover
- failover [SQL Server], AlwaysOn Availability Groups
ms.assetid: 419f655d-3f9a-4e7d-90b9-f0bab47b3178
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 43b80003afbb83090aa7575aa038f6bebe7958a4
ms.sourcegitcommit: 2f868a77903c1f1c4cecf4ea1c181deee12d5b15
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2020
ms.locfileid: "91670893"
---
# <a name="perform-a-planned-manual-failover-of-an-always-on-availability-group-sql-server"></a>Executar um failover manual planejado de um grupo de disponibilidade Always On (SQL Server)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
Este tópico descreve como fazer um failover manual sem perda de dados (um *failover manual planejado*) em um grupo de disponibilidade AlwaysOn usando o[!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], o [!INCLUDE[tsql](../../../includes/tsql-md.md)] ou o PowerShell no [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]. Um grupo de disponibilidade faz failover no nível de uma réplica de disponibilidade. Um failover manual planejado, como qualquer failover de grupo de disponibilidade AlwaysOn, faz a transição de uma réplica secundária para a função primária. Paralelamente, o failover faz a transição da réplica primária antiga para a função secundária.  
  
Um failover manual planejado é compatível apenas quando a réplica primária e a réplica secundária de destino estão executando no modo de confirmação síncrona e estão sincronizadas no momento. Um failover manual planejado preserva todos os dados nos bancos de dados secundários unidos no grupo de disponibilidade, na réplica secundária de destino. Depois que a réplica primária antiga faz a transição para a função secundária, seus bancos de dados tornam-se bancos de dados secundários. Em seguida, eles começam a sincronizar com os novos bancos de dados primários. Depois que a transição de todos é feita para o estado SYNCHRONIZED, a nova réplica secundária se torna qualificada para servir como o destino de uma futuro failover manual planejado.  
  
> [!NOTE]  
>  Se as réplicas secundárias e primárias estiverem configuradas para o modo de failover automático, depois que a réplica secundária for sincronizada, ela também poderá servir como o destino de um failover automático. Para obter mais informações, veja [Modos de disponibilidade &#40;grupos de disponibilidade AlwaysOn&#41;](../../../database-engine/availability-groups/windows/availability-modes-always-on-availability-groups.md).  
   
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de começar 

>[!IMPORTANT]
>Existem procedimentos específicos para fazer failover de um grupo de disponibilidade de escala de leitura sem nenhum gerenciador de cluster. Quando um grupo de disponibilidade tiver CLUSTER_TYPE = NONE, siga os procedimentos em [Fazer failover da réplica primária em um grupo de disponibilidade de escala de leitura](#fail-over-the-primary-replica-on-a-read-scale-availability-group).

###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> Limitações e restrições 
  
- Um comando de failover é retornado assim que a réplica secundária de destino aceitar o comando. No entanto, a recuperação de banco de dados ocorre de forma assíncrona depois que o grupo de disponibilidade terminar o failover. 
- A consistência do banco de dados entre bancos de dados dentro do grupo de disponibilidade pode não ser mantida no failover. 
  
    > [!NOTE] 
    >  O suporte a transações distribuídas e bancos de dados varia de acordo com o SQL Server e versões do sistema operacional. Para obter mais informações, veja [Transações entre bancos de dados e transações distribuídas para espelhamento de banco de dados e de grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/transactions-always-on-availability-and-database-mirroring.md). 
  
###  <a name="prerequisites-and-restrictions"></a><a name="Prerequisites"></a> Pré-requisitos e restrições 
  
-   A réplica secundária de destino e a réplica primária devem estar executando em modo de disponibilidade de confirmação síncrona. 
-   Nesse momento, a réplica secundária de destino deve estar sincronizada com a réplica primária. Todos os bancos de dados secundários nessa réplica secundária devem estar unidos no grupo de disponibilidade. Eles também devem estar sincronizados com os bancos de dados primários correspondentes (isto é, os bancos de dados secundários locais devem ser SINCRONIZADOS). 
  
    > [!TIP] 
    >  Para determinar a prontidão do failover de uma réplica secundária, consulte a coluna **is_failover_ready** na exibição de gerenciamento dinâmico [sys.dm_hadr_database_replica_cluster_states](../../../relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-cluster-states-transact-sql.md). Como alternativa, você pode verificar a coluna **Prontidão de Failover** do [painel do grupo AlwaysOn](../../../database-engine/availability-groups/windows/use-the-always-on-dashboard-sql-server-management-studio.md). 
-   Esta tarefa tem suporte apenas na réplica secundária de destino. Você deve estar conectado à instância de servidor que hospeda a réplica secundária de destino. 
  
###  <a name="security"></a><a name="Security"></a> Segurança 
  
####  <a name="permissions"></a><a name="Permissions"></a> Permissões 
 A permissão ALTER AVAILABILITY GROUP é necessária no grupo de disponibilidade. A permissão CONTROL AVAILABILITY GROUP, ALTER ANY AVAILABILITY GROUP ou CONTROL SERVER também é necessária. 
  
##  <a name="use-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Usar o SQL Server Management Studio 
 Para fazer failover de um grupo de disponibilidade manualmente: 
  
1. No Pesquisador de Objetos, conecte-se a uma instância do servidor que hospeda uma réplica secundária do grupo de disponibilidade que precise ser submetido ao failover. Expanda a árvore de servidor. 
  
2. Expanda os nós **Alta Disponibilidade AlwaysOn** e **Grupos de Disponibilidade** . 
  
3. Clique com o botão direito do mouse no grupo de disponibilidade a ser submetido ao failover e selecione **Failover**. 
  
4. O assistente de Grupo de Disponibilidade de Failover é iniciado. Para obter mais informações, veja [Usar o assistente para Grupo de Disponibilidade de Failover &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-fail-over-availability-group-wizard-sql-server-management-studio.md). 
  
##  <a name="use-transact-sql"></a><a name="TsqlProcedure"></a> Usar o Transact-SQL 
 Para fazer failover de um grupo de disponibilidade manualmente: 
  
1. Conecte-se à instância do servidor que hospeda a réplica secundária de destino. 
  
2. Use a instrução [ALTER AVAILABILITY GROUP](../../../t-sql/statements/alter-availability-group-transact-sql.md) , da seguinte maneira: 
  
     ALTER AVAILABILITY GROUP *group_name* FAILOVER 
  
     Na instrução, *group_name* é o nome do grupo de disponibilidade. 
  
     O exemplo a seguir faz failover manual do grupo de disponibilidade *MyAg* para a réplica secundária conectada: 
  
    ```  
    ALTER AVAILABILITY GROUP MyAg FAILOVER;  
    ```  
  
##  <a name="use-powershell"></a><a name="PowerShellProcedure"></a> Usar o PowerShell 
 Para fazer failover de um grupo de disponibilidade manualmente: 
  
1. Altere o diretório (**cd**) para a instância do servidor que hospeda a réplica secundária de destino. 
  
2. Use o cmdlet **Switch-SqlAvailabilityGroup** . 
  
    > [!NOTE] 
    >  Para exibir a sintaxe de um cmdlet, use o cmdlet **Get-Help** no ambiente do [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] PowerShell. Para obter mais informações, veja [Obter ajuda do SQL Server PowerShell](../../../powershell/sql-server-powershell.md). 
  
     O exemplo a seguir faz failover manual do grupo de disponibilidade *MyAg* para a réplica secundária com o caminho especificado: 
  
    ```  
    Switch-SqlAvailabilityGroup -Path SQLSERVER:\Sql\SecondaryServer\InstanceName\AvailabilityGroups\MyAg  
    ```  
  
    Para configurar e usar o provedor do SQL Server PowerShell: 
  
    -   [Provedor do SQL Server PowerShell](../../../powershell/sql-server-powershell-provider.md) 
    -   [Obter ajuda do SQL Server PowerShell](../../../powershell/sql-server-powershell.md) 

##  <a name="follow-up-after-you-manually-fail-over-an-availability-group"></a><a name="FollowUp"></a> Acompanhamento: após fazer failover manual de um grupo de disponibilidade 
 Se você tiver feito failover fora do [!INCLUDE[ssFosAuto](../../../includes/ssfosauto-md.md)] do grupo de disponibilidade, ajuste os votos de quorum dos nós de clustering de failover do Windows Server para refletir a nova configuração do grupo de disponibilidade. Para obter mais informações, veja [WSFC &#40;Clustering de Failover do Windows Server &#41; com o SQL Server](../../../sql-server/failover-clusters/windows/windows-server-failover-clustering-wsfc-with-sql-server.md). 

<a name = "ReadScaleOutOnly"><a/>

## <a name="fail-over-the-primary-replica-on-a-read-scale-availability-group"></a>Fazer failover da réplica primária em um grupo de disponibilidade de escala de leitura

[!INCLUDE[Force failover](../../../includes/ss-force-failover-read-scale-out.md)]

## <a name="see-also"></a>Confira também 

 * [Visão geral de grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md) 
 * [Failover e modos de failover &#40;grupos de disponibilidade AlwaysOn&#41;](../../../database-engine/availability-groups/windows/failover-and-failover-modes-always-on-availability-groups.md) 
 * [Executar um failover manual forçado de um grupo de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/perform-a-forced-manual-failover-of-an-availability-group-sql-server.md) 
  
