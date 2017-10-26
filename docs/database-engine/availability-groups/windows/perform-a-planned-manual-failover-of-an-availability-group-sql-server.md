---
title: Executar um failover manual planejado de um grupo de disponibilidade (SQL Server) | Microsoft Docs
ms.custom: 
ms.date: 05/17/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.availabilitygroup.manualfailover.f1
helpviewer_keywords:
- Availability Groups [SQL Server], failover
- failover [SQL Server], AlwaysOn Availability Groups
ms.assetid: 419f655d-3f9a-4e7d-90b9-f0bab47b3178
caps.latest.revision: 36
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.workload: On Demand
ms.translationtype: HT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 5017d65bb6324f7137c4b5a2a2e0e59b95829748
ms.contentlocale: pt-br
ms.lasthandoff: 08/02/2017

---
# <a name="perform-a-planned-manual-failover-of-an-availability-group-sql-server"></a>Executar um failover manual planejado de um grupo de disponibilidade (SQL Server)
  Este tópico descreve como fazer um failover manual sem perda de dados (um *failover manual planejado*) em um grupo de disponibilidade AlwaysOn usando [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../../includes/tsql-md.md)]ou o PowerShell no [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]. Um grupo de disponibilidade faz failover no nível de uma réplica de disponibilidade. Um failover manual planejado, como qualquer failover do [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] , faz a transição de uma réplica secundária e, simultaneamente, faz a transição da réplica primária antiga para a função secundária.  
  
 Um failover manual planejado, que é suportado apenas quando a réplica primária e a réplica secundária de destino estão executando em modo de confirmação síncrona e estão sincronizadas no momento, preserva todos os dados nos bancos de dados secundários que estão unidos ao grupo de disponibilidade em uma réplica secundária de destino. Quando a réplica primária antiga faz a transição para a função secundária, seus bancos de dados se tornam bancos de dados secundários e começam a ser sincronizados com os novos bancos de dados primários. Depois que a transição de todos é feita para o estado SYNCHRONIZED, a nova réplica secundária se torna qualificada para servir como o destino de uma futuro failover manual planejado.  
  
