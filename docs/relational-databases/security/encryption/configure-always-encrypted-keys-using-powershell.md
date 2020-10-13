---
title: Provisionar chaves do Always Encrypted usando o PowerShell | Microsoft Docs
description: Saiba como provisionar chaves para o Always Encrypted usando o módulo do SqlServer PowerShell para fornecer acesso de controle às chaves de criptografia e ao banco de dados.
ms.custom: ''
ms.date: 06/26/2019
ms.prod: sql
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
ms.assetid: 3bdf8629-738c-489f-959b-2f5afdaf7d61
author: jaszymas
ms.author: jaszymas
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 69f237c91f99f5bae5044b05aef669df8ef417d5
ms.sourcegitcommit: 4d370399f6f142e25075b3714e5c2ce056b1bfd0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/09/2020
ms.locfileid: "91867582"
---
# <a name="provision-always-encrypted-keys-using-powershell"></a>Provisionar chaves do Always Encrypted usando o PowerShell
[!INCLUDE [SQL Server Azure SQL Database](../../../includes/applies-to-version/sql-asdb.md)]

    
Este artigo fornece as etapas para provisionar chaves para Always Encrypted usando o [módulo do SqlServer PowerShell](../../../powershell/sql-server-powershell-provider.md). Você pode usar o PowerShell para provisionar chaves Always Encrypted [com e sem separação de funções](../../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md#KeyManagementRoles), oferecendo controle sobre quem tem acesso à criptografia de chaves real no repositório de chaves e quem tem acesso ao banco de dados. 

Para obter uma visão geral do gerenciamento de chaves do Always Encrypted, incluindo algumas práticas recomendadas de alto nível, confira [Visão geral do gerenciamento de chaves para Always Encrypted](../../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md).
Para obter informações sobre como começar a usar o módulo do SqlServer PowerShell para Always Encrypted, consulte [Configurar Always Encrypted usando o PowerShell](../../../relational-databases/security/encryption/configure-always-encrypted-using-powershell.md).


## <a name="key-provisioning-without-role-separation"></a><a name="KeyProvisionWithoutRoles"></a> Provisionamento de chave sem separação de funções

O método de provisionamento de chave descrito nesta seção não dá suporte à separação de funções entre os Administradores de Segurança e DBAs. Algumas das etapas a seguir combinam operações em chaves físicas com operações em metadados de chaves. Portanto, esse método de provisionamento das chaves é recomendado para organizações que usam o modelo de DevOps ou se o banco de dados está hospedado na nuvem e a principal meta é impedir que os administradores de nuvem (mas não os DBAs locais) acessem dados confidenciais. Isso não é recomendável se os adversários em potencial incluem DBAs ou se os DBAs não devem ter acesso a dados confidenciais.

Antes de executar as etapas que envolvem o acesso a chaves de texto não criptografado ou ao repositório de chaves (identificado na coluna **Acessa chaves de texto não criptografado/repositório de chaves** na tabela abaixo), verifique se o ambiente do PowerShell está sendo executado em um computador seguro e diferente do computador que hospeda o banco de dados. Para obter mais informações, consulte [Considerações de Segurança para o Gerenciamento de Chaves](overview-of-key-management-for-always-encrypted.md#security-considerations-for-key-management).


Tarefa  |Artigo  |Acessa chaves de texto não criptografado/repositório de chaves  |Acessar banco de dados   
---------|---------|---------|---------
Etapa 1. Crie uma chave mestra de coluna em um repositório de chaves.<br><br>**Observação:** O módulo do SqlServer PowerShell não dá suporte a essa etapa. Para realizar essa tarefa da linha de comando, use ferramentas especificas para o repositório de chaves selecionado. |[Criar e armazenar chaves mestras de coluna para Always Encrypted](../../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md) | Sim | Não     
Etapa 2.  Inicie um ambiente do PowerShell e importe o módulo do SqlServer PowerShell.  |   [Configurar Always Encrypted usando o PowerShell](../../../relational-databases/security/encryption/configure-always-encrypted-using-powershell.md)   |    Não    | Não         
Etapa 3.  Conecte-se ao servidor e banco de dados.     |     [Conectar a um banco de dados](../../../relational-databases/security/encryption/configure-always-encrypted-using-powershell.md#connectingtodatabase)    |    Não     | Sim         
Etapa 4.  Crie um objeto *SqlColumnMasterKeySettings* contendo informações sobre o local da sua chave mestra de coluna. SqlColumnMasterKeySettings é um objeto que existe na memória (no PowerShell). Use o cmdlet específico para o repositório de chaves.   |     [New-SqlAzureKeyVaultColumnMasterKeySettings](/powershell/sqlserver/sqlserver/vlatest/new-sqlazurekeyvaultcolumnmasterkeysettings)<br><br>[New-SqlCertificateStoreColumnMasterKeySettings](/powershell/sqlserver/sqlserver/vlatest/new-sqlcertificatestorecolumnmasterkeysettings)<br><br>[New-SqlCngColumnMasterKeySettings](/powershell/sqlserver/sqlserver/vlatest/new-sqlcngcolumnmasterkeysettings)<br><br>[New-SqlCspColumnMasterKeySettings](/powershell/sqlserver/sqlserver/vlatest/new-sqlcspcolumnmasterkeysettings)        |   Não      | Não         
Etapa 5.  Crie os metadados da chave mestra de coluna no banco de dados.      |    [New-SqlColumnMasterKey](/powershell/sqlserver/sqlserver/vlatest/new-sqlcolumnmasterkey)<br><br>**Observação:** nos bastidores, o cmdlet emite a instrução [CREATE COLUMN MASTER KEY (Transact-SQL)](../../../t-sql/statements/create-column-master-key-transact-sql.md) para criar metadados de chave.|    Não     |    Sim
Etapa 6.  Autentique no Azure se a chave mestra de coluna estiver armazenada no Cofre de Chaves do Azure. | [Add-SqlAzureAuthenticationContext](/powershell/sqlserver/sqlserver/vlatest/add-sqlazureauthenticationcontext)    |  Sim   | Não         
Etapa 7.  Gere uma nova chave de criptografia de coluna, criptografe-a com a chave mestra de coluna e crie metadados de chave de criptografia de coluna no banco de dados.     |    [New-SqlColumnEncryptionKey](/powershell/sqlserver/sqlserver/vlatest/new-sqlcolumnencryptionkey)<br><br>**Observação:** use uma variação do cmdlet que gera e criptografa internamente uma chave de criptografia de coluna.<br><br>**Observação:** nos bastidores, o cmdlet emite a instrução [CREATE COLUMN ENCRYPTION KEY (Transact-SQL)](../../../t-sql/statements/create-column-encryption-key-transact-sql.md) para criar metadados de chave.  | Sim | Sim
  

## <a name="windows-certificate-store-without-role-separation-example"></a>Repositório de Certificados do Windows sem separação de funções (exemplo)

Esse script é um exemplo de ponta a ponta para gerar uma chave mestra de coluna que é um certificado no Repositório de Certificados do Windows, gerando e criptografando uma chave de criptografia de coluna e criando metadados de chave em um banco de dados do SQL Server. 


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

# Create a SqlColumnMasterKeySettings object for your column master key. 
$cmkSettings = New-SqlCertificateStoreColumnMasterKeySettings -CertificateStoreLocation "CurrentUser" -Thumbprint $cert.Thumbprint

# Create column master key metadata in the database.
$cmkName = "CMK1"
New-SqlColumnMasterKey -Name $cmkName -InputObject $database -ColumnMasterKeySettings $cmkSettings


# Generate a column encryption key, encrypt it with the column master key and create column encryption key metadata in the database. 
$cekName = "CEK1"
New-SqlColumnEncryptionKey -Name $cekName  -InputObject $database -ColumnMasterKey $cmkName
```

## <a name="azure-key-vault-without-role-separation-example"></a>Cofre de Chaves do Azure sem separação de funções (exemplo)

Esse script é um exemplo de ponta a ponta para provisionar e configurar um Cofre de Chaves do Azure, gerar uma chave mestra de coluna no cofre, gerar e criptografar uma chave de criptografia de coluna e criar metadados de chave em um Banco de Dados SQL do Azure.


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

# Connect to your database (Azure SQL database).
Import-Module "SqlServer"
$serverName = "<Azure SQL server name>.database.windows.net"
$databaseName = "<database name>"
# Change the authentication method in the connection string, if needed.
$connStr = "Server = " + $serverName + "; Database = " + $databaseName + "; Authentication = Active Directory Integrated"
$database = Get-SqlDatabase -ConnectionString $connStr

# Create a SqlColumnMasterKeySettings object for your column master key. 
$cmkSettings = New-SqlAzureKeyVaultColumnMasterKeySettings -KeyURL $akvKey.ID

# Create column master key metadata in the database.
$cmkName = "CMK1"
New-SqlColumnMasterKey -Name $cmkName -InputObject $database -ColumnMasterKeySettings $cmkSettings

# Authenticate to Azure
Add-SqlAzureAuthenticationContext -Interactive

# Generate a column encryption key, encrypt it with the column master key and create column encryption key metadata in the database. 
$cekName = "CEK1"
New-SqlColumnEncryptionKey -Name $cekName -InputObject $database -ColumnMasterKey $cmkName
```

## <a name="cngksp-without-role-separation-example"></a>CNG/KSP sem separação de funções (exemplo)

Esse script é um exemplo de ponta a ponta para gerar uma chave mestra de coluna em um repositório de chaves que implementa a API CNG (Cryptography Next Generation), gerando e criptografando uma chave de criptografia de coluna e criando metadados de chave em um banco de dados do SQL Server.

O exemplo utiliza o repositório de chaves que usa o Provedor de Armazenamento de Chaves do Microsoft Software. Você pode optar por modificar o exemplo para usar outro repositório, como o módulo de segurança de hardware. Para fazer isso, você precisará verificar se o KSP (provedor de repositório de chaves) que implementa a CNG para seu dispositivo está instalado corretamente em seu computador. Você precisará substituir `Microsoft Software Key Storage Provider` pelo nome do KSP do dispositivo.


```powershell
# Create a column master key in a key store that has a CNG provider, a.k.a key store provider (KSP).
$cngProviderName = "Microsoft Software Key Storage Provider" # If you have an HSM, you can use a KSP for your HSM instead of a Microsoft KSP
$cngAlgorithmName = "RSA"
$cngKeySize = 2048 # Recommended key size for Always Encrypted column master keys
$cngKeyName = "AlwaysEncryptedKey" # Name identifying your new key in the KSP
$cngProvider = New-Object System.Security.Cryptography.CngProvider($cngProviderName)
$cngKeyParams = New-Object System.Security.Cryptography.CngKeyCreationParameters
$cngKeyParams.provider = $cngProvider
$cngKeyParams.KeyCreationOptions = [System.Security.Cryptography.CngKeyCreationOptions]::OverwriteExistingKey
$keySizeProperty = New-Object System.Security.Cryptography.CngProperty("Length", [System.BitConverter]::GetBytes($cngKeySize), [System.Security.Cryptography.CngPropertyOptions]::None);
$cngKeyParams.Parameters.Add($keySizeProperty)
$cngAlgorithm = New-Object System.Security.Cryptography.CngAlgorithm($cngAlgorithmName)
$cngKey = [System.Security.Cryptography.CngKey]::Create($cngAlgorithm, $cngKeyName, $cngKeyParams)

# Import the SqlServer module.
Import-Module "SqlServer"

# Connect to your database.
$serverName = "<server name>"
$databaseName = "<database name>"
# Change the authentication method in the connection string, if needed.
$connStr = "Server = " + $serverName + "; Database = " + $databaseName + "; Integrated Security = True"
$database = Get-SqlDatabase -ConnectionString $connStr

# Create a SqlColumnMasterKeySettings object for your column master key. 
$cmkSettings = New-SqlCngColumnMasterKeySettings -CngProviderName $cngProviderName -KeyName $cngKeyName

# Create column master key metadata in the database.
$cmkName = "CMK1"
New-SqlColumnMasterKey -Name $cmkName -InputObject $database -ColumnMasterKeySettings $cmkSettings

# Generate a column encryption key, encrypt it with the column master key and create column encryption key metadata in the database. 
$cekName = "CEK1"
New-SqlColumnEncryptionKey -Name $cekName -InputObject $database -ColumnMasterKey $cmkName
```

## <a name="key-provisioning-with-role-separation"></a><a name="KeyProvisionWithRoles"></a> Provisionamento de chave com separação de funções

Esta seção fornece as etapas para configurar a criptografia na qual os administradores de segurança não têm acesso ao banco de dados e os administradores de banco de dados não têm acesso às chaves de texto não criptografado ou ao repositório de chaves.


### <a name="security-administrator"></a>Administrador de segurança

Antes de executar as etapas que envolvem o acesso a chaves de texto não criptografado ou ao repositório de chaves (identificado na coluna **Acessa chaves de texto não criptografado/repositório de chaves** na tabela abaixo), verifique se:
1.  O ambiente do PowerShell é executado em um computador seguro diferente daquele que hospeda o banco de dados.
2.  Os DBAs na sua organização não têm acesso ao computador (isso sabotaria o propósito da separação de funções).

Para obter mais informações, consulte [Considerações de Segurança para o Gerenciamento de Chaves](overview-of-key-management-for-always-encrypted.md#security-considerations-for-key-management).


Tarefa  |Artigo  |Acessa chaves de texto não criptografado/repositório de chaves  |Acessar banco de dados  
---------|---------|---------|---------
Etapa 1. Crie uma chave mestra de coluna em um repositório de chaves.<br><br>**Observação:** O módulo do SqlServer não dá suporte a essa etapa. Para realizar essa tarefa da linha de comando, você precisa usar ferramentas especificas para o tipo do seu repositório de chaves.     | [Criar e armazenar chaves mestras de coluna para Always Encrypted](../../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md)  |    Sim    | Não 
Etapa 2.  Inicie uma sessão do PowerShell e importe o módulo do SqlServer.      |     [Importar o módulo do SqlServer](../../../relational-databases/security/encryption/configure-always-encrypted-using-powershell.md#importsqlservermodule)     | Não | Não         
Etapa 3.  Crie um objeto *SqlColumnMasterKeySettings* contendo informações sobre o local da sua chave mestra de coluna. *SqlColumnMasterKeySettings* é um objeto que existe na memória (no PowerShell). Use o cmdlet específico para o repositório de chaves. |      [New-SqlAzureKeyVaultColumnMasterKeySettings](/powershell/sqlserver/sqlserver/vlatest/new-sqlazurekeyvaultcolumnmasterkeysettings)<br><br>[New-SqlCertificateStoreColumnMasterKeySettings](/powershell/sqlserver/sqlserver/vlatest/new-sqlcertificatestorecolumnmasterkeysettings)<br><br>[New-SqlCngColumnMasterKeySettings](/powershell/sqlserver/sqlserver/vlatest/new-sqlcngcolumnmasterkeysettings)<br><br>[New-SqlCspColumnMasterKeySettings](/powershell/sqlserver/sqlserver/vlatest/new-sqlcspcolumnmasterkeysettings)   | Não         | Não         
Etapa 4.  Autentique no Azure, se a chave mestra de coluna estiver armazenada no Cofre de Chaves do Azure |    [Add-SqlAzureAuthenticationContext](/powershell/sqlserver/sqlserver/vlatest/add-sqlazureauthenticationcontext)    |Sim|Não         
Etapa 5.  Gere uma nova chave de criptografia de coluna, criptografe-a com a chave mestra para produzir um valor criptografado da chave de criptografia de coluna.     |   [New-SqlColumnEncryptionKeyEncryptedValue](/powershell/sqlserver/sqlserver/vlatest/new-sqlcolumnencryptionkeyencryptedvalue)     |    Sim    | Não        
Etapa 6.  Compartilhe o local da nova chave mestra de coluna (o nome do provedor e o caminho principal da chave mestra de coluna) e do valor criptografado da chave de criptografia de coluna para o DBA.  | Confira os exemplos abaixo.        |   Não      | Não         

### <a name="dba"></a>DBA 

Os DBAs usam as informações recebidas do Administrador de Segurança (etapa 6 acima) para criar e gerenciar os metadados de chave Always Encrypted no banco de dados.

Tarefa  |Artigo  |Acessa chaves de texto não criptografado  |Acessar banco de dados   
---------|---------|---------|---------
Etapa 1.  Forneça o local da chave mestra de coluna e um valor criptografado da chave de criptografia de coluna para o Administrador de Segurança. |Confira os exemplos abaixo. | Não | Não
Etapa 2.  Inicie um ambiente do PowerShell e importe o módulo do SqlServer.  | [Configurar Always Encrypted usando o PowerShell](../../../relational-databases/security/encryption/configure-always-encrypted-using-powershell.md)  | Não | Não
Etapa 3.  Conecte-se ao seu servidor e um banco de dados. | [Conectar a um banco de dados](../../../relational-databases/security/encryption/configure-always-encrypted-using-powershell.md#connectingtodatabase) | Não | Sim
Etapa 4.  Crie um objeto SqlColumnMasterKeySettings contendo informações sobre o local da sua chave mestra de coluna. SqlColumnMasterKeySettings é um objeto que existe na memória. | New-SqlColumnMasterKeySettings | Não | Não
Etapa 5. Crie os metadados da chave mestra de coluna no banco de dados | [New-SqlColumnMasterKey](/powershell/sqlserver/sqlserver/vlatest/new-sqlcolumnmasterkey)<br>**Observação:** nos bastidores, o cmdlet emite a instrução [CREATE COLUMN MASTER KEY (Transact-SQL)](../../../t-sql/statements/create-column-master-key-transact-sql.md) para criar metadados da chave mestra da coluna. | Não | Sim
Etapa 6. Crie os metadados de chave de criptografia de coluna no banco de dados. | New-SqlColumnEncryptionKey<br>**Observação:** DBAs usam uma variação do cmdlet que cria apenas os metadados de chave de criptografia de coluna.<br>Nos bastidores, o cmdlet emite a instrução [CREATE COLUMN ENCRYPTION KEY (Transact-SQL)](../../../t-sql/statements/create-column-encryption-key-transact-sql.md) para criar metadados da chave de criptografia de coluna. | Não | Sim
  
## <a name="windows-certificate-store-with-role-separation-example"></a>Repositório de Certificados do Windows com separação de funções (exemplo)

### <a name="security-administrator"></a>Administrador de segurança


```powershell
# Create a column master key in Windows Certificate Store.
$storeLocation = "CurrentUser"
$certPath = "Cert:" + $storeLocation + "\My"
$cert = New-SelfSignedCertificate -Subject "AlwaysEncryptedCert" -CertStoreLocation $certPath -KeyExportPolicy Exportable -Type DocumentEncryptionCert -KeyUsage DataEncipherment -KeySpec KeyExchange

# Import the SqlServer module
Import-Module "SqlServer"

# Create a SqlColumnMasterKeySettings object for your column master key. 
$cmkSettings = New-SqlCertificateStoreColumnMasterKeySettings -CertificateStoreLocation "CurrentUser" -Thumbprint $cert.Thumbprint

# Generate a column encryption key, encrypt it with the column master key to produce an encrypted value of the column encryption key.
$encryptedValue = New-SqlColumnEncryptionKeyEncryptedValue -TargetColumnMasterKeySettings $cmkSettings

# Share the location of the column master key and an encrypted value of the column encryption key with a DBA, via a CSV file on a share drive
$keyDataFile = "Z:\keydata.txt"
"KeyStoreProviderName, KeyPath, EncryptedValue" > $keyDataFile
$cmkSettings.KeyStoreProviderName + ", " + $cmkSettings.KeyPath + ", " + $encryptedValue >> $keyDataFile

# Read the key data back to verify
$keyData = Import-Csv $keyDataFile
$keyData.KeyStoreProviderName
$keyData.KeyPath
$keyData.EncryptedValue 
```

### <a name="dba"></a>DBA

```powershell
# Obtain the location of the column master key and the encrypted value of the column encryption key from your Security Administrator, via a CSV file on a share drive.
$keyDataFile = "Z:\keydata.txt"
$keyData = Import-Csv $keyDataFile

# Import the SqlServer module
Import-Module "SqlServer"

# Connect to your database.
$serverName = "<server name>"
$databaseName = "<database name>"
$connStr = "Server = " + $serverName + "; Database = " + $databaseName + "; Integrated Security = True"
$database = Get-SqlDatabase -ConnectionString $connStr

# Create a SqlColumnMasterKeySettings object for your column master key. 
$cmkSettings = New-SqlColumnMasterKeySettings -KeyStoreProviderName $keyData.KeyStoreProviderName -KeyPath $keyData.KeyPath

# Create column master key metadata in the database.
$cmkName = "CMK1"
New-SqlColumnMasterKey -Name $cmkName -InputObject $database -ColumnMasterKeySettings $cmkSettings

# Generate a  column encryption key, encrypt it with the column master key and create column encryption key metadata in the database. 
$cekName = "CEK1"
New-SqlColumnEncryptionKey -Name $cekName -InputObject $database -ColumnMasterKey $cmkName -EncryptedValue $keyData.EncryptedValue
```  
 
## <a name="next-steps"></a>Próximas etapas    
- [Configurar a criptografia de coluna usando o Always Encrypted com o PowerShell](configure-column-encryption-using-powershell.md)  
- [Girar chaves do Always Encrypted usando o PowerShell](../../../relational-databases/security/encryption/rotate-always-encrypted-keys-using-powershell.md)
- [Desenvolver aplicativos usando o Always Encrypted](always-encrypted-client-development.md)

## <a name="see-also"></a>Consulte Também    
- [Always Encrypted](../../../relational-databases/security/encryption/always-encrypted-database-engine.md)    
- [Visão geral do gerenciamento de chaves do Always Encrypted](../../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md)
- [Criar e armazenar chaves mestras de coluna para Always Encrypted](../../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md)
- [Configurar Always Encrypted usando o PowerShell](../../../relational-databases/security/encryption/configure-always-encrypted-using-powershell.md)
- [Provisionar chaves Always Encrypted usando o SQL Server Management Studio](configure-always-encrypted-keys-using-ssms.md)
- [CREATE COLUMN MASTER KEY (Transact-SQL)](../../../t-sql/statements/create-column-master-key-transact-sql.md)
- [DROP COLUMN MASTER KEY (Transact-SQL)](../../../t-sql/statements/drop-column-master-key-transact-sql.md)
- [CREATE COLUMN ENCRYPTION KEY (Transact-SQL)](../../../t-sql/statements/create-column-encryption-key-transact-sql.md)
- [ALTER COLUMN ENCRYPTION KEY (Transact-SQL)](../../../t-sql/statements/alter-column-encryption-key-transact-sql.md)
- [DROP COLUMN ENCRYPTION KEY (Transact-SQL)](../../../t-sql/statements/drop-column-encryption-key-transact-sql.md) 
- [sys.column_master_keys (Transact-SQL)](../../../relational-databases/system-catalog-views/sys-column-master-keys-transact-sql.md)
- [sys.column_encryption_keys (Transact-SQL)](../../../relational-databases/system-catalog-views/sys-column-encryption-keys-transact-sql.md)