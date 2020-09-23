---
title: Criar um grupo de disponibilidade usando o PowerShell
description: Saiba como usar cmdlets do PowerShell para criar e configurar um grupo de disponibilidade Always On usando o PowerShell no SQL Server 2019 (15.x).
ms.custom: seodec18
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: how-to
helpviewer_keywords:
- Availability Groups [SQL Server], creating
ms.assetid: bc69a7df-20fa-41e1-9301-11317c5270d2
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 6562517c088de44044baaa6b2b0b80b4243eb9fa
ms.sourcegitcommit: cc23d8646041336d119b74bf239a6ac305ff3d31
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/23/2020
ms.locfileid: "91116238"
---
# <a name="create-an-always-on-availability-group-using-powershell"></a>Criar um grupo de disponibilidade Always On usando o PowerShell
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  Esse tópico descreve como usar os cmdlets do PowerShell para criar e configurar um grupo de disponibilidade AlwaysOn usando o PowerShell no [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]. Um *grupo de disponibilidade* define um conjunto de bancos de dados de usuários que realizará o failover como uma única unidade e um conjunto de parceiros de failover, conhecido como *réplicas de disponibilidade*, que oferece suporte a failover.  
  
> [!NOTE]  
> Para obter uma introdução aos grupos de disponibilidade, confira [Visão geral dos grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](~/database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md).  
  
> [!NOTE]  
> Como alternativa para o uso dos cmdlets do PowerShell, você pode usar o assistente para Criar Grupo de Disponibilidade ou o [!INCLUDE[tsql](../../../includes/tsql-md.md)]. Para obter mais informações, veja [Usar a caixa de diálogo Novo Grupo de Disponibilidade &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-new-availability-group-dialog-box-sql-server-management-studio.md) ou [Criar um grupo de disponibilidade &#40;Transact-SQL&#41;](../../../database-engine/availability-groups/windows/create-an-availability-group-transact-sql.md).  

## <a name="before-you-begin"></a>Antes de começar
### <a name="prerequisites-restrictions-and-recommendations"></a><a name="PrerequisitesRestrictions"></a> Pré-requisitos, restrições e recomendações  

- Antes de criar um grupo de disponibilidade, verifique se cada instância de host do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] reside em um nó diferente do WSFC (Windows Server Failover Clustering) de um único cluster de failover do WSFC. Verifique também se suas instâncias de servidor atendem aos outros pré-requisitos de instância de servidor, se todos os outros requisitos do [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] são atendidos e se você está ciente das recomendações. Para obter mais informações, é altamente recomendável que você leia [Pré-requisitos, restrições e recomendações para grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](~/database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md).  

### <a name="permissions"></a><a name="Permissions"></a> Permissões  
 Requer a associação na função de servidor fixa **sysadmin** e a permissão de servidor CREATE AVAILABILITY GROUP, a permissão ALTER ANY AVAILABILITY GROUP ou a permissão CONTROL SERVER.  

## <a name="using-powershell-to-create-and-configure-an-availability-group"></a><a name="PowerShellProcedure"></a> Usando o PowerShell para criar e configurar um grupo de disponibilidade  
 
A tabela a seguir lista as tarefas básicas envolvidas na configuração de um grupo de disponibilidade e indica as tarefas com suporte nos cmdlets do PowerShell. As tarefas [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] devem ser executadas na sequência em que são apresentadas na tabela.  
  
