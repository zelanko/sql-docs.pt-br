---
title: Criar um grupo de disponibilidade (SQL Server PowerShell) | Microsoft Docs
ms.custom: 
ms.date: 05/17/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Availability Groups [SQL Server], creating
ms.assetid: bc69a7df-20fa-41e1-9301-11317c5270d2
caps.latest.revision: 41
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: a76ee0a40eab0d72f1db4bfe8d2817179063ea4e
ms.contentlocale: pt-br
ms.lasthandoff: 08/02/2017

---
# <a name="create-an-availability-group-sql-server-powershell"></a>Criar um Grupo de disponibilidade (SQL Server PowerShell)
  Esse tópico descreve como usar os cmdlets do PowerShell para criar e configurar um grupo de disponibilidade AlwaysOn usando o PowerShell no [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]. Um *grupo de disponibilidade* define um conjunto de bancos de dados de usuários que realizará o failover como uma única unidade e um conjunto de parceiros de failover, conhecido como *réplicas de disponibilidade*, que oferece suporte a failover.  
  
> [!NOTE]  
>  Para obter uma introdução aos grupos de disponibilidade, confira [Visão geral dos grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](~/database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md).  
  
-   **Antes de começar:**  
  
     [Pré-requisitos, restrições e recomendações](#PrerequisitesRestrictions)  
  
     [Segurança](#Security)  
  
     [Resumo de tarefas e cmdlets de PowerShell correspondentes](#SummaryPSStatements)  
  
     [Para configurar e usar o provedor do SQL Server PowerShell](#PsProviderLinks)  
  
-   **Para criar e configurar um grupo de disponibilidade com:**  [Usando o PowerShell para criar e configurar um grupo de disponibilidade](#PowerShellProcedure)  
  
-   **Exemplos:**  [Usando o PowerShell para criar um grupo de disponibilidade](#ExampleConfigureGroup)  
  
-   [Tarefas relacionadas](#RelatedTasks)  
  
-   [Conteúdo relacionado](#RelatedContent)  
  
> [!NOTE]  
>  Como alternativa para o uso dos cmdlets do PowerShell, você pode usar o assistente para Criar Grupo de Disponibilidade ou o [!INCLUDE[tsql](../../../includes/tsql-md.md)]. Para obter mais informações, veja [Usar a caixa de diálogo Novo Grupo de Disponibilidade &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-new-availability-group-dialog-box-sql-server-management-studio.md) ou [Criar um grupo de disponibilidade &#40;Transact-SQL&#41;](../../../database-engine/availability-groups/windows/create-an-availability-group-transact-sql.md).  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
 É recomendável que você leia esta seção antes de tentar criar seu primeiro grupo de disponibilidade.  
  
###  <a name="PrerequisitesRestrictions"></a> Pré-requisitos, restrições e recomendações  
  
-   Antes de criar um grupo de disponibilidade, verifique se cada instância de host do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] reside em um nó diferente do WSFC (Windows Server Failover Clustering) de um único cluster de failover do WSFC. Verifique também se suas instâncias de servidor atendem aos outros pré-requisitos de instância de servidor, se todos os outros requisitos do [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] são atendidos e se você está ciente das recomendações. Para obter mais informações, é altamente recomendável que você leia [Prerequisites, Restrictions, and Recommendations for Always On Availability Groups &#40;SQL Server&#41;](~/database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md).  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Requer associação na função de servidor fixa **sysadmin** e a permissão de servidor CREATE AVAILABILITY GROUP, a permissão ALTER ANY AVAILABILITY GROUP ou CONTROL SERVER.  
  
###  <a name="SummaryPSStatements"></a> Resumo de tarefas e cmdlets de PowerShell correspondentes  
 A tabela a seguir lista as tarefas básicas envolvidas na configuração de um grupo de disponibilidade e indica as tarefas com suporte nos cmdlets do PowerShell. As tarefas [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] devem ser executadas na sequência em que são apresentadas na tabela.  
  
|Tarefa|Cmdlets do PowerShell (se disponíveis) ou instrução Transact-SQL|Local de execução da tarefa**\***|  
|----------|--------------------------------------------------------------------|---------------------------------|  
|Criar ponto de extremidade de espelhamento de banco de dados (uma vez por instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] )|**New-SqlHadrEndPoint**|Executar em cada instância de servidor que não tem ponto de extremidade de espelhamento de banco de dados.<br /><br /> Observação: para alterar um ponto de extremidade de espelhamento de banco de dados existente, use **Set-SqlHadrEndpoint**.|  
|Criar grupo de disponibilidade|Primeiro, use o cmdlet **New-SqlAvailabilityReplica** com o parâmetro **-AsTemplate** para criar um objeto da réplica de disponibilidade na memória para cada uma das duas réplicas de disponibilidade que você pretende incluir no grupo de disponibilidade.<br /><br /> Em seguida, crie o grupo de disponibilidade usando o cmdlet **New-SqlAvailabilityGroup** e referenciando os objetos da réplica de disponibilidade.|Execute na instância de servidor que deve hospedar a réplica primária inicial.|  
|Unir a réplica secundária ao grupo de disponibilidade|**Join-SqlAvailabilityGroup**|Execute em cada instância de servidor que hospeda uma réplica secundária.|  
|Preparar os banco de dados secundários|**Backup-SqlDatabase** e **Restore-SqlDatabase**|Crie backups na instância de servidor que hospeda a réplica primária.<br /><br /> Restaure backups em cada instância de servidor que hospeda uma réplica secundária usando o parâmetro de restauração **NoRecovery** . Se os caminhos dos arquivos forem diferentes nos computadores que hospedam a réplica primária e a réplica secundária de destino, use também o parâmetro de restauração **RelocateFile** .|  
|Iniciar a sincronização de dados unindo cada banco de dados secundário ao grupo de disponibilidade|**Add-SqlAvailabilityDatabase**|Execute em cada instância de servidor que hospeda uma réplica secundária.|  
  
 \*Para executar uma tarefa específica, altere o diretório (**cd**) para as instâncias de servidor indicadas.  
  
###  <a name="PsProviderLinks"></a> Para configurar e usar o provedor do SQL Server PowerShell  
  
-   [Provedor do SQL Server PowerShell](../../../relational-databases/scripting/sql-server-powershell-provider.md)  
  
-   [Obter Ajuda do SQL Server PowerShell](../../../relational-databases/scripting/get-help-sql-server-powershell.md)  
  
##  <a name="PowerShellProcedure"></a> Usando o PowerShell para criar e configurar um grupo de disponibilidade  
  
> [!NOTE]  
>  Para exibir a sintaxe e um exemplo de um cmdlet, use o cmdlet **Get-Help** no ambiente do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] PowerShell. Para obter mais informações, consulte [Get Help SQL Server PowerShell](../../../relational-databases/scripting/get-help-sql-server-powershell.md).  
  
1.  Altere o diretório (**cd**) para a instância do servidor que hospedará a réplica primária.  
  
2.  Crie um objeto da réplica de disponibilidade na memória para a réplica primária.  
  
3.  Crie um objeto da réplica de disponibilidade na memória para cada réplica secundária.  
  
4.  Crie o grupo de disponibilidade.  
  
    > [!NOTE]  
    >  O tamanho máximo de um nome de grupo de disponibilidade é 128 caracteres.  
  
5.  Una a nova réplica secundária ao grupo de disponibilidade. Para obter mais informações, veja [Unir uma réplica secundária a um grupo de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/join-a-secondary-replica-to-an-availability-group-sql-server.md).  
  
6.  Para cada banco de dados do grupo de disponibilidade, crie um banco de dados secundário restaurando backups recentes do banco de dados primário, usando RESTORE WITH NORECOVERY.  
  
7.  Una cada novo banco de dados secundário ao grupo de disponibilidade. Para obter mais informações, veja [Unir uma réplica secundária a um grupo de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/join-a-secondary-replica-to-an-availability-group-sql-server.md).  
  
8.  Se desejar, use o comando **dir** do Windows para verificar o conteúdo do novo grupo de disponibilidade.  
  
> [!NOTE]  
>  Se as contas de serviço [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] das instâncias do servidor forem executadas em diferentes contas de usuário de domínio, em cada instância do servidor, crie um logon para a outra instância do servidor e conceda a permissão CONNECT a esse logon para o ponto de extremidade de espelhamento do banco de dados local.  
  
##  <a name="ExampleConfigureGroup"></a> Exemplo: usando o PowerShell para criar um grupo de disponibilidade  
 O exemplo doe PowerShell a seguir cria e configura um grupo de disponibilidade simples denominado `MyAG` com duas réplicas de disponibilidade e um banco de dados de disponibilidade. O exemplo:  
  
1.  Faz backup do `MyDatabase` e de seu log de transações.  
  
2.  Restaura o `MyDatabase` e seu log de transações usando a opção **-NoRecovery** .  
  
3.  Cria uma representação na memória da réplica primária, que será hospedada pela instância local do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] (denominada `PrimaryComputer\Instance`).  
  
4.  Cria uma representação na memória da réplica secundária, que será hospedada por uma instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] (denominada `SecondaryComputer\Instance`).  
  
5.  Cria um grupo de disponibilidade denominado `MyAG`.  
  
6.  Une a réplica secundária ao grupo de disponibilidade.  
  
7.  Une o banco de dados secundário ao grupo de disponibilidade.  
  
```  
# Backup my database and its log on the primary  
Backup-SqlDatabase `  
    -Database "MyDatabase" `  
    -BackupFile "\\share\backups\MyDatabase.bak" `  
    -ServerInstance "PrimaryComputer\Instance"  
  
Backup-SqlDatabase `  
    -Database "MyDatabase" `  
    -BackupFile "\\share\backups\MyDatabase.log" `  
    -ServerInstance "PrimaryComputer\Instance" `  
    -BackupAction Log   
  
# Restore the database and log on the secondary (using NO RECOVERY)  
Restore-SqlDatabase `  
    -Database "MyDatabase" `  
    -BackupFile "\\share\backups\MyDatabase.bak" `  
    -ServerInstance "SecondaryComputer\Instance" `  
    -NoRecovery  
  
Restore-SqlDatabase `  
    -Database "MyDatabase" `  
    -BackupFile "\\share\backups\MyDatabase.log" `  
    -ServerInstance "SecondaryComputer\Instance" `  
    -RestoreAction Log `  
    -NoRecovery  
  
# Create an in-memory representation of the primary replica.  
$primaryReplica = New-SqlAvailabilityReplica `  
    -Name "PrimaryComputer\Instance" `  
    -EndpointURL "TCP://PrimaryComputer.domain.com:5022" `  
    -AvailabilityMode "SynchronousCommit" `  
    -FailoverMode "Automatic" `  
    -Version 12 `  
    -AsTemplate  
  
# Create an in-memory representation of the secondary replica.  
$secondaryReplica = New-SqlAvailabilityReplica `  
    -Name "SecondaryComputer\Instance" `  
    -EndpointURL "TCP://SecondaryComputer.domain.com:5022" `  
    -AvailabilityMode "SynchronousCommit" `  
    -FailoverMode "Automatic" `  
    -Version 12 `  
    -AsTemplate  
  
# Create the availability group  
New-SqlAvailabilityGroup `  
    -Name "MyAG" `  
    -Path "SQLSERVER:\SQL\PrimaryComputer\Instance" `  
    -AvailabilityReplica @($primaryReplica,$secondaryReplica) `  
    -Database "MyDatabase"  
  
# Join the secondary replica to the availability group.  
Join-SqlAvailabilityGroup -Path "SQLSERVER:\SQL\SecondaryComputer\Instance" -Name "MyAG"  
  
# Join the secondary database to the availability group.  
Add-SqlAvailabilityDatabase -Path "SQLSERVER:\SQL\SecondaryComputer\Instance\AvailabilityGroups\MyAG" -Database "MyDatabase"  
```  
  
##  <a name="RelatedTasks"></a> Tarefas relacionadas  
 **Para configurar uma instância de servidor para grupos de disponibilidade AlwaysOn**  
  
-   [Habilitar e desabilitar Grupos de Disponibilidade AlwaysOn &#40;SQL Server&#41;](~/database-engine/availability-groups/windows/enable-and-disable-always-on-availability-groups-sql-server.md)  
  
-   [Criar um ponto de extremidade de espelhamento de banco de dados para grupos de disponibilidade AlwaysOn &#40;SQL Server PowerShell&#41;](~/database-engine/availability-groups/windows/database-mirroring-always-on-availability-groups-powershell.md)  
  
 **Para configurar um grupo de disponibilidade e propriedades de réplica**  
  
-   [Alterar o modo de disponibilidade de uma réplica de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/change-the-availability-mode-of-an-availability-replica-sql-server.md)  
  
-   [Alterar o modo de failover de uma réplica de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/change-the-failover-mode-of-an-availability-replica-sql-server.md)  
  
-   [Criar ou configurar um ouvinte do grupo de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server.md)  
  
-   [Configurar a política de failover flexível para controlar condições de failover automático &#40;Grupos de disponibilidade AlwaysOn&#41;](~/database-engine/availability-groups/windows/configure-flexible-automatic-failover-policy.md)  
  
-   [Especificar a URL do ponto de extremidade ao adicionar ou modificar uma réplica de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/specify-endpoint-url-adding-or-modifying-availability-replica.md)  
  
-   [Configurar backup em réplicas de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/configure-backup-on-availability-replicas-sql-server.md)  
  
-   [Configurar o acesso somente leitura em uma réplica de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/configure-read-only-access-on-an-availability-replica-sql-server.md)  
  
-   [Configurar o roteamento somente leitura para um grupo de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/configure-read-only-routing-for-an-availability-group-sql-server.md)  
  
-   [Alterar o período de tempo limite da sessão de uma réplica de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/change-the-session-timeout-period-for-an-availability-replica-sql-server.md)  
  
 **Para concluir a configuração do grupo de disponibilidade**  
  
-   [Unir uma réplica secundária a um grupo de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/join-a-secondary-replica-to-an-availability-group-sql-server.md)  
  
-   [Preparar um banco de dados secundário manualmente para um grupo de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/manually-prepare-a-secondary-database-for-an-availability-group-sql-server.md)  
  
-   [Unir um banco de dados secundário a um grupo de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/join-a-secondary-database-to-an-availability-group-sql-server.md)  
  
-   [Criar ou configurar um ouvinte do grupo de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server.md)  
  
 **Maneiras alternativas de criar um grupo de disponibilidade**  
  
-   [Usar o Assistente de Grupo de Disponibilidade &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-availability-group-wizard-sql-server-management-studio.md)  
  
-   [Usar a caixa de diálogo Novo Grupo de Disponibilidade &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-new-availability-group-dialog-box-sql-server-management-studio.md)  
  
-   [Criar um grupo de disponibilidade &#40;Transact-SQL&#41;](../../../database-engine/availability-groups/windows/create-an-availability-group-transact-sql.md)  
  
 **Para solucionar problemas de configuração dos grupos de disponibilidade AlwaysOn**  
  
-   [Solucionar problemas de configuração de grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](~/database-engine/availability-groups/windows/troubleshoot-always-on-availability-groups-configuration-sql-server.md)  
  
-   [Solução de problemas de uma operação de adição de arquivos com falha &#40;Grupos de disponibilidade de AlwaysOn&#41;](~/database-engine/availability-groups/windows/troubleshoot-a-failed-add-file-operation-always-on-availability-groups.md)  
  
##  <a name="RelatedContent"></a> Conteúdo relacionado  
  
-   **Blogs:**  
  
     [Série de aprendizado do AlwaysOn – HADRON: uso do pool de trabalho para bancos de dados habilitados para HADRON](http://blogs.msdn.com/b/psssql/archive/2012/05/17/Always%20On-hadron-learning-series-worker-pool-usage-for-hadron-enabled-databases.aspx)  
  
     [Configurando o AlwaysOn com o SQL Server PowerShell](https://blogs.msdn.microsoft.com/sqlalwayson/2012/02/03/configuring-alwayson-with-sql-server-powershell/)  
  
     [Blogs da equipe do AlwaysOn do SQL Server: o blog oficial da equipe do AlwaysOn do SQL Server](https://blogs.msdn.microsoft.com/sqlalwayson/)  
  
     [Blogs dos engenheiros do CSS SQL Server](http://blogs.msdn.com/b/psssql/)  
  
-   **Vídeos:**  
  
     [Microsoft SQL Server codinome “Denali” Série AlwaysOn, Parte 1: Introduzindo a próxima geração de solução de alta disponibilidade](http://channel9.msdn.com/Events/TechEd/NorthAmerica/2011/DBI302)  
  
     [Microsoft SQL Server codinome “Denali” Série AlwaysOn, Parte 2: Criando uma solução de alta disponibilidade de missão crítica usando AlwaysOn](http://channel9.msdn.com/Events/TechEd/NorthAmerica/2011/DBI404)  
  
-   **Whitepapers:**  
  
     [Guia de soluções AlwaysOn do Microsoft SQL Server para alta disponibilidade e recuperação de desastre](http://go.microsoft.com/fwlink/?LinkId=227600)  
  
     [White papers da Microsoft para SQL Server 2012](http://msdn.microsoft.com/library/hh403491.aspx)  
  
     [White papers da equipe de consultoria do cliente do SQL Server](http://sqlcat.com/)  
  
## <a name="see-also"></a>Consulte também  
 [O ponto de extremidade de espelhamento de banco de dados &#40;SQL Server&#41;](../../../database-engine/database-mirroring/the-database-mirroring-endpoint-sql-server.md)   
 [Visão geral dos Grupos de Disponibilidade AlwaysOn &#40;SQL Server&#41;](~/database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)  
  
  








