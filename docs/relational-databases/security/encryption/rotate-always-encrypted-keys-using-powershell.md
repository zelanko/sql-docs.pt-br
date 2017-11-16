---
title: Girar as chaves Always Encrypted usando o PowerShell | Microsoft Docs
ms.custom: 
ms.date: 05/17/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: dbe-security
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 5117b4fd-c8d3-48d5-87c9-756800769f31
caps.latest.revision: "19"
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 8c3ac81162f54adbbbc5256f622b465cfc08425b
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="rotate-always-encrypted-keys-using-powershell"></a>Girar chaves Always Encrypted usando o PowerShell
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

Este artigo fornece as etapas para girar chaves para Always Encrypted usando o módulo do SqlServer PowerShell. Para obter informações sobre como começar a usar o módulo do SqlServer PowerShell para Always Encrypted, consulte [Configurar Always Encrypted usando o PowerShell](../../../relational-databases/security/encryption/configure-always-encrypted-using-powershell.md).

O giro de chaves Always Encrypted é o processo de substituir uma chave existente por uma nova. Pode ser necessário girar uma chave se ela tiver sido comprometida ou para manter a conformidade com políticas e regulamentos da sua organização que exigem que chaves criptográficas sejam giradas com regularidade. 

Always Encrypted usa dois tipos de chaves, portanto, há dois fluxos de trabalho de rotação de chaves de alto nível; rotação de chaves mestras de coluna e chaves de criptografia de coluna.

* **Rotação de chaves de criptografia da coluna** - envolve descriptografar dados criptografados com a chave atual e criptografá-los novamente usando a nova chave de criptografia de coluna. Como girar uma chave de criptografia de coluna requer acesso ao banco de dados e às chaves, a rotação de chaves de criptografia de coluna só pode ser executada sem a separação de funções.
* **Rotação de chave mestra de coluna** - envolve a descriptografia de chaves de criptografia de coluna que são protegidas com a chave mestra de coluna atual, criptografando-os novamente usando a nova chave mestra de coluna e atualizando os metadados para os dois tipos de chaves. A rotação de chave mestra de coluna pode ser concluída com ou sem a separação de funções (usando o módulo do SqlServer PowerShell).


## <a name="column-master-key-rotation-without-role-separation"></a>Rotação de chave mestra da coluna sem separação de funções
O método de girar uma chave mestra de coluna descrito nesta seção não dá suporte à separação de funções entre um Administrador de Segurança e um DBA. Algumas das etapas abaixo combinam operações nas chaves físicas com operações em metadados de chaves, por isso esse fluxo de trabalho é recomendado para organizações que usam o modelo de DevOps ou quando o banco de dados está hospedado na nuvem e o principal objetivo for impedir que os administradores de nuvem (mas não os DBAs locais) acessem dados confidenciais. Isso não é recomendável se os adversários em potencial incluem DBAs, ou se os DBAs simplesmente não devem ter acesso a dados confidenciais.  


| Tarefa | Artigo | Acessa chaves de texto não criptografado/repositório de chaves| Acessar banco de dados
|:---|:---|:---|:---
|Etapa 1. Crie uma nova chave mestra de coluna em um repositório de chaves.<br><br>**Observação:** o módulo do SqlServer PowerShell não dá suporte a essa etapa. Para realizar essa tarefa da linha de comando, você precisa usar ferramentas especificas para o seu repositório de chaves. | Criar e armazenar chaves mestras de coluna (Always Encrypted)| Sim | Não
|Etapa 2. Inicie um ambiente do PowerShell e importe o módulo do SqlServer | [Importar o módulo do SqlServer](../../../relational-databases/security/encryption/configure-always-encrypted-using-powershell.md#importsqlservermodule) | Não | Não
|Etapa 3. Conecte-se ao servidor e banco de dados. | [Conectando a um banco de dados](../../../relational-databases/security/encryption/configure-always-encrypted-using-powershell.md#connectingtodatabase) | Não | Sim
|Etapa 4. Crie um objeto SqlColumnMasterKeySettings contendo informações sobre o local da sua nova chave mestra de coluna. SqlColumnMasterKeySettings é um objeto que existe na memória (no PowerShell). Para criá-lo, você precisa usar o cmdlet específico para o repositório de chaves. |[New-SqlAzureKeyVaultColumnMasterKeySettings](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/new-sqlazurekeyvaultcolumnmasterkeysettings)<br><br>[New-SqlCertificateStoreColumnMasterKeySettings](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/new-sqlcertificatestorecolumnmasterkeysettings)<br><br>[New-SqlCngColumnMasterKeySettings](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/new-sqlcngcolumnmasterkeysettings)<br><br>[New-SqlCspColumnMasterKeySettings](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/new-sqlcspcolumnmasterkeysettings)<br> | Não | Não
|Etapa 5. Crie os metadados da nova chave mestra de coluna no banco de dados. | [New-SqlColumnMasterKey](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/new-sqlcolumnmasterkey)<br><br>**Observação:** nos bastidores, esse cmdlet emite a instrução [CREATE COLUMN MASTER KEY (Transact-SQL)](../../../t-sql/statements/create-column-master-key-transact-sql.md) para criar metadados de chave. | Não | Sim
|Etapa 6. Autentique no Azure, se a chave mestra de coluna atual ou nova estiverem armazenadas no Cofre de Chaves do Azure | [Add-SqlAzureAuthenticationContext](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/add-sqlazureauthenticationcontext) | Sim | Não
|Etapa 7. Inicie a rotação criptografando cada uma das chaves de criptografia de coluna, que atualmente está protegida pela chave mestra de coluna antiga, usando a nova chave mestra de coluna. Após essa etapa, cada chave de criptografia de coluna afetada (associada com a chave mestra de coluna antiga que está sendo girado) é criptografada com ambas as chaves mestras de coluna antiga e nova, e os dois valores são criptografados nos metadados do banco de dados.| [Invoke-SqlColumnMasterKeyRotation](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/invoke-sqlcolumnmasterkeyrotation) | Sim | Sim
|Etapa 8. Coordene com os administradores de todos os aplicativos que consultam colunas criptografadas no banco de dados (e são protegidos pela chave mestra de coluna antiga), para que eles possam garantir os aplicativos possam acessar a nova chave mestra de coluna.| [Criar e armazenar chaves mestras de coluna (Always Encrypted)](../../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md) | Sim | Não
|Etapa 9. Conclua a rotação<br><br>**Observação:** antes de executar essa etapa, verifique se todos os aplicativos que consultam colunas criptografadas que são protegidas com a chave mestra de coluna antiga foram configurados para usar a nova chave mestra de coluna. Se você executar essa etapa prematuramente, alguns desses aplicativos não poderão descriptografar os dados. Conclua a rotação removendo os valores criptografados dos bancos de dados que foram criados com a chave mestra de coluna antiga. Isso remove a associação entre a chave mestra de coluna antiga e as chaves de criptografia de coluna que ela protege. |[Complete-SqlColumnMasterKeyRotation](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/complete-sqlcolumnmasterkeyrotation)| Não | Sim
|Etapa 10. Remova os metadados de chave mestra de coluna antiga. |[Remove-SqlColumnMasterKey](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/remove-sqlcolumnmasterkey)| Não | Sim

> [!NOTE]
> É altamente recomendável não excluir a chave mestra de coluna antiga permanentemente após a rotação. Em vez disso, você deve manter a chave mestra de coluna antiga em seu repositório de chaves atual ou arquivá-la em outro local seguro. Se você restaurar seu banco de dados de um arquivo de backup para um ponto *anterior à* configuração da nova chave mestra de coluna, precisará da chave antiga para acessar os dados.

### <a name="rotating-a-column-master-key-without-role-separation-windows-certificate-example"></a>Girando uma chave mestra de coluna sem separação de funções (exemplo de Certificado do Windows)

O script abaixo é um exemplo de ponta a ponta que substitui uma chave mestra de coluna existente (CMK1) por uma nova chave mestra de coluna (CMK2).

```
# Create a new column master key in Windows Certificate Store.
$cert = New-SelfSignedCertificate -Subject "AlwaysEncryptedCert" -CertStoreLocation Cert:CurrentUser\My -KeyExportPolicy Exportable -Type DocumentEncryptionCert -KeyUsage KeyEncipherment -KeySpec KeyExchange -KeyLength 2048

# Import the SqlServer module
Import-Module "SqlServer"

# Connect to your database.
$serverName = "<server name>"
$databaseName = "<database name>"
$connStr = "Server = " + $serverName + "; Database = " + $databaseName + "; Integrated Security = True"
$connection = New-Object Microsoft.SqlServer.Management.Common.ServerConnection
$connection.ConnectionString = $connStr
$connection.Connect()
$server = New-Object Microsoft.SqlServer.Management.Smo.Server($connection)
$database = $server.Databases[$databaseName]

# Create a SqlColumnMasterKeySettings object for your new column master key. 
$newCmkSettings = New-SqlCertificateStoreColumnMasterKeySettings -CertificateStoreLocation "CurrentUser" -Thumbprint $cert.Thumbprint

# Create metadata for your new column master key in the database.
$newCmkName = "CMK2"
New-SqlColumnMasterKey -Name $newCmkName -InputObject $database -ColumnMasterKeySettings $newCmkSettings

# Initiate the rotation from the current column master key to the new column master key.
$oldCmkName = "CMK1"
Invoke-SqlColumnMasterKeyRotation -SourceColumnMasterKeyName $oldCmkName -TargetColumnMasterKeyName $newCmkName -InputObject $database

# Complete the rotation of the old column master key.
Complete-SqlColumnMasterKeyRotation -SourceColumnMasterKeyName $oldCmkName  -InputObject $database

# Remove the old column master key metadata.
Remove-SqlColumnMasterKey -Name $oldCmkName -InputObject $database
```

## <a name="column-master-key-rotation-with-role-separation"></a>Rotação de chave mestra da coluna com separação de funções

O fluxo de trabalho de rotação de chave mestra de coluna descrito nesta seção garante a separação entre um Administrador de Segurança e um DBA.

> [!IMPORTANT]
> Antes de executar as etapas em que *Acessa chaves de texto não criptografado/repositório de chaves*=**Sim** na tabela a seguir (etapas que acessam chaves de texto não criptografado ou o repositório de chaves), verifique se o ambiente do PowerShell é executado em um computador seguro diferente daquele que hospeda o banco de dados. Para obter mais informações, consulte [Considerações de Segurança para o Gerenciamento de Chaves](../../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md#SecurityForKeyManagement).


### <a name="part-1-dba"></a>Parte 1: DBA

Um DBA recupera metadados da chave mestra de coluna a ser girada e das chaves de criptografia do coluna afetadas associadas à chave mestra de coluna atual. O DBA compartilha todas essas informações com um Administrador de Segurança.


| Tarefa | Artigo | Acessa chaves de texto não criptografado/repositório de chaves| Acessar banco de dados
|:---|:---|:---|:---
|Etapa 1. Inicie um ambiente do PowerShell e importe o módulo do SqlServer. | [Importar o módulo do SqlServer](../../../relational-databases/security/encryption/configure-always-encrypted-using-powershell.md#importsqlservermodule) | Não | Nenhuma
|Etapa 2. Conecte-se ao seu servidor e um banco de dados. | [Conectar a um banco de dados](../../../relational-databases/security/encryption/configure-always-encrypted-using-powershell.md#connectingtodatabase) | Não | Sim
|Etapa 3. Recupere os metadados da chave mestra de coluna antiga.| [Get-SqlColumnMasterKey](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/get-sqlcolumnmasterkey) | Não | Sim
|Etapa 4. Recupere os metadados das chaves de criptografia de coluna, protegidas pela antiga chave mestra de coluna, incluindo seus valores criptografados. | [Get-SqlColumnEncryptionKey](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/get-sqlcolumnencryptionkey) | Não | Sim
|Etapa 5. Compartilhe o local da chave mestra de coluna (o nome do provedor e o caminho principal da chave mestra de coluna) e dos valores criptografados das chaves de criptografia de coluna correspondentes, protegidas pela chave mestra de coluna antiga.| Veja os exemplos abaixo. | Não | Não

### <a name="part-2-security-administrator"></a>Parte 2: Administrador de Segurança

O Administrador de Segurança gera uma nova chave mestra de coluna, criptografa novamente as chaves de criptografia de coluna afetadas com a nova chave mestra de coluna e compartilha as informações da nova chave mestra de coluna, bem como o conjunto de novos valores criptografados para as chaves de criptografia de coluna afetadas, com o DBA.

| Tarefa | Artigo | Acessar chaves de texto não criptografado/repositório de chaves| Acessar banco de dados
|:---|:---|:---|:---
|Etapa 1. Obtenha com o DBA o local da chave mestra de coluna antiga e dos valores criptografados das chaves de criptografia de coluna correspondentes, protegidas pela chave mestra de coluna antiga.|N/A<br>Veja os exemplos abaixo.|Não| Não
|Etapa 2. Crie uma nova chave mestra de coluna em um repositório de chaves.<br><br>**Observação:** o módulo do SqlServer não dá suporte a essa etapa. Para realizar essa tarefa da linha de comando, você precisa usar ferramentas especificas para o tipo do seu repositório de chaves.|[Criando e armazenando chaves mestras de coluna (Always Encrypted)](../../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md)| Sim | Não
|Etapa 3. Inicie um ambiente do PowerShell e importe o módulo do SqlServer. | [Importar o módulo do SqlServer](../../../relational-databases/security/encryption/configure-always-encrypted-using-powershell.md#importsqlservermodule) | Não | Não
|Etapa 4. Crie um objeto SqlColumnMasterKeySettings contendo informações sobre o local da sua chave mestra de coluna **antiga** . SqlColumnMasterKeySettings é um objeto que existe na memória (no PowerShell). |New-SqlColumnMasterKeySettings| Não | Não
|Etapa 5. Crie um objeto SqlColumnMasterKeySettings contendo informações sobre o local da sua **nova** chave mestra de coluna. SqlColumnMasterKeySettings é um objeto que existe na memória (no PowerShell). Para criá-lo, você precisa usar o cmdlet específico para o repositório de chaves. | [New-SqlAzureKeyVaultColumnMasterKeySettings](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/new-sqlazurekeyvaultcolumnmasterkeysettings)<br><br>[New-SqlCertificateStoreColumnMasterKeySettings](https://msdn.microsoft.com/library/mt759816.aspx)<br><br>[New-SqlCngColumnMasterKeySettings](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/new-sqlcngcolumnmasterkeysettings)<br><br>[New-SqlCspColumnMasterKeySettings](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/new-sqlcspcolumnmasterkeysettings)| Não | Não
|Etapa 6. Autentique no Azure se a chave mestra de coluna antiga (atual) ou nova estiverem armazenadas no Cofre de Chaves do Azure. | [Add-SqlAzureAuthenticationContext](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/add-sqlazureauthenticationcontext) | Sim | Não
|Etapa 7. Criptografe novamente cada valor das chaves de criptografia de coluna, que atualmente está protegida pela chave mestra de coluna antiga, usando a nova chave mestra de coluna. | [New-SqlColumnEncryptionKeyEncryptedValue](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/new-sqlcolumnencryptionkeyencryptedvalue)<br><br>**Observação:** ao chamar esse cmdlet, passe os objetos SqlColumnMasterKeySettings para ambas as chaves mestras de coluna antiga e nova, juntamente com um valor da chave de criptografia de coluna a ser recriptografada.|Sim|Não
|Etapa 8. Compartilhe o local da nova chave mestra de coluna (o nome do provedor e o caminho principal da chave mestra de coluna) e do conjunto de novos valores criptografados das chaves de criptografia de coluna, com seu DBA.| Veja os exemplos abaixo. | Não | Não

> [!NOTE]
> É altamente recomendável não excluir a chave mestra de coluna antiga permanentemente após a rotação. Em vez disso, você deve manter a chave mestra de coluna antiga em seu repositório de chaves atual ou arquivá-la em outro local seguro. Se você restaurar seu banco de dados de um arquivo de backup para um ponto *anterior à* configuração da nova chave mestra de coluna, precisará da chave antiga para acessar os dados.


### <a name="part-3-dba"></a>Parte 3: DBA

O DBA cria metadados para a nova chave mestra de coluna e atualiza os metadados das chaves de criptografia de coluna afetadas para adicionar o novo conjunto de valores criptografados. Nesta etapa, o DBA também coordena com os administradores dos aplicativos consultando colunas de criptografia, que garantem que o aplicativo pode acessar a nova chave mestra de coluna. Depois que todos os aplicativos são configurados para usar a nova chave mestra de coluna, o DBA remove o conjunto antigo de valores criptografados e os metadados da chave mestra de coluna antiga.

| Tarefa | Artigo | Acessar chaves de texto não criptografado/repositório de chaves| Acessar banco de dados
|:---|:---|:---|:---
|Etapa 1. Obtenha do Administrador de Segurança o local da nova chave mestra de coluna e o novo conjunto de valores criptografados das chaves de criptografia de coluna correspondentes, protegidas pela chave mestra de coluna antiga.| Veja os exemplos abaixo. | Não | Não
|Etapa 2. Inicie um ambiente do PowerShell e importe o módulo do SqlServer. | [Importar o módulo do SqlServer](../../../relational-databases/security/encryption/configure-always-encrypted-using-powershell.md#importsqlservermodule) | Não | Não
|Etapa 3. Conecte-se ao seu servidor e um banco de dados. | [Conectando a um banco de dados](../../../relational-databases/security/encryption/configure-always-encrypted-using-powershell.md#connectingtodatabase) | Não | Sim
|Etapa 4. Crie um objeto SqlColumnMasterKeySettings contendo informações sobre o local da sua nova chave mestra de coluna. SqlColumnMasterKeySettings é um objeto que existe na memória (no PowerShell). |New-SqlColumnMasterKeySettings| Não| Não
|Etapa 5. Crie os metadados da nova chave mestra de coluna no banco de dados.|[New-SqlColumnMasterKey](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/new-sqlcolumnmasterkey)<br><br>**Observação:** nos bastidores, esse cmdlet emite a instrução [CREATE COLUMN MASTER KEY (Transact-SQL)](../../../t-sql/statements/create-column-master-key-transact-sql.md) para criar metadados de chave. | Não | Sim
|Etapa 6. Recupere os metadados das chaves de criptografia de coluna, protegidas pela antiga chave mestra de coluna.| [Get-SqlColumnEncryptionKey](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/get-sqlcolumnencryptionkey)| Não | Sim
|Etapa 7. Adicione um novo valor criptografado (produzido usando a nova chave mestra de coluna) aos metadados para cada chave de criptografia de coluna afetada.|[Add-SqlColumnEncryptionKeyValue](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/add-sqlcolumnencryptionkeyvalue)|Não|Sim
|Etapa 8. Coordene com os administradores de todos os aplicativos que consultam colunas criptografadas no banco de dados (e são protegidos pela chave mestra de coluna antiga), para que eles possam garantir os aplicativos possam acessar a nova chave mestra de coluna.|[Criando e armazenando chaves mestras de coluna (Always Encrypted)](../../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md)| Não|Não
|Etapa 9. Conclua a rotação removendo os valores criptografados associados à chave mestra de coluna antiga do banco de dados.<br><br>**Observação:** antes de executar essa etapa, verifique se todos os aplicativos que consultam colunas criptografadas que são protegidas com a chave mestra de coluna antiga foram configurados para usar a nova chave mestra de coluna. Se você executar essa etapa prematuramente, alguns desses aplicativos não poderão descriptografar os dados.<br><br>Essa etapa remove uma associação entre a chave mestra de coluna antiga e as chaves de criptografia de coluna que ela protege. | [Complete-SqlColumnMasterKeyRotation](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/complete-sqlcolumnmasterkeyrotation)<br><br>Outra opção, você pode usar [Remove-SqlColumnEncryptionKeyValue](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/remove-sqlcolumnencryptionkeyvalue) | Não|Sim
|Etapa 10. Remover os metadados da chave mestra de coluna antiga do banco de dados| [Remove-SqlColumnMasterKey](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/remove-sqlcolumnmasterkey)| Não|Sim

### <a name="rotating-a-column-master-key-with-role-separation-windows-certificate-example"></a>Girar uma chave mestra de coluna com separação de funções (exemplo de Certificado do Windows)

O script abaixo é um exemplo de ponta a ponta para gerar uma nova chave mestra de coluna que é o certificado no repositório de Certificados do Windows, girando uma chave mestra de coluna existente (atual) para substituí-la pela nova chave mestra de coluna. O script supõe que o banco de dados de destino contém a chave mestra de coluna, chamada CMK1 (que será girada), o qual criptografa algumas chaves de criptografia de coluna.

Parte 1: DBA

```
# Import the SqlServer module.
Import-Module "SqlServer"

# Connect to your database.
$serverName = "<server name>"
$databaseName = "<database name>"
$connStr = "Server = " + $serverName + "; Database = " + $databaseName + "; Integrated Security = True"
$connection = New-Object Microsoft.SqlServer.Management.Common.ServerConnection
$connection.ConnectionString = $connStr
$connection.Connect()
$server = New-Object Microsoft.SqlServer.Management.Smo.Server($connection)
$database = $server.Databases[$databaseName]

# Retrieve the data about the old column master key, which needs to be rotated.
$oldCmkName = "CMK1"
$oldCmk = Get-SqlColumnMasterKey -Name $oldCmkName -InputObject $database


# Share the location of the old column master key with a Security Administrator, via a CSV file on a share drive.
$oldCmkDataFile = "Z:\oldcmkdata.txt"
"KeyStoreProviderName, KeyPath" > $oldCmkDataFile
$oldCmk.KeyStoreProviderName +", " + $oldCmk.KeyPath >> $oldCmkDataFile


# Find column encryption keys associated with the old column master key and provide the encrypted values of column encryption keys to the Security Administrator, via a CSV file on a share drive.
$ceks = Get-SqlColumnEncryptionKey -InputObject $database
$oldCekValuesFile = "Z:\oldcekvalues.txt"
"CEKName, CEKEncryptedValue" > $oldCekValuesFile 
for($i=0; $i -lt $ceks.Length; $i++){
    if($ceks[$i].ColumnEncryptionKeyValues.Length -eq 2) {
        # This column encryption has 2 encrypted values - let's check, if it is associated with the old column master key.
        if($ceks[$i].ColumnEncryptionKeyValues[0].ColumnMasterKeyName -eq $oldCmkName -or $ceks[$i].ColumnEncryptionKeyValues[1].ColumnMasterKeyName -eq $oldCmkName) {
            Write-Host $ceks[$i].Name "already has 2 encrypted values and therefore" $oldCmkName + "cannot be rotated"
            exit 1
        }
    }
    if($ceks[$i].ColumnEncryptionKeyValues[0].ColumnMasterKeyName -eq $oldCmkName) {# This column encryption key has 1 encrypted value that was produced using the old column master key
        # Save the name and the encrypted value of the column encryption key in the file.
        $encryptedValue =  "0x" + -join ($ceks[$i].ColumnEncryptionKeyValues[0].EncryptedValue |  foreach {$_.ToString("X2") } )
        $ceks[$i].Name + "," + $encryptedValue >> $oldCekValuesFile
    }
} 
```


Parte 2: Administrador de Segurança

```
# Obtain the location of the old column master key and the encrypted values of the corresponding column encryption keys, from your DBA, via a CSV file on a share drive.
$oldCmkDataFile = "Z:\oldcmkdata.txt"
$oldCmkData = Import-Csv $oldCmkDataFile
$oldCekValuesFile = "Z:\oldcekvalues.txt"
$oldCekValues = @(Import-Csv $oldCekValuesFile)

# Create a new column master key in Windows Certificate Store.
$storeLocation = "CurrentUser"
$certPath = "Cert:\" + $storeLocation + "\My"
$cert = New-SelfSignedCertificate -Subject "AlwaysEncryptedCert" -CertStoreLocation $certPath -KeyExportPolicy Exportable -Type DocumentEncryptionCert -KeyUsage DataEncipherment -KeySpec KeyExchange

# Import the SqlServer module.
Import-Module "SqlServer"

# Create a SqlColumnMasterKeySettings object for your old column master key. 
$oldCmkSettings = New-SqlColumnMasterKeySettings -KeyStoreProviderName $oldCmkData.KeyStoreProviderName -KeyPath $oldCmkData.KeyPath

# Create a SqlColumnMasterKeySettings object for your new column master key. 
$newCmkSettings = New-SqlCertificateStoreColumnMasterKeySettings -CertificateStoreLocation $storeLocation -Thumbprint $cert.Thumbprint


# Prepare a CSV file, you will use to share the encrypted values of column encryption keys, produced using the new column master key.
$newCekValuesFile = "Z:\newcekvalues.txt"
"CEKName, CEKEncryptedValue" > $newCekValuesFile

# Re-encrypt each value with the new column master key and save the new encrypted value in the file.
for($i=0; $i -lt $oldCekValues.Count; $i++){
    # Re-encrypt each value with the new CMK
    $newValue = New-SqlColumnEncryptionKeyEncryptedValue -TargetColumnMasterKeySettings $newCmkSettings -ColumnMasterKeySettings $oldCmkSettings -EncryptedValue $oldCekValues[$i].CEKEncryptedValue
    $oldCekValues[$i].CEKName + ", " + $newValue >> $newCekValuesFile
}

# Share the new column master key data with your DBA, via a CSV file.
$newCmkDataFile = $home + "\newcmkdata.txt"
"KeyStoreProviderName, KeyPath" > $newCmkDataFile
$newCmkSettings.KeyStoreProviderName +", " + $newCmkSettings.KeyPath >> $newCmkDataFile
```


Parte 3: DBA

```
# Obtain the location of the new column master key and the new encrypted values of the corresponding column encryption keys, from your Security Administrator, via a CSV file on a share drive.
$newCmkDataFile = "Z:\newcmkdata.txt"
$newCmkData = Import-Csv $newCmkDataFile
$newCekValuesFile = "Z:\newcekvalues.txt"
$newCekValues = @(Import-Csv $newCekValuesFile)

# Import the SqlServer module.
Import-Module "SqlServer"

# Connect to your database.
$serverName = "<server name>"
$databaseName = "<database name>"
$connStr = "Server = " + $serverName + "; Database = " + $databaseName + "; Integrated Security = True"
$connection = New-Object Microsoft.SqlServer.Management.Common.ServerConnection
$connection.ConnectionString = $connStr
$connection.Connect()
$server = New-Object Microsoft.SqlServer.Management.Smo.Server($connection)
$database = $server.Databases[$databaseName]

# Create a SqlColumnMasterKeySettings object for your new column master key. 
$newCmkSettings = New-SqlColumnMasterKeySettings -KeyStoreProviderName $newCmkData.KeyStoreProviderName -KeyPath $newCmkData.KeyPath
# Create metadata for the new column master key in the database.
$newCmkName = "CMK2"
New-SqlColumnMasterKey -Name $newCmkName -InputObject $database -ColumnMasterKeySettings $newCmkSettings


# Get all CEK objects
$oldCmkName = "CMK1"
$ceks = Get-SqlColumnEncryptionKey -InputObject $database
for($i=0; $i -lt $ceks.Length; $i++){
    if($ceks[$i].ColumnEncryptionKeyValues.Length -eq 2) {# This column encryption key has 2 encrypted values. Let's check, if it is associated with the old CMK.
        if($ceks[$i].ColumnEncryptionKeyValues[0].ColumnMasterKeyName -eq $oldCmkName -or $ceks[$i].ColumnEncryptionKeyValues[1].ColumnMasterKeyName -eq $oldCmkName) {
            Write-Host $ceks[$i].Name "already has 2 encrypted values and therefore" $oldCmkName + "cannot be rotated"
            exit 1
        }
    }
    if($ceks[$i].ColumnEncryptionKeyValues[0].ColumnMasterKeyName -eq $oldCmkName) {
        # Find the corresponding new encrypted value, received from the Security Administrator.
        $newValueRow = ($newCekValues| Where-Object {$_.CEKName -eq $ceks[$i].Name }[0])
        # Update the column encryption key metadata object by adding the new encrypted value
        Add-SqlColumnEncryptionKeyValue -ColumnMasterKeyName $newCmkName -Name $ceks[$i].Name -EncryptedValue $newValueRow.CEKEncryptedValue -InputObject $database 
    }
}

# Complete the rotation of the current column master key.
Complete-SqlColumnMasterKeyRotation -SourceColumnMasterKeyName $oldCmkName  -InputObject $database

# Remove the old column master key.
Remove-SqlColumnMasterKey -Name $oldCmkName -InputObject $database
```


## <a name="rotating-a-column-encryption-key"></a>Girando uma chave de criptografia de coluna

Girar uma chave de criptografia da coluna envolve descriptografar os dados criptografados com a chave atual em todas as colunas e criptografá-los novamente usando a nova chave de criptografia de coluna. Esse fluxo de trabalho de rotação requer acesso às chaves e ao banco de dados, não podendo, portanto, ser executado com a separação de funções. Observe que girar uma chave de criptografia de coluna pode demorar muito tempo se as tabelas que contém as colunas criptografadas com a chave que está sendo girada forem grandes. Portanto, sua organização precisa planejar uma rotação de chave de criptografia de coluna com muito cuidado.

Você pode girar uma chave de criptografia de coluna usando uma abordagem offline ou online. O primeiro método é provavelmente mais rápido, mas não é possível gravar seus aplicativos nas tabelas afetadas. A segunda abordagem provavelmente levará mais tempo, mas você pode limitar o intervalo de tempo durante o qual as tabelas afetadas não estão disponíveis para os aplicativos. Veja [Configurar criptografia de coluna usando o PowerShell](../../../relational-databases/security/encryption/configure-column-encryption-using-powershell.md) e [Set-SqlColumnEncryption](https://msdn.microsoft.com/library/mt759790.aspx) para obter mais detalhes.

| Tarefa | Artigo | Acessa chaves de texto não criptografado/repositório de chaves| Acessar banco de dados
|:---|:---|:---|:---
|Etapa 1. Inicie um ambiente do PowerShell e importe o módulo do SqlServer. | [Importar o módulo do SqlServer](../../../relational-databases/security/encryption/configure-always-encrypted-using-powershell.md#importsqlservermodule) | Não | Não
|Etapa 2. Conecte-se ao seu servidor e um banco de dados. | [Conectando a um banco de dados](../../../relational-databases/security/encryption/configure-always-encrypted-using-powershell.md#connectingtodatabase) | Não | Sim
|Etapa 3. Autentique no Azure se a chave mestra de coluna (que protege a chave de criptografia de coluna a ser girada) estiver armazenada no Cofre de Chaves do Azure. | [Add-SqlAzureAuthenticationContext](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/add-sqlazureauthenticationcontext) | Sim | Não
|Etapa 4. Gere uma nova chave de criptografia de coluna, criptografe-a com a chave mestra de coluna e crie metadados de chave de criptografia de coluna no banco de dados.  | [New-SqlColumnEncryptionKey](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/new-sqlcolumnencryptionkey)<br><br>**Observação:** use uma variação do cmdlet que gera e criptografa internamente uma chave de criptografia de coluna.<br>Nos bastidores, esse cmdlet emite a instrução [CREATE COLUMN ENCRYPTION KEY (Transact-SQL)](../../../t-sql/statements/create-column-encryption-key-transact-sql.md) para criar metadados de chave. | Sim | Sim
|Etapa 5. Localize todas as colunas criptografadas com a chave de criptografia de coluna antiga. | [Guia de Programação do SQL Server Management Objects (SMO)](../../../relational-databases/server-management-objects-smo/sql-server-management-objects-smo-programming-guide.md) | Não | Sim
|Etapa 6. Crie um objeto *SqlColumnEncryptionSettings* para cada coluna afetada.  SqlColumnMasterKeySettings é um objeto que existe na memória (no PowerShell). Especifica o esquema de criptografia de destino para uma coluna. Nesse caso, o objeto deve especificar que a coluna afetada deve ser criptografada usando a nova chave de criptografia de coluna. | [New-SqlColumnEncryptionSettings](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/new-sqlcolumnencryptionkeysettings) | Não | Não
|Etapa 7. Criptografe novamente as colunas identificadas na etapa 5 usando a nova chave de criptografia de coluna. | [Set-SqlColumnEncryption](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/set-sqlcolumnencryption)<br><br>**Observação:** esta etapa pode levar muito tempo. Seus aplicativos não poderão acessar as tabelas por meio da operação inteira ou parte dela, dependendo da abordagem (online versus offline) que você seleciona. | Sim | Sim
|Etapa 8. Remova os metadados da chave de criptografia de coluna antiga. | [Remove-SqlColumnEncryptionKey](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/remove-sqlcolumnencryptionkey) | Não | Sim

### <a name="example---rotating-a-column-encryption-key"></a>Exemplo: girando uma chave de criptografia de coluna

O script abaixo demonstra a rotação de uma chave de criptografia de coluna.  O script supõe que o banco de dados de destino contém algumas colunas criptografadas com uma chave de criptografia de coluna chamada CEK1 (que será girada), a qual é protegida usando uma chave mestra de coluna chamada CMK1 (a chave mestra de coluna não está armazenada no Cofre de Chaves do Azure).


```
# Import the SqlServer module.
Import-Module "SqlServer"

# Connect to your database.
$serverName = "<server name>"
$databaseName = "<database name>"
$connStr = "Server = " + $serverName + "; Database = " + $databaseName + "; Integrated Security = True"
$connection = New-Object Microsoft.SqlServer.Management.Common.ServerConnection
$connection.ConnectionString = $connStr
$connection.Connect()
$server = New-Object Microsoft.SqlServer.Management.Smo.Server($connection)
$database = $server.Databases[$databaseName]

# Generate a new column encryption key, encrypt it with the column master key and create column encryption key metadata in the database. 
$cmkName = "CMK1"
$newCekName = "CEK2"
New-SqlColumnEncryptionKey -Name $newCekName -InputObject $database -ColumnMasterKey $cmkName 


# Find all columns encrypted with the old column encryption key, and create a SqlColumnEncryptionSetting object for each column.
$ces = @()
$oldCekName = "CEK1"
$tables = $database.Tables
for($i=0; $i -lt $tables.Count; $i++){
    $columns = $tables[$i].Columns
    for($j=0; $j -lt $columns.Count; $j++) {
        if($columns[$j].isEncrypted -and $columns[$j].ColumnEncryptionKeyName -eq $oldCekName) {
            $threeColPartName = $tables[$i].Schema + "." + $tables[$i].Name + "." + $columns[$j].Name 
            $ces += New-SqlColumnEncryptionSettings -ColumnName $threeColPartName -EncryptionType $columns[$j].EncryptionType -EncryptionKey $newCekName
        }
     }
}

# Re-encrypt all columns, currently encrypted with the old column encryption key, using the new column encryption key.
Set-SqlColumnEncryption -ColumnEncryptionSettings $ces -InputObject $database -UseOnlineApproach -MaxDowntimeInSeconds 120 -LogFileDirectory .

# Remove the old column encryption key metadata.
Remove-SqlColumnEncryptionKey -Name $oldCekName -InputObject $database
```


  
## <a name="next-steps"></a>Próximas etapas  
    
- [Desenvolver aplicativos usando o Always Encrypted com o Provedor de Dados .NET Framework para SQL Server](../../../relational-databases/security/encryption/always-encrypted-client-development.md)
  
## <a name="additional-resources"></a>Recursos adicionais  

- [Visão geral do gerenciamento de chaves do Always Encrypted](../../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md)
- [Configurar Always Encrypted usando o PowerShell](../../../relational-databases/security/encryption/configure-always-encrypted-using-powershell.md)    
- [Always Encrypted (mecanismo de banco de dados)](../../../relational-databases/security/encryption/always-encrypted-database-engine.md)
- [Blog do Always Encrypted](https://blogs.msdn.microsoft.com/sqlsecurity/tag/always-encrypted/)

