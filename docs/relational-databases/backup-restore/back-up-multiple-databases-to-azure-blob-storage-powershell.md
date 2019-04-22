---
title: Fazer backup de vários bancos de dados para o armazenamento de Blobs do Azure – PowerShell | Microsoft Docs
ms.custom: ''
ms.date: 05/21/2016
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
ms.assetid: f7008339-e69d-4e20-9265-d649da670460
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 09e32f92112844e8a291d212e271281636df55e1
ms.sourcegitcommit: aa4f594ec6d3e85d0a1da6e69fa0c2070d42e1d8
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2019
ms.locfileid: "59242464"
---
# <a name="back-up-multiple-databases-to-azure-blob-storage---powershell"></a>Fazer backup de vários bancos de dados para o Armazenamento de Blobs do Azure – PowerShell
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Este tópico fornece scripts de exemplo que podem ser usados para automatizar backups no serviço do armazenamento do Blob do Windows Azure usando os cmdlets do PowerShell.  
  
## <a name="overview-of-powershell-cmdlets-for-backup-and-restore"></a>Visão geral de cmdlets do PowerShell para backup e restauração  
 **Backup-SqlDatabase** e **Restore-SqlDatabase** são os dois cmdlets principais disponíveis para fazer operações de backup e restauração. Além disso, há outros cmdlets que podem ser necessários para automatizar backups no armazenamento do Blob do Windows Azure, como o conjunto de cmdlets **SqlCredential** . A seguir, é apresentada uma lista de cmdlets do PowerShell disponíveis no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] que são usados em operações de backup e restauração:  
  
 Backup-SqlDatabase  
 Este cmdlet é usado para criar um backup do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 Restore-SqlDatabase  
 Usado para restaurar um banco de dados.  
  
 New-SqlCredential  
 Este cmdlet é usado para criar uma Credencial SQL a ser usada para o backup do SQL Server no armazenamento do Windows Azure. Para obter mais informações sobre credenciais e seu uso no backup e na restauração do SQL Server, veja [Backup e restauração do SQL Server com o Serviço de Armazenamento de Blobs do Microsoft Azure](../../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md).  
  
 Get-SqlCredential  
 Este cmdlet é usado para recuperar o objeto Credential e suas propriedades.  
  
 Remove-SqlCredential  
 Exclui o objeto Credencial SQL  
  
 Set-SqlCredential  
 Este cmdlet é usado para alterar ou definir as propriedades do objeto SQL Credential.  
  
> [!TIP]  
>  Os cmdlets Credential são usados no backup e na restauração para cenários de armazenamento de Blob do Windows Azure.  
  
### <a name="powershell-for-multi-database-multi-instance-backup-operations"></a>PowerShell para operações de backup com várias instâncias e bancos de dados  
 As seções a seguir incluem scripts para várias operações, como a criação de uma Credencial SQL em várias instâncias do SQL Server, fazendo backup de todos os bancos de dados de usuário em uma instância do SQL Server etc. Você pode usar esses scripts para automatizar ou agendar operações de backup de acordo com os requisitos do seu ambiente. Os scripts fornecidos aqui são exemplos, e podem ser modificados ou estendidos para seu ambiente.  

[!INCLUDE[Freshness](../../includes/paragraph-content/fresh-note-steps-feedback.md)]

 Estas são as considerações sobre os exemplos de script:  
  
1.  **Navegar em caminhos do SQL Server PowerShell:** O Windows PowerShell implementa cmdlets para navegar na estrutura do caminho que representa a hierarquia de objetos por um provedor do PowerShell. Ao navegar até um nó do caminho, você pode usar outros cmdlets para executar operações básicas no objeto atual.  
  
2.  Cmdlet **Get-ChildItem**: As informações retornadas pelo **Get-ChildItem** dependem do local em um caminho do SQL Server PowerShell. Por exemplo, se o local estiver no nível do computador, esse cmdlet retornará todas as instâncias do mecanismo de banco de dados do SQL Server instaladas no computador. Como outro exemplo, se o local estiver no nível do objeto, como os bancos de dados, este cmdlet retornará uma lista de objetos de banco de dados.  Por padrão, o cmdlet **Get-ChildItem** não retorna nenhum objeto do sistema.  Usando o parâmetro -Force, você poderá ver os objetos do sistema.  
  
     Para obter mais informações, consulte [Navigate SQL Server PowerShell Paths](../../relational-databases/scripting/navigate-sql-server-powershell-paths.md).  
  
3.  Embora cada exemplo de código possa ser testado independentemente com a alteração dos valores de variáveis, a criação de uma conta de armazenamento do Windows Azure e de uma Credencial SQL são pré-requisitos e, portanto, necessária a todas as operações de backup e restauração no serviço de armazenamento de Blob do Windows Azure.  
  
