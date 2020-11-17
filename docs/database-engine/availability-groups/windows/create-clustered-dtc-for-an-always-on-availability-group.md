---
title: Criar recurso DTC clusterizado para um grupo de disponibilidade
description: Este tópico descreve uma configuração completa de um recurso DTC clusterizado para o Grupo de Disponibilidade AlwaysOn do SQL Server.
ms.custom: seodec18
ms.date: 08/30/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: how-to
ms.assetid: 0e332aa4-2c48-4bc4-a404-b65735a02cea
author: cawrites
ms.author: chadam
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 306d77b9bf980179ff69514e0e609fc109c78632
ms.sourcegitcommit: 54cd97a33f417432aa26b948b3fc4b71a5e9162b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/13/2020
ms.locfileid: "94584358"
---
# <a name="create-clustered-dtc-resource-for-an-always-on-availability-group"></a>Criar recurso DTC clusterizado para um grupo de disponibilidade Always On

[!INCLUDE[sql windows only](../../../includes/applies-to-version/sql-windows-only.md)]

Este tópico descreve uma configuração completa de um recurso DTC clusterizado para o Grupo de Disponibilidade AlwaysOn do SQL Server. A configuração completa pode levar até uma hora para ser concluída. 

O passo a passo cria um recurso DTC clusterizado e os Grupos de Disponibilidade do SQL Server para se alinharem aos requisitos descritos em [Cluster DTC para Grupos de Disponibilidade do SQL Server](../../../database-engine/availability-groups/windows/cluster-dtc-for-sql-server-2016-availability-groups.md).

O passo a passo usa scripts do PowerShell e T-SQL (Transact-SQL).  Muitos dos scripts T-SQL exigem que o **Modo SQLCMD** seja habilitado.  Para obter mais informações sobre o **Modo SQLCMD**, consulte [Habilitar script SQLCMD no Editor de Consultas](../../../ssms/scripting/edit-sqlcmd-scripts-with-query-editor.md).  O módulo do PowerShell **FailoverClusters** deve ser importado.  Para obter mais informações sobre como importar um módulo do PowerShell, confira [Importar um módulo do PowerShell](/powershell/scripting/developer/module/importing-a-powershell-module).  Este passo a passo se baseia no seguinte:
- Todos os requisitos de [Pré-requisitos, restrições e recomendações para Grupos de Disponibilidade AlwaysOn (SQL Server)](../../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md) foram atendidos.  
- O domínio é `contoso.lab`.
- O usuário tem a permissão de objetos Create Computer na UO em que o recurso de Nome de Rede do DTC será criado.
- O usuário é um usuário de domínio que tem direitos de administrador em todos os nós do cluster.
- Um compartilhamento de arquivos chamado `sqlbackups` foi criado para backups.
- As instâncias padrão do SQL Server são nomeadas `SQLNODE1` e `SQLNODE2`.
- A mesma conta de serviço é usada em todas as instâncias do SQL Server.
- O usuário é um membro da função fixa sysadmin do SQL Server em todas as instâncias do SQL Server.
- O resultado padrão das transações que o DTC não puder resolver será definido como `presume commit`.
- O ponto de extremidade de espelhamento usará a porta `5022`.
- Não existem outros Grupos de Disponibilidade nem recursos DTC clusterizados.
- Detalhes do cluster (existente):
  - Nome: `Cluster`
  - Nome da rede: `Cluster Network 1`
  - Nós: `SQLNODE1, SQLNODE2`
  - Armazenamento compartilhado: `Cluster Disk 3` (pertencentes a `SQLNODE1`)
- Detalhes do cluster (a ser criado):
  - Recurso de nome de rede: `DTCnet1`
  - Recurso de nome de rede do DTC: `DTC1`
  - Recurso Disco Físico do DTC: `DTCDisk1`
  - Recurso de IP e sub-rede do DTC: `192.168.2.54`, `255.255.255.0`
  - Recurso de IP do DTC: `DTCIP1`

