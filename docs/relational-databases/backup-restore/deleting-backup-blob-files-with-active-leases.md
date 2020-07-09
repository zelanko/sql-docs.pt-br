---
title: Excluindo arquivos de blob de backup com concessões ativas | Microsoft Docs
description: Se um backup ou uma restauração do SQL Server falhar, um blob no Armazenamento do Azure poderá se tornar órfão. Saiba como excluir um blob órfão.
ms.custom: ''
ms.date: 08/17/2017
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
ms.assetid: 13a8f879-274f-4934-a722-b4677fc9a782
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: f51c01570aa5149e24ca1cb37af4b6bafe35ee0f
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85737814"
---
# <a name="delete-backup-blob-files-with-active-leases"></a>Excluir arquivos de blob de backup com concessões ativas

 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

Ao fazer backup para o armazenamento do Microsoft Azure ou restaurar nele, o SQL Server adquirirá uma concessão infinita para bloquear o acesso exclusivo ao blob. Quando o processo de backup ou restauração for concluído com êxito, a concessão será liberada. Se um backup ou uma restauração falhar, o processo de backup tentará limpar qualquer blob inválido. Entretanto, se o backup falhar devido a uma falha de conectividade de rede prolongada ou contínua, o processo de backup pode não ser capaz de obter acesso ao blob e o blob pode permanecer órfão. Isso significa que o blob não poderá ser gravado ou excluído até que a concessão seja liberada. Este tópico descreve como liberar (interromper) a concessão e excluir o blob.
  
