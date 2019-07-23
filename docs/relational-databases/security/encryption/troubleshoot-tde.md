---
title: Erros comuns de Transparent Data Encryption com chaves gerenciadas pelo cliente no Azure Key Vault | Microsoft Docs
description: Solucione problemas de TDE (Transparent Data Encryption) com uma configuração do Azure Key Vault.
helpviewer_keywords:
- troublshooting, tde akv
- tde akv configuration, troubleshooting
- tde troubleshooting
author: aliceku
ms.prod: sql
ms.technology: security
ms.reviewer: vanto
ms.topic: conceptual
ms.date: 04/26/2019
ms.author: aliceku
monikerRange: = azuresqldb-current || = azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: f67d1ed9bf809baaa4d934947e86d3fd1b7ed0b9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68111530"
---
# <a name="common-errors-for-transparent-data-encryption-with-customer-managed-keys-in-azure-key-vault"></a>Erros comuns de Transparent Data Encryption com chaves gerenciadas pelo cliente no Azure Key Vault

[!INCLUDE[appliesto-xx-asdb-asdw-xxx-md.md](../../../includes/appliesto-xx-asdb-asdw-xxx-md.md)]
Este artigo descreve os requisitos para usar a TDE (Transparent Data Encryption) com chaves gerenciadas pelo cliente no Azure Key Vault e como identificar e resolver erros comuns.

## <a name="requirements"></a>Requisitos

Para solucionar a TDE com um protetor de TDE gerenciado pelo cliente no Key Vault, é necessário atender a esses requisitos:

- A instância lógica do SQL Server e o cofre de chaves devem estar localizados na mesma região.
- A identidade da instância lógica do SQL Server fornecida pelo Azure AD (Azure Active Directory), a AppId no Azure Key Vault, deve ser de um locatário na assinatura original. Se o servidor for movido para uma assinatura diferente daquela onde foi criado, a identidade do servidor (AppId) deve ser recriada.
- O cofre de chaves deve estar em execução. Para saber como verificar o status do cofre de chaves, confira o [Azure Resource Health](https://docs.microsoft.com/azure/service-health/resource-health-overview). Para se inscrever para receber notificações, leia sobre os [grupos de ação](https://docs.microsoft.com/azure/azure-monitor/platform/action-groups).
- Em um cenário de recuperação de desastres geográficos, os dois cofres de chaves precisam conter o mesmo material de chave para que um failover funcione.
- O servidor lógico deve ter uma identidade do Azure AD (uma AppId) para autenticar o cofre de chaves.
- A AppId precisa ter acesso ao cofre de chaves e deve ter as permissões Obter, Encapsular e Desencapsular nas chaves selecionadas como Protetores de TDE.

Para saber mais, confira as [Diretrizes para configurar a TDE com o Azure Key Vault](https://docs.microsoft.com/azure/sql-database/transparent-data-encryption-byok-azure-sql#guidelines-for-configuring-tde-with-azure-key-vault).

## <a name="common-misconfigurations"></a>Configurações incorretas comuns

A maioria dos problemas que ocorrem ao usar TDE com o Key Vault é causada por um dos erros de configuração a seguir:

### <a name="the-key-vault-is-unavailable-or-doesnt-exist"></a>O cofre de chaves não está disponível ou não existe

- O cofre de chaves foi excluído por engano.
- O firewall foi configurado para o Azure Key Vault, mas não permite o acesso aos serviços da Microsoft.

### <a name="no-permissions-to-access-the-key-vault-or-the-key-doesnt-exist"></a>Sem permissão para acessar o cofre de chaves ou a chave não existe

- A chave foi excluída por engano.
- A AppId da instância lógica do SQL Server foi excluída por engano.
- A instância lógica do SQL Server foi movida para uma assinatura diferente. Uma nova AppId deve ser criada se o servidor lógico for movido para uma assinatura diferente.
- As permissões concedidas à AppId para as chaves não são suficientes (não incluem Obter, Encapsular e Desencapsular).
- As permissões da AppId da instância lógica do SQL Server foram revogadas.

## <a name="identify-and-resolve-common-errors"></a>Identificar e resolver erros comuns

Nesta seção, listaremos as etapas de solução de problemas para os erros mais comuns.

### <a name="missing-server-identity"></a>Identidade de servidor ausente

**Mensagem de erro**

_401 AzureKeyVaultNoServerIdentity – a identidade do servidor não está configurada corretamente no servidor. Contate o suporte._

**Detecção**

Use o comando ou cmdlet a seguir para garantir que uma identidade seja atribuída à instância lógica do SQL Server:

- Azure PowerShell: [Get-AzureRMSqlServer](https://docs.microsoft.com/powershell/module/AzureRM.Sql/Get-AzureRmSqlServer?view=azurermps-6.13.0) 

- CLI do Azure: [az-sql-server-show](https://docs.microsoft.com/cli/azure/sql/server?view=azure-cli-latest#az-sql-server-show)

**Mitigação**

Use o cmdlet ou o comando a seguir para configurar uma AppId (identidade do Azure AD) para a instância lógica do SQL Server:

- Azure PowerShell: [Set-AzureRmSqlServer](https://docs.microsoft.com/powershell/module/azurerm.sql/set-azurermsqlserver?view=azurermps-6.13.0) com a opção `-AssignIdentity`.

- CLI do Azure: [az sql server update](https://docs.microsoft.com/cli/azure/sql/server?view=azure-cli-latest#az-sql-server-update) com a opção `--assign_identity`.

No portal do Azure, vá até o cofre de chaves e depois às **Políticas de acesso**. Conclua estas etapas: 

 1. Use o botão **Adicionar Novo** para adicionar a AppId ao servidor criado na etapa anterior. 
 1. Atribua as seguintes permissões de chave: Obter, Encapsular e Desencapsular 

Para saber mais, confira [Atribuir uma identidade do Azure AD ao seu servidor](https://docs.microsoft.com/azure/sql-database/transparent-data-encryption-byok-azure-sql-configure?view=sql-server-2017&viewFallbackFrom=azuresqldb-current#step-1-assign-an-azure-ad-identity-to-your-server).

> [!IMPORTANT]
> Se a instância lógica do SQL Server for movida para uma nova assinatura após a configuração inicial da TDE com o Key Vault, repita a etapa para configurar a identidade do Azure AD para criar a AppId. Em seguida, adicione a AppId ao cofre de chaves e atribua as permissões corretas para a chave. 
>

### <a name="missing-key-vault"></a>Cofre de chaves ausente

**Mensagem de erro**

_AzureKeyVaultConnectionFailed 503 – não foi possível concluir a operação no servidor porque houve falha nas tentativas de conexão ao Azure Key Vault._

**Detecção**

Para identificar o URI da chave e o cofre de chaves:

1. Use o comando ou cmdlet a seguir para obter o URI da chave de uma determinada instância lógica do SQL Server:

    - Azure PowerShell: [Get-AzureRmSqlServerKeyVaultKey](https://docs.microsoft.com/powershell/module/azurerm.sql/get-azurermsqlserverkeyvaultkey?view=azurermps-6.13.0)

    - CLI do Azure: [az-sql-server-tde-key-show](https://docs.microsoft.com/cli/azure/sql/server/tde-key?view=azure-cli-latest#az-sql-server-tde-key-show) 

1. Use o URI da chave para identificar o cofre de chaves:

    - Azure PowerShell: você pode inspecionar as propriedades da variável $MyServerKeyVaultKey para obter detalhes sobre o cofre de chaves.

    - CLI do Azure: inspecione o protetor de criptografia do servidor retornado para obter detalhes sobre o cofre de chaves.

**Mitigação**

Confirme se o cofre de chaves está disponível:

- Verifique se o cofre de chaves está disponível e se a instância lógica do SQL Server tem acesso.
- Se o cofre de chaves estiver protegido por um firewall, verifique se a caixa de seleção para permitir que os serviços da Microsoft acessem o cofre de chaves está marcada.
- Se o cofre de chaves for excluído por engano, será necessário refazer a configuração desde o início.


### <a name="missing-key"></a>Chave ausente

**Mensagens de erro**

_ServerKeyNotFound 404 – a chave do servidor solicitada não foi encontrada na assinatura atual._ 

_409 ServerKeyDoesNotExists – a chave do servidor não existe._

**Detecção**

Para identificar o URI da chave e o cofre de chaves:

- Use o cmdlet ou comando em [Cofre da chave ausente](#missing-key-vault) para identificar a chave URI adicionada à instância lógica do SQL Server. Executar os comandos retorna a lista de chaves.

**Mitigação**

Confirme se o protetor de TDE está presente no Key Vault:

1. Identifique o cofre de chaves e vá até ele no portal do Azure.
1. Certifique-se de que a chave identificada pelo URI da chave esteja presente.

### <a name="missing-permissions"></a>Permissões ausentes

**Mensagem de erro**

_401 AzureKeyVaultMissingPermissions – o servidor não tem as permissões necessárias no Azure Key Vault._

**Detecção**

Como identificar o URI da chave e o cofre de chaves: 

- Use o cmdlet ou comando em [Cofre da chave ausente](#missing-key-vault) para identificar o cofre de chaves que a instância lógica do SQL Server utiliza.

**Mitigação**

Confirme se a instância lógica do SQL Server tem permissões para o cofre de chaves e se as permissões estão corretas para acessar a chave:

- No portal do Azure, vá até o cofre de chaves > **Políticas de acesso**. Localize a AppId da instância lógica do SQL Server.  
- Se a AppId estiver presente, verifique se ela tem as seguintes permissões de chave: Obter, Encapsular e Desencapsular.
- Se a AppId não estiver presente, adicione-a usando o botão **Adicionar Novo**. 

## <a name="next-steps"></a>Próximas etapas

- Confira as [Diretrizes para configurar a TDE com o Azure Key Vault](https://docs.microsoft.com/azure/sql-database/transparent-data-encryption-byok-azure-sql#guidelines-for-configuring-tde-with-azure-key-vault).
- Saiba mais sobre o [Azure Resource Health](https://docs.microsoft.com/azure/service-health/resource-health-overview).
- Reveja como [atribuir uma identidade do Azure AD ao seu servidor](https://docs.microsoft.com/azure/sql-database/transparent-data-encryption-byok-azure-sql-configure?view=sql-server-2017&viewFallbackFrom=azuresqldb-current#step-1-assign-an-azure-ad-identity-to-your-server).
