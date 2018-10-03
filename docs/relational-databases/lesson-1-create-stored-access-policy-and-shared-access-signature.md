---
title: 'Lição 1: Criar uma política de acesso armazenado e uma assinatura de acesso compartilhado | Microsoft Docs'
ms.custom: ''
ms.date: 06/02/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
ms.assetid: 41674d9d-8132-4bff-be4d-85a861419f3d
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 88524c24e2967a061bab32b7d1695a57c2d2ad89
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47818777"
---
# <a name="lesson-1-create-stored-access-policy-and-shared-access-signature"></a>Lição 1: Criar uma política de acesso armazenado e uma assinatura de acesso compartilhado
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
Nesta lição, você aprenderá a usar um script do [Azure PowerShell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/) para criar uma assinatura de acesso compartilhado em um contêiner de blobs do Azure usando uma política de acesso armazenado.  
  
> [!NOTE]  
> Esse script é escrito com o Azure PowerShell 5.0.10586.  
  
Uma assinatura de acesso compartilhado é um URI que concede direitos de acesso restrito a contêineres, blobs, filas ou tabelas. Uma política de acesso armazenado fornece um nível adicional de controle sobre as assinaturas de acesso compartilhado do servidor, incluindo revogação, expiração ou extensão do acesso. Ao usar essa nova melhoria, você precisa criar uma política em um contêiner com direitos de leitura, gravação e lista.  
  
Você pode criar uma política de acesso armazenado e uma assinatura de acesso compartilhado usando o Azure PowerShell, o SDK do Armazenamento do Azure, a API REST do Azure ou um utilitário de terceiros. Este tutorial demonstra como usar um script do Azure PowerShell para concluir esta tarefa. O script usa o modelo de implantação do Resource Manager e cria os seguintes novos recursos  
  
-   Grupo de recursos  
  
-   Conta de armazenamento  
  
-   Contêiner de blobs do Azure  
  
-   Política do SAS  
  
Esse script começa declarando diversas variáveis para especificar os nomes dos recursos acima e os nomes dos seguintes valores de entrada necessários:  
  
-   Um nome de prefixo usado na nomeação de outros objetos de recurso  
  
-   Nome da assinatura  
  
-   Local do datacenter  
  
> [!NOTE]  
> Esse script é escrito de forma que você possa usar os recursos de modelo de implantação clássica ou ARM existentes.  
  
O script é concluído com a geração da instrução CREATE CREDENCIAL apropriada que você usará na [Lição 2: Criar uma credencial do SQL Server usando uma assinatura de acesso compartilhado](../relational-databases/lesson-2-create-a-sql-server-credential-using-a-shared-access-signature.md). Essa instrução é copiada na área de transferência para você e é gerada no console para exibição.  
  
Para criar uma política no contêiner e gerar uma chave SAS (Assinatura de Acesso Compartilhado), siga estas etapas:  
  
1.  Abra a janela do Windows PowerShell ou o ISE do Windows PowerShell (consulte os requisitos de versão acima).  
  
2.  Edite e execute o script a seguir.  
  
    ```  
    <#   
    This script uses the Azure Resource model and creates a new ARM storage account.  
    Modify this script to use an existing ARM or classic storage account   
    using the instructions in comments within this script  
    #>  
    # Define global variables for the script  
    $prefixName = '<a prefix name>'  # used as the prefix for the name for various objects  
    $subscriptionName='<your subscription name>'   # the name  of subscription name you will use  
    $locationName = '<a data center location>'  # the data center region you will use  
    $storageAccountName= $prefixName + 'storage' # the storage account name you will create or use  
    $containerName= $prefixName + 'container'  # the storage container name to which you will attach the SAS policy with its SAS token  
    $policyName = $prefixName + 'policy' # the name of the SAS policy  
  
    <#   
    Using Azure Resource Manager deployment model  
    Comment out this entire section and use the classic storage account name to use an existing classic storage account  
    #>  
  
    # Set a variable for the name of the resource group you will create or use  
    $resourceGroupName=$prefixName + 'rg'   
  
    # adds an authenticated Azure account for use in the session   
    Login-AzureRmAccount    
  
    # set the tenant, subscription and environment for use in the rest of   
    Set-AzureRmContext -SubscriptionName $subscriptionName   
  
    # create a new resource group - comment out this line to use an existing resource group  
    New-AzureRmResourceGroup -Name $resourceGroupName -Location $locationName   
  
    # Create a new ARM storage account - comment out this line to use an existing ARM storage account  
    New-AzureRmStorageAccount -Name $storageAccountName -ResourceGroupName $resourceGroupName -Type Standard_RAGRS -Location $locationName   
  
    # Get the access keys for the ARM storage account  
    $accountKeys = Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $storageAccountName  
  
    # Create a new storage account context using an ARM storage account  
    $storageContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $accountKeys[0].Value 
  
    <#  
    Using the Classic deployment model  
    Use the following four lines to use an existing classic storage account  
    #>  
    #Classic storage account name  
    #Add-AzureAccount  
    #Select-AzureSubscription -SubscriptionName $subscriptionName #provide an existing classic storage account  
    #$accountKeys = Get-AzureStorageKey -StorageAccountName $storageAccountName  
    #$storageContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $accountKeys.Primary  
  
    # The remainder of this script works with either the ARM or classic sections of code above  
  
    # Creates a new container in blob storage  
    $container = New-AzureStorageContainer -Context $storageContext -Name $containerName  
  
    # Sets up a Stored Access Policy and a Shared Access Signature for the new container  
    $policy = New-AzureStorageContainerStoredAccessPolicy -Container $containerName -Policy $policyName -Context $storageContext -StartTime $(Get-Date).ToUniversalTime().AddMinutes(-5) -ExpiryTime $(Get-Date).ToUniversalTime().AddYears(10) -Permission rwld

    # Gets the Shared Access Signature for the policy  
    $sas = New-AzureStorageContainerSASToken -name $containerName -Policy $policyName -Context $storageContext
    Write-Host 'Shared Access Signature= '$($sas.Substring(1))''  
  
    # Outputs the Transact SQL to the clipboard and to the screen to create the credential using the Shared Access Signature  
    Write-Host 'Credential T-SQL'  
    $tSql = "CREATE CREDENTIAL [{0}] WITH IDENTITY='Shared Access Signature', SECRET='{1}'" -f $cbc.Uri,$sas.Substring(1)   
    $tSql | clip  
    Write-Host $tSql  
  
    ```  
  
3.  Após a conclusão do script, a instrução CREATE CREDENCIAL estará localizada na área de transferência para uso na próxima lição.  
  
**Próxima lição:**  
  
[Lição 2: Criar uma credencial do SQL Server usando uma assinatura de acesso compartilhado](../relational-databases/lesson-2-create-a-sql-server-credential-using-a-shared-access-signature.md)  
  
## <a name="see-also"></a>Consulte Também  
[Assinaturas de Acesso Compartilhado, parte 1: Noções básicas sobre o modelo SAS](https://azure.microsoft.com/documentation/articles/storage-dotnet-shared-access-signature-part-1/)  
[Criar contêiner](https://msdn.microsoft.com/library/azure/dd179468.aspx)  
[Definir ACL do contêiner](https://msdn.microsoft.com/library/azure/dd179391.aspx)  
[Obter ACL do contêiner](https://msdn.microsoft.com/library/azure/dd179469.aspx)  
  
  
  