|Tarefa|Cmdlets do PowerShell (se disponíveis) ou instrução Transact-SQL|Local de execução da tarefa|  
|----------|--------------------------------------------------------------------|---------------------------------|  
|Criar ponto de extremidade de espelhamento de banco de dados (uma vez por instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] )|**New-SqlHadrEndPoint**|Executar em cada instância de servidor que não tem ponto de extremidade de espelhamento de banco de dados.<br /><br />Para alterar um ponto de extremidade de espelhamento de banco de dados existente, use **Set-SqlHadrEndpoint**.|  
|Criar grupo de disponibilidade|Primeiro, use o cmdlet **New-SqlAvailabilityReplica** com o parâmetro **-AsTemplate** para criar um objeto da réplica de disponibilidade na memória para cada uma das duas réplicas de disponibilidade que você pretende incluir no grupo de disponibilidade.<br /><br /> Em seguida, crie o grupo de disponibilidade usando o cmdlet **New-SqlAvailabilityGroup** e referenciando os objetos da réplica de disponibilidade.|Execute na instância de servidor que deve hospedar a réplica primária inicial.|  
|Unir a réplica secundária ao grupo de disponibilidade|**Join-SqlAvailabilityGroup**|Execute em cada instância de servidor que hospeda uma réplica secundária.|  
|Preparar os banco de dados secundários|**Backup-SqlDatabase** e **Restore-SqlDatabase**|Crie backups na instância de servidor que hospeda a réplica primária.<br /><br /> Restaure backups em cada instância de servidor que hospeda uma réplica secundária usando o parâmetro de restauração **NoRecovery** . Se os caminhos dos arquivos forem diferentes nos computadores que hospedam a réplica primária e a réplica secundária de destino, use também o parâmetro de restauração **RelocateFile** .|  
|Iniciar a sincronização de dados unindo cada banco de dados secundário ao grupo de disponibilidade|**Add-SqlAvailabilityDatabase**|Execute em cada instância de servidor que hospeda uma réplica secundária.|  
  
> [!NOTE]
> Para executar as tarefas fornecidas, altere o diretório (**cd**) para as instâncias de servidor indicadas.  

## <a name="using-powershell"></a>Usando o PowerShell

Configure e use o [Provedor do SQL Server PowerShell](../../../relational-databases/scripting/sql-server-powershell-provider.md). 

> [!NOTE]  
> Para exibir a sintaxe e um exemplo de um cmdlet, use o cmdlet **Get-Help** no ambiente do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] PowerShell. Para obter mais informações, consulte [Get Help SQL Server PowerShell](../../../relational-databases/scripting/get-help-sql-server-powershell.md).  

1. Altere o diretório (**cd**) para a instância do servidor que hospedará a réplica primária.  
  
1. Crie um objeto da réplica de disponibilidade na memória para a réplica primária.  
  
1. Crie um objeto da réplica de disponibilidade na memória para cada réplica secundária.  
  
1. Crie o grupo de disponibilidade.  
  
    > [!NOTE]  
    > O tamanho máximo de um nome de grupo de disponibilidade é 128 caracteres.  

1. Ingresse a nova réplica secundária no grupo de disponibilidade; confira [Ingressar uma réplica secundária em um grupo de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/join-a-secondary-replica-to-an-availability-group-sql-server.md).  
  
1. Para cada banco de dados do grupo de disponibilidade, crie um banco de dados secundário restaurando backups recentes do banco de dados primário, usando RESTORE WITH NORECOVERY.  
  
1. Ingresse cada novo banco de dados secundário no grupo de disponibilidade; confira [Ingressar uma réplica secundária em um grupo de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/join-a-secondary-replica-to-an-availability-group-sql-server.md).  
  
1. (opcional) Use o comando **dir** do Windows para verificar o conteúdo do novo grupo de disponibilidade.  
  
> [!NOTE]  
> Se as contas de serviço [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] das instâncias do servidor forem executadas em diferentes contas de usuário de domínio, em cada instância do servidor, crie um logon para a outra instância do servidor e conceda a permissão CONNECT a esse logon para o ponto de extremidade de espelhamento do banco de dados local.  

### <a name="example"></a><a name="ExampleConfigureGroup"></a> Exemplo
O exemplo doe PowerShell a seguir cria e configura um grupo de disponibilidade simples denominado `<myAvailabilityGroup>` com duas réplicas de disponibilidade e um banco de dados de disponibilidade. O exemplo:  

1. Faz backup do `<myDatabase>` e de seu log de transações.  

1. Restaura o `<myDatabase>` e seu log de transações usando a opção **-NoRecovery** .  

1. Cria uma representação na memória da réplica primária, que será hospedada pela instância local do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] (denominada `PrimaryComputer\Instance`).  

