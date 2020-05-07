---
title: 'Fazer backup de vários bancos de dados: Armazenamento do Blobs do Azure'
description: Este artigo fornece scripts de exemplo que podem ser usados para automatizar backups no SQL Server para o serviço de Armazenamento de Blobs do Azure usando cmdlets do PowerShell.
titleSuffix: PowerShell
ms.custom: seo-lt-2019
ms.date: 12/17/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
ms.assetid: f7008339-e69d-4e20-9265-d649da670460
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: cd19075f0a9f0d807dd2523f28b46c190e0f981a
ms.sourcegitcommit: 9afb612c5303d24b514cb8dba941d05c88f0ca90
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/28/2020
ms.locfileid: "82220558"
---
# <a name="back-up-multiple-databases-to-azure-blob-storage---powershell"></a>Fazer backup de vários bancos de dados para o Armazenamento de Blobs do Azure – PowerShell

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Este tópico fornece scripts de exemplo que podem ser usados para automatizar backups no serviço do Armazenamento do Blobs do Azure usando os cmdlets do PowerShell.  
  
## <a name="overview-of-powershell-cmdlets-for-backup-and-restore"></a>Visão geral de cmdlets do PowerShell para backup e restauração

**Backup-SqlDatabase** e **Restore-SqlDatabase** são os dois cmdlets principais disponíveis para fazer operações de backup e restauração.

Além disso, há outros cmdlets que podem ser necessários para automatizar backups no Armazenamento de Blobs do Microsoft Azure, como o conjunto de cmdlets **SqlCredential**.

Para obter uma lista de todos os cmdlets disponíveis, confira [Cmdlets do SQL Server](/powershell/module/sqlserver).
  
> [!TIP]  
> Os cmdlets **SqlCredential** são usados em cenários de backup e restauração no Armazenamento de Blobs do Azure. Para obter mais informações sobre as credenciais e seu uso, confira [Backup e restauração do SQL Server com o Serviço de Armazenamento de Blobs do Microsoft Azure](../../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md).
  
### <a name="powershell-for-multi-database-multi-instance-backup-operations"></a>PowerShell para operações de backup com várias instâncias e bancos de dados

As seções a seguir incluem scripts para várias operações, como a criação de uma credencial do SQL em várias instâncias do SQL Server, o backup de todos os bancos de dados de usuário em uma instância do SQL Server, entre outros. Você pode usar esses scripts para automatizar ou agendar operações de backup de acordo com os requisitos do seu ambiente. Os scripts fornecidos aqui são exemplos, e podem ser modificados ou estendidos para seu ambiente.  
  
Estas são as considerações sobre os exemplos de script:  
  
- O SQL Server PowerShell implementa cmdlets para navegação na estrutura do caminho que representa a hierarquia de objetos compatíveis com um provedor do PowerShell. Ao navegar até um nó do caminho, você pode usar outros cmdlets para executar operações básicas no objeto atual.

  Para obter mais informações, consulte [Navigate SQL Server PowerShell Paths](../../relational-databases/scripting/navigate-sql-server-powershell-paths.md).

- Cmdlet **Get-ChildItem**: As informações retornadas pelo **Get-ChildItem** dependem do local em um caminho do SQL Server PowerShell. Por exemplo, se o local estiver no nível do computador, esse cmdlet retornará todas as instâncias do mecanismo de banco de dados do SQL Server instaladas no computador. Ou, se a localização estiver no nível do objeto, como bancos de dados, ele retornará uma lista de objetos de banco de dados. Por padrão, o cmdlet **Get-ChildItem** não retorna nenhum objeto do sistema. Use o parâmetro `–Force` para ver os objetos do sistema.

- Uma conta de armazenamento do Azure e uma credencial do SQL são pré-requisitos necessários e para todas as operações de backup e restauração no serviço de Armazenamento de Blobs do Azure.
  
### <a name="create-a-sql-credential-on-all-instances-of-sql-server"></a>Criar uma credencial do SQL em todas as instâncias do SQL Server

O script a seguir pode ser usado para criar uma credencial do SQL genérica em todas as instâncias do SQL Server em um computador. Se já houver uma credencial com o mesmo nome em uma das instâncias do computador, o script mostrará o erro e continuará.  
  
```powershell
# load the sqlps module
import-module sqlps  
  
# set parameters
$sqlPath = "sqlserver:\sql\$($env:COMPUTERNAME)"
$storageAccount = "<myStorageAccount>"  
$storageKey = "<myStorageAccessKey>"  
$secureString = ConvertTo-SecureString $storageKey -AsPlainText -Force  
$credentialName = "myCredential-$(Get-Random)"

Write-Host "Generate credential: " $credentialName
  
#cd to sql server and get instances  
cd $sqlPath
$instances = Get-ChildItem

#loop through instances and create a SQL credential, output any errors
foreach ($instance in $instances)  {
    try {
        $path = "$($sqlPath)\$($instance.DisplayName)\credentials"
        New-SqlCredential -Name $credentialName -Identity $storageAccount -Secret $secureString -Path $path -ea Stop | Out-Null
        Write-Host "...generated credential $($path)\$($credentialName)."  }
    catch { Write-Host $_.Exception.Message } }
```

