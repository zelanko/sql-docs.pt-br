---
title: Adicionar uma réplica secundária a um grupo de disponibilidade (SQL Server) | Microsoft Docs
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
- Availability Groups [SQL Server], availability replicas
- Availability Groups [SQL Server], configuring
ms.assetid: 6669dcce-85f9-495f-aadf-7f62cff4a9da
caps.latest.revision: 36
author: rothja
ms.author: jroth
manager: jhubbard
ms.openlocfilehash: 4232462d49268b8abab26444adb41d240f62d77a
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36008715"
---
# <a name="add-a-secondary-replica-to-an-availability-group-sql-server"></a>Adicionar uma réplica secundária a um grupo de disponibilidade (SQL Server)
  Este tópico descreve como adicionar uma réplica secundária a um grupo de disponibilidade AlwaysOn existente usando o [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], o [!INCLUDE[tsql](../../../includes/tsql-md.md)]ou o PowerShell no [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)].  
  
-   **Antes de começar:**  
  
     [Pré-requisitos e restrições](#PrerequisitesRestrictions)  
  
     [Segurança](#Security)  
  
-   **Para adicionar uma réplica usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [PowerShell](#PowerShellProcedure)  
  
-   **Acompanhamento:**  [depois de adicionar uma réplica secundária](#FollowUp)  
  
## <a name="before-you-begin"></a>Antes de começar  
 É recomendável que você leia esta seção antes de tentar criar seu primeiro grupo de disponibilidade.  
  
##  <a name="PrerequisitesRestrictions"></a> Pré-requisitos e restrições  
  
-   Você deve estar conectado à instância do servidor que hospeda a réplica primária.  
  
 Para obter mais informações, consulte [Pré-requisitos, restrições e recomendações para grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](prereqs-restrictions-recommendations-always-on-availability.md).  
  
##  <a name="Security"></a> Segurança  
  
###  <a name="Permissions"></a> Permissões  
 Requer a permissão ALTER AVAILABILITY GROUP no grupo de disponibilidade, a permissão CONTROL AVAILABILITY GROUP, a permissão ALTER ANY AVAILABILITY GROUP ou a permissão CONTROL SERVER.  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
 **Para adicionar uma réplica**  
  
1.  No Pesquisador de Objetos, conecte-se à instância de servidor que hospeda a réplica primária e expanda a árvore de servidores.  
  
2.  Expanda os nós **Alta Disponibilidade AlwaysOn** e **Grupos de Disponibilidade** .  
  
3.  Clique com o botão direito do mouse no grupo de disponibilidade e selecione um dos comandos a seguir:  
  
    -   Para iniciar o Assistente para Adicionar Réplica ao Grupo de Disponibilidade, selecione o comando **Adicionar Réplica** . Para obter mais informações, veja [Usar o Assistente para Adicionar Réplica ao Grupo de Disponibilidade &#40;SQL Server Management Studio&#41;](use-the-add-replica-to-availability-group-wizard-sql-server-management-studio.md).  
  
    -   Opcionalmente, selecione o comando **Propriedades** para abrir a caixa de diálogo **Propriedades do Grupo de Disponibilidade** . As etapas para adicionar uma réplica nesta caixa de diálogo são:  
  
        1.  No painel **Réplicas de Disponibilidade** da caixa de diálogo, clique no botão **Adicionar** . Isso cria e seleciona uma entrada de réplica na qual o campo Instância do Servidor em branco é selecionado.  
  
        2.  Insira o nome de uma instância do servidor que atenda aos pré-requisitos para hospedar uma réplica de disponibilidade.  
  
         Para adicionar mais uma réplica, repita as etapas acima. Ao concluir a especificação das réplicas, clique em **OK** para concluir a operação.  
  
##  <a name="TsqlProcedure"></a> Usando o Transact-SQL  
 **Para adicionar uma réplica**  
  
1.  Conecte-se à instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que hospeda a réplica primária.  
  
2.  Adicione a nova réplica secundária ao grupo de disponibilidade usando a cláusula ADD REPLICA ON da instrução ALTER AVAILABILITY GROUP. As opções ENDPOINT_URL, AVAILABILITY_MODE e FAILOVER_MODE são necessárias em uma cláusula ADD REPLICA ON. As outras opções de réplica – BACKUP_PRIORITY, SECONDARY_ROLE, PRIMARY_ROLE e SESSION_TIMEOUT – são opcionais. Para obter mais informações, consulte [ALTER AVAILABILITY GROUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-availability-group-transact-sql).  
  
     Por exemplo, a instrução [!INCLUDE[tsql](../../../includes/tsql-md.md)] a seguir cria uma nova réplica para um grupo de disponibilidade denominado `MyAG` na instância de servidor padrão hospedada por `COMPUTER04`cuja URL de ponto de extremidade é `TCP://COMPUTER04.Adventure-Works.com:5022'`. Esta réplica dá suporte a failover manual e ao modo de disponibilidade de confirmação assíncrona.  
  
    ```  
    ALTER AVAILABILITY GROUP MyAG ADD REPLICA ON 'COMPUTER04'   
       WITH (  
             ENDPOINT_URL = 'TCP://COMPUTER04.Adventure-Works.com:5022',  
             AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,  
             FAILOVER_MODE = MANUAL  
             );  
    ```  
  
##  <a name="PowerShellProcedure"></a> Usando o PowerShell  
 **Para adicionar uma réplica**  
  
1.  Altere o diretório (`cd`) para a instância do servidor que hospeda a réplica primária.  
  
2.  Use o cmdlet **New-SqlAvailabilityReplica** .  
  
     Por exemplo, o comando a seguir adiciona uma réplica de disponibilidade a um grupo de disponibilidade existente denominado `MyAg`. Esta réplica dá suporte a failover manual e ao modo de disponibilidade de confirmação assíncrona. Na função secundária, esta réplica dará suporte a conexões de acesso de leitura, permitindo descarregar o processamento somente leitura para esta réplica.  
  
    ```  
    $agPath = "SQLSERVER:\Sql\PrimaryServer\InstanceName\AvailabilityGroups\MyAg"  
    $endpointURL = "TCP://PrimaryServerName.domain.com:5022"  
    $failoverMode = "Manual"  
    $availabilityMode = "AsynchronousCommit"  
    $secondaryReadMode = "AllowAllConnections"  
  
    New-SqlAvailabilityReplica -Name SecondaryServer\Instance `   
    -EndpointUrl $endpointURL `   
    -FailoverMode $failoverMode `   
    -AvailabilityMode $availabilityMode `   
    -ConnectionModeInSecondaryRole $secondaryReadMode `   
    -Path $agPath  
    ```  
  
    > [!NOTE]  
    >  Para exibir a sintaxe de um cmdlet, use o `Get-Help` cmdlet o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ambiente do PowerShell. Para obter mais informações, consulte [Get Help SQL Server PowerShell](../../../powershell/sql-server-powershell.md).  
  
 **Para configurar e usar o provedor do SQL Server PowerShell**  
  
-   [Provedor do SQL Server PowerShell](../../../powershell/sql-server-powershell-provider.md)  
  
##  <a name="FollowUp"></a> Acompanhamento: depois de adicionar uma réplica secundária  
 Para adicionar uma réplica para um grupo de disponibilidade existente, você deve executar as seguintes etapas:  
  
1.  Conecte-se à instância do servidor que deve hospedar a nova réplica secundária.  
  
2.  Una a nova réplica secundária ao grupo de disponibilidade. Para obter mais informações, consulte [Unir uma réplica secundária a um grupo de disponibilidade &#40;SQL Server&#41;](join-a-secondary-replica-to-an-availability-group-sql-server.md).  
  
3.  Para cada banco de dados do grupo de disponibilidade, crie um banco de dados secundário na instância do servidor que está hospedando a réplica secundária. Para obter mais informações, consulte [Preparar um banco de dados secundário manualmente para um grupo de disponibilidade &#40;SQL Server&#41;](manually-prepare-a-secondary-database-for-an-availability-group-sql-server.md).  
  
4.  Una cada um dos novos bancos de dados secundários ao grupo de disponibilidade. Para obter mais informações, consulte [Unir um banco de dados secundário a um grupo de disponibilidade &#40;SQL Server&#41;](join-a-secondary-database-to-an-availability-group-sql-server.md).  
  
##  <a name="RelatedTasks"></a> Tarefas relacionadas  
 **Para gerenciar uma réplica de disponibilidade**  
  
-   [Unir uma réplica secundária a um grupo de disponibilidade &#40;SQL Server&#41;](join-a-secondary-replica-to-an-availability-group-sql-server.md)  
  
-   [Remover uma réplica secundária de um grupo de disponibilidade &#40;SQL Server&#41;](remove-a-secondary-replica-from-an-availability-group-sql-server.md)  
  
-   [Configurar o acesso somente leitura em uma réplica de disponibilidade &#40;SQL Server&#41;](configure-read-only-access-on-an-availability-replica-sql-server.md)  
  
-   [Alterar o modo de disponibilidade de uma réplica de disponibilidade &#40;SQL Server&#41;](change-the-availability-mode-of-an-availability-replica-sql-server.md)  
  
-   [Alterar o modo de failover de uma réplica de disponibilidade &#40;SQL Server&#41;](change-the-failover-mode-of-an-availability-replica-sql-server.md)  
  
-   [Alterar o período de tempo limite da sessão de uma réplica de disponibilidade &#40;SQL Server&#41;](change-the-session-timeout-period-for-an-availability-replica-sql-server.md)  
  
-   [Alterar o período de tempo limite da sessão de uma réplica de disponibilidade &#40;SQL Server&#41;](change-the-session-timeout-period-for-an-availability-replica-sql-server.md)  
  
## <a name="see-also"></a>Consulte também  
 [ALTER AVAILABILITY GROUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-availability-group-transact-sql)   
 [Visão geral dos grupos de disponibilidade do AlwaysOn &#40;do SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [Criação e configuração de grupos de disponibilidade &#40;SQL Server&#41;](creation-and-configuration-of-availability-groups-sql-server.md)   
 [Use o painel AlwaysOn &#40;SQL Server Management Studio&#41;](use-the-always-on-dashboard-sql-server-management-studio.md)   
 [Monitorar grupos de disponibilidade &#40;Transact-SQL&#41;](monitor-availability-groups-transact-sql.md)  
  
  