## <a name="1-check-operating-system"></a>1. Verificar sistema operacional
Para as transações distribuídas com suporte, o [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] deve ser executado no Windows Server 2016 ou Windows Server 2012 R2.  Para o Windows Server 2012 R2, é necessário instalar a atualização na KB3090973 disponível em [https://support.microsoft.com/kb/3090973](https://support.microsoft.com/kb/3090973).  Esse script verificará a versão do sistema operacional e se o hotfix 3090973 precisa ser instalado.  Execute o Script do PowerShell a seguir no `SQLNODE1`.

```powershell  
# A few OS checks

\<#
Script: 
    1) is re-runnable 
    2) will work on any node in the cluster, and 
    3) will execute against every node in the cluster
#>

$nodes = (Get-ClusterNode).Name;
foreach ($node in $nodes) {

    # At least 2012 R2
    $os = (Get-WmiObject -class Win32_OperatingSystem -ComputerName $node).caption;
    IF($os -like "*2012 R2*" -or $os -like "*2016*")
    {
        Write-Host "$os is supported on $node.";
    }
    ELSE
    {
        Write-Host "STOP!  $os is not supported on $node.";
    }
    
    # KB 3090973
    IF($os -like "*2012 R2*")
    {
        $kb = Get-Hotfix -ComputerName $node | Where {$_.HotFixID -eq 'KB3090973'};
        IF($kb)
        {
            Write-Host "KB3090973 is installed on $node."
        }
        ELSE
        {
            Write-Host "HotFixID KB3090973 must be applied on $node.  See https://support.microsoft.com/kb/3090973 for additional information and to download the hotfix.";
        }
    }
    ELSE
    {
        Write-Host "KB3090973 is not applicable to $os on $node."
    }
}
```  
## <a name="2---configure-firewall-rules"></a>2.   Configurar regras de firewall
Esse script vai configurar o firewall para permitir o tráfego do DTC em cada SQL Server que hospeda uma réplica do grupo de disponibilidade, bem como em qualquer outro servidor que participe da transação distribuída.  O script também vai configurar o firewall para permitir conexões para o ponto de extremidade de espelhamento de banco de dados.  Execute o Script do PowerShell a seguir no `SQLNODE1`.

```powershell  
# Configure Firewall

\<#
Script: 
    1) is re-runnable 
    2) will work on any node in the cluster, and 
    3) will execute against every node in the cluster
#>

$nodes = (Get-ClusterNode).Name;
foreach ($node in $nodes) {
    Get-NetFirewallRule -CimSession $node -DisplayGroup 'Distributed Transaction Coordinator' -Enabled False -ErrorAction SilentlyContinue | Enable-NetFirewallRule;
    New-NetFirewallRule -CimSession $node -DisplayName 'SQL Server Mirroring' -Description 'Port 5022 for SQL Server Mirroring' -Action Allow -Direction Inbound -Protocol TCP -LocalPort 5022 -RemotePort Any -LocalAddress Any -RemoteAddress Any;
    };
```  
## <a name="3--configure-in-doubt-xact-resolution"></a>3.  Configurar **in-doubt xact resolution** 
Esse script vai configurar a opção **in-doubt xact resolution** de configuração do servidor como "presume commit" para as transações incertas.  Execute o script T-SQL a seguir no SSMS (SQL Server Management Studio) para `SQLNODE1`, no **modo SQLCMD**.

```sql  
/*******************************************************************
    Execute script in its entirety on SQLNODE1 in SQLCMD mode
*******************************************************************/

-- Configure in-doubt xact resolution on all SQL Server instances to presume commit
IF (SELECT CAST(value_in_use as bit) FROM sys.configurations WITH (NOLOCK) WHERE [name] = N'show advanced options') = 0
BEGIN   
    EXEC sp_configure 'show advanced options', 1;
    RECONFIGURE;
END

-- Configure the server to presume commit for in-doubt transactions.
IF (SELECT CAST(value as bit) FROM sys.configurations WITH (NOLOCK) WHERE [name] = N'in-doubt xact resolution') <> 1
BEGIN   
    EXEC sp_configure 'in-doubt xact resolution', 1;
    RECONFIGURE;
END
GO
-----------------------------------------------------------------------------

:connect SQLNODE2
IF (SELECT CAST(value_in_use as bit) FROM sys.configurations WITH (NOLOCK) WHERE [name] = N'show advanced options') = 0
BEGIN   
    EXEC sp_configure 'show advanced options', 1;
    RECONFIGURE;
END

-- Configure the server to presume commit for in-doubt transactions.
IF (SELECT CAST(value as bit) FROM sys.configurations WITH (NOLOCK) WHERE [name] = N'in-doubt xact resolution') <> 1
BEGIN   
    EXEC sp_configure 'in-doubt xact resolution', 1;
    RECONFIGURE;
END
GO
-----------------------------------------------------------------------------
```

## <a name="4-create-test-databases"></a>4. Criar bancos de dados de teste
O script criará um banco de dados chamado `AG1` no `SQLNODE1` e um banco de dados chamado `dtcDemoAG1` no `SQLNODE2`.  Execute o script T-SQL a seguir no SSMS para `SQLNODE1` no **modo SQLCMD**.

```sql  
/*******************************************************************
    Execute script in its entirety on SQLNODE1 in SQLCMD mode
*******************************************************************/

-- On SQLNODE1 
USE master;
SET NOCOUNT ON;

IF  EXISTS (SELECT * FROM sys.databases WHERE name = N'AG1')
BEGIN
    DROP DATABASE AG1;
END
GO

CREATE DATABASE AG1;
ALTER DATABASE AG1 SET RECOVERY FULL WITH NO_WAIT;
ALTER AUTHORIZATION ON DATABASE::AG1 to sa;
GO

USE AG1;
CREATE TABLE [dbo].[Names] (
        [Name] [varchar](64) NULL,
        [EditDate] datetime
        );

INSERT Names
VALUES ('AG1', GETDATE());
GO


-- Against SQNODE2
:connect SQLNODE2
USE master;
SET NOCOUNT ON;

IF  EXISTS (SELECT * FROM sys.databases WHERE name = N'dtcDemoAG1')
BEGIN
    DROP DATABASE dtcDemoAG1;
END
GO

CREATE DATABASE dtcDemoAG1;
ALTER DATABASE dtcDemoAG1 SET RECOVERY SIMPLE WITH NO_WAIT;
ALTER AUTHORIZATION ON DATABASE::dtcDemoAG1 to sa;
GO

USE dtcDemoAG1;
CREATE TABLE [dbo].[Names] (
        [Name] [varchar](64) NULL,
        [EditDate] datetime
        );
GO    
----------------------------------------------------------------
```
## <a name="5---create-endpoints"></a>5.   Criar pontos de extremidade
Esse script criará um ponto de extremidade chamado `AG1_endpoint` que escuta na porta TCP `5022`.  Execute o script T-SQL a seguir no SSMS para `SQLNODE1` no **modo SQLCMD**.

```sql  
/**********************************************
Execute on SQLNODE1 in SQLCMD mode
**********************************************/

-- Create endpoint on server instance that hosts the primary replica:
IF NOT EXISTS (SELECT * FROM sys.database_mirroring_endpoints)
BEGIN
    CREATE ENDPOINT AG1_endpoint
    AUTHORIZATION [sa]
        STATE=STARTED 
        AS TCP (LISTENER_PORT=5022) 
        FOR DATABASE_MIRRORING (ROLE=ALL);
END
GO
-----------------------------------------------------------------------------

:connect SQLNODE2
IF NOT EXISTS (SELECT * FROM sys.database_mirroring_endpoints)
BEGIN
    CREATE ENDPOINT AG1_endpoint
    AUTHORIZATION [sa]
        STATE=STARTED 
        AS TCP (LISTENER_PORT=5022) 
        FOR DATABASE_MIRRORING (ROLE=ALL);
END
GO
-----------------------------------------------------------------------------
```

## <a name="6---prepare-databases-for-availability-group"></a>6.   Preparar bancos de dados para o Grupo de Disponibilidade
O script fará backup do `AG1` no `SQLNODE1` e o restaurará no `SQLNODE2`.  Execute o script T-SQL a seguir no SSMS para `SQLNODE1` no **modo SQLCMD**.

```sql  
/*******************************************************************
    Execute script in its entirety on SQLNODE1 in SQLCMD mode
*******************************************************************/

-- Backup database
BACKUP DATABASE AG1 
TO DISK = N'\\sqlnode1\sqlbackups\AG1.bak' 
WITH FORMAT, STATS = 10;

-- Backup transaction log
BACKUP LOG AG1
TO DISK = N'\\sqlnode1\sqlbackups\AG1_Log.bak'
WITH FORMAT, STATS = 10;
GO


-- Restore database and logs on secondary WITH NORECOVERY
:connect SQLNODE2
USE [master]
RESTORE DATABASE AG1 
FROM DISK = N'\\sqlnode1\sqlbackups\AG1.bak' 
WITH NORECOVERY, STATS = 10;

RESTORE LOG AG1 
FROM DISK = N'\\sqlnode1\sqlbackups\AG1_Log.bak'
WITH NORECOVERY, STATS = 10;
GO
```

## <a name="7---create-availability-group"></a>7.   Criar grupo de disponibilidade
[!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] deve ser criado com o comando **CREATE AVAILABILITY GROUP** e a cláusula **WITH DTC_SUPPORT = PER_DB**.  No momento, você não pode alterar um grupo de disponibilidade existente.  O Assistente de Novo Grupo de Disponibilidade não permite habilitar o suporte a DTC para um novo Grupo de Disponibilidade.  O script a seguir criará o novo Grupo de Disponibilidade e unirá o secundário.  Execute o script T-SQL a seguir no SSMS para `SQLNODE1` no **modo SQLCMD**.

```sql  
/*******************************************************************
    Execute script in its entirety on SQLNODE1 in SQLCMD mode
*******************************************************************/

--  Create Availability Group on SQLNODE1 
USE master;
CREATE AVAILABILITY GROUP DTCAG1
WITH (DTC_SUPPORT = PER_DB) 
FOR DATABASE AG1
REPLICA ON 
  'SQLNODE1' WITH
     (
     ENDPOINT_URL = 'TCP://SQLNODE1.contoso.lab:5022', 
     AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,
     FAILOVER_MODE = MANUAL
     ),
  'SQLNODE2' WITH 
     (
     ENDPOINT_URL = 'TCP://SQLNODE2.contoso.lab:5022',
     AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,
     FAILOVER_MODE = MANUAL
     ); 
GO


-- SQLNODE2
-- Join secondary replica to the Availability Group 
:connect SQLNODE2
ALTER AVAILABILITY GROUP DTCag1 JOIN;

-- Join database to the Availability Group
ALTER DATABASE AG1 SET HADR AVAILABILITY GROUP = DTCAG1;
GO
```

> [!IMPORTANT]
> Não é possível habilitar o DTC em um [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] existente.  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] aceitará a seguinte sintaxe para um Grupo de Disponibilidade existente:  
> 
> USE master;    
> ALTERAR GRUPO DE DISPONIBILIDADE \<availability_group\>  
> SET (DTC_Support = Per_DB)  
> 
> No entanto, na verdade, nenhuma alteração de configuração será feita.  É possível confirmar a configuração **dtc_support** com a seguinte consulta T-SQL:  
> 
> Selecione o nome dtc_support em availability_groups  
> 
> A única maneira de habilitar o suporte a DTC em um Grupo de Disponibilidade é criando um Grupo de Disponibilidade com o Transact-SQL.
 
