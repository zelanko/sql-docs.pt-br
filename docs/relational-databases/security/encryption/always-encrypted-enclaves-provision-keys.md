---
title: Provisionar chaves habilitadas para enclave | Microsoft Docs
ms.custom: ''
ms.date: 10/01/2019
ms.prod: sql
ms.reviewer: vanto
ms.prod_service: database-engine, sql-database
ms.technology: security
ms.topic: conceptual
author: jaszymas
ms.author: jaszymas
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: 6b87620704416df94cf21cda05d1a64a8159eb32
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "73595581"
---
# <a name="provision-enclave-enabled-keys"></a>Provisionar chaves habilitadas para enclave
[!INCLUDE [tsql-appliesto-ssver15-xxxx-xxxx-xxx-winonly](../../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx-winonly.md)]

Este artigo descreve como provisionar chaves habilitadas para enclave compatíveis com cálculos dentro dos enclaves seguros no servidor usados para [Always Encrypted com enclaves seguros](always-encrypted-enclaves.md). 

As diretrizes e os processos gerais para [gerenciar chaves de Always Encrypted](overview-of-key-management-for-always-encrypted.md) se aplicam quando você provisiona chaves habilitadas para enclave. Este artigo aborda detalhes específicos do Always Encrypted com enclaves seguros.

Para provisionar uma chave mestra de coluna habilitada para enclave usando o SQL Server Management Studio ou o PowerShell, verifique se a nova chave é compatível com as computações de enclave. Isso fará com que a ferramenta (SSMS ou PowerShell) gere a instrução `CREATE COLUMN MASTER KEY` que define o `ENCLAVE_COMPUTATIONS` nos metadados da chave mestra de colunas no banco de dados. Para obter mais informações, veja [CREATE COLUMN MASTER KEY (Transact-SQL)](../../../t-sql/statements/create-column-master-key-transact-sql.md). 

A ferramenta também assinará digitalmente as propriedades mestras de coluna com a chave mestra de coluna e armazenará a assinatura nos metadados do banco de dados. A assinatura evita a violação mal-intencionada da configuração `ENCLAVE_COMPUTATIONS`. Os drivers do cliente SQL verificam as assinaturas antes de permitir o uso do enclave. Isso proporciona aos administradores da segurança o controle de quais dados da coluna podem ser calculados dentro de enclave.

O `ENCLAVE_COMPUTATIONS` é imutável, ou seja, você não pode alterá-lo depois de definir a chave mestra de coluna nos metadados. Para habilitar computações de enclave usando uma chave de criptografia de coluna, que uma determinada chave mestra de coluna criptografa, você precisará girar a chave mestra de coluna e substituí-la por uma chave mestra de coluna habilitada para enclave. Confira [Girar chaves habilitadas para enclave](always-encrypted-enclaves-rotate-keys.md).

> [!NOTE]
> Atualmente, o SSMS e o PowerShell são compatíveis com chaves mestras de coluna habilitadas para enclave armazenadas no Azure Key Vault ou no repositório de certificados do Windows. Não há compatibilidade com módulos de segurança de hardware (usando CNG ou CAPI).

Para criar uma chave de criptografia de coluna habilitada para enclave, você precisará selecionar uma chave mestra de coluna habilitada para enclave para criptografar a nova chave. 

As seções a seguir fornecem mais detalhes sobre como provisionar chaves habilitadas para enclave usando o SSMS e o PowerShell.

## <a name="provision-enclave-enabled-keys-using-sql-server-management-studio"></a>Provisionar chaves habilitadas para enclave usando o SQL Server Management Studio
No SQL Server Management Studio 18.3 ou superior, você pode provisionar:
- Uma chave mestra de coluna habilitada para enclave usando o diálogo **Nova chave mestra de coluna**.
- Uma chave de criptografia de coluna habilitada para enclave usando o diálogo **Nova chave de criptografia de coluna**.

> [!NOTE]
> No momento, o [assistente do Always Encrypted](always-encrypted-wizard.md) não é compatível com a geração de chaves habilitadas para enclave. No entanto, você pode criar chaves habilitadas para enclave usando os diálogos acima primeiro e, em seguida, ao executar o assistente, selecione uma criptografia de coluna já existente habilitada para o enclave para as colunas que você deseja criptografar.

