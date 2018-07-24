---
title: 'PowerShell e CLI: habilitar a TDE do SQL usando sua própria chave do Azure Key Vault | Microsoft Docs'
description: Saiba como configurar um Data Warehouse e um Banco de Dados SQL do Azure para começar a usar a TDE (Transparent Data Encryption) para a criptografia em repouso usando o PowerShell ou CLI.
keywords: ''
documentationcenter: ''
author: aliceku
manager: craigg
editor: ''
ms.prod: ''
ms.reviewer: ''
ms.suite: sql
ms.prod_service: sql-database, sql-data-warehouse
ms.service: sql-database
ms.tgt_pltfrm: ''
ms.devlang: azurecli, powershell
ms.topic: conceptual
ms.date: 06/28/2018
ms.author: aliceku
monikerRange: = azuresqldb-current || = azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: d9419443e554c225bd2ee6708c8448787160b6de
ms.sourcegitcommit: c7a98ef59b3bc46245b8c3f5643fad85a082debe
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/12/2018
ms.locfileid: "38979170"
---
# <a name="powershell-and-cli-enable-transparent-data-encryption-using-your-own-key-from-azure-key-vault"></a>PowerShell e CLI: habilitar a Transparent Data Encryption usando sua própria chave no Azure Key Vault

[!INCLUDE[appliesto-xx-asdb-asdw-xxx-md](../../../includes/appliesto-xx-asdb-asdw-xxx-md.md)]

Este guia de instruções explica como usar uma chave do Azure Key Vault para a TDE (Transparent Data Encryption) no Data Warehouse ou no Banco de Dados SQL. Para saber mais sobre a TDE com suporte a BYOK (Bring Your Own Key), visite [TDE com Bring Your Own Key para SQL do Azure](transparent-data-encryption-byok-azure-sql.md). 

## <a name="prerequisites-for-powershell"></a>Pré-requisitos para PowerShell

