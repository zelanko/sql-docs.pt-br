---
title: "PowerShell – Remover um Protetor de TDE – SQL do Azure | Microsoft Docs"
description: "Guia de instruções para responder a um Protetor de TDE potencialmente comprometido para um Data Warehouse ou Banco de Dados SQL do Azure usando a TDE com suporte a BYOK (Bring Your Own Key)."
keywords: 
services: sql-database
documentationcenter: 
author: becczhang
manager: cguyer
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: security
ms.workload: Inactive
ms.tgt_pltfrm: 
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: rebeccaz
ms.openlocfilehash: 5756f318196967169dfbd0272b3ea9af365cdb5a
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="remove-a-transparent-data-encryption-tde-protector-using-powershell"></a>Remover um Protetor de TDE (Transparent Data Encryption) usando o PowerShell

[!INCLUDE[tsql-appliesto-xxxxxx-asdb-asdw-xxx-md](../../../includes/tsql-appliesto-xxxxxx-asdb-asdw-xxx-md.md)]

## <a name="prerequisites"></a>Pré-requisitos
- Você deve ter uma assinatura do Azure e ser um administrador na assinatura
- Você deve ter o Azure PowerShell versão 4.2.0 ou posterior instalado e em execução. 
- Este guia de instruções pressupõe que você já está usando uma chave do Azure Key Vault como o Protetor de TDE para um Data Warehouse ou Banco de Dados SQL do Azure. Consulte [Transparent Data Encryption com o suporte a BYOK](transparent-data-encryption-byok-azure-sql.md) para saber mais.

## <a name="overview"></a>Visão geral
Este guia de instruções descreve como responder a um Protetor de TDE potencialmente comprometido para um Data Warehouse ou Banco de Dados SQL do Azure que está usando a TDE com o suporte a BYOK (Bring Your Own Key). Para saber mais sobre o suporte a BYOK para TDE, consulte a [página de visão geral](transparent-data-encryption-byok-azure-sql.md). 

Os procedimentos a seguir devem ser feitos apenas em casos extremos ou em ambientes de teste. Examine o guia de instruções com cuidado, pois excluir ativamente os Protetores de TDE usados do Azure Key Vault pode resultar em **perda de dados**. 

Se alguma vez houver suspeita de que uma chave está comprometida, como um serviço ou usuário ter tido acesso não autorizado à chave, é melhor excluí-la.

Tenha em mente que após o Protetor de TDE ser excluído no Key Vault, **todas as conexões com os bancos de dados criptografados no servidor são bloqueadas e esses bancos de dados ficam offline e são descartados dentro de 24 horas**. Backups antigos criptografados com a chave comprometida não são mais acessíveis.

Este guia de instruções trata de duas abordagens dependendo do resultado desejado após a resposta ao incidente:
- Para manter os Data Warehouses/Bancos de Dados SQL do Azure **acessíveis**
- Para tornar os Data Warehouses/Bancos de Dados SQL do Azure **inacessíveis**

## <a name="to-keep-the-encrypted-resources-accessible"></a>Para manter os recursos criptografados acessíveis
1. Crie um [nova chave no Key Vault](https://docs.microsoft.com/powershell/module/azurerm.keyvault/add-azurekeyvaultkey?view=azurermps-4.1.0). Verifique se essa nova chave é criada em um cofre de chaves separado do Protetor de TDE potencialmente comprometido, uma vez que o controle de acesso é provisionado no nível do cofre. 
2. Adicione a nova chave ao servidor usando os cmdlets [Add-AzureRmSqlServerKeyVaultKey](/powershell/module/azurerm.sql/add-azurermsqlserverkeyvaultkey) e [Set-AzureRmSqlServerTransparentDataEncryptionProtector](/powershell/module/azurerm.sql/set-azurermsqlservertransparentdataencryptionprotector) e atualize-a como o novo Protetor de TDE do servidor.

   ```powershell
   # Add the key from Key Vault to the server  
   Add-AzureRmSqlServerKeyVaultKey `
   -ResourceGroupName <SQLDatabaseResourceGroupName> `
   -ServerName <LogicalServerName> `
   -KeyId <KeyVaultKeyId>
   
   # Set the key as the TDE protector for all resources under the server
   Set-AzureRmSqlServerTransparentDataEncryptionProtector `
   -ResourceGroupName <SQLDatabaseResourceGroupName> `
   -ServerName <LogicalServerName> `
   -Type AzureKeyVault -KeyId <KeyVaultKeyId> 
   ```

3. Verifique se o servidor e todas as réplicas foram atualizados para o novo Protetor de TDE usando o cmdlet [Get-AzureRmSqlServerTransparentDataEncryptionProtector](/powershell/module/azurerm.sql/get-azurermsqlservertransparentdataencryptionprotector). 

   >[!NOTE]
   > Pode levar alguns minutos para que o novo Protetor de TDE se propague para todos os bancos de dados e bancos de dados secundários no servidor.
   >

   ```powershell
   Get-AzureRmSqlServerTransparentDataEncryptionProtector `
   -ServerName <LogicalServerName> `
   -ResourceGroupName <SQLDatabaseResourceGroupName>
   ```

4. Faça um [backup da nova chave](/powershell/module/azurerm.keyvault/backup-azurekeyvaultkey) no Key Vault.

   ```powershell
   <# -OutputFile parameter is optional; 
   if removed, a file name is automatically generated. #>
   Backup-AzureKeyVaultKey `
   -VaultName <KeyVaultName> `
   -Name <KeyVaultKeyName> `
   -OutputFile <DesiredBackupFilePath>
   ```
 
5. Exclua a chave comprometida do Key Vault usando o cmdlet [Remove-AzureKeyVaultKey](/powershell/module/azurerm.keyvault/remove-azurekeyvaultkey). 

   ```powershell
   Remove-AzureKeyVaultKey `
   -VaultName <KeyVaultName> `
   -Name <KeyVaultKeyName>
   ```
 
6. Para restaurar uma chave no Key Vault no futuro usando o cmdlet [Restore-AzureKeyVaultKey](/powershell/module/azurerm.keyvault/restore-azurekeyvaultkey):
   ```powershell
   Restore-AzureKeyVaultKey `
   -VaultName <KeyVaultName> `
   -InputFile <BackupFilePath>
   ```
 
## <a name="to-make-the-encrypted-resources-inaccessible"></a>Para tornar os recursos criptografados inacessíveis
1. Remova os bancos de dados que estão sendo criptografados pela chave potencialmente comprometida.
Os bancos de dados e arquivos de log têm o backup realizado automaticamente, portanto, é possível fazer uma restauração pontual do banco de dados em qualquer ponto (contanto que você forneça a chave). Os bancos de dados devem ser descartados antes da exclusão de um Protetor de TDE ativo para evitar a possível perda de dados de até 10 minutos das transações mais recentes. 
2. Faça backup do material de chave do Protetor de TDE no Key Vault.
3. Remova a chave potencialmente comprometida do Key Vault

## <a name="next-steps"></a>Próximas etapas

- Saiba como girar o Protetor de TDE de um servidor para atender aos requisitos de segurança: [Girar o Protetor de Transparent Data Encryption usando o PowerShell](transparent-data-encryption-byok-azure-sql-key-rotation.md)

- Introdução ao suporte para Bring Your Own Key para a TDE: [Ativar a TDE usando sua própria chave do Key Vault usando o PowerShell](transparent-data-encryption-byok-azure-sql-configure.md)