> [!NOTE]
> A instrução `-ea Stop | Out-Null` é usada para a saída de exceção definida pelo usuário. Se você preferir mensagens de erro padrão do PowerShell, essa instrução poderá ser removida. 

### <a name="remove-a-sql-credential-from-all-instances-of-sql-server"></a>Remover uma credencial do SQL de todas as instâncias do SQL Server

O script a seguir pode ser usado para remover uma credencial específica de todas as instâncias do SQL Server instaladas no computador. Se a credencial não existir em uma instância específica, uma mensagem de erro será exibida e o script continuará até todas as instâncias serem verificadas.  
  
```powershell
import-module sqlps

$sqlPath = "sqlserver:\sql\$($env:COMPUTERNAME)"
$credentialName = "<myCredential>"

Write-Host "Delete credential: " $credentialName

cd $sqlPath
$instances = Get-ChildItem

#loop through instances and delete a SQL credential
foreach ($instance in $instances)  {
    try {
        $path = "$($sqlPath)\$($instance.DisplayName)\credentials\$($credentialName)"
        Remove-SqlCredential -Path $path -ea Stop | Out-Null
        Write-Host "...deleted credential $($path)."  }
    catch { Write-Host $_.Exception.Message } }
```  
  
### <a name="full-backup-for-all-databases"></a>Backup completo de todos os bancos de dados

O script a seguir cria backup de todos os bancos de dados no computador. Isso inclui os bancos de dados de usuário e o banco de dados de sistema **msdb** . O script filtra os bancos de dados de sistema **tempdb** e **model** .  
  
```powershell
import-module sqlps  

$sqlPath = "sqlserver:\sql\$($env:COMPUTERNAME)"
$storageAccount = "<myStorageAccount>"  
$blobContainer = "<myBlobContainer>"  
$backupUrlContainer = "https://$storageAccount.blob.core.windows.net/$blobContainer/"  
$credentialName = "<myCredential>"

Write-Host "Backup database: " $backupUrlContainer
  
cd $sqlPath
$instances = Get-ChildItem

#loop through instances and backup all databases (excluding tempdb and model)
foreach ($instance in $instances)  {
    $path = "$($sqlPath)\$($instance.DisplayName)\databases"
    $databases = Get-ChildItem -Force -Path $path | Where-object {$_.name -ne "tempdb" -and $_.name -ne "model"}

    foreach ($database in $databases) {
        try {
            $databasePath = "$($path)\$($database.Name)"
            Write-Host "...starting backup: " $databasePath
            Backup-SqlDatabase -Database $database.Name -Path $path -BackupContainer $backupUrlContainer -SqlCredential $credentialName -Compression On
            Write-Host "...backup complete."  }
        catch { Write-Host $_.Exception.Message } } }
```  
  
### <a name="full-backup-for-system-databases-only-on-a-specific-instance-of-sql-server"></a>Backup completo apenas dos bancos de dados do sistema em uma instância específica do SQL Server

O script completo a seguir pode ser usado para fazer backup dos bancos de dados **master** e **msdb** em uma instância nomeada do SQL Server. O mesmo script pode ser usado para qualquer instância, com a alteração do valor do parâmetro da instância. A instância padrão do SQL Server é chamada `DEFAULT`.
  
```powershell
import-module sqlps  

$sqlPath = "sqlserver:\sql\$($env:COMPUTERNAME)"
$instanceName = "DEFAULT"
$storageAccount = "<myStorageAccount>"  
$blobContainer = "<myBlobContainer>"  
$backupUrlContainer = "https://$storageAccount.blob.core.windows.net/$blobContainer/"  
$credentialName = "<myCredential>"

Write-Host "Backup database: " $instanceName " to " $backupUrlContainer
  
cd "$($sqlPath)\$($instanceName)"

#loop through instance and backup specific databases
$databases = "master", "msdb"  
foreach ($database in $databases) {
    try {
        Write-Host "...starting backup: " $database
        Backup-SqlDatabase -Database $database -BackupContainer $backupUrlContainer -SqlCredential $credentialName -Compression On
        Write-Host "...backup complete." }
    catch { Write-Host $_.Exception.Message } }
```  
  
## <a name="see-also"></a>Confira também

[Backup e restauração do SQL Server no serviço de Armazenamento de Blobs do Azure](../../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md)

[Solução de problemas e melhores práticas de backup do SQL Server para URL](../../relational-databases/backup-restore/sql-server-backup-to-url-best-practices-and-troubleshooting.md)
