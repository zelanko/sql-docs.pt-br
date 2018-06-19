---
title: PowerShell – Girar o Protetor de TDE – SQL do Azure | Microsoft Docs
description: Saiba como girar o Protetor de TDE (Transparent Data Encryption) para um SQL Server do Azure.
keywords: ''
services: sql-database
documentationcenter: ''
author: becczhang
manager: jhubbard
editor: ''
ms.prod: ''
ms.reviewer: ''
ms.suite: sql
ms.prod_service: sql-database, sql-data-warehouse
ms.service: sql-database
ms.custom: ''
ms.tgt_pltfrm: ''
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: ryzhang26
monikerRange: = azuresqldb-current || = azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: 45dc9d4d9f4681fde06f75e8fa666c6584bcf863
ms.sourcegitcommit: a78fa85609a82e905de9db8b75d2e83257831ad9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2018
ms.locfileid: "35696737"
---
# <a name="rotate-the-transparent-data-encryption-tde-protector-using-powershell"></a>Girar o Protetor de TDE (Transparent Data Encryption) usando o PowerShell 
[!INCLUDE[appliesto-xx-asdb-asdw-xxx-md](../../../includes/appliesto-xx-asdb-asdw-xxx-md.md)]

Este guia de instruções descreve a rotação de chaves para um SQL Server do Azure usando um Protetor de TDE do Azure Key Vault. Girar um Protetor de TDE de um SQL Server do Azure significa alternar para uma nova chave assimétrica que protege os bancos de dados no servidor. A rotação de chaves é uma operação online e deve levar somente alguns segundos para ser concluída, porque isso descriptografa e criptografa novamente apenas a chave de criptografia de dados do banco de dados, não o banco de dados inteiro.

Este guia aborda as duas opções para girar o Protetor de TDE no servidor.

> [!NOTE]
> Um SQL Data Warehouse em pausa deverá ser retomado antes das rotações de chave.
>

> [!IMPORTANT]
> **Não exclua** versões anteriores da chave depois de uma sobreposição.  Quando as chaves são sobrepostas, alguns dados ainda são criptografados com chaves anteriores, como os backups mais antigos do banco de dados. 
>

## <a name="prerequisites"></a>Prerequisites

- Este guia de instruções pressupõe que você já está usando uma chave do Azure Key Vault como o Protetor de TDE para um Data Warehouse ou Banco de Dados SQL do Azure. Consulte [Transparent Data Encryption com o suporte a BYOK](transparent-data-encryption-byok-azure-sql.md).
- Você deve ter o Azure PowerShell versão 3.7.0 ou posterior instalado e em execução. 
- [Recomendado, mas opcional] Crie o material da chave para o Protetor de TDE em um HSM (módulo de segurança de hardware) ou repositório de chave local primeiro e importe o material da chave para o Azure Key Vault. Siga as [instruções para usar um HSM (módulo de segurança de hardware) e o Key Vault](https://docs.microsoft.com/azure/key-vault/key-vault-get-started) para saber mais.

## <a name="option-1-auto-rotation"></a>Opção 1: rotação automática

Gere uma nova versão da chave do Protetor de TDE existente no Key Vault, sob o mesmo nome de chave e cofre de chaves. O serviço do SQL do Azure é iniciado usando essa nova versão dentro de 24 horas. 

Para criar uma nova versão do Protetor de TDE usando o cmdlet [Add-AzureKeyVaultKey](/powershell/module/azurerm.keyvault/add-azurekeyvaultkey):

   ```powershell
   Add-AzureKeyVaultKey `
   -VaultName <KeyVaultName> `
   -Name <KeyVaultKeyName> `
   -Destination <HardwareOrSoftware>
   ```

## <a name="option-2-manual-rotation"></a>Opção 2: rotação manual

A opção usa os cmdlets [Add-AzureKeyVaultKey](/powershell/module/azurerm.keyvault/add-azurekeyvaultkey), [Add-AzureRmSqlServerKeyVaultKey](/powershell/module/azurerm.sql/add-azurermsqlserverkeyvaultkey) e [Set-AzureRmSqlServerTransparentDataEncryptionProtector](/powershell/module/azurerm.sql/set-azurermsqlservertransparentdataencryptionprotector) para adicionar uma chave totalmente nova, que pode estar sob um novo nome de chave ou até mesmo outro cofre de chaves. 

>[!NOTE]
>O tamanho combinado do nome do cofre de chaves e o nome da chave não pode exceder 94 caracteres.
>

   ```powershell
   # Add a new key to Key Vault
   Add-AzureKeyVaultKey `
   -VaultName <KeyVaultName> `
   -Name <KeyVaultKeyName> `
   -Destination <HardwareOrSoftware>

   # Add the new key from Key Vault to the server
   Add-AzureRmSqlServerKeyVaultKey `
   -KeyId <KeyVaultKeyId> `
   -ServerName <LogicalServerName> `
   -ResourceGroup <SQLDatabaseResourceGroupName>   
  
   <# Set the key as the TDE protector for all resources 
   under the server #>
   Set-AzureRmSqlServerTransparentDataEncryptionProtector `
   -Type AzureKeyVault `
   -KeyId <KeyVaultKeyId> `
   -ServerName <LogicalServerName> `
   -ResourceGroup <SQLDatabaseResourceGroupName>
   ```
  
## <a name="other-useful-powershell-cmdlets"></a>Outros cmdlets úteis do PowerShell

- Para alternar o Protetor de TDE do modo gerenciado pela Microsoft para o BYOK, use o cmdlet [Set-AzureRmSqlServerTransparentDataEncryptionProtector](/powershell/module/azurerm.sql/set-azurermsqlservertransparentdataencryptionprotector).

   ```powershell
   Set-AzureRmSqlServerTransparentDataEncryptionProtector `
   -Type AzureKeyVault `
   -KeyId <KeyVaultKeyId> `
   -ServerName <LogicalServerName> `
   -ResourceGroup <SQLDatabaseResourceGroupName>
   ```

- Para alternar o Protetor de TDE do modo BYOK para o gerenciado pela Microsoft, use o cmdlet [Set-AzureRmSqlServerTransparentDataEncryptionProtector](/powershell/module/azurerm.sql/set-azurermsqlservertransparentdataencryptionprotector).

   ```powershell
   Set-AzureRmSqlServerTransparentDataEncryptionProtector `
   -Type ServiceManaged `
   -ServerName <LogicalServerName> `
   -ResourceGroup <SQLDatabaseResourceGroupName> 
   ``` 

## <a name="next-steps"></a>Próximas etapas

- No caso de um risco de segurança, saiba como remover um Protetor de TDE potencialmente comprometido: [Remover uma chave potencialmente comprometida](transparent-data-encryption-byok-azure-sql-remove-tde-protector.md) 

- Introdução ao suporte para Bring Your Own Key para a TDE: [Ativar a TDE usando sua própria chave do Key Vault usando o PowerShell](transparent-data-encryption-byok-azure-sql-configure.md)
