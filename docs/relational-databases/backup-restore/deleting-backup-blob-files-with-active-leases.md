---
title: "Excluindo arquivos de blob de backup com concessões ativas | Microsoft Docs"
ms.custom: 
ms.date: 08/17/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: backup-restore
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-backup-restore
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 13a8f879-274f-4934-a722-b4677fc9a782
caps.latest.revision: "16"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e9d8368d268caf86958ce90229c69f792a1ff036
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/18/2018
---
# <a name="delete-backup-blob-files-with-active-leases"></a>Excluir arquivos de blob de backup com concessões ativas
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Ao fazer backup para o Armazenamento do Microsoft Azure ou restaurar nele, o SQL Server adquirirá uma concessão infinita para bloquear o acesso exclusivo ao blob. Quando o processo de backup ou restauração for concluído com êxito, a concessão será liberada. Se um backup ou uma restauração falhar, o processo de backup tentará limpar qualquer blob inválido. Entretanto, se o backup falhar devido a uma falha de conectividade de rede prolongada ou contínua, o processo de backup pode não ser capaz de obter acesso ao blob e o blob pode permanecer órfão. Isso significa que o blob não poderá ser gravado ou excluído até que a concessão seja liberada. Este tópico descreve como liberar (interromper) a concessão e excluir o blob. 
  
 Para obter mais informações sobre tipos de concessão, leia este [artigo](http://go.microsoft.com/fwlink/?LinkId=275664).  
  
 Se a operação de backup falhar, o resultado poderá ser um arquivo de backup inválido. O arquivo de blob de backup pode ter também uma concessão ativa, impedindo que ele seja excluído ou substituído. Para excluir ou substituir esses blobs, primeiro a concessão deve ser liberada (interrompida). Se houver falhas de backup, recomendamos que você limpe as concessões e exclua os blobs. Você também pode limpar as concessões e excluir os blobs periodicamente como parte de suas tarefas de gerenciamento de armazenamento.  
  
 Se houver uma falha na restauração, as próximas restaurações não serão bloqueadas, portanto, talvez não haja problemas com a concessão ativa. A interrupção da concessão só é necessária quando você precisa substituir ou excluir o blob.  
  
## <a name="manage-orphaned-blobs"></a>Gerenciar blobs órfãos  
 As etapas a seguir descrevem como efetuar a limpeza após uma atividade de restauração ou backup com falha. Você pode realizar todas as etapas usando scripts do PowerShell. A seção a seguir inclui um exemplo de script do PowerShell:  
  
1.  **Identificar os blobs com concessões:** se houver um script ou um processo que execute os processos de backup, você poderá capturar a falha no script ou no processo e usá-la para limpar os blobs.  Você também pode usar o LeaseStats e as propriedades do LeastState para identificar blobs que contêm concessões. Depois de ter identificado os blobs, examine a lista e verifique a validade do arquivo de backup antes de excluir o blob.  
  
2.  **Interromper a concessão:** uma solicitação autorizada pode interromper a concessão sem fornecer uma ID de concessão. Consulte [aqui](http://go.microsoft.com/fwlink/?LinkID=275664) para obter mais informações.  
  
    > [!TIP]  
    >  O SQL Server emite uma ID de concessão para estabelecer o acesso exclusivo durante a operação de restauração. A ID de concessão da restauração é BAC2BAC2BAC2BAC2BAC2BAC2BAC2BAC2.  
  
3.  **Excluir o Blob:** para excluir um blob com uma concessão ativa, primeiro você deve interromper a concessão.  
  
###  <a name="Code_Example"></a> Exemplo de script do PowerShell  
  
> [!IMPORTANT]  
>  Se você estiver executando o PowerShell 2.0, você poderá ter problemas ao carregar o assembly do Microsoft WindowsAzure.Storage.dll. Recomendamos que você atualize o [Powershell](https://docs.microsoft.com/powershell/) para solucionar o problema. Você também pode usar a seguinte solução para o PowerShell 2.0:  
>   
>  -   Crie ou modifique o arquivo powershell.exe.config para carregar os assemblies do .NET 2.0 e do .NET 4.0 em tempo de execução com o seguinte:  
>   
>     ```  
>     \<?xml version="1.0"?>   
>     <configuration>   
>         <startup useLegacyV2RuntimeActivationPolicy="true">   
>             <supportedRuntime version="v4.0.30319"/>   
>             <supportedRuntime version="v2.0.50727"/>   
>         </startup>   
>     </configuration>  
>   
>     ```  
  
 O script de exemplo a seguir identifica os blobs com concessões ativas e, em seguida, os interrompe. O exemplo também demonstra como filtrar IDs de concessão da versão.  
  
**Dicas para executar este script**  
  
> [!WARNING]  
>  Se um backup para o serviço de armazenamento de Blobs do Microsoft Azure estiver em execução ao mesmo tempo que o script, o backup poderá falhar porque esse script interromperá a concessão que o backup estiver tentando adquirir ao mesmo tempo. Execute este script durante uma janela de manutenção ou quando não houver backups em execução ou que serão executados.  
  
1.  Ao executar este script, será solicitado que você forneça valores para a conta de armazenamento, a chave de armazenamento, o contêiner e os parâmetros de caminho e nome do assembly de armazenamento do Azure. O caminho do armazenamento do assembly é o diretório de instalação da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. O nome de arquivo do assembly de armazenamento é Microsoft.WindowsAzure.Storage.dll. O seguinte é um exemplo dos prompts e valores inseridos:  
  
    ```  
    cmdlet  at command pipeline position 1  
    Supply values for the following parameters:  
    storageAccount: mycloudstorageaccount  
    storageKey: 0BopKY7eEha3gBnistYk+904nf  
    blobContainer: mycontainer   
    storageAssemblyPath: C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Binn\Microsoft.WindowsAzure.Storage.dll  
    ```  
  
2.  Se não houver blobs com arrendamentos bloqueados, a seguinte mensagem será exibida:  
  
     **Não há nenhum blob com status de concessão bloqueado**  
  
     Se houver blobs com arrendamentos bloqueados, você verá as seguintes mensagens:  
  
     **Interrompendo arrendamentos**  
  
     **A concessão na \<URL do Blob> é uma concessão de restauração: você verá esta mensagem apenas se tiver um blob com uma concessão de restauração que ainda está ativa.**  
  
     **A concessão na \<URL do Blob> não é uma concessão de restauração Interrompendo concessão na \<URL do Bob>.**  
  
```  
param(  
       [Parameter(Mandatory=$true)]  
       [string]$storageAccount,  
       [Parameter(Mandatory=$true)]  
       [string]$storageKey,  
       [Parameter(Mandatory=$true)]  
       [string]$blobContainer,  
       [Parameter(Mandatory=$true)]  
       [string]$storageAssemblyPath  
)  
  
# Well known Restore Lease ID  
$restoreLeaseId = "BAC2BAC2BAC2BAC2BAC2BAC2BAC2BAC2"  
  
# Load the storage assembly without locking the file for the duration of the PowerShell session  
$bytes = [System.IO.File]::ReadAllBytes($storageAssemblyPath)  
[System.Reflection.Assembly]::Load($bytes)  
  
$cred = New-Object 'Microsoft.WindowsAzure.Storage.Auth.StorageCredentials' $storageAccount, $storageKey  
  
$client = New-Object 'Microsoft.WindowsAzure.Storage.Blob.CloudBlobClient' "https://$storageAccount.blob.core.windows.net", $cred  
  
$container = $client.GetContainerReference($blobContainer)  
  
#list all the blobs  
$allBlobs = $container.ListBlobs($null,$true) 
  
$lockedBlobs = @()  
# filter blobs that are have Lease Status as "locked"  
foreach($blob in $allBlobs)  
{  
    $blobProperties = $blob.Properties   
    if($blobProperties.LeaseStatus -eq "Locked")  
    {  
        $lockedBlobs += $blob  
  
    }  
}  
  
if ($lockedBlobs.Count -eq 0)  
    {   
        Write-Host " There are no blobs with locked lease status"  
    }  
if($lockedBlobs.Count -gt 0)  
{  
    write-host "Breaking leases"  
    foreach($blob in $lockedBlobs )   
    {  
        try  
        {  
            $blob.AcquireLease($null, $restoreLeaseId, $null, $null, $null)  
            Write-Host "The lease on $($blob.Uri) is a restore lease"  
        }  
        catch [Microsoft.WindowsAzure.Storage.StorageException]  
        {  
            if($_.Exception.RequestInformation.HttpStatusCode -eq 409)  
            {  
                Write-Host "The lease on $($blob.Uri) is not a restore lease"  
            }  
        }  
  
        Write-Host "Breaking lease on $($blob.Uri)"  
        $blob.BreakLease($(New-TimeSpan), $null, $null, $null) | Out-Null  
    }  
}  
  
```  
  
## <a name="see-also"></a>Consulte também  
 [Práticas recomendadas e solução de problemas de backup do SQL Server para URL](../../relational-databases/backup-restore/sql-server-backup-to-url-best-practices-and-troubleshooting.md)  
  
  