## <a name="8--prepare-cluster-resources"></a><a name="ClusterDTC"></a>8.  Preparar recursos de cluster

Esse script vai preparar os recursos dependentes do DTC: Disco e IP.  O armazenamento compartilhado será adicionado ao Windows Cluster.  Os recursos de rede serão criados e o DTC será criado e transformado em um recurso para o Grupo de Disponibilidade.  Execute o Script do PowerShell a seguir no `SQLNODE1`. Obrigado, [Allan Hirt](https://sqlha.com/2013/03/12/how-to-properly-configure-dtc-for-clustered-instances-of-sql-server-with-windows-server-2008-r2/), pelo script!

```powershell  
# Create a clustered Microsoft Distributed Transaction Coordinator properly in the resource group with SQL Server

\<#----------------------------------- Begin User Input -----------------------------------#>
$AGgrp = "DTCag1";                          # Name of the WSFC resource group that will contain the DTC resource

$WSFC = (Get-Cluster).Name;                 # Windows Failover Cluster name
$DTCnetwk = "Cluster Network 1"             # WSFC Network to use for the DTC IP address

$ClusterAvailableDisk = "Cluster Disk 3";   # Designated disk that can support failover clustering and is visible to all nodes, but not yet part of the set of clustered disks
$DTCdisk = "DTCDisk1";                      # Name of the disk to be used with DTC

$DTCipresnm = "DTCIP1";                     # WSFC Friendly Name of the DTC's IP resource 
$DTCipaddr = "192.168.2.54";                # IP address of the DTC resource 
$DTCsubnet = "255.255.255.0";               # Subnet for the DTC IP address 
$DTCnetnm = "DTCNet1";                      # WSFC Friendly Name of the Network Name resource
$DTCresnm = "DTC1";                         # Name of the WSFC DTC Network Name resource; Name must be unique in AD
\<#------------------------------------ End User Input ------------------------------------#>


# Make a new disk available for use in a failover cluster.
Get-ClusterAvailableDisk | Where {$_.Name -eq $ClusterAvailableDisk} | Add-ClusterDisk;

# Rename disk
$resource = Get-ClusterResource $ClusterAvailableDisk; $resource.Name = $DTCdisk;

# Create the IP resource
Add-ClusterResource -Name $DTCipresnm -ResourceType "IP Address" -Group $AGgrp;

# Set the network to use, IP address, and subnet
# All three have to be configured at the same time
$DTCIPres = Get-ClusterResource $DTCipresnm;
$ntwk = New-Object Microsoft.FailoverClusters.PowerShell.ClusterParameter $DTCipres,Network,$DTCnetwk;
$ipaddr = New-Object Microsoft.FailoverClusters.PowerShell.ClusterParameter $DTCipres,Address,$DTCipaddr;
$subnet = New-Object Microsoft.FailoverClusters.PowerShell.ClusterParameter $DTCipres,SubnetMask,$dtcsubnet;

$setdtcipparams = $ntwk,$ipaddr,$subnet;
$setdtcipparams | Set-ClusterParameter;

# Create the Network Name resource
Add-ClusterResource $DTCnetnm -ResourceType "Network Name" -Group $AGgrp;

# Set the value for the Network Name resource
Get-ClusterResource $DTCnetnm | Set-ClusterParameter DnsName $DTCresnm;

# Add the IP address as a depenency of the Network Name resource
Add-ClusterResourceDependency $DTCnetnm $DTCipresnm;

# Create the Distributed Transaction Coordinator resource
Add-ClusterResource $DTCresnm -ResourceType "Distributed Transaction Coordinator" -Group $AGgrp;

# Add the Network Name as a depenency of the DTC resource
Add-ClusterResourceDependency $DTCresnm $DTCnetnm;

# Move the disk into the resource group with SQL Server
Move-ClusterResource -Name $DTCdisk -Group $AGgrp;

# Add the disk as a depenency of the DTC resource
Add-ClusterResourceDependency $DTCresnm $DTCdisk;

# Bring the IP resource online
Start-ClusterResource $DTCipresnm;

# Bring the Network Name resource online
Start-ClusterResource $DTCnetnm;

# Bring the DTC resource online
Start-ClusterResource $DTCresnm;
```  

## <a name="9---enable-network-dtc"></a>9.   Habilitar o DTC de Rede 

O script a seguir habilitará o Acesso de DTC de Rede do serviço DTC clusterizado para permitir que computadores remotos se inscrevam em transações distribuídas pela rede.  Execute o Script do PowerShell a seguir no `SQLNODE1`.

```powershell  
# Enable Network DTC access for the clustered DTC service

\<#
Script: 
    1) is re-runnable 
    2) will work on any node in the cluster, and 
    3) will execute against every node in the cluster
#>

# Enter Name of DTC resource

$DtcName = "DTC1";
\<# ------- End of User Input ------- #>

[bool]$restart = 0;
$node = (Get-ClusterResource -Name $DtcName).OwnerNode.Name;
$DtcSettings = Get-DtcNetworkSetting -DtcName $DtcName;

IF ($DtcSettings.InboundTransactionsEnabled -eq $false)   
{
    Set-DtcNetworkSetting -CimSession $node -DtcName $DtcName -AuthenticationLevel "Mutual" -InboundTransactionsEnabled $true -Confirm:$false;
    $restart = 1;
}

IF ($DtcSettings.OutboundTransactionsEnabled -eq $false)   
{
    Set-DtcNetworkSetting -CimSession $node -DtcName $DtcName -AuthenticationLevel "Mutual" -OutboundTransactionsEnabled $true -Confirm:$false;
    $restart = 1;
}

IF ($restart -eq 1)
{
    Stop-Dtc -CimSession $node -DtcName $DTCname -Confirm:$false;
    Start-Dtc -CimSession $node -DtcName $DTCname;
}
```  

## <a name="10--disable-and-stop-the-local-dtc-service-on-each-node"></a>10.  Desabilitar e interromper o serviço DTC local em cada nó

Para garantir que as transações distribuídas usem o recurso DTC clusterizado, desabilite o DTC local em ambos os nós.  O script a seguir desabilitará e interromperá o serviço DTC local em cada nó.  Execute o Script do PowerShell a seguir no `SQLNODE1`.
```powershell  
# Disable local DTC service

\<#
Script: 
    1) is re-runnable 
    2) will work on any node in the cluster, and 
    3) will execute against every node in the cluster
#>

$DTCname = 'Local';
$nodes = (Get-ClusterNode).Name;

 foreach ($node in $nodes) {

    $service = Get-WmiObject -class Win32_Service -computername $node -Filter "Name='MSDTC'";
    IF ($service.StartMode -ne 'Disabled')
    {
        $service.ChangeStartMode('Disabled');
    }
    
    IF ($service.State -ne 'Stopped')
    {
        $service.StopService();
    }
}
```  

## <a name="11--cycle-the-ssnoversion-service-for-each-instance"></a>11.  Realize um ciclo do serviço [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] em cada instância

Com o serviço DTC clusterizado totalmente configurado, será necessário interromper e reiniciar cada instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] no Grupo de Disponibilidade para garantir que o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] seja inscrito para usar esse serviço DTC.

