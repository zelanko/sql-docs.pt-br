---
title: Remover uma réplica secundária de um grupo de disponibilidade (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql12.swb.availabilitygroup.removesecondaryar.f1
helpviewer_keywords:
- Availability Groups [SQL Server], availability replicas
- Availability Groups [SQL Server], configuring
ms.assetid: 35ddc8b6-3e7c-4417-9a0a-d4987a09ddf7
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: b927483f5e57272460f1c2f0f1c4b1bca56a3abe
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "72782943"
---
# <a name="remove-a-secondary-replica-from-an-availability-group-sql-server"></a>Remover uma réplica secundária de um grupo de disponibilidade (SQL Server)
  Este tópico descreve como remover uma réplica secundária de um grupo de disponibilidade AlwaysOn usando o [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], o [!INCLUDE[tsql](../../../includes/tsql-md.md)]ou o PowerShell no [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)].  
  
-   **Antes de começar:**  
  
     [Limitações e restrições](#Restrictions)  
  
     [Pré-requisitos](#Prerequisites)  
  
     [Segurança](#Security)  
  
-   **Para remover uma réplica secundária usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [PowerShell](#PowerShellProcedure)  
  
-   **Acompanhamento:**  [depois de remover uma réplica secundária](#PostBestPractices)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> Limitações e restrições  
  
-   Esta tarefa tem suporte apenas na réplica primária.  
  
-   Apenas uma réplica secundária pode ser removida de um grupo de disponibilidade.  
  
###  <a name="prerequisites"></a><a name="Prerequisites"></a> Pré-requisitos  
  
-   Conecte-se à instância do servidor que hospeda a réplica primária do grupo de disponibilidade.  
  
###  <a name="security"></a><a name="Security"></a> Segurança  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permissões  
 Requer a permissão ALTER AVAILABILITY GROUP no grupo de disponibilidade, a permissão CONTROL AVAILABILITY GROUP, a permissão ALTER ANY AVAILABILITY GROUP ou a permissão CONTROL SERVER.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
 **Para remover uma réplica secundária**  
  
1.  No Pesquisador de Objetos, conecte-se à instância de servidor que hospeda a réplica primária e expanda a árvore de servidores.  
  
2.  Expanda os nós **Alta Disponibilidade AlwaysOn** e **Grupos de Disponibilidade** .  
  
3.  Selecione o grupo de disponibilidade e expanda o nó **Réplicas de Disponibilidade** .  
  
4.  Essa etapa depende de se você deseja remover várias réplicas ou apenas uma réplica, da seguinte maneira:  
  
    -   Para remover várias réplicas, use o painel **Detalhes do Pesquisador de Objetos** para exibir e selecionar todas as réplicas que você deseja remover. Para obter mais informações, veja [Usar os detalhes do Pesquisador de Objetos para monitorar grupos de disponibilidade &#40;SQL Server Management Studio&#41;](use-object-explorer-details-to-monitor-availability-groups.md).  
  
    -   Para remover uma única réplica, selecione-a no painel **Pesquisador de Objetos** ou no painel **Detalhes do Pesquisador de Objetos** .  
  
5.  Clique com o botão direito do mouse na réplica ou réplicas secundárias selecionadas e selecione **Remover do Grupo de Disponibilidade** no menu de comando.  
  
6.  Na caixa de diálogo **Remover Réplicas Secundárias do Grupo de Disponibilidade** , para remover todas as réplicas secundárias listadas, clique em **OK**. Se você não desejar remover todas as réplicas listadas, clique em **Cancelar**.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Usando o Transact-SQL  
 **Para remover uma réplica secundária**  
  
1.  Conecte-se à instância de servidor que hospeda a réplica primária.  
  
2.  Use a instrução [ALTER AVAILABILITY GROUP](/sql/t-sql/statements/alter-availability-group-transact-sql) , da seguinte maneira:  
  
     ALTER AVAILABILITY GROUP *group_name* REMOVE REPLICA ON '*instance_name*' [,...*n*]  
  
     em que *group_name* é o nome do grupo de disponibilidade e *instance_name* é a instância do servidor no qual a réplica secundária está localizada.  
  
     O exemplo a seguir remove a réplica secundária do grupo de disponibilidade *MyAG* . A réplica secundária de destino está localizada em uma instância de servidor denominada *HADR_INSTANCE* em um computador denominado *COMPUTER02*.  
  
    ```sql
    ALTER AVAILABILITY GROUP MyAG REMOVE REPLICA ON 'COMPUTER02\HADR_INSTANCE';  
    ```  
  
##  <a name="using-powershell"></a><a name="PowerShellProcedure"></a> Usando o PowerShell  
 **Para remover uma réplica secundária**  
  
1.  Altere o diretório (`cd`) para a instância do servidor que hospeda a réplica primária.  
  
2.  Use o cmdlet **Remove-SqlAvailabilityReplica** .  
  
     Por exemplo, o comando a seguir remove a réplica de disponibilidade no servidor `MyReplica` do grupo de disponibilidade denominado `MyAg`.  Este comando deve ser executado na instância do servidor que hospeda a réplica primária do grupo de disponibilidade.  
  
    ```powershell
    Remove-SqlAvailabilityReplica -Path SQLSERVER:\SQL\PrimaryServer\InstanceName\AvailabilityGroups\MyAg\AvailabilityReplicas\MyReplica  
    ```  
  
    > [!NOTE]  
    >  Para exibir a sintaxe de um cmdlet, use o cmdlet `Get-Help` no ambiente do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] PowerShell. Para obter mais informações, consulte [Get Help SQL Server PowerShell](../../../powershell/sql-server-powershell.md).  
  
 **Para configurar e usar o provedor do SQL Server PowerShell**  
  
-   [Provedor do SQL Server PowerShell](../../../powershell/sql-server-powershell-provider.md)  
  
##  <a name="follow-up-after-removing-a-secondary-replica"></a><a name="PostBestPractices"></a> Acompanhamento: depois de remover uma réplica secundária  
 Se você especificar uma réplica que não esteja disponível atualmente, quando a réplica for colocada online, descobrirá que foi removida.  
  
 A remoção de uma réplica faz com que ela pare de receber dados. Depois que uma réplica secundária confirmar que foi removida do repositório global, a réplica removerá as configurações de grupo de disponibilidade de seus bancos de dados, que permanecem na instância do servidor local no estado RECOVERING.  
  
## <a name="see-also"></a>Consulte Também  
 [Visão geral do Grupos de Disponibilidade AlwaysOn &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [Adicionar uma réplica secundária a um grupo de disponibilidade &#40;SQL Server&#41;](add-a-secondary-replica-to-an-availability-group-sql-server.md)   
 [Remover um grupo de disponibilidade &#40;SQL Server&#41;](remove-an-availability-group-sql-server.md)  
