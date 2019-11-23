---
title: Remover um banco de dados primário de um grupo de disponibilidade (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql12.swb.availabilitygroup.removeprimarydb.f1
helpviewer_keywords:
- primary databases [SQL Server], in availability group
- Availability Groups [SQL Server], removing
- Availability Groups [SQL Server], configuring
- Availability Groups [SQL Server], databases
ms.assetid: 6d4ca31e-ddf0-44bf-be5e-a5da060bf096
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 06b9dac5f9074b335afff7c6b71980618a3020ce
ms.sourcegitcommit: a165052c789a327a3a7202872669ce039bd9e495
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/22/2019
ms.locfileid: "72782866"
---
# <a name="remove-a-primary-database-from-an-availability-group-sql-server"></a>Remover um banco de dados primário de um grupo de disponibilidade (SQL Server)
  Este tópico descreve como remover o banco de dados primário e os bancos de dados secundários correspondentes de um grupo de disponibilidade AlwaysOn usando o [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], o [!INCLUDE[tsql](../../../includes/tsql-md.md)] ou o PowerShell no [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)].  
  
-   **Antes de começar:**  
  
     [Pré-requisitos e restrições](#Prerequisites)  
  
     [Segurança](#Security)  
  
-   **Para remover um banco de dados de disponibilidade usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [PowerShell](#PowerShellProcedure)  
  
-   **Acompanhamento:**  [depois de remover um banco de dados de disponibilidade de um grupo de disponibilidade](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Prerequisites"></a> Pré-requisitos e restrições  
  
-   Esta tarefa tem suporte apenas em réplicas primárias. Você deve estar conectado à instância do servidor que hospeda a réplica primária.  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Requer a permissão ALTER AVAILABILITY GROUP no grupo de disponibilidade, a permissão CONTROL AVAILABILITY GROUP, a permissão ALTER ANY AVAILABILITY GROUP ou a permissão CONTROL SERVER.  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
 **Para remover um banco de dados de disponibilidade**  
  
1.  No Pesquisador de Objetos, conecte-se à instância do servidor que hospeda a réplica primária do banco de dados ou bancos de dados a serem removidos e expanda a árvore de servidores.  
  
2.  Expanda os nós **Alta Disponibilidade AlwaysOn** e **Grupos de Disponibilidade** .  
  
3.  Selecione o grupo de disponibilidade e expanda o nó **Bancos de Dados de Disponibilidade** .  
  
4.  Essa etapa depende de se você deseja remover vários grupos de bancos de dados ou apenas um banco de dados, da seguinte maneira:  
  
    -   Para remover vários bancos de dados, use o painel **Detalhes do Pesquisador de Objetos** para exibir e selecionar todos os bancos de dados que você deseja remover. Para obter mais informações, veja [Usar os detalhes do Pesquisador de Objetos para monitorar grupos de disponibilidade &#40;SQL Server Management Studio&#41;](use-object-explorer-details-to-monitor-availability-groups.md).  
  
    -   Para remover um único banco de dados, selecione-o no painel **Pesquisador de Objetos** ou no painel **Detalhes do Pesquisador de Objetos** .  
  
5.  Clique com o botão direito do mouse no banco de dados ou bancos de dados selecionados e selecione **Remover Banco de Dados do Grupo de Disponibilidade** no menu de comando.  
  
6.  Na caixa de diálogo **Remover Bancos de Dados do Grupo de Disponibilidade** , para remover todos os bancos de dados listados, clique em **OK**. Se você não desejar remover todos os bancos de dados listados, clique em **Cancelar**.  
  
##  <a name="TsqlProcedure"></a> Usando Transact-SQL  
 **Para remover um banco de dados de disponibilidade**  
  
1.  Conecte-se à instância de servidor que hospeda a réplica primária.  
  
2.  Use a instrução [ALTER AVAILABILITY GROUP](/sql/t-sql/statements/alter-availability-group-transact-sql) , da seguinte maneira:  
  
     ALTER AVAILABILITY GROUP *group_name* REMOVE DATABASE *availability_database_name*  
  
     em que *group_name* é o nome do grupo de disponibilidade e *database_name* é o nome do banco de dados a ser removido.  
  
     O exemplo a seguir remove um banco de dados denominado `Db6` do grupo de disponibilidade `MyAG` .  
  
    ```sql
    ALTER AVAILABILITY GROUP MyAG REMOVE DATABASE Db6;  
    ```  
  
##  <a name="PowerShellProcedure"></a> Usando o PowerShell  
 **Para remover um banco de dados de disponibilidade**  
  
1.  Altere o diretório (`cd`) para a instância do servidor que hospeda a réplica primária.  
  
2.  Use o cmdlet `Remove-SqlAvailabilityDatabase`, especificando o nome do banco de dados de disponibilidade a ser removido do grupo de disponibilidade. Quando você está conectado a uma instância do servidor que hospeda a réplica primária, o banco de dados primário e os bancos de dados secundários correspondentes são todos removidos do grupo de disponibilidade.  
  
     Por exemplo, o comando a seguir remove o banco de dados de disponibilidade `MyDb9` do grupo de disponibilidade denominado `MyAg`. Como o comando é executado na instância do servidor que hospeda a réplica primária, o banco de dados primário e todos os bancos de dados secundários correspondentes são removidos do grupo de disponibilidade. A sincronização de dados não ocorrerá mais para este banco de dados em nenhuma réplica secundária.  
  
    ```powershell
    Remove-SqlAvailabilityDatabase -Path SQLSERVER:\Sql\PrimaryComputer\InstanceName\AvailabilityGroups\MyAg\Databases\MyDb9  
    ```  
  
    > [!NOTE]  
    >  Para exibir a sintaxe de um cmdlet, use o cmdlet `Get-Help` no ambiente do [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] PowerShell. Para saber mais, confira [Get Help SQL Server PowerShell](../../../powershell/sql-server-powershell.md).  
  
 **Para configurar e usar o provedor do SQL Server PowerShell**  
  
-   [Provedor do SQL Server PowerShell](../../../powershell/sql-server-powershell-provider.md)  
  
##  <a name="FollowUp"></a> Acompanhamento: depois de remover um banco de dados de disponibilidade de um grupo de disponibilidade  
 A remoção de um banco de dados de disponibilidade do grupo de disponibilidade termina a sincronização de dados entre o banco de dados primário antigo e os bancos de dados secundários correspondentes. O banco de dados primário antigo permanece online. Todos os bancos de dados secundários correspondentes são colocados no estado RESTORING.  
  
 Neste ponto, há maneiras alternativas de lidar com um banco de dados secundário removido:  
  
-   Se você não precisar mais de um determinado banco de dados secundário, você poderá removê-lo.  
  
     Para obter mais informações, veja [Excluir um banco de dados](../../../relational-databases/databases/delete-a-database.md).  
  
-   Se desejar acessar um banco de dados secundário depois que ele foi removido do grupo de disponibilidade, você poderá recuperá-lo. No entanto, se você recuperar um banco de dados secundário removido, dois bancos de dados independentes divergentes com o mesmo nome estarão online. Você deve verificar se os clientes podem acessar só um deles, normalmente o banco de dados primário mais recente.  
  
     Para obter mais informações, veja [Recuperar um banco de dados sem restaurar dados &#40;Transact-SQL&#41;](../../../relational-databases/backup-restore/recover-a-database-without-restoring-data-transact-sql.md).  
  
## <a name="see-also"></a>Consulte também  
 [Visão geral do &#40;grupos de disponibilidade AlwaysOn&#41; SQL Server](overview-of-always-on-availability-groups-sql-server.md)   
 [Remover um banco de dados secundário de um grupo de disponibilidade &#40;SQL Server&#41;](remove-a-secondary-database-from-an-availability-group-sql-server.md)  
