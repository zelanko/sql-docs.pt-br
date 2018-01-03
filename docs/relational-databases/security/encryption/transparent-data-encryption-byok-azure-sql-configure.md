---
title: "PowerShell: habilitar a TDE usando sua própria chave do Azure Key Vault | Microsoft Docs"
description: "Saiba como configurar um Data Warehouse e um Banco de dados SQL do Azure para começar a usar a TDE (Transparent Data Encryption) para a criptografia em repouso usando o PowerShell."
keywords: 
documentationcenter: 
author: aliceku
manager: craigg
editor: 
ms.prod: 
ms.reviewer: 
ms.suite: sql
ms.prod_service: sql-database, sql-data-warehouse
ms.service: sql-database
ms.component: security
ms.workload: On Demand
ms.tgt_pltfrm: 
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: aliceku
ms.openlocfilehash: 0acfd9faa668d1e86cb82496bdd97dc6a0ec2bc8
ms.sourcegitcommit: b603dcac7326bba387befe68544619e026e6a15e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="powershell-enable-transparent-data-encryption-using-your-own-key-from-azure-key-vault"></a>PowerShell: habilitar a Transparent Data Encryption usando sua própria chave do Azure Key Vault
[!INCLUDE[appliesto-xx-asdb-asdw-xxx-md](../../../includes/appliesto-xx-asdb-asdw-xxx-md.md)]

Este guia de instruções explica como usar uma chave do Azure Key Vault para a TDE (Transparent Data Encryption) no Data Warehouse ou no Banco de Dados SQL. Para saber mais sobre a TDE com suporte a BYOK (Bring Your Own Key), visite [TDE com Bring Your Own Key para SQL do Azure](transparent-data-encryption-byok-azure-sql.md). 

## <a name="prerequisites"></a>Prerequisites

- Você deve ter uma assinatura do Azure e ser um administrador na assinatura.
- [Recomendado, mas opcional] Ter um HSM (módulo de segurança de hardware) ou repositório de chaves local para criar uma cópia local do material da chave do Protetor de TDE.
- Você deve ter o Azure PowerShell versão 4.2.0 ou posterior instalado e em execução. 
- Criar um Azure Key Vault e uma chave para usar para a TDE.
   - [Instruções do PowerShell do Key Vault](https://docs.microsoft.com/azure/key-vault/key-vault-get-started)
   - [Instruções para usar um HSM (módulo de segurança de hardware) e o Key Vault](https://docs.microsoft.com/azure/key-vault/key-vault-get-started#a-idhsmaif-you-want-to-use-a-hardware-security-module-hsm)
- A chave deve ter os seguintes atributos para ser usada para TDE:
   - Nenhuma data de expiração
   - Não estar desabilitada
   - Ser capaz de executar as operações *get*, *wrap key* e *unwrap key*

## <a name="step-1-assign-an-aad-identity-to-your-server"></a>Etapa 1. Atribuir uma identidade do AAD ao seu servidor 

Se você tiver um servidor existente, use o seguinte para adicionar uma identidade do AAD ao seu servidor:

   ```powershell
   $server = Set-AzureRmSqlServer `
   -ResourceGroupName <SQLDatabaseResourceGroupName> `
   -ServerName <LogicalServerName> `
   -AssignIdentity
   ```

Se você estiver criando um servidor, use o cmdlet [New-AzureRmSqlServer](/powershell/module/azurerm.sql/new-azurermsqlserver) com a marca -Identity para adicionar uma identidade do AAD durante a criação do servidor:

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
>Um exemplo de KeyId do Key Vault: https://contosokeyvault.vault.azure.net/keys/Key1/1a1a2b2b3c3c4d4d5e5e6f6f7g7g8h8h
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

## <a name="step-5-check-the-encryption-state-and-encryption-activity-of-the-database-or-data-warehouse"></a>Etapa 5. Verificar o estado de criptografia e a atividade de criptografia do banco de dados ou data warehouse

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