### <a name="create-a-sql-credential-on-all-the-instances-of-sql-server"></a>Criar uma Credencial SQL em todas as instâncias do SQL Server  
 Há dois scripts de exemplo e ambos criam uma Credencial SQL “mybackupToURL” em todas as instâncias do SQL Server em um computador. O primeiro exemplo é simples, e cria as credenciais e não intercepta exceções.  Por exemplo, se já houvesse uma credencial existente com o mesmo nome em uma das instâncias do computador, o script apresentaria falha. O segundo exemplo intercepta erros e permite que o script continue.  
  
```  
  
import-module sqlps  
  
# create variables  
$storageAccount = "mystorageaccount"  
$storageKey = "<storageaccesskeyvalue>"  
$secureString = convertto-securestring $storageKey  -asplaintext -force  
$credentialName = "mybackuptoURL"  
  
#cd to computer level  
cd SQLServer:\SQL\$env:COMPUTERNAME  
# get the list of instances  
$instances = Get-childitem  
#pipe the instances to new-sqlcredentail cmdlet to create SQL credential  
$instances | new-sqlcredential -Name $credentialName  -Identity $storageAccount -Secret $secureString  
```  
  
```  
  
import-module sqlps  
  
# set the parameter values  
  
$storageAccount = "mystorageaccount"  
$storageKey = "<storageaccesskeyvalue>"  
$secureString = convertto-securestring $storageKey  -asplaintext -force  
$credentialName = "mybackuptoURL"  
  
#cd to computer level  
cd SQLServer:\SQL\$env:COMPUTERNAME  
# get the list of instances  
$instances = Get-childitem  
#loop through instances and create a SQL credential, output any errors  
foreach ($instance in $instances)  
{  
    Try  
{  
     new-sqlcredential -Name $credentialName -path "SQLServer:\SQL\$($instance.name)" -Identity $storageAccount -Secret $secureString -ea Stop   
}  
Catch [Exception]  
    {  
  
            write-host "instance - $($instance.name): "$_.Exception.Message  
  
    }  
  
 }  
  
```  
  
### <a name="remove-a-sql-credential-from-all-the-instances-of-sql-server"></a>Remover uma Credencial SQL de todas as instâncias do SQL Server  
 Este script pode ser usado para remover uma credencial específica de todas as instâncias do SQL Server instaladas no computador. Se o objeto Credential não existir em uma instância específica, será exibida uma mensagem de erro, e o script continuará até que todas as instâncias sejam verificadas.  
  
```  
  
import-module sqlps  
  
cd SQLServer:\SQL\$env:COMPUTERNAME  
$credentialName = "mybackuptoURL"  
  
$instances = Get-childitem  
  
foreach ($instance in $instances)  
   {   
    try  
        {  
            $path = "SQLServer:\SQL\$($instance.name)\credentials\$credentialName"   
            Remove-sqlCredential -path $path -ea stop   
         }  
         catch [Exception]  
         {  
            write-host $_.Exception.Message  
  
        }  
  
    }  
```  
  
### <a name="full-database-backup-for-all-databases-including-system-databases"></a>Backup completo de todos os bancos de dados (INCLUINDO BANCOS DE DADOS DO SISTEMA)  
 O script a seguir cria backup de todos os bancos de dados no computador. Isso inclui os bancos de dados de usuário e o banco de dados de sistema **msdb** . O script filtra os bancos de dados de sistema **tempdb** e **model** .  
  
```  
  
import-module sqlps  
# set the parameter values  
$storageAccount = "mystorageaccount"  
$blobContainer = "privatecontainertest"  
$backupUrlContainer = "https://$storageAccount.blob.core.windows.net/$blobContainer/"  
$credentialName = "mybackuptoURL"  
  
# cd to computer level  
  
cd SQLServer:\SQL\$env:COMPUTERNAME  
$instances = Get-childitem   
# loop through each instances and backup up all the  databases -filter out tempdb and model databases  
  
 foreach ($instance in $instances)  
 {  
   $path = "sqlserver:\sql\$($instance.name)\databases"  
   $alldatabases = get-childitem -Force -path $path |Where-object {$_.name -ne "tempdb" -and $_.name -ne "model"}   
  
   $alldatabases | Backup-SqlDatabase -BackupContainer $backupUrlContainer -SqlCredential $credentialName -Compression On -script   
 }  
  
```  
  
### <a name="full-database-backup-for-all-user-databases"></a>Backup completo de TODOS os bancos de dados de usuário  
 O script a seguir pode ser usado para fazer backup de todos as bancos de dados de usuário em todas as instâncias do SQL Server no computador.  
  
```  
  
import-module sqlps   
  
$storageAccount = "mystorageaccount"  
$blobContainer = "privatecontainertest"  
$backupUrlContainer = "https://$storageAccount.blob.core.windows.net/$blobContainer/"  
$credentialName = "mybackuptoURL"  
  
# cd to computer level  
  
cd SQLServer:\SQL\$env:COMPUTERNAME  
$instances = Get-childitem   
# loop through each instances and backup up all the user databases  
 foreach ($instance in $instances)  
 {  
    $databases = dir "sqlserver:\sql\$($instance.name)\databases"  
   $databases | Backup-SqlDatabase -BackupContainer $backupUrlContainer -SqlCredential $credentialName -Compression On   
 }  
```  
  
### <a name="full-database-backup-for-master-and-msdb-system-databases-on-all-the-instances-of-sql-server"></a>Backup completo de banco de dados para MASTER e MSDB (BANCOS DE DADOS DO SISTEMA) em todas as instâncias do SQL Server  
 O script a seguir pode ser usado para fazer backup dos bancos de dados **master** e **msdb** em todas as instâncias do SQL Server instaladas no computador.  
  
```  
  
import-module sqlps  
  
$storageAccount = "mystorageaccount"  
$blobContainer = "privatecontainertest"  
$backupUrlContainer = "https://$storageAccount.blob.core.windows.net/$blobContainer/"  
$credentialName = "mybackupToUrl"  
$sysDbs = "master", "msdb"  
  
#cd to computer level  
cd SQLServer:\SQL\$env:COMPUTERNAME  
$instances = Get-childitem   
foreach ($instance in $instances)  
 {  
      foreach ($s in $sysdbs)  
     {  
Backup-SqlDatabase -Database $s -path "sqlserver:\sql\$($instance.name)" -BackupContainer  $backupUrlContainer -SqlCredential $credentialName -Compression On   
}    
 }  
  
```  
  
### <a name="full-database-backup-for-all-user-databases-on-an-instance-of-sql-server"></a>Backup completo de todos os bancos de dados de usuário em uma instância do SQL Server  
 O script a seguir é usado para fazer backup somente dos bancos de dados de usuário disponíveis em uma instância nomeada do SQL Server. O mesmo script pode ser usado como instância padrão no computador alterando o valor do parâmetro $srvPath.  
  
```  
  
import-module sqlps  
  
$storageAccount = "mystorageaccount"  
$blobContainer = "privatecontainertest"  
$backupUrlContainer = "https://$storageAccount.blob.core.windows.net/$blobContainer/"  
$srvPath = "SQLServer:\SQL\$env:COMPUTERNAME\INSTANCENAME"  # for default instance, the $srvpath variable is "SQLServer:\SQL\$env:COMPUTERNAME\DEFAULT"  
$credentialName = "mybackupToUrl"  
  
#cd to computer level  
cd SQLServer:\SQL\$env:COMPUTERNAME  
  
#retrieves the database objects for a specific instance  
$databases = dir $srvPath\databases  
  
#backup all the user databases  
$databases | Backup-SqlDatabase -BackupContainer $backupUrlContainer -SqlCredential $credentialName -Compression On  
```  
  
### <a name="full-database-backup-for-only-system-databases-master-and-msdb-on-an-instance-of-sql-server"></a>Backup completo somente para os bancos de dados de sistema (MASTER e MSDB) em uma instância do SQL Server  
 O script completo a seguir pode ser usado para fazer backup dos bancos de dados **master** e **msdb** em uma instância nomeada do SQL Server. O mesmo script pode ser usado como instância padrão no computador alterando o valor do parâmetro $srvPath.  
  
```  
  
import-module sqlps  
  
$storageAccount = "mystorageaccount"  
$blobContainer = "privatecontainertest"  
$backupUrlContainer = "https://$storageAccount.blob.core.windows.net/$blobContainer/"  
$srvPath = "SQLServer:\SQL\$env:COMPUTERNAME\INSTANCENAME" # for default instance, the $srvpath variable is "SQLServer:\SQL\$env:COMPUTERNAME\DEFAULT"  
$credentialName = "mybackupToUrl"  
  
#navigate to instance level  
cd $srvPath  
  
$sysDbs = "master", "msdb"  
foreach ($s in $sysDbs)   
{  
Backup-SqlDatabase -Database $s -BackupContainer $backupUrlContainer -SqlCredential $credentialName -Compression On  
}  
  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Backup e restauração do SQL Server com o Serviço de Armazenamento de Blobs do Microsoft Azure](../../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md)   
 [Práticas recomendadas e solução de problemas de backup do SQL Server para URL](../../relational-databases/backup-restore/sql-server-backup-to-url-best-practices-and-troubleshooting.md)  
  
  