### <a name="provision-enclave-enabled-column-master-keys-with-the-new-column-master-key-dialog"></a>Provisionar chaves mestras de coluna habilitadas para enclave com o diálogo Nova chave mestra de coluna
Para provisionar uma chave mestra de coluna habilitada para enclave, siga as etapas em [Provisionar chaves mestras de coluna com o diálogo Nova chave mestra de coluna](configure-always-encrypted-keys-using-ssms.md#provision-column-master-keys-with-the-new-column-master-key-dialog). Certifique-se de selecionar **Permitir computações de enclave**. Veja a captura de tela abaixo:

![Permitir computações de enclave](./media/always-encrypted-enclaves/allow-enclave-computations.png)

> [!NOTE]
> A caixa de seleção **Permitir computações de enclave** será exibida somente se a instância de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] contiver um enclave seguro inicializado corretamente. Para mais informações, confira [Configurar o tipo de enclave para Always Encrypted](../../../database-engine/configure-windows/configure-column-encryption-enclave-type.md).

> [!TIP]
> Para verificar se uma chave mestra de coluna está habilitada para enclave, clique com o botão direito do mouse nela no Pesquisador de Objetos e selecione **Propriedades**. Se a chave estiver habilitada para enclave, **Computações de enclave: permitido** aparecerá na janela que mostra as propriedades da chave. Como alternativa, você pode usar a exibição [sys.column_master_keys (Transact-SQL)](../../system-catalog-views/sys-column-master-keys-transact-sql.md).