Na primeira vez em que o serviço [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] exigir uma transação distribuída, ele é inscrito em um serviço DTC. O serviço do SQL Server continuará a usar o serviço DTC até que ele seja reiniciado. Se um serviço DTC clusterizado estiver disponível, o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] será inscrito no serviço DTC clusterizado. Se um serviço DTC clusterizado não estiver disponível, o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] será inscrito no serviço DTC local. Para verificar se o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] é inscrito no serviço DTC clusterizado, interrompa e reinicie cada instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. 

Siga as etapas contidas no script T-SQL abaixo:
```sql  
/*
Gracefully cycle the SQL Server service and failover the Availability Group
    a.  On SQLNODE2, cycle the SQL Server service from SQL Server Configuration Manger

    b.  On SQLNODE2 failover the Availability Group to SQLNODE2
        Execute T-SQL script, below, on SQLNODE2 (Use Results to Text)

    c.  On SQLNODE1, cycle the SQL Server service from SQL Server Configuration Manger

    d.  On SQLNODE1 failover the Availability Group to SQLNODE1 once the databases are back in sync.
        Execute T-SQL script, below, on SQLNODE1 (Use Results to Text)
*/

SET NOCOUNT ON;

-- Ensure replica is secondary
IF (
SELECT rs.is_primary_replica 
    FROM sys.availability_groups ag
    JOIN sys.dm_hadr_database_replica_states rs
    ON  ag.group_id = rs.group_id
    WHERE ag.name = N'DTCag1'
    AND rs.is_local = 1) = 0
BEGIN
    -- Wait for SYNCHRONIZED state
    DECLARE @ctr tinyint = 0;
    declare @msg varchar(128);
    WHILE (SELECT synchronization_state 
        FROM sys.availability_groups ag
        JOIN sys.dm_hadr_database_replica_states rs
        ON  ag.group_id = rs.group_id
        WHERE ag.name = N'DTCag1'
        AND rs.is_primary_replica = 0
        AND rs.is_local = 1) <> 2
    BEGIN
        WAITFOR DELAY '00:00:01'
        SET @ctr += 1
        SET @msg = 'Waiting for databases to become synchronized. Duration in seconds: ' + cast(@ctr AS varchar(3))
        RAISERROR (@msg, 0, 1) WITH NOWAIT
    END

    ALTER AVAILABILITY GROUP DTCAG1 FAILOVER;
    SELECT 'Failover complete' AS [Sucess]
END
ELSE BEGIN
    SELECT 'This instance is the primary replica.  Connect to the secondary replica and try again.' AS [Error]
END

```

