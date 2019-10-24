---
title: Executar um failover manual planejado de um grupo de disponibilidade (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql12.swb.availabilitygroup.manualfailover.f1
helpviewer_keywords:
- Availability Groups [SQL Server], failover
- failover [SQL Server], AlwaysOn Availability Groups
ms.assetid: 419f655d-3f9a-4e7d-90b9-f0bab47b3178
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c81f5b22aa61dce596896ccd90bfb1d56054742d
ms.sourcegitcommit: a165052c789a327a3a7202872669ce039bd9e495
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/22/2019
ms.locfileid: "72782966"
---
# <a name="perform-a-planned-manual-failover-of-an-availability-group-sql-server"></a>Executar um failover manual planejado de um grupo de disponibilidade (SQL Server)
  Este tópico descreve como fazer um failover manual sem perda de dados (um *failover manual planejado*) em um grupo de disponibilidade AlwaysOn usando o[!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], o [!INCLUDE[tsql](../../../includes/tsql-md.md)] ou o PowerShell no [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]. Um grupo de disponibilidade faz failover no nível de uma réplica de disponibilidade. Um failover manual planejado, como qualquer failover do [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] , faz a transição de uma réplica secundária e, simultaneamente, faz a transição da réplica primária antiga para a função secundária.  
  
 Um failover manual planejado, que é suportado apenas quando a réplica primária e a réplica secundária de destino estão executando em modo de confirmação síncrona e estão sincronizadas no momento, preserva todos os dados nos bancos de dados secundários que estão unidos ao grupo de disponibilidade em uma réplica secundária de destino. Quando a réplica primária antiga faz a transição para a função secundária, seus bancos de dados se tornam bancos de dados secundários e começam a ser sincronizados com os novos bancos de dados primários. Depois que a transição de todos é feita para o estado SYNCHRONIZED, a nova réplica secundária se torna qualificada para servir como o destino de uma futuro failover manual planejado.  
  
> [!NOTE]  
>  Se as réplicas secundárias e primárias estiverem configuradas para o modo de failover automático, quando a réplica secundária for sincronizada, ela também poderá servir como o destino de um failover automático. Para obter mais informações, consulte [Modos de disponibilidade &#40;Grupos de Disponibilidade AlwaysOn&#41;](availability-modes-always-on-availability-groups.md).  
  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Restrictions"></a> Limitações e Restrições  
  
-   Um comando de failover é retornado assim que a réplica secundária de destino aceitar o comando. No entanto, a recuperação de banco de dados ocorre de forma assíncrona depois que o grupo de disponibilidade terminar o failover.  
  
-   A consistência do banco de dados entre bancos de dados dentro do grupo de disponibilidade não é mantida no failover.  
  
    > [!NOTE]  
    >  Não há suporte para transações entre bancos de dados e transações distribuídas no [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]. Para obter mais informações, consulte [Transações envolvendo todos os bancos de dados sem suporte para espelhamento de banco de dados ou Grupos de Disponibilidade AlwaysOn &#40;SQL Server&#41;](transactions-always-on-availability-and-database-mirroring.md).  
  
###  <a name="Prerequisites"></a> Pré-requisitos e restrições  
  
-   A réplica secundária de destino e a réplica primária devem estar executando em modo de disponibilidade de confirmação síncrona.  
  
-   A réplica primária de destino deve estar sincronizada com a réplica primária. Isso requer que todos os bancos de dados secundários dessa réplica secundária ao grupo tenham sido unidos ao grupo de disponibilidade e tenham sido sincronizados com os bancos de dados primários correspondentes (quer dizer, os bancos de dados secundários locais devem estar SYNCHRONIZED).  
  
    > [!TIP]  
    >  Para determinar a prontidão do failover de uma réplica secundária, consulte a coluna **is_failover_ready** na exibição de gerenciamento dinâmico [sys.dm_hadr_database_cluster_states](/sql/relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-cluster-states-transact-sql) ou consulte a coluna **Prontidão de Failover** do [Painel de Grupo AlwaysOn](use-the-always-on-dashboard-sql-server-management-studio.md).  
  
-   Esta tarefa tem suporte apenas na réplica secundária de destino. Você deve estar conectado à instância de servidor que hospeda a réplica secundária de destino.  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Requer a permissão ALTER AVAILABILITY GROUP no grupo de disponibilidade, a permissão CONTROL AVAILABILITY GROUP, a permissão ALTER ANY AVAILABILITY GROUP ou a permissão CONTROL SERVER.  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
 **Para fazer o failover de um grupo de disponibilidade manualmente**  
  
1.  No Pesquisador de Objetos, conecte-se a uma instância do servidor que hospeda uma réplica secundária do grupo de disponibilidade que precise passar por failover e expanda a árvore de servidores.  
  
2.  Expanda os nós **Alta Disponibilidade AlwaysOn** e **Grupos de Disponibilidade** .  
  
3.  Clique com o botão direito do mouse no grupo de disponibilidade do qual fazer failover e selecione o comando **Failover** .  
  
4.  Isso inicia o Assistente de Grupo de Disponibilidade de Failover. Para obter mais informações, consulte [Usar o Assistente de Grupo de Disponibilidade de Failover &#40;SQL Server Management Studio&#41;](use-the-fail-over-availability-group-wizard-sql-server-management-studio.md).  
  
##  <a name="TsqlProcedure"></a> Usando Transact-SQL  
 **Para fazer o failover de um grupo de disponibilidade manualmente**  
  
1.  Conecte-se à instância do servidor que hospeda a réplica secundária de destino.  
  
2.  Use a instrução [ALTER AVAILABILITY GROUP](/sql/t-sql/statements/alter-availability-group-transact-sql) , da seguinte maneira:  
  
     ALTER AVAILABILITY GROUP *group_name* FAILOVER  
  
     em que *group_name* é o nome do grupo de disponibilidade.  
  
     O exemplo a seguir faz o failover manual do grupo de disponibilidade *MyAg* para a réplica secundária conectada.  
  
    ```sql
    ALTER AVAILABILITY GROUP MyAg FAILOVER;  
    ```  
  
##  <a name="PowerShellProcedure"></a> Usando o PowerShell  
 **Para fazer o failover de um grupo de disponibilidade manualmente**  
  
1.  Altere o diretório (`cd`) para a instância do servidor que hospeda a réplica secundária de destino.  
  
2.  Use o cmdlet `Switch-SqlAvailabilityGroup`.  
  
    > [!NOTE]  
    >  Para exibir a sintaxe de um cmdlet, use o cmdlet `Get-Help` no ambiente do [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] PowerShell. Para obter mais informações, consulte [Get Help SQL Server PowerShell](../../../powershell/sql-server-powershell.md).  
  
     O exemplo a seguir faz o failover manual do grupo de disponibilidade *MyAg* para a réplica secundária com o caminho especificado.  
  
    ```powershell
    Switch-SqlAvailabilityGroup -Path SQLSERVER:\Sql\SecondaryServer\InstanceName\AvailabilityGroups\MyAg  
    ```  
  
 **Para configurar e usar o provedor do SQL Server PowerShell**  
  
-   [Provedor do SQL Server PowerShell](../../../powershell/sql-server-powershell-provider.md)  
  
-   [Obter Ajuda do SQL Server PowerShell](../../../powershell/sql-server-powershell.md)  
  
##  <a name="FollowUp"></a> Acompanhamento: após o failover manual de um grupo de disponibilidade  
 Se você fez failover fora do [!INCLUDE[ssFosAuto](../../../includes/ssfosauto-md.md)] do grupo de disponibilidade, ajuste os votos de quorum dos nós WSFC para refletir sua nova configuração de grupo de disponibilidade. Para obter mais informações, consulte [Clustering de Failover do Windows Server &#40;WSFC&#41; com SQL Server](../../../sql-server/failover-clusters/windows/windows-server-failover-clustering-wsfc-with-sql-server.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Visão geral do &#40;grupos de disponibilidade AlwaysOn&#41; SQL Server](overview-of-always-on-availability-groups-sql-server.md)    
 [Failover e modos &#40;de failover&#41; grupos de disponibilidade AlwaysOn](failover-and-failover-modes-always-on-availability-groups.md)    
 [Executar um failover manual forçado de um grupo de disponibilidade &#40;SQL Server&#41;](perform-a-forced-manual-failover-of-an-availability-group-sql-server.md)  
