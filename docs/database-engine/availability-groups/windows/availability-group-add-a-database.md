---
title: Adicionar um banco de dados a um grupo de disponibilidade (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 05/17/2016
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.suite: sql
ms.technology: high-availability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- primary databases [SQL Server], in availability group
- Availability Groups [SQL Server], configuring
- Availability Groups [SQL Server], databases
ms.assetid: 2a54eef8-9e8e-4e04-909c-6970112d55cc
caps.latest.revision: 33
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: e79db11df550c278aecfb1b6b95d4574d9fb9f4e
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="availability-group---add-a-database"></a>Grupo de disponibilidade – adicionar um banco de dados
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Este tópico descreve como adicionar um banco de dados a um grupo de disponibilidade AlwaysOn usando o [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], o [!INCLUDE[tsql](../../../includes/tsql-md.md)]ou o PowerShell no [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)].  
  
-   **Antes de começar:**  
  
     [Pré-requisitos e restrições](#Prerequisites)  
  
     [Permissões](#Permissions)  
  
-   **Para adicionar um banco de dados a um grupo de disponibilidade usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [PowerShell](#PowerShellProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Prerequisites"></a> Pré-requisitos e restrições  
  
-   Você deve estar conectado à instância do servidor que hospeda a réplica primária.  
  
-   O banco de dados deve residir na instância do servidor que hospeda a réplica primária e atender aos pré-requisitos e restrições para bancos de dados de disponibilidade. Para obter mais informações, veja [Pré-requisitos, restrições e recomendações para grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md).  
  
###  <a name="Security"></a> Segurança  
  
###  <a name="Permissions"></a> Permissões  
 Requer a permissão ALTER AVAILABILITY GROUP no grupo de disponibilidade, a permissão CONTROL AVAILABILITY GROUP, a permissão ALTER ANY AVAILABILITY GROUP ou a permissão CONTROL SERVER.  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
 **Para adicionar um banco de dados a um grupo de disponibilidade**  
  
1.  No Pesquisador de Objetos, conecte-se à instância de servidor que hospeda a réplica primária e expanda a árvore de servidores.  
  
2.  Expanda os nós **Alta Disponibilidade AlwaysOn** e **Grupos de Disponibilidade**.  
  
3.  Clique com o botão direito do mouse no grupo de disponibilidade e selecione um dos comandos a seguir:  
  
    -   Para iniciar o Assistente para Adicionar Banco de Dados a um Grupo de Disponibilidade, selecione o comando **Adicionar Banco de Dados** . Para obter mais informações, consulte [Usar o Assistente para Adicionar Banco de Dados ao Grupo de disponibilidade &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/availability-group-add-database-to-group-wizard.md).  
  
    -   Para adicionar um ou mais bancos de dados especificando-os na caixa de diálogo **Propriedades do Grupo de Disponibilidade** , selecione o comando **Propriedades** . As etapas para adicionar um banco de dados são as seguintes:  
  
        1.  No painel **Bancos de dados de Disponibilidade** , clique no botão **Adicionar** . Isto cria e seleciona um campo de banco de dados em branco.  
  
        2.  Digite o nome de um banco de dados que atenda aos pré-requisitos dos bancos de dados de disponibilidade.  
  
         Para adicionar outro banco de dados, repita as etapas acima. Ao concluir a especificação dos bancos de dados é feito, clique em **OK** para concluir a operação.  
  
         Depois que você usar a caixa de diálogo **Propriedades do Grupo de Disponibilidade** para adicionar um banco de dados a um grupo de disponibilidade, configure o banco de dados secundário correspondente em cada instância de servidor que hospeda uma réplica secundária. Para obter mais informações, veja [Iniciar movimentação de dados em um banco de dados secundário &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/start-data-movement-on-an-always-on-secondary-database-sql-server.md).  
  
##  <a name="TsqlProcedure"></a> Usando o Transact-SQL  
 **Para adicionar um banco de dados a um grupo de disponibilidade**  
  
1.  Conecte-se à instância de servidor que hospeda a instância do servidor que hospeda a réplica primária.  
  
2.  Use a instrução [ALTER AVAILABILITY GROUP](../../../t-sql/statements/alter-availability-group-transact-sql.md) , da seguinte maneira:  
  
     ALTER AVAILABILITY GROUP *group_name* ADD DATABASE *database_name* [,...*n*]  
  
     em que *group_name* é o nome do grupo de disponibilidade e *database_name* é o nome de um banco de dados a ser adicionado ao grupo.  
  
     O exemplo a seguir adiciona o banco de dados *MyDb3* ao grupo de disponibilidade *MyAG* .  
  
    ```  
    -- Connect to the server instance that hosts the primary replica.  
    -- Add an existing database to the availability group.  
    ALTER AVAILABILITY GROUP MyAG ADD DATABASE MyDb3;  
    GO  
    ```  
  
3.  Depois que você adicionar um banco de dados a um grupo de disponibilidade, configure o banco de dados secundário correspondente em cada instância de servidor que hospeda uma réplica secundária. Para obter mais informações, veja [Iniciar movimentação de dados em um banco de dados secundário &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/start-data-movement-on-an-always-on-secondary-database-sql-server.md).  
  
##  <a name="PowerShellProcedure"></a> Usando o PowerShell  
 **Para adicionar um banco de dados a um grupo de disponibilidade**  
  
1.  Altere o diretório (**cd**) para a instância de servidor que hospeda a réplica primária.  
  
2.  Use o cmdlet **Add-SqlAvailabilityDatabase** .  
  
     Por exemplo, o comando a seguir adiciona o banco de dados secundário `MyDd` ao grupo de disponibilidade `MyAG` , cuja réplica primária é hospedada por `PrimaryServer\InstanceName`.  
  
    ```  
  
    Add-SqlAvailabilityDatabase `   
    -Path SQLSERVER:\SQL\PrimaryServer\InstanceName\AvailabilityGroups\MyAG `   
    -Database "MyDb"  
    ```  
  
    > [!NOTE]  
    >  Para exibir a sintaxe de um cmdlet, use o cmdlet **Get-Help** no ambiente do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] PowerShell. Para obter mais informações, consulte [Get Help SQL Server PowerShell](../../../relational-databases/scripting/get-help-sql-server-powershell.md).  
  
3.  Depois que você adicionar um banco de dados a um grupo de disponibilidade, configure o banco de dados secundário correspondente em cada instância de servidor que hospeda uma réplica secundária. Para obter mais informações, veja [Iniciar movimentação de dados em um banco de dados secundário &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/start-data-movement-on-an-always-on-secondary-database-sql-server.md).  
  
 **Para configurar e usar o provedor do SQL Server PowerShell**  
  
-   [Provedor do SQL Server PowerShell](../../../relational-databases/scripting/sql-server-powershell-provider.md)  
  
 Para obter um exemplo completo, consulte [Exemplo (PowerShell)](#PSExample), abaixo.  
  
###  <a name="PSExample"></a> Exemplo (PowerShell)  
 O exemplo a seguir mostra o processo completo para preparar um banco de dados secundário de um banco de dados na instância de servidor que hospeda a réplica primária de um grupo de disponibilidade, adicionando o banco de dados a um grupo de disponibilidade (como um banco de dados primário) e unindo o banco de dados secundário ao grupo de disponibilidade. Primeiro, o exemplo faz backup do banco de dados e de seu log de transação. Em seguida, o exemplo restaura os backups de banco de dados e log para as instâncias de servidor que hospedam uma réplica secundária.  
  
 O exemplo chama **Add-SqlAvailabilityDatabase** duas vezes. Primeiro, na réplica primária, para adicionar o banco de dados ao grupo de disponibilidade. Em seguida, na réplica secundária, para unir o banco de dados secundário nessa réplica ao grupo de disponibilidade. Se você tiver mais de uma réplica secundária, restaure e junção una o banco de dados secundário em cada um deles.  
  
```  
$DatabaseBackupFile = "\\share\backups\MyDatabase.bak"  
$LogBackupFile = "\\share\backups\MyDatabase.trn"  
$MyAgPrimaryPath = "SQLSERVER:\SQL\PrimaryServer\InstanceName\AvailabilityGroups\MyAg"  
$MyAgSecondaryPath = "SQLSERVER:\SQL\SecondaryServer\InstanceName\AvailabilityGroups\MyAg"  
  
Backup-SqlDatabase -Database "MyDatabase" -BackupFile $DatabaseBackupFile -ServerInstance "PrimaryServer\InstanceName"  
Backup-SqlDatabase -Database "MyDatabase" -BackupFile $LogBackupFile -ServerInstance "PrimaryServer\InstanceName" -BackupAction 'Log'  
  
Restore-SqlDatabase -Database "MyDatabase" -BackupFile $DatabaseBackupFile -ServerInstance "SecondaryServer\InstanceName" -NoRecovery  
Restore-SqlDatabase -Database "MyDatabase" -BackupFile $LogBackupFile -ServerInstance "SecondaryServer\InstanceName" -RestoreAction 'Log' -NoRecovery  
  
Add-SqlAvailabilityDatabase -Path $MyAgPrimaryPath -Database "MyDatabase"  
Add-SqlAvailabilityDatabase -Path $MyAgSecondaryPath -Database "MyDatabase"  
  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Visão geral dos grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Criação e configuração de grupos de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/creation-and-configuration-of-availability-groups-sql-server.md)   
 [Usar o Painel AlwaysOn &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-always-on-dashboard-sql-server-management-studio.md)   
 [Monitorar grupos de disponibilidade &#40;Transact-SQL&#41;](../../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)  
  
  
