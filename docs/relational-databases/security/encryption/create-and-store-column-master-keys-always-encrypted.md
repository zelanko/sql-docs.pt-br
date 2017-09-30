---
title: Criar e armazenar chaves mestras de coluna (Always Encrypted) | Microsoft Docs
ms.custom: 
ms.date: 07/01/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-security
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 856e8061-c604-4ce4-b89f-a11876dd6c88
caps.latest.revision: 26
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: 96ec352784f060f444b8adcae6005dd454b3b460
ms.openlocfilehash: 9c4dfd2aa4f511e9ef7615dccf05ed46757f1e0c
ms.contentlocale: pt-br
ms.lasthandoff: 09/27/2017

---
# <a name="create-and-store-column-master-keys-always-encrypted"></a>Criar e armazenar chaves mestras de coluna (Always Encrypted)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

*Chaves mestras de coluna* são chaves de proteção de chave usadas no Always Encrypted para criptografar chaves de criptografia de coluna. As chaves mestras de coluna devem ser armazenadas em um repositório de chaves confiável e precisam estar acessíveis aos aplicativos que precisam criptografar ou descriptografar dados e às ferramentas para a configuração do Sempre Criptografado e o gerenciamento de chaves Sempre Criptografado.

Este artigo fornece detalhes para selecionar um repositório de chaves e criar chaves mestras de coluna para o Sempre Criptografado. Para obter uma visão detalhada, confira [Overview of Key Management for Always Encrypted](../../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md)(Visão geral do gerenciamento de chaves do Sempre Criptografado).

## <a name="selecting-a-key-store-for-your-column-master-key"></a>Selecionando um repositório de chaves para sua chave mestra de coluna

O Always Encrypted dá suporte a vários repositórios de chaves para armazenar chaves mestras de coluna do Always Encrypted. Os repositórios de chaves com suporte variam de acordo com o driver e a versão utilizada.

Há duas categorias de alto nível de repositórios de chaves a serem consideradas – *Repositórios de Chaves Locais*e *Repositórios de Chaves Centralizados*.

###  <a name="local-or-centralized-key-store"></a>Repositório de Chaves Local ou Centralizado?

* **Repositórios de Chaves Locais** – só podem ser usados por aplicativos em computadores que contêm o repositório de chaves local. Em outras palavras, você precisa replicar o repositório de chaves e a chave em cada computador que executa o aplicativo. Um exemplo de um repositório de chaves local é o Repositório de Certificados do Windows. Ao usar um repositório de chaves local, você precisa verificar se o repositório de chaves existe em todos os computadores que hospedam o aplicativo e se o computador contém as chaves mestras de coluna que o aplicativo precisa para acessar os dados protegidos usando o Sempre Criptografado. Quando você provisiona uma chave mestra de coluna pela primeira vez ou quando altera (gira) a chave, é necessário verificar se a chave é implantada em todos os computadores que hospedam o(s) aplicativo(s).

* **Repositórios de Chaves Centralizados** – atende a aplicativos em vários computadores. Um exemplo de um repositório de chaves centralizado é o [Cofre de Chaves do Azure](https://azure.microsoft.com/services/key-vault/). Normalmente, um repositório de chaves centralizado facilita o gerenciamento de chaves, pois não é necessário manter várias cópias das chaves mestras de coluna em vários computadores. Você precisa garantir que os aplicativos estão configurados para se conectarem ao repositório de chaves centralizado.

### <a name="which-key-stores-are-supported-in-always-encrypted-enabled-client-drivers"></a>Quais repositórios de chaves têm suporte em drivers de cliente habilitados para Sempre Criptografado?

Drivers de cliente habilitados para Sempre Criptografado são drivers de cliente do SQL Server que têm suporte interno para incorporar o Sempre Criptografado nos aplicativos cliente. Os drivers habilitados para Sempre Criptografado incluem alguns provedores internos de repositórios de chaves populares. Observe que alguns drivers também permitem implementar e registrar um provedor personalizado de repositórios de chaves mestras de coluna, para que você possa usar qualquer repositório de chaves, mesmo se não houver nenhum provedor interno para ele. Ao decidir entre um provedor interno e um provedor personalizado, considere que o uso de um provedor interno, normalmente, significa menos alterações em seus aplicativos (em alguns casos, é necessária apenas a alteração de uma cadeia de conexão de banco de dados).

Os provedores internos disponíveis dependem do driver, da versão do driver e do sistema operacional selecionados.  Confira a documentação do Sempre Criptografado de seu driver específico para determinar quais repositórios de chaves têm suporte pronto para uso e se o driver dá suporte a provedores personalizados de repositórios de chaves.

- [Desenvolver aplicativos usando o Always Encrypted com o Provedor de Dados .NET Framework para SQL Server](../../../relational-databases/security/encryption/develop-using-always-encrypted-with-net-framework-data-provider.md)


### <a name="supported-tools"></a>Ferramentas com suporte

Você pode usar o [SQL Server Management Studio](../../../ssms/sql-server-management-studio-ssms.md) e o [módulo SqlServer do PowerShell](https://blogs.technet.microsoft.com/dataplatforminsider/2016/06/30/sql-powershell-july-2016-update) para configurar o Always Encrypted e gerenciar chaves dele. Para obter uma lista de quais repositórios de chaves essas ferramenta dão suporte, veja:

- [Configurar o Always Encrypted usando o SQL Server Management Studio](../../../relational-databases/security/encryption/configure-always-encrypted-using-sql-server-management-studio.md)
- [Configurar o Always Encrypted usando o PowerShell](../../../relational-databases/security/encryption/configure-always-encrypted-using-powershell.md)


## <a name="creating-column-master-keys-in-windows-certificate-store"></a>Criando chaves mestras de coluna no Repositório de Certificados do Windows    

Uma chave mestra de coluna pode ser um certificado armazenado no Repositório de Certificados do Windows. Observe que um driver habilitado para Sempre Criptografado não verifica uma data de validade nem uma cadeia de autoridade de certificado. Um certificado é usado apenas como um par de chaves consistindo em uma chave pública e uma chave privada.

Para ser uma chave mestra de coluna válida, um certificado deve:
* ser um certificado X.509.
* ser armazenado em uma das duas localizações de repositório de certificados: *computador local* ou *usuário atual*. (Para criar um certificado no local repositório de certificados do computador local, é necessário ser um administrador no computador de destino.)
* conter uma chave privada (o tamanho recomendado das chaves no certificado é de 2.048 bits ou superior).
* ser criado para a troca de chaves.


Há várias maneiras de criar um certificado que é uma chave mestra de coluna válida, mas a opção mais simples é criar um certificado autoassinado.


### <a name="create-a-self-signed-certificate-using-powershell"></a>Criar um certificado autoassinado usando o PowerShell

Use o cmdlet [New-SelfSignedCertificate](https://technet.microsoft.com/library/hh848633.aspx) para criar um certificado autoassinado. O exemplo a seguir mostra como gerar um certificado que pode ser usado como uma chave mestra de coluna para o Sempre Criptografado.

```
New-SelfSignedCertificate is a Windows PowerShell cmdlet that creates a self-signed certificate. The below examples show how to generate a certificate that can be used as a column master key for Always Encrypted.
$cert = New-SelfSignedCertificate -Subject "AlwaysEncryptedCert" -CertStoreLocation Cert:CurrentUserMy -KeyExportPolicy Exportable -Type DocumentEncryptionCert -KeyUsage KeyEncipherment -KeySpec KeyExchange -KeyLength 2048 

# To create a certificate in the local machine certificate store location you need to run the cmdlet as an administrator.
$cert = New-SelfSignedCertificate -Subject "AlwaysEncryptedCert" -CertStoreLocation Cert:LocalMachineMy -KeyExportPolicy Exportable -Type DocumentEncryptionCert -KeyUsage KeyEncipherment -KeySpec KeyExchange -KeyLength 2048
```

### <a name="create-a-self-signed-certificate-using-sql-server-management-studio-ssms"></a>Criar um certificado autoassinado usando o SSMS (SQL Server Management Studio)

Para obter detalhes, veja [Configure Always Encrypted using SQL Server Management Studio](../../../relational-databases/security/encryption/configure-always-encrypted-using-sql-server-management-studio.md)(Configurar o Sempre Criptografado usando o SQL Server Management Studio).
Para obter um tutorial passo a passo que usa o SSMS e armazena as chaves do Always Encrypted no Repositório de Certificados do Windows, veja [Always Encrypted – Proteger dados confidenciais no Banco de Dados SQL com a criptografia de banco de dados e armazenar as chaves de criptografia no Repositório de Certificados do Windows](https://azure.microsoft.com/documentation/articles/sql-database-always-encrypted/).


### <a name="making-certificates-available-to-applications-and-users"></a>Disponibilizando certificados para aplicativos e usuários

Se a chave mestra de coluna for um certificado armazenado na localização do repositório de certificados do *computador local* , você precisará exportar o certificado com a chave privada e importá-lo para todos os computadores que hospedam aplicativos que devem criptografar ou descriptografar dados armazenados em colunas criptografadas ou ferramentas para a configuração do Always Encrypted e o gerenciamento das chaves do Always Encrypted. Além disso, cada usuário deve ter uma permissão de leitura para o certificado armazenado na localização do repositório de certificados do computador local para poder usar o certificado como uma chave mestra de coluna.

Se a chave mestra de coluna for um certificado armazenado na localização do repositório de certificados do *computador local* , você precisará exportar o certificado com a chave privada e importá-lo para a localização do repositório de certificados do usuário atual de todas as contas de usuário que executam aplicativos que devem criptografar ou descriptografar dados armazenados em colunas criptografadas ou ferramentas para a configuração do Always Encrypted e o gerenciamento das chaves do Always Encrypted (em todos os computadores que contém esses aplicativos ou essas ferramentas). Nenhuma configuração de permissão é necessária – depois de fazer logon em um computador, um usuário pode acessar todos os certificados em sua localização do repositório de certificados do usuário atual.

#### <a name="using-powershell"></a>Usando o PowerShell
Use os cmdlets [Import-PfxCertificate](https://msdn.microsoft.com/library/hh848625.aspx) e [Export-PfxCertificate](https://msdn.microsoft.com/library/hh848635.aspx) para importar e exportar um certificado.

#### <a name="using-microsoft-management-console"></a>Usando o Console de Gerenciamento Microsoft 

Para conceder a um usuário a permissão *Leitura* para um certificado armazenado na localização do repositório de certificados do computador local, siga estas etapas:

1.  Abra um prompt de comando e digite **mmc**.
2.  No console do MMC, no menu **Arquivo** , clique em **Adicionar/Remover Snap-in**.
3.  Na caixa de diálogo **Adicionar/Remover Snap-in** , clique em **Adicionar**.
4.  Na caixa de diálogo **Adicionar Snap-in Autônomo** , clique em **Certificados**e em **Adicionar**.
5.  Na caixa de diálogo Snap-in de **certificados** , clique em **Conta de computador**e em **Concluir**.
6.  Na caixa de diálogo **Adicionar Snap-in Autônomo** , clique em **Fechar**.
7.  Na caixa de diálogo **Adicionar/Remover Snap-in**, clique em **OK**.
8.  No snap-in de **Certificados**, localize o certificado na pasta **Certificados > Pessoal**, clique com o botão direito do mouse no Certificado, aponte para **Todas as Tarefas** e clique em **Gerenciar Chaves Privadas**.
9.  Na caixa de diálogo **Segurança**, adicione permissões de leitura para uma conta de usuário, se necessário.

## <a name="creating-column-master-keys-in-azure-key-vault"></a>Criando chaves mestras de coluna no Cofre de Chaves do Azure

O Cofre de Chaves do Azure ajudará a proteger segredos e chaves de criptografia, sendo uma opção conveniente para armazenar chaves mestras de coluna do Sempre Criptografado, especialmente se seus aplicativos estiverem hospedados no Azure. Para criar uma chave no [Cofre de Chaves do Azure](https://azure.microsoft.com/documentation/articles/key-vault-get-started/), é necessário ter uma [assinatura do Azure](https://azure.microsoft.com/free/) e um Cofre de Chaves do Azure.

#### <a name="using-powershell"></a>Usando o PowerShell

O exemplo a seguir cria um novo Cofre de Chaves do Azure e uma chave e, em seguida, concede permissões ao usuário desejado.

```
# Create a column master key in Azure Key Vault.
Login-AzureRmAccount
$SubscriptionId = "<Azure subscription ID>"
$resourceGroup = "<resource group name>"
$azureLocation = "<key vault location>"
$akvName = "<key vault name>"
$akvKeyName = "<column master key name>"
$azureCtx = Set-AzureRMContext -SubscriptionId $SubscriptionId # Sets the context for the below cmdlets to the specified subscription.
New-AzureRmResourceGroup –Name $resourceGroup –Location $azureLocation # Creates a new resource group - skip, if you desire group already exists.
New-AzureRmKeyVault -VaultName $akvName -ResourceGroupName $resourceGroup -Location $azureLocation -SKU premium # Creates a new key vault - skip if your vault already exists.
Set-AzureRmKeyVaultAccessPolicy -VaultName $akvName -ResourceGroupName $resourceGroup -PermissionsToKeys get, create, delete, list, update, import, backup, restore, wrapKey, unwrapKey, sign, verify -UserPrincipalName $azureCtx.Account
$akvKey = Add-AzureKeyVaultKey -VaultName $akvName -Name $akvKeyName -Destination HSM
```

#### <a name="sql-server-management-studio-ssms"></a>SQL Server Management Studio (SSMS)

Para obter um tutorial passo a passo que usa o SSMS e armazena as chaves do Always Encrypted em um Cofre de Chaves do Azure, veja [Always Encrypted – Proteger dados confidenciais no Banco de Dados SQL com a criptografia de dados e armazenar as chaves de criptografia no Cofre de Chaves do Azure](https://azure.microsoft.com/documentation/articles/sql-database-always-encrypted-azure-key-vault).

### <a name="making-azure-key-vault-keys-available-to-applications-and-users"></a>Disponibilizando as chaves do Cofre de Chaves do Azure para aplicativos e usuários

Ao usar uma chave do Cofre de Chaves do Azure como uma chave mestra de coluna, seu aplicativo precisa se autenticar no Azure e a identidade do aplicativo precisa ter as seguintes permissões no cofre de chaves: *get*, *unwrapKey*e *verify*. 

Para provisionar as chaves de criptografia de coluna protegidas com uma chave mestra de coluna armazenada no Cofre de Chaves do Azure, é necessário ter as permissões *get*, *unwrapKey*, *wrapKey*, *sign*e *verify* . Além disso, para criar uma nova chave em um Cofre de Chaves do Azure, é necessário ter a permissão *create* ; para listar o conteúdo da chave de cofres, você precisa da permissão *list* .

#### <a name="using-powershell"></a>Usando o PowerShell

Para permitir que usuários e aplicativos acessem as chaves reais no Cofre de Chaves do Azure, é necessário definir a política de acesso do cofre ([Set-AzureRmKeyVaultAccessPolicy](https://msdn.microsoft.com/library/mt603625.aspx)):

```
$vaultName = "<vault name>"
$resourceGroupName = "<resource group name>"
$userPrincipalName = "<user to grant access to>"
$clientId = "<client Id>"

# grant users permissions to the keys:
Set-AzureRmKeyVaultAccessPolicy -VaultName $vaultName -ResourceGroupName $resourceGroupName -PermissionsToKeys create,get,wrapKey,unwrapKey,sign,verify,list -UserPrincipalName $userPrincipalName
# grant applications permissions to the keys:
Set-AzureRmKeyVaultAccessPolicy  -VaultName $vaultName  -ResourceGroupName $resourceGroupName -ServicePrincipalName $clientId -PermissionsToKeys get,wrapKey,unwrapKey,sign,verify,list
```

## <a name="creating-column-master-keys-in-hardware-security-modules-using-cng"></a>Criando chaves mestras de coluna em módulos de segurança de hardware usando o CNG

Uma chave mestra de coluna do Sempre Criptografado pode ser armazenada em um repositório de chaves que implementa a API do CNG (Cryptography Next Generation). Normalmente, esse tipo de repositório é um HSM (módulo de segurança de hardware). Um HSM é um dispositivo físico que protege e gerencia chaves digitais e fornece processamento de criptografia. Tradicionalmente, os HSMs são fornecidos na forma de um cartão plug-in ou um dispositivo externo que é anexado diretamente a um computador (HSMs locais) ou a um servidor de rede.

Para disponibilizar um HSM para aplicativos em determinado computador, um KSP (Provedor de Armazenamento de Chaves), que implementa o CNG, deve ser instalado e configurado no computador. Um driver de cliente do Sempre Criptografado (um provedor de repositórios de chaves mestras de coluna no driver), usa o KSP para criptografar e descriptografar as chaves de criptografia de coluna, protegidas com a chave mestra de coluna armazenada no repositório de chaves.

O Windows inclui o Provedor de Armazenamento de Chaves do Software Microsoft – um KSP baseado em software, que pode ser usado para fins de teste. Veja [CNG Key Storage Providers](https://msdn.microsoft.com/library/windows/desktop/bb931355.aspx)(Provedores de Armazenamento de Chaves do CNG).

### <a name="creating-column-master-keys-in-a-key-store-using-cngksp"></a>Criando chaves mestras de coluna em um repositório de chaves usando o CNG/KSP

Uma chave mestra de coluna deve ser uma chave assimétrica (um par de chaves pública/privada), que usa o algoritmo RSA. O tamanho de chave recomendado é de 2.048 ou maior.

#### <a name="using-hsm-specific-tools"></a>Usando ferramentas específicas do HSM
Confira a documentação do HSM.

#### <a name="using-powershell"></a>Usando o PowerShell

Você pode usar as APIs do .NET para criar uma chave em um repositório de chaves usando o CNG no PowerShell.


```
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
```

#### <a name="using-sql-server-management-studio"></a>Usando o SQL Server Management Studio

Veja [Provisioning Column Master using SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/mt757096.aspx#Anchor_2)(Provisionando chaves mestras usando o SQL Server Management Studio [SSMS]).


### <a name="making-cng-keys-available-to-applications-and-users"></a>Disponibilizando chaves do CNG para aplicativos e usuários

Confira a documentação do HSM e do KSP para saber como configurar o KSP em um computador e conceder acesso ao HSM a aplicativos e usuários.

## <a name="creating-column-master-keys-in-hardware-security-modules-using-capi"></a>Criando chaves mestras de coluna em módulos de segurança de hardware usando a CAPI

Uma chave mestra de coluna do Sempre Criptografado pode ser armazenada em um repositório de chaves que implementa a CAPI (Cryptography API). Normalmente, um repositório desse tipo é um HSM (módulo de segurança de hardware) – um dispositivo físico que protege e gerencia chaves digitais e fornece processamento de criptografia. Tradicionalmente, os HSMs são fornecidos na forma de um cartão plug-in ou um dispositivo externo que é anexado diretamente a um computador (HSMs locais) ou a um servidor de rede.

Para disponibilizar um HSM para aplicativos em determinado computador, um CSP (Provedor de Serviços de Criptografia), que implementa a CAPI, deve ser instalado e configurado no computador. Um driver de cliente do Sempre Criptografado (um provedor de repositórios de chaves mestras de coluna no driver), usa o CSP para criptografar e descriptografar as chaves de criptografia de coluna, protegidas com a chave mestra de coluna armazenada no repositório de chaves. Observação: a CAPI é uma API herdada e preterida. Se um KSP estiver disponível para o HSM, será recomendável usá-lo, em vez de um CSP ou uma CAPI.

Um CSP deve dar suporte ao algoritmo RSA para ser usado com o Sempre Criptografado.

O Windows inclui os seguintes CSPs baseados em software (não apoiados por um HSM) que dão suporte ao RSA e que podem ser usados para fins de teste: Microsoft Enhanced RSA e AES Cryptographic Provider.

### <a name="creating-column-master-keys-in-a-key-store-using-capicsp"></a>Criando chaves mestras de coluna em um repositório de chaves usando a CAPI ou o CSP

Uma chave mestra de coluna deve ser uma chave assimétrica (um par de chaves pública/privada), que usa o algoritmo RSA. O tamanho de chave recomendado é de 2.048 ou maior.

#### <a name="using-hsm-specific-tools"></a>Usando ferramentas específicas do HSM
Confira a documentação do HSM.

#### <a name="using-sql-server-management-studio-ssms"></a>Usando o SSMS (SQL Server Management Studio)
Veja a seção Provisionando chaves mestras de coluna em Configure Always Encrypted using SQL Server Management Studio (Configurar o Sempre Criptografado usando o SQL Server Management Studio).

 
### <a name="making-cng-keys-available-to-applications-and-users"></a>Disponibilizando chaves do CNG para aplicativos e usuários
Confira a documentação do HSM e do CSP para saber como configurar o CSP em um computador e conceder acesso ao HSM a aplicativos e usuários.
 
 
## <a name="next-steps"></a>Próximas etapas  
  
- [Configurar chaves do Always Encrypted usando o PowerShell](../../../relational-databases/security/encryption/configure-always-encrypted-keys-using-powershell.md)
- [Girar chaves Always Encrypted usando o PowerShell](../../../relational-databases/security/encryption/rotate-always-encrypted-keys-using-powershell.md)
- [Configurar o Always Encrypted usando o SQL Server Management Studio](../../../relational-databases/security/encryption/configure-always-encrypted-using-sql-server-management-studio.md)

  
## <a name="additional-resources"></a>Recursos adicionais  

- [Overview of Key Management for Always Encrypted](../../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md)
- [Always Encrypted (mecanismo de banco de dados)](../../../relational-databases/security/encryption/always-encrypted-database-engine.md)
- [Desenvolver aplicativos usando o Always Encrypted com o Provedor de Dados .NET Framework para SQL Server](../../../relational-databases/security/encryption/develop-using-always-encrypted-with-net-framework-data-provider.md)
- [Blog do Always Encrypted](https://blogs.msdn.microsoft.com/sqlsecurity/tag/always-encrypted/)
    