## <a name="12--test-configuration"></a>12.  Testar a configuração

Esse teste usa um servidor vinculado do `SQLNODE1` para o `SQLNODE2` para criar uma transação distribuída.  Garanta que a réplica primária do Grupo de Disponibilidade está no `SQLNODE1`. Para testar a configuração, você vai:

- Criar servidores vinculados
- Executar uma transação distribuída

### <a name="create-linked-servers"></a>Criar servidores vinculados  
O script a seguir criará dois servidores vinculados no `SQLNODE1`.  Execute o script T-SQL a seguir no SSMS para `SQLNODE1`.

```sql  
-- SQLNODE1
IF NOT EXISTS (SELECT * FROM sys.servers where name = N'SQLNODE1')
BEGIN
    EXEC master.dbo.sp_addlinkedserver @server = N'SQLNODE1';   
END

IF NOT EXISTS (SELECT * FROM sys.servers where name = N'SQLNODE2')
BEGIN
    EXEC master.dbo.sp_addlinkedserver @server = N'SQLNODE2';   
END
 ```

### <a name="execute-a-distributed-transaction"></a>Executar uma transação distribuída
Esse script primeiro retornará as estatísticas atuais de transação do DTC.  Em seguida, o script executará uma transação distribuída usando bancos de dados no `SQLNODE1` e `SQLNODE2`.  Em seguida, o script retornará novamente estatísticas de transação do DTC que agora deverão ter uma contagem maior.  Conecte-se fisicamente ao `SQLNODE1` e execute o script T-SQL a seguir no SSSMS para `SQLNODE1` no **modo SQLCMD**.

```sql  
/*******************************************************************
    Execute script in its entirety on SQLNODE1 in SQLCMD mode
    Must be physically connected to SQLNODE1
*******************************************************************/

USE AG1;
SET NOCOUNT ON;

-- Get Baseline
!! Powershell; $DtcNameC = Get-DtcClusterDefault; Get-DtcTransactionsStatistics -DtcName $DtcNameC;

SET XACT_ABORT ON
BEGIN DISTRIBUTED TRANSACTION
    INSERT INTO SQLNODE1.[AG1].[dbo].[Names] VALUES ('TestValue1', GETDATE());
    INSERT INTO SQLNODE2.[dtcDemoAG1].[dbo].[Names] VALUES ('TestValue2', GETDATE());
COMMIT TRAN
GO

-- Review DTC Transaction Statistics
!! Powershell; $DtcNameC = Get-DtcClusterDefault; Get-DtcTransactionsStatistics -DtcName $DtcNameC;
```

> [!IMPORTANT]
> A instrução `USE AG1` deve ser executada para garantir que o contexto do banco de dados é definido como `AG1`.  Caso contrário, você receberá a seguinte mensagem de erro: "O contexto da transação está sendo usado por outra sessão."