1. Cria uma representação na memória da réplica secundária, que será hospedada por uma instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] (denominada `SecondaryComputer\Instance`).  

1. Cria um grupo de disponibilidade denominado `<myAvailabilityGroup>`.  

1. Une a réplica secundária ao grupo de disponibilidade.  

1. Une o banco de dados secundário ao grupo de disponibilidade.  

```powershell
# Backup my database and its log on the primary  
Backup-SqlDatabase `  
    -Database "<myDatabase>" `  
    -BackupFile "\\share\backups\<myDatabase>.bak" `  
    -ServerInstance "PrimaryComputer\Instance"  
  
Backup-SqlDatabase `  
    -Database "<myDatabase>" `  
    -BackupFile "\\share\backups\<myDatabase>.log" `  
    -ServerInstance "PrimaryComputer\Instance" `  
    -BackupAction Log   
  
# Restore the database and log on the secondary (using NO RECOVERY)  
Restore-SqlDatabase `  
    -Database "<myDatabase>" `  
    -BackupFile "\\share\backups\<myDatabase>.bak" `  
    -ServerInstance "SecondaryComputer\Instance" `  
    -NoRecovery  
  
Restore-SqlDatabase `  
    -Database "<myDatabase>" `  
    -BackupFile "\\share\backups\<myDatabase>.log" `  
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
    -Name "<myAvailabilityGroup>" `  
    -Path "SQLSERVER:\SQL\PrimaryComputer\Instance" `  
    -AvailabilityReplica @($primaryReplica,$secondaryReplica) `  
    -Database "<myDatabase>"  
  
# Join the secondary replica to the availability group.  
Join-SqlAvailabilityGroup -Path "SQLSERVER:\SQL\SecondaryComputer\Instance" -Name "<myAvailabilityGroup>"  
  
# Join the secondary database to the availability group.  
Add-SqlAvailabilityDatabase -Path "SQLSERVER:\SQL\SecondaryComputer\Instance\AvailabilityGroups\<myAvailabilityGroup>" -Database "<myDatabase>"  
```  
  
## <a name="related-tasks"></a><a name="RelatedTasks"></a> Tarefas relacionadas  
 **Para configurar uma instância de servidor para grupos de disponibilidade AlwaysOn**  
  
- [Habilitar e desabilitar Grupos de Disponibilidade AlwaysOn &#40;SQL Server&#41;](~/database-engine/availability-groups/windows/enable-and-disable-always-on-availability-groups-sql-server.md)  
  
- [Criar um ponto de extremidade de espelhamento de banco de dados para grupos de disponibilidade AlwaysOn &#40;SQL Server PowerShell&#41;](~/database-engine/availability-groups/windows/database-mirroring-always-on-availability-groups-powershell.md)  
  
 **Para configurar um grupo de disponibilidade e propriedades de réplica**  
  
- [Alterar o modo de disponibilidade de uma réplica de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/change-the-availability-mode-of-an-availability-replica-sql-server.md)  
  
- [Alterar o modo de failover de uma réplica de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/change-the-failover-mode-of-an-availability-replica-sql-server.md)  
  
- [Criar ou configurar um ouvinte do grupo de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server.md)  
  
- [Configurar a política de failover flexível para controlar condições de failover automático &#40;Grupos de disponibilidade AlwaysOn&#41;](~/database-engine/availability-groups/windows/configure-flexible-automatic-failover-policy.md)  
  
- [Especificar a URL do ponto de extremidade ao adicionar ou modificar uma réplica de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/specify-endpoint-url-adding-or-modifying-availability-replica.md)  
  
- [Configurar backup em réplicas de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/configure-backup-on-availability-replicas-sql-server.md)  
  
- [Configurar o acesso somente leitura em uma réplica de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/configure-read-only-access-on-an-availability-replica-sql-server.md)  
  
- [Configurar o roteamento somente leitura para um grupo de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/configure-read-only-routing-for-an-availability-group-sql-server.md)  
  
- [Alterar o período de tempo limite da sessão de uma réplica de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/change-the-session-timeout-period-for-an-availability-replica-sql-server.md)  
  
 **Para concluir a configuração do grupo de disponibilidade**  
  
- [Unir uma réplica secundária a um grupo de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/join-a-secondary-replica-to-an-availability-group-sql-server.md)  
  
- [Preparar um banco de dados secundário manualmente para um grupo de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/manually-prepare-a-secondary-database-for-an-availability-group-sql-server.md)  
  
- [Unir um banco de dados secundário a um grupo de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/join-a-secondary-database-to-an-availability-group-sql-server.md)  
  
- [Criar ou configurar um ouvinte do grupo de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server.md)  
  
 **Maneiras alternativas de criar um grupo de disponibilidade**  
  
- [Usar o Assistente de Grupo de Disponibilidade &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-availability-group-wizard-sql-server-management-studio.md)  
  
- [Usar a caixa de diálogo Novo Grupo de Disponibilidade &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-new-availability-group-dialog-box-sql-server-management-studio.md)  
  
- [Criar um grupo de disponibilidade &#40;Transact-SQL&#41;](../../../database-engine/availability-groups/windows/create-an-availability-group-transact-sql.md)  
  
 **Para solucionar problemas de configuração dos grupos de disponibilidade AlwaysOn**  
  
- [Solucionar problemas de configuração de grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](~/database-engine/availability-groups/windows/troubleshoot-always-on-availability-groups-configuration-sql-server.md)  
  
- [Solução de problemas de uma operação de adição de arquivos com falha &#40;Grupos de disponibilidade de AlwaysOn&#41;](~/database-engine/availability-groups/windows/troubleshoot-a-failed-add-file-operation-always-on-availability-groups.md)  
  
## <a name="related-content"></a><a name="RelatedContent"></a> Conteúdo relacionado  
  
- **Blogs:**  
  
     [Série de aprendizado do AlwaysOn – HADRON: uso do pool de trabalho para bancos de dados habilitados para HADRON](https://docs.microsoft.com/archive/blogs/psssql/alwayson-hadron-learning-series-worker-pool-usage-for-hadron-enabled-databases)  
  
     [Configurando o AlwaysOn com o SQL Server PowerShell](https://blogs.msdn.microsoft.com/sqlalwayson/2012/02/03/configuring-alwayson-with-sql-server-powershell/)  
  
     [Blogs da equipe do AlwaysOn do SQL Server: o blog oficial da equipe do AlwaysOn do SQL Server](https://blogs.msdn.microsoft.com/sqlalwayson/)  
  
     [Blogs dos engenheiros do CSS SQL Server](https://docs.microsoft.com/archive/blogs/psssql/)  
  
- **Vídeos:**  
  
     [Microsoft SQL Server codinome “Denali” Série AlwaysOn, Parte 1: Introduzindo a próxima geração de solução de alta disponibilidade](https://channel9.msdn.com/Events/TechEd/NorthAmerica/2011/DBI302)  
  
     [Microsoft SQL Server codinome “Denali” Série AlwaysOn, Parte 2: Criando uma solução de alta disponibilidade de missão crítica usando AlwaysOn](https://channel9.msdn.com/Events/TechEd/NorthAmerica/2011/DBI404)  
  
- **Whitepapers:**  
  
     [Guia de soluções AlwaysOn do Microsoft SQL Server para alta disponibilidade e recuperação de desastre](https://go.microsoft.com/fwlink/?LinkId=227600)  
  
     [White papers da Microsoft para SQL Server 2012](https://msdn.microsoft.com/library/hh403491.aspx)  
  
     [White papers da equipe de consultoria do cliente do SQL Server](https://techcommunity.microsoft.com/t5/DataCAT/bg-p/DataCAT/)  
  
## <a name="see-also"></a>Consulte Também  
 [O ponto de extremidade de espelhamento de banco de dados &#40;SQL Server&#41;](../../../database-engine/database-mirroring/the-database-mirroring-endpoint-sql-server.md)   
 [Visão geral dos grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](~/database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)