> [!NOTE]  
>  Se as réplicas secundárias e primárias estiverem configuradas para o modo de failover automático, quando a réplica secundária for sincronizada, ela também poderá servir como o destino de um failover automático. Para obter mais informações, consulte [Modos de disponibilidade &#40;Grupos de disponibilidade AlwaysOn&#41;](../../../database-engine/availability-groups/windows/availability-modes-always-on-availability-groups.md).  
  
-   **Antes de começar:**  
  
     [Limitações e restrições](#Restrictions)  
  
     [Pré-requisitos e restrições](#Prerequisites)  
  
     [Segurança](#Security)  
  
-   **Para fazer o failover de um grupo de disponibilidade manualmente usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [PowerShell](#PowerShellProcedure)  
  
-   **Acompanhamento:**  [depois do failover manual de um grupo de disponibilidade](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Restrictions"></a> Limitações e restrições  
  
-   Um comando de failover é retornado assim que a réplica secundária de destino aceitar o comando. No entanto, a recuperação de banco de dados ocorre de forma assíncrona depois que o grupo de disponibilidade terminar o failover.  
  
-   A consistência do banco de dados entre bancos de dados dentro do grupo de disponibilidade pode não ser mantida no failover.  
  
    > [!NOTE]  
    >  O suporte a transações distribuídas e bancos de dados varia de acordo com o SQL Server e versões do sistema operacional. Para obter mais informações, consulte [Transações entre bancos de dados e transações distribuídas para espelhamento de banco de dados e grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/transactions-always-on-availability-and-database-mirroring.md).  
  
###  <a name="Prerequisites"></a> Pré-requisitos e restrições  
  
-   A réplica secundária de destino e a réplica primária devem estar executando em modo de disponibilidade de confirmação síncrona.  
  
-   A réplica primária de destino deve estar sincronizada com a réplica primária. Isso requer que todos os bancos de dados secundários dessa réplica secundária ao grupo tenham sido unidos ao grupo de disponibilidade e tenham sido sincronizados com os bancos de dados primários correspondentes (quer dizer, os bancos de dados secundários locais devem estar SYNCHRONIZED).  
  
    > [!TIP]  
    >  Para determinar a prontidão do failover de uma réplica secundária, consulte a coluna **is_failover_ready** na exibição de gerenciamento dinâmico [sys.dm_hadr_database_cluster_states](../../../relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-cluster-states-transact-sql.md) ou consulte a coluna **Prontidão de Failover** do [Painel de Grupo AlwaysOn](../../../database-engine/availability-groups/windows/use-the-always-on-dashboard-sql-server-management-studio.md).  
  
-   Esta tarefa tem suporte apenas na réplica secundária de destino. Você deve estar conectado à instância de servidor que hospeda a réplica secundária de destino.  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Requer a permissão ALTER AVAILABILITY GROUP no grupo de disponibilidade, a permissão CONTROL AVAILABILITY GROUP, a permissão ALTER ANY AVAILABILITY GROUP ou a permissão CONTROL SERVER.  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
 **Para fazer o failover de um grupo de disponibilidade manualmente**  
  
1.  No Pesquisador de Objetos, conecte-se a uma instância do servidor que hospeda uma réplica secundária do grupo de disponibilidade que precise passar por failover e expanda a árvore de servidores.  
  
2.  Expanda os nós **Alta Disponibilidade AlwaysOn** e **Grupos de Disponibilidade** .  
  
3.  Clique com o botão direito do mouse no grupo de disponibilidade do qual fazer failover e selecione o comando **Failover** .  
  
4.  Isso inicia o Assistente de Grupo de Disponibilidade de Failover. Para obter mais informações, consulte [Usar o Assistente de Grupo de Disponibilidade de Failover &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-fail-over-availability-group-wizard-sql-server-management-studio.md).  
  
##  <a name="TsqlProcedure"></a> Usando Transact-SQL  
 **Para fazer o failover de um grupo de disponibilidade manualmente**  
  
1.  Conecte-se à instância do servidor que hospeda a réplica secundária de destino.  
  
2.  Use a instrução [ALTER AVAILABILITY GROUP](../../../t-sql/statements/alter-availability-group-transact-sql.md) , da seguinte maneira:  
  
     ALTER AVAILABILITY GROUP *group_name* FAILOVER  
  
     em que *group_name* é o nome do grupo de disponibilidade.  
  
     O exemplo a seguir faz o failover manual do grupo de disponibilidade *MyAg* para a réplica secundária conectada.  
  
    ```  
    ALTER AVAILABILITY GROUP MyAg FAILOVER;  
    ```  
  
##  <a name="PowerShellProcedure"></a> Usando o PowerShell  
 **Para fazer o failover de um grupo de disponibilidade manualmente**  
  
1.  Altere o diretório (**cd**) para a instância de servidor que hospeda a réplica secundária de destino.  
  
2.  Use o cmdlet **Switch-SqlAvailabilityGroup** .  
  
    > [!NOTE]  
    >  Para exibir a sintaxe de um cmdlet, use o cmdlet **Get-Help** no ambiente do [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] PowerShell. Para obter mais informações, consulte [Get Help SQL Server PowerShell](../../../relational-databases/scripting/get-help-sql-server-powershell.md).  
  
     O exemplo a seguir faz o failover manual do grupo de disponibilidade *MyAg* para a réplica secundária com o caminho especificado.  
  
    ```  
    Switch-SqlAvailabilityGroup -Path SQLSERVER:\Sql\SecondaryServer\InstanceName\AvailabilityGroups\MyAg  
    ```  
  
 **Para configurar e usar o provedor do SQL Server PowerShell**  
  
-   [Provedor do SQL Server PowerShell](../../../relational-databases/scripting/sql-server-powershell-provider.md)  
  
-   [Get Help SQL Server PowerShell](../../../relational-databases/scripting/get-help-sql-server-powershell.md)  
  
##  <a name="FollowUp"></a> Acompanhamento: após o failover manual de um grupo de disponibilidade  
 Se você fez failover fora do [!INCLUDE[ssFosAuto](../../../includes/ssfosauto-md.md)] do grupo de disponibilidade, ajuste os votos de quorum dos nós WSFC para refletir sua nova configuração de grupo de disponibilidade. Para obter mais informações, consulte [Clustering de Failover do Windows Server &#40;WSFC&#41; com SQL Server](../../../sql-server/failover-clusters/windows/windows-server-failover-clustering-wsfc-with-sql-server.md).  
  
## <a name="see-also"></a>Consulte também  
 [Visão geral dos grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Failover e modos de failover &#40;Grupos de Disponibilidade AlwaysOn&#41;](../../../database-engine/availability-groups/windows/failover-and-failover-modes-always-on-availability-groups.md)   
 [Executar um failover manual forçado de um grupo de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/perform-a-forced-manual-failover-of-an-availability-group-sql-server.md)  
  
  