### <a name="provision-enclave-enabled-column-encryption-keys-with-the-new-column-encryption-key-dialog"></a>Provisionar chaves de criptografia de coluna habilitadas para enclave usando o diálogo Nova chave de criptografia de coluna
Para provisionar uma chave de criptografia de coluna habilitada para enclave, siga as etapas em [Provisionar chaves de criptografia de coluna com o diálogo Nova chave de criptografia de coluna](configure-always-encrypted-keys-using-ssms.md#provision-column-encryption-keys-with-the-new-column-encryption-key-dialog). Ao selecionar uma chave mestra de coluna, verifique se ela está habilitada para enclave.

> [!TIP]
> Para verificar se uma chave de criptografia de coluna está habilitada para enclave, clique com o botão direito do mouse nela no Pesquisador de Objetos e selecione **Propriedades**. Se a chave estiver habilitada para enclave, **Computações de enclave: permitido** aparecerá na janela que mostra as propriedades da chave.

## <a name="provision-enclave-enabled-keys-using-powershell"></a>Provisionar chaves habilitadas para enclave usando o PowerShell
Para provisionar chaves habilitadas para enclave usando o PowerShell, você precisa do módulo do SqlServer PowerShell versão 21.1.18179 ou superior.

Em geral, os fluxos de trabalho de provisionamento de chave do PowerShell (com e sem separação de função) para Always Encrypted, descritos em [Provisionar chaves Always Encrypted usando o PowerShell](configure-always-encrypted-keys-using-powershell.md) também se aplicam a chaves habilitadas para enclave. Esta seção descreve detalhes específicos de chaves habilitadas para enclave.

O módulo SqlServer PowerShell estende o [**New-SqlCertificateStoreColumnMasterKeySettings**](https://docs.microsoft.com/powershell/module/sqlserver/new-sqlcertificatestorecolumnmasterkeysettings) e [**New-SqlAzureKeyVaultColumnMasterKeySettings**](https://docs.microsoft.com/powershell/module/sqlserver/new-sqlazurekeyvaultcolumnmasterkeysettings) com o parâmetro `-AllowEnclaveComputations` para permitir que você especifique uma chave mestra de coluna habilitada para enclave durante o processo de provisionamento. Um cmdlet cria um objeto local que contém as propriedades de uma chave mestra de coluna (armazenada no Azure Key Vault ou no repositório de certificados do Windows). Se especificada, a propriedade `-AllowEnclaveComputations` marcará a chave como habilitada para enclave no objeto local. Ela também faz com que o cmdlet acesse a chave mestra de coluna referenciada (no Azure Key Vault ou no repositório de certificados do Windows) para assinar digitalmente as propriedades da chave. Depois de criar um objeto de configurações para uma nova chave mestra de coluna habilitada para enclave, você pode usá-lo em uma invocação subsequente do cmdlet [**New-SqlColumnMasterKey**](https://docs.microsoft.com/powershell/module/sqlserver/new-sqlcolumnmasterkey) para criar um objeto de metadados que descreve a nova chave no banco de dados.

O provisionamento de chaves de criptografia de coluna habilitadas para enclave não é diferente do provisionamento de chaves de criptografia de coluna que não são habilitadas para enclave. Você só precisa certificar-se de que uma chave mestra de coluna usada para criptografar a nova chave de criptografia de coluna esteja habilitada para enclave.

> [!NOTE]
> O módulo SqlServer PowerShell atualmente não é compatível com o provisionamento de chaves habilitadas para enclave armazenadas em módulos de segurança de hardware (usando CNG ou CAPI).

### <a name="example---provision-enclave-enabled-keys-using-windows-certificate-store"></a>Exemplo – Provisionamento de chaves habilitadas para enclave usando o repositório de certificados do Windows
O exemplo de ponta a ponta abaixo mostra como provisionar chaves habilitadas para enclave, armazenando a chave mestra de coluna armazenada no repositório de certificados do Windows. Esse script é baseado no exemplo em [Repositório de Certificados do Windows sem separação de funções (exemplo)](configure-always-encrypted-keys-using-powershell.md#windows-certificate-store-without-role-separation-example). É importante observar o uso do parâmetro `-AllowEnclaveComputations` no cmdlet [**New-SqlCertificateStoreColumnMasterKeySettings**](https://docs.microsoft.com/powershell/module/sqlserver/new-sqlcertificatestorecolumnmasterkeysettings), que é a única diferença entre os fluxos de trabalho nos dois exemplos.

```powershell
# Create a column master key in Windows Certificate Store.
$cert = New-SelfSignedCertificate -Subject "AlwaysEncryptedCert" -CertStoreLocation Cert:CurrentUser\My -KeyExportPolicy Exportable -Type DocumentEncryptionCert -KeyUsage DataEncipherment -KeySpec KeyExchange

# Import the SqlServer module.
Import-Module "SqlServer"

# Connect to your database.
$serverName = "<server name>"
$databaseName = "<database name>"
# Change the authentication method in the connection string, if needed.
$connStr = "Server = " + $serverName + "; Database = " + $databaseName + "; Integrated Security = True"
$database = Get-SqlDatabase -ConnectionString $connStr

# Create a SqlColumnMasterKeySettings object for your column master key
# using the -AllowEnclaveComputations parameter.
$cmkSettings = New-SqlCertificateStoreColumnMasterKeySettings -CertificateStoreLocation "CurrentUser" -Thumbprint $cert.Thumbprint -AllowEnclaveComputations

# Create column master key metadata in the database.
$cmkName = "CMK1"
New-SqlColumnMasterKey -Name $cmkName -InputObject $database -ColumnMasterKeySettings $cmkSettings

# Generate a column encryption key, encrypt it with the column master key and create column encryption key metadata in the database. 
$cekName = "CEK1"
New-SqlColumnEncryptionKey -Name $cekName  -InputObject $database -ColumnMasterKey $cmkName
```

### <a name="example---provision-enclave-enabled-keys-using-azure-key-vault"></a>Exemplo – Provisionamento de chaves habilitadas para enclave usando o Azure Key Vault
O exemplo de ponta a ponta abaixo mostra como provisionar chaves habilitadas para enclave, armazenando a chave mestra de coluna no Azure Key Vault. O script é baseado no exemplo em [Azure Key Vault sem separação de funções (exemplo)](configure-always-encrypted-keys-using-powershell.md#azure-key-vault-without-role-separation-example). É importante observar duas diferenças entre o fluxo de trabalho para chaves habilitadas para enclave em comparação com as chaves que não são habilitadas para enclave. 
- No script abaixo, o [**New-SqlCertificateStoreColumnMasterKeySettings**](https://docs.microsoft.com/powershell/module/sqlserver/new-sqlcertificatestorecolumnmasterkeysettings) usa o parâmetro `-AllowEnclaveComputations` para tornar a nova chave mestra de coluna habilitada para enclave. 
- O script abaixo chama o cmdlet [**Add-SqlAzureAuthenticationContext**](https://docs.microsoft.com/powershell/module/sqlserver/add-sqlazureauthenticationcontext) para entrar no Azure antes de chamar o cmdlet [**New-SqlAzureKeyVaultColumnMasterKeySettings**](https://docs.microsoft.com/powershell/module/sqlserver/new-sqlazurekeyvaultcolumnmasterkeysettings). Primeiro, é necessário entrar no Azure, pois o parâmetro `-AllowEnclaveComputations` faz com que o **New-SqlAzureKeyVaultColumnMasterKeySettings** chame o Azure Key Vault para assinar as propriedades da chave mestra de coluna.

```powershell
# Create a column master key in Azure Key Vault.
Import-Module Az
Connect-AzAccount
$SubscriptionId = "<Azure SubscriptionId>"
$resourceGroup = "<resource group name>"
$azureLocation = "<datacenter location>"
$akvName = "<key vault name>"
$akvKeyName = "<key name>"
$azureCtx = Set-AzConteXt -SubscriptionId $SubscriptionId # Sets the context for the below cmdlets to the specified subscription.
New-AzResourceGroup -Name $resourceGroup -Location $azureLocation # Creates a new resource group - skip, if your desired group already exists.
New-AzKeyVault -VaultName $akvName -ResourceGroupName $resourceGroup -Location $azureLocation # Creates a new key vault - skip if your vault already exists.
Set-AzKeyVaultAccessPolicy -VaultName $akvName -ResourceGroupName $resourceGroup -PermissionsToKeys get, create, delete, list, wrapKey,unwrapKey, sign, verify -UserPrincipalName $azureCtx.Account
$akvKey = Add-AzureKeyVaultKey -VaultName $akvName -Name $akvKeyName -Destination "Software"

# Connect to your database.
$serverName = "<server name>"
$databaseName = "<database name>"
# Change the authentication method in the connection string, if needed.
$connStr = "Server = " + $serverName + "; Database = " + $databaseName + "; Integrated Security = True"
$database = Get-SqlDatabase -ConnectionString $connStr

# Authenticate to Azure - it is required before calling the next cmdlet.
Add-SqlAzureAuthenticationContext -Interactive

# Create a SqlColumnMasterKeySettings object for your column master key. 
$cmkSettings = New-SqlAzureKeyVaultColumnMasterKeySettings -KeyURL $akvKey.ID -AllowEnclaveComputations

# Create column master key metadata in the database.
$cmkName = "CMK1"
New-SqlColumnMasterKey -Name $cmkName -InputObject $database -ColumnMasterKeySettings $cmkSettings

# Generate a column encryption key, encrypt it with the column master key and create column encryption key metadata in the database. 
$cekName = "CEK1"
New-SqlColumnEncryptionKey -Name $cekName -InputObject $database -ColumnMasterKey $cmkName
```

## <a name="next-steps"></a>Próximas etapas
- [Consultar colunas usando o Always Encrypted com enclaves seguros](always-encrypted-enclaves-query-columns.md)
- [Configurar a criptografia de coluna in-loco usando o Always Encrypted com enclaves seguros](always-encrypted-enclaves-configure-encryption.md)
- [Habilitar o Always Encrypted com enclaves seguros para as colunas criptografadas existentes](always-encrypted-enclaves-enable-for-encrypted-columns.md)
- [Desenvolver aplicativos usando o Always Encrypted com enclaves seguros](always-encrypted-enclaves-client-development.md) 

## <a name="see-also"></a>Consulte Também  
- [Tutorial: Introdução ao Always Encrypted com enclaves seguros usando o SSMS](../tutorial-getting-started-with-always-encrypted-enclaves.md)
- [Gerenciar chaves para Always Encrypted com enclaves seguros](always-encrypted-enclaves-manage-keys.md)
- [CREATE COLUMN MASTER KEY (Transact-SQL)](../../../t-sql/statements/create-column-master-key-transact-sql.md) 