- Você deve ter uma assinatura do Azure e ser um administrador na assinatura.
- [Recomendado, mas opcional] Ter um HSM (módulo de segurança de hardware) ou repositório de chaves local para criar uma cópia local do material da chave do Protetor de TDE.
- Você deve ter o Azure PowerShell versão 4.2.0 ou posterior instalado e em execução. 
- Criar um Azure Key Vault e uma chave para usar para a TDE.
   - [Instruções do PowerShell do Key Vault](https://docs.microsoft.com/azure/key-vault/key-vault-get-started)
   - [Instruções para usar um HSM (módulo de segurança de hardware) e o Key Vault](https://docs.microsoft.com/azure/key-vault/key-vault-get-started#a-idhsmaif-you-want-to-use-a-hardware-security-module-hsm)
 - O cofre de chaves deve ter as seguintes propriedades para ser usado para TDE:
   - [exclusão reversível](https://docs.microsoft.com/azure/key-vault/key-vault-ovw-soft-delete)
   - [Como usar a exclusão reversível do Key Vault com o PowerShell](https://docs.microsoft.com/azure/key-vault/key-vault-soft-delete-powershell) 
- A chave deve ter os seguintes atributos para ser usada para TDE:
   - Nenhuma data de expiração
   - Não estar desabilitada
   - Ser capaz de executar as operações *get*, *wrap key* e *unwrap key*

## <a name="step-1-assign-an-azure-ad-identity-to-your-server"></a>Etapa 1. Atribuir uma identidade do Microsoft Azure AD ao seu servidor 

Se você tiver um servidor existente, use o seguinte para adicionar uma identidade do Microsoft Azure AD ao seu servidor:

   ```powershell
   $server = Set-AzureRmSqlServer `
   -ResourceGroupName <SQLDatabaseResourceGroupName> `
   -ServerName <LogicalServerName> `
   -AssignIdentity
   ```

Se você estiver criando um servidor, use o cmdlet [New-AzureRmSqlServer](/powershell/module/azurerm.sql/new-azurermsqlserver) com a marca -Identity para adicionar uma identidade do Microsoft Azure AD durante a criação do servidor:

   ```powershell
   $server = New-AzureRmSqlServer `
   -ResourceGroupName <SQLDatabaseResourceGroupName> `
   -Location <RegionName> `
   -ServerName <LogicalServerName> `
   -ServerVersion "12.0" `
   -SqlAdministratorCredentials <PSCredential> `
   -AssignIdentity 
   ```

## <a name="step-2-grant-key-vault-permissions-to-your-server"></a>Etapa 2. Conceder permissões do Key Vault para seu servidor

Use o cmdlet [Set-AzureRmKeyVaultAccessPolicy](/powershell/module/azurerm.keyvault/set-azurermkeyvaultaccesspolicy) para conceder acesso ao servidor ao cofre de chaves antes de usar uma chave dele para a TDE.

   ```powershell
   Set-AzureRmKeyVaultAccessPolicy  `
   -VaultName <KeyVaultName> `
   -ObjectId $server.Identity.PrincipalId `
   -PermissionsToKeys get, wrapKey, unwrapKey
   ```

## <a name="step-3-add-the-key-vault-key-to-the-server-and-set-the-tde-protector"></a>Etapa 3. Adicionar a chave do Key Vault ao servidor e definir o Protetor de TDE

- Use o cmdlet [Add-AzureRmSqlServerKeyVaultKey](/powershell/module/azurerm.sql/add-azurermsqlserverkeyvaultkey) para adicionar a chave do Key Vault ao servidor.
- Use o cmdlet [Set-AzureRmSqlServerTransparentDataEncryptionProtector](/powershell/module/azurerm.sql/set-azurermsqlservertransparentdataencryptionprotector) para definir a chave como o Protetor de TDE para todos os recursos do servidor.
- Use o cmdlet [Get-AzureRmSqlServerTransparentDataEncryptionProtector](/powershell/module/azurerm.sql/get-azurermsqlservertransparentdataencryptionprotector) para confirmar que o Protetor de TDE foi configurado como pretendido.

> [!Note]
> O tamanho combinado do nome do cofre de chaves e o nome da chave não pode exceder 94 caracteres.
> 

>[!Tip]
>Um exemplo KeyId do Key Vault: https://contosokeyvault.vault.azure.net/keys/Key1/1a1a2b2b3c3c4d4d5e5e6f6f7g7g8h8h
>

   ```powershell
   <# Add the key from Key Vault to the server #>
   Add-AzureRmSqlServerKeyVaultKey `
   -ResourceGroupName <SQLDatabaseResourceGroupName> `
   -ServerName <LogicalServerName> `
   -KeyId <KeyVaultKeyId>

   <# Set the key as the TDE protector for all resources under the server #>
   Set-AzureRmSqlServerTransparentDataEncryptionProtector `
   -ResourceGroupName <SQLDatabaseResourceGroupName> `
   -ServerName <LogicalServerName> `
   -Type AzureKeyVault `
   -KeyId <KeyVaultKeyId> 

   <# To confirm that the TDE protector was configured as intended: #>
   Get-AzureRmSqlServerTransparentDataEncryptionProtector `
   -ResourceGroupName <SQLDatabaseResourceGroupName> `
   -ServerName <LogicalServerName> 
   ```

## <a name="step-4-turn-on-tde"></a>Etapa 4. Ativar a TDE 

Use o cmdlet [Set-AzureRMSqlDatabaseTransparentDataEncryption](/powershell/module/azurerm.sql/set-azurermsqldatabasetransparentdataencryption) para ativar a TDE.

   ```powershell
   Set-AzureRMSqlDatabaseTransparentDataEncryption `
   -ResourceGroupName <SQLDatabaseResourceGroupName> `
   -ServerName <LogicalServerName> `
   -DatabaseName <DatabaseName> `
   -State "Enabled"
   ```

Agora, o banco de dados ou o data warehouse tem a TDE habilitada com uma chave de criptografia no Key Vault.

## <a name="step-5-check-the-encryption-state-and-encryption-activity"></a>Etapa 5. Verificar o estado de criptografia e a atividade de criptografia

Use o cmdlet [Get-AzureRMSqlDatabaseTransparentDataEncryption](/powershell/module/azurerm.sql/get-azurermsqldatabasetransparentdataencryption) para obter o estado de criptografia e o [Get-AzureRMSqlDatabaseTransparentDataEncryptionActivity](/powershell/module/azurerm.sql/get-azurermsqldatabasetransparentdataencryptionactivity) para verificar o progresso da criptografia para um banco de dados ou data warehouse.

   ```powershell
   # Get the encryption state
   Get-AzureRMSqlDatabaseTransparentDataEncryption `
   -ResourceGroupName <SQLDatabaseResourceGroupName> `
   -ServerName <LogicalServerName> `
   -DatabaseName <DatabaseName> `

   <# Check the encryption progress for a database or data warehouse #>
   Get-AzureRMSqlDatabaseTransparentDataEncryptionActivity `
   -ResourceGroupName <SQLDatabaseResourceGroupName> `
   -ServerName <LogicalServerName> `
   -DatabaseName <DatabaseName>  
   ```

## <a name="other-useful-powershell-cmdlets"></a>Outros cmdlets úteis do PowerShell

- Use o cmdlet [Set-AzureRMSqlDatabaseTransparentDataEncryption](/powershell/module/azurerm.sql/set-azurermsqldatabasetransparentdataencryption) para desligar a TDE.

   ```powershell
   Set-AzureRMSqlDatabaseTransparentDataEncryption `
   -ServerName <LogicalServerName> `
   -ResourceGroupName <SQLDatabaseResourceGroupName> `
   -DatabaseName <DatabaseName> `
   -State "Disabled”
   ```
 
- Use o cmdlet [Get-AzureRmSqlServerKeyVaultKey](/powershell/module/azurerm.sql/get-azurermsqlserverkeyvaultkey) para retornar a lista de chaves do Key Vault adicionadas ao servidor.

   ```powershell
   <# KeyId is an optional parameter, to return a specific key version #>
   Get-AzureRmSqlServerKeyVaultKey `
   -ServerName <LogicalServerName> `
   -ResourceGroupName <SQLDatabaseResourceGroupName>
   ```
 
- Use o cmdlet [Remove-AzureRmSqlServerKeyVaultKey](/powershell/module/azurerm.sql/remove-azurermsqlserverkeyvaultkey) para remover uma chave do Key Vault do servidor.

   ```powershell
   <# The key set as the TDE Protector cannot be removed. #>
   Remove-AzureRmSqlServerKeyVaultKey `
   -KeyId <KeyVaultKeyId> `
   -ServerName <LogicalServerName> `
   -ResourceGroupName <SQLDatabaseResourceGroupName>   
   ```
 
## <a name="troubleshooting"></a>Solução de problemas

Verifique o seguinte se ocorrer um problema:
- Se não for possível encontrar o cofre de chaves, verifique se você está na assinatura correta usando o cmdlet [Get-AzureRmSubscription](/powershell/module/azurerm.profile/get-azurermsubscription).

   ```powershell
   Get-AzureRmSubscription `
   -SubscriptionId <SubscriptionId>
   ```

- Se a nova chave não puder ser adicionada ao servidor ou a nova chave não puder ser atualizada como o Protetor de TDE, verifique o seguinte:
   - A chave não deve ter uma data de expiração
   - A chave deve ter as operações *get*, *wrap key* e *unwrap key* habilitadas.

## <a name="next-steps"></a>Próximas etapas

- Saiba como girar o Protetor de TDE de um servidor para atender aos requisitos de segurança: [Girar o Protetor de Transparent Data Encryption usando o PowerShell](transparent-data-encryption-byok-azure-sql-key-rotation.md).
- No caso de um risco de segurança, saiba como remover um Protetor de TDE potencialmente comprometido: [Remover uma chave potencialmente comprometida](transparent-data-encryption-byok-azure-sql-remove-tde-protector.md). 

## <a name="prerequisites-for-cli"></a>Pré-requisitos para a CLI

- Você deve ter uma assinatura do Azure e ser um administrador na assinatura.
- [Recomendado, mas opcional] Ter um HSM (módulo de segurança de hardware) ou repositório de chaves local para criar uma cópia local do material da chave do Protetor de TDE.
- Interface de linha de comando versão 2.0 ou posterior. Para instalar a versão mais recente e conectar-se à sua assinatura do Azure, consulte [Instalar e configurar a Interface de linha de comando de plataforma cruzada do Azure 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest). 
- Criar um Azure Key Vault e uma chave para usar para a TDE.
   - [Gerenciar o Key Vault usando a CLI 2.0](https://docs.microsoft.com/azure/key-vault/key-vault-manage-with-cli2)
   - [Instruções para usar um HSM (módulo de segurança de hardware) e o Key Vault](https://docs.microsoft.com/azure/key-vault/key-vault-get-started#a-idhsmaif-you-want-to-use-a-hardware-security-module-hsm)
 - O cofre de chaves deve ter as seguintes propriedades para ser usado para TDE:
   - [exclusão reversível](https://docs.microsoft.com/azure/key-vault/key-vault-ovw-soft-delete)
   - [Como usar a exclusão reversível do Key Vault com a CLI](https://docs.microsoft.com/azure/key-vault/key-vault-soft-delete-cli) 
- A chave deve ter os seguintes atributos para ser usada para TDE:
   - Nenhuma data de expiração
   - Não estar desabilitada
   - Ser capaz de executar as operações *get*, *wrap key* e *unwrap key*
   
## <a name="step-1-create-a-server-and-assign-an-azure-ad-identity-to-your-server"></a>Etapa 1. Criar um servidor e atribuir uma identidade do Microsoft Azure AD ao seu servidor
      cli
      # create server (with identity) and database
      az sql server create -n "ServerName" -g "ResourceGroupName" -l "westus" -u "cloudsa" -p "YourFavoritePassWord99@34" -I 
      az sql db create -n "DatabaseName" -g "ResourceGroupName" -s "ServerName" 
      

 
## <a name="step-2-grant-key-vault-permissions-to-your-server"></a>Etapa 2. Conceder permissões do Key Vault para seu servidor
      cli
      # create key vault, key and grant permission
      az keyvault create -n "VaultName" -g "ResourceGroupName" 
      az keyvault key create -n myKey -p software --vault-name "VaultName" 
      az keyvault set-policy -n "VaultName" --object-id "ServerIdentityObjectId" -g "ResourceGroupName" --key-permissions wrapKey unwrapKey get list 
      

 
## <a name="step-3-add-the-key-vault-key-to-the-server-and-set-the-tde-protector"></a>Etapa 3. Adicionar a chave do Key Vault ao servidor e definir o Protetor de TDE
  
     cli
     # add server key and update encryption protector
      az sql server key create -g "ResourceGroupName" -s "ServerName" -t "AzureKeyVault" -u "FullVersionedKeyUri 
      az sql server tde-key update -g "ResourceGroupName" -s "ServerName" -t AzureKeyVault -u "FullVersionedKeyUri" 
      
  
  > [!Note]
> O tamanho combinado do nome do cofre de chaves e o nome da chave não pode exceder 94 caracteres.
> 

>[!Tip]
>Um exemplo KeyId do Key Vault: https://contosokeyvault.vault.azure.net/keys/Key1/1a1a2b2b3c3c4d4d5e5e6f6f7g7g8h8h
>
  
## <a name="step-4-turn-on-tde"></a>Etapa 4. Ativar a TDE 
      cli
      # enable encryption
      az sql db tde create -n "DatabaseName" -g "ResourceGroupName" -s "ServerName" --status Enabled 
      

Agora, o banco de dados ou o data warehouse tem a TDE habilitada com uma chave de criptografia no Key Vault.

## <a name="step-5-check-the-encryption-state-and-encryption-activity"></a>Etapa 5. Verificar o estado de criptografia e a atividade de criptografia

     cli
      # get encryption scan progress
      az sql db tde show-activity -n "DatabaseName" -g "ResourceGroupName" -s "ServerName" 

      # get whether encryption is on or off
      az sql db tde show-configuration -n "DatabaseName" -g "ResourceGroupName" -s "ServerName" 

## <a name="sql-cli-references"></a>Referências da CLI do SQL

https://docs.microsoft.com/cli/azure/sql?view=azure-cli-latest 

https://docs.microsoft.com/cli/azure/sql/server/key?view=azure-cli-latest 

https://docs.microsoft.com/cli/azure/sql/server/tde-key?view=azure-cli-latest 

https://docs.microsoft.com/cli/azure/sql/db/tde?view=azure-cli-latest 

