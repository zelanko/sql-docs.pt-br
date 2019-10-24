---
title: Excluindo arquivos de blob de backup com concessões ativas | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
ms.assetid: 13a8f879-274f-4934-a722-b4677fc9a782
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 663bab775aff9a04a4a9d93f2bcbd0e193b18f37
ms.sourcegitcommit: a165052c789a327a3a7202872669ce039bd9e495
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/22/2019
ms.locfileid: "72783063"
---
# <a name="deleting-backup-blob-files-with-active-leases"></a>Excluindo arquivos de blob de backup com arrendamentos ativos
  Ao fazer backup ou restaurar do armazenamento do Azure, o SQL Server adquire uma concessão infinita para bloquear o acesso exclusivo ao blob. Quando o processo de backup ou restauração for concluído com êxito, a concessão será liberada. Se um backup ou uma restauração falhar, o processo de backup tentará limpar qualquer blob inválido. Entretanto, se o backup falhar devido a uma falha de conectividade de rede prolongada ou contínua, o processo de backup pode não ser capaz de obter acesso ao blob e o blob pode permanecer órfão. Isso significa que o blob só poderá ser gravado ou excluído quando a concessão for liberada. Este tópico descreve como liberar a concessão e excluir o blob.  
  
 Para obter mais informações sobre os tipos de arrendamentos, leia este [artigo](https://go.microsoft.com/fwlink/?LinkId=275664).  
  
 Se a operação de backup falhar, isso poderá resultar em um arquivo de backup que não é válido.  O arquivo de blob de backup pode ter também uma concessão ativa, impedindo que ele seja excluído ou substituído.  Para excluir ou substituir esses blobs, primeiro a concessão deve ser interrompida. Se houver falhas de backup, recomendamos que você limpe as concessões e exclua os blobs. Você também pode optar por fazer a limpeza periódica como parte das tarefas de gerenciamento de armazenamento.  
  
 Se houver uma falha na restauração, as restaurações subsequentes não serão bloqueadas e, portanto, a concessão ativa possivelmente não será um problema. A interrupção da concessão só é necessária quando você precisa substituir ou excluir o blob.  
  
## <a name="managing-orphaned-blobs"></a>Gerenciando blobs órfãos  
 As etapas a seguir descrevem como efetuar a limpeza após uma atividade de restauração ou backup com falha. Todas as etapas podem ser executadas por meio dos scripts do PowerShell. Um exemplo de código é fornecido na seção a seguir:  
  
1.  **Identificando os blobs que têm arrendamentos:** Se você tiver um script ou processo que executa os processos de backup, talvez possa capturar a falha no script ou processo e usá-la para limpar os blobs.   Você também pode usar as propriedades LeaseStats e LeastState para identificar os blobs que têm arrendamentos neles. Após identificar os blobs, recomendamos que você examine a lista e verifique a validade do arquivo de backup antes de excluir o blob.  
  
2.  **Interrompendo a concessão:** uma solicitação autorizada pode interromper a concessão sem fornecer uma ID de concessão. Consulte [aqui](https://go.microsoft.com/fwlink/?LinkID=275664) para obter mais informações.  
  
    > [!TIP]  
    >  O SQL Server emite uma ID de concessão para estabelecer o acesso exclusivo durante a operação de restauração. A ID de concessão da restauração é BAC2BAC2BAC2BAC2BAC2BAC2BAC2BAC2.  
  
3.  **Excluindo o blob:** para excluir um blob que tem uma concessão ativa, primeiro você deve interromper a concessão.  
  
###  <a name="Code_Example"></a> Exemplo de script do PowerShell  
 **\* \* \* importantes \*** Se você estiver executando o PowerShell 2,0, poderá ter problemas ao carregar o assembly Microsoft WindowsAzure. Storage. dll. Recomendamos que você atualize o Powershell 3.0 para resolver o problema. Você também pode usar a seguinte solução para o PowerShell 2.0:  
  
-   Crie ou modifique o arquivo powershell.exe.config para carregar os assemblies do .NET 2.0 e do .NET 4.0 em tempo de execução com o seguinte:  
  
    ```xml
    <?xml version="1.0"?>
    <configuration>
        <startup useLegacyV2RuntimeActivationPolicy="true">
            <supportedRuntime version="v4.0.30319"/>
            <supportedRuntime version="v2.0.50727"/>
        </startup>
    </configuration>
    ```  
  
 O exemplo a seguir ilustra a identificação de blobs que têm arrendamentos ativos e sua interrupção. O exemplo também demonstra como filtrar IDs de concessão da versão.  
  
 Dicas para executar este script  
  
> [!WARNING]  
>  Se um backup para o serviço de armazenamento de BLOBs do Azure estiver em execução ao mesmo tempo que esse script, o backup poderá falhar, pois esse script interromperá a concessão que o backup está tentando adquirir ao mesmo tempo. Recomendamos a execução deste script durante uma janela de manutenção ou quando não houver nenhum backup programado para execução.  
  
1.  Ao executar esse script, você será solicitado a fornecer valores para a conta de armazenamento, a chave de armazenamento, o contêiner e os parâmetros de caminho e nome do assembly de armazenamento do Azure. O caminho do armazenamento do assembly é o diretório de instalação da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. O nome de arquivo do assembly de armazenamento é Microsoft.WindowsAzure.Storage.dll. O seguinte é um exemplo dos prompts e valores inseridos:  
  
    ```  
    cmdlet  at command pipeline position 1  
    Supply values for the following parameters:  
    storageAccount: mycloudstorageaccount  
    storageKey: 0BopKY7eEha3gBnistYk+904nf  
    blobContainer: mycontainer   
    storageAssemblyPath: C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\Binn\Microsoft.WindowsAzure.Storage.dll  
    ```  
  
2.  Se não houver nenhum blob que tenha bloqueado arrendamentos, você verá a seguinte mensagem:  
  
     **Não há nenhum blob com status de concessão bloqueado**  
  
     Se houver blobs com arrendamentos bloqueados, você verá as seguintes mensagens:  
  
     **Interrompendo arrendamentos**  
  
     **A concessão na \<URL do Blob> é uma concessão de restauração: você verá esta mensagem apenas se tiver um blob com uma concessão de restauração que ainda está ativa.**  
  
     **A concessão na \<URL do Blob> não é uma concessão de restauração Interrompendo concessão na \<URL do Bob>.**  
  
```powershell
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
$allBlobs = $container.ListBlobs()
  
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
    Write-Host "Breaking leases"  
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
  
## <a name="see-also"></a>Consulte Também  
 [Melhores práticas e solução de problemas de backup do SQL Server para URL](sql-server-backup-to-url-best-practices-and-troubleshooting.md)  