Para obter mais informações sobre tipos de concessão, leia este [artigo](https://go.microsoft.com/fwlink/?LinkId=275664).  
  
Se a operação de backup falhar, o resultado poderá ser um arquivo de backup inválido. O arquivo de blob de backup pode ter também uma concessão ativa, impedindo que ele seja excluído ou substituído. Para excluir ou substituir esses blobs, primeiro a concessão deve ser liberada (interrompida). Se houver falhas de backup, recomendamos que você limpe as concessões e exclua os blobs. Você também pode limpar as concessões e excluir os blobs periodicamente como parte de suas tarefas de gerenciamento de armazenamento.  
  
Se houver uma falha na restauração, as próximas restaurações não serão bloqueadas, portanto, talvez não haja problemas com a concessão ativa. A interrupção da concessão só é necessária quando você precisa substituir ou excluir o blob.  
  
## <a name="manage-orphaned-blobs"></a>Gerenciar blobs órfãos

As etapas a seguir descrevem como efetuar a limpeza após uma atividade de restauração ou backup com falha. Você pode realizar todas as etapas usando scripts do PowerShell. A seção a seguir inclui um exemplo de script do PowerShell:  
  
1. **Identificar blobs com concessões:** Se houver um script ou um processo que execute os processos de backup, você poderá capturar a falha no script ou no processo e usá-la para limpar os blobs.  Você também pode usar o LeaseStats e as propriedades do LeastState para identificar blobs que contêm concessões. Depois de ter identificado os blobs, examine a lista e verifique a validade do arquivo de backup antes de excluir o blob.  
  
1. **Interromper a concessão:** Uma solicitação autorizada pode interromper a concessão sem fornecer uma ID de concessão. Consulte [aqui](https://go.microsoft.com/fwlink/?LinkID=275664) para obter mais informações.  
  
    > [!TIP]  
    > O SQL Server emite uma ID de concessão para estabelecer o acesso exclusivo durante a operação de restauração. A ID de concessão da restauração é BAC2BAC2BAC2BAC2BAC2BAC2BAC2BAC2.  
  
1. **Excluir o Blob:** Para excluir um blob com uma concessão ativa, primeiro, é necessário interromper a concessão.  

###  <a name="powershell-script-example"></a><a name="Code_Example"></a> Exemplo de script do PowerShell  
  
> [!IMPORTANT]
> Se você estiver executando o PowerShell 2.0, você poderá ter problemas ao carregar o assembly do Microsoft WindowsAzure.Storage.dll. Recomendamos que você atualize o [Powershell](https://docs.microsoft.com/powershell/) para solucionar o problema. Use também a seguinte solução alternativa para criar ou modificar o arquivo powershell.exe.config para carregar os assemblies do.NET 2.0 e do.NET 4.0 em runtime com o seguinte:  
>
> ```xml
> <?xml version="1.0"?>
>     <configuration>
>         <startup useLegacyV2RuntimeActivationPolicy="true">
>             <supportedRuntime version="v4.0.30319"/>
>             <supportedRuntime version="v2.0.50727"/>
>         </startup>
>     </configuration>  
> ```  
  
 O script de exemplo a seguir identifica os blobs com concessões ativas e, em seguida, os interrompe. O exemplo também demonstra como filtrar IDs de concessão da versão.  
  
#### <a name="tips-on-running-this-script"></a>Dicas para executar este script
  
> [!WARNING]  
> Se um backup no serviço de Armazenamento de Blobs do Azure estiver em execução ao mesmo tempo que o script, o backup poderá falhar, porque esse script interromperá a concessão que o backup está tentando adquirir simultaneamente. Execute este script durante uma janela de manutenção ou quando não houver backups em execução ou que serão executados.  
  
- Antes de executar esse script, você deverá adicionar valores para a conta de armazenamento, a chave de armazenamento, o contêiner e os parâmetros de caminho e nome do assembly de armazenamento do Azure. O caminho do armazenamento do assembly é o diretório de instalação da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. O nome de arquivo do assembly de armazenamento é Microsoft.WindowsAzure.Storage.dll.
  
- Se não houver blobs com concessões bloqueadas, você deverá ver a seguinte mensagem: `There are no blobs with locked lease status`
  
- Se houver blobs com concessões bloqueadas, você deverá ver as seguintes mensagens: `Breaking Leases`, `The lease on <URL of the Blob> is a restore lease: You will see this message only if you have a blob with a restore lease that is still active.` e `The lease on <URL of the Blob> is not a restore lease Breaking lease on <URL of the Bob>.`
  
```powershell
$storageAccount = "<myStorageAccount>"
$storageKey = "<myStorageKey>"
$blobContainer = "<myBlobContainer>"
$storageAssemblyPathName = "<myStorageAssemblyPathName>"
  
# well known Restore Lease ID  
$restoreLeaseId = "BAC2BAC2BAC2BAC2BAC2BAC2BAC2BAC2"  
  
# load the storage assembly without locking the file for the duration of the PowerShell session  
$bytes = [System.IO.File]::ReadAllBytes($storageAssemblyPath)  
[System.Reflection.Assembly]::Load($bytes)  
  
$cred = New-Object 'Microsoft.WindowsAzure.Storage.Auth.StorageCredentials' $storageAccount, $storageKey  
$client = New-Object 'Microsoft.WindowsAzure.Storage.Blob.CloudBlobClient' "https://$storageAccount.blob.core.windows.net", $cred  
$container = $client.GetContainerReference($blobContainer)  
  
# list all the blobs  
$blobs = $container.ListBlobs($null,$true)
  
# filter blobs that are have Lease Status as "locked"
$lockedBlobs = @()  
foreach($blob in $blobs)  
{  
    $blobProperties = $blob.Properties
    if($blobProperties.LeaseStatus -eq "Locked")  
    {  
        $lockedBlobs += $blob  
    }  
}  

if($lockedBlobs.Count -gt 0)  
{  
    Write-Host "Breaking leases..."
    foreach($blob in $lockedBlobs )
    {  
        try  
        {  
            $blob.AcquireLease($null, $restoreLeaseId, $null, $null, $null)  
            Write-Host "The lease on $($blob.Uri) is a restore lease."  
        }  
        catch [Microsoft.WindowsAzure.Storage.StorageException]  
        {  
            if($_.Exception.RequestInformation.HttpStatusCode -eq 409)  
            {  
                Write-Host "The lease on $($blob.Uri) is not a restore lease."  
            }  
        }  
  
        Write-Host "Breaking lease on $($blob.Uri)."  
        $blob.BreakLease($(New-TimeSpan), $null, $null, $null) | Out-Null  
    }  
} else { Write-Host " There are no blobs with locked lease status." }
```  
  
## <a name="see-also"></a>Confira também

[Solução de problemas e melhores práticas de backup do SQL Server para URL](../../relational-databases/backup-restore/sql-server-backup-to-url-best-practices-and-troubleshooting.md)  
