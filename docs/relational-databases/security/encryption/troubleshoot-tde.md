---
title: Erros comuns e resoluções com TDE (Transparent Data Encryption) com chaves gerenciadas pelo cliente no AKV (Azure Key Vault) | Microsoft Docs
description: Solucionar problemas de criptografia de TDE (Transparent Data Encryption) com a configuração do Azure Key Vault.
helpviewer_keywords:
- troublshooting, tde akv
- tde akv configuration, troubleshooting
- tde troubleshooting
author: aliceku
manager: craigg
ms.prod: sql
ms.technology: security
ms.reviewer: vanto
ms.topic: conceptual
ms.date: 04/26/2019
ms.author: aliceku
monikerRange: = azuresqldb-current || = azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: 1366d0a20ed39b466d1a2f6cb3e84f0f30e17f9f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66718088"
---
# <a name="common-errors-and-resolutions-with-transparent-data-encryption-tde-with-customer-managed-keys-in-azure-key-vault-akv"></a>Erros comuns e resoluções com TDE (Transparent Data Encryption) com chaves gerenciadas pelo cliente no AKV (Azure Key Vault)

[!INCLUDE[appliesto-xx-asdb-asdw-xxx-md.md](../../../includes/appliesto-xx-asdb-asdw-xxx-md.md)]
Este tópico contém informações sobre os seguintes problemas:  
  
- Requisitos  
- Como identificar e resolver os erros mais comuns

## <a name="requirements"></a>Requisitos
Para solucionar problemas de [TDE com o Protetor de TDE gerenciado pelo cliente na configuração de AKV](https://docs.microsoft.com/azure/sql-database/transparent-data-encryption-byok-azure-sql#guidelines-for-configuring-tde-with-azure-key-vault), vamos começar confirmando os seguintes requisitos:
- O SQL Server lógico e o cofre de chaves precisam estar localizados na mesma região.
- A identidade do SQL Server lógico fornecida pelo Azure Active Directory (APPID no Azure Key Vault) é limitada a um locatário na assinatura original.  Se o servidor foi movido para outra assinatura, a identidade do servidor (APPID) precisa ser recriada.
- O cofre de chaves precisa estar ativo e em execução. Saiba mais sobre [Azure Resource Health](https://docs.microsoft.com/azure/service-health/resource-health-overview) para verificar o status do cofre de chaves e [Grupos de Ação](https://docs.microsoft.com/azure/azure-monitor/platform/action-groups) para inscrever-se para receber notificações.
- No cenário de recuperação de desastres geográfica, ambos os cofres de chaves precisam conter o mesmo material de chave para um failover funcionar.
- O servidor lógico precisa ter uma identidade (APPID) do AAD (Azure Active Directory) para autenticar-se no cofre de chaves.
- A APPID precisa ter acesso ao cofre de chaves e permissões para encapsular, desencapsular e obter para as chaves selecionadas como Protetores de TDE.

A maioria dos problemas encontrados ao usar TDE com o AKV deve-se a um dos erros de configuração seguir:

### <a name="key-vault-unavailable-or-doesnt-exist"></a>Cofre de chaves não está disponível ou não existe?
- Cofre de chaves excluído por engano
- Firewall configurado para o Azure Key Vault sem permitir o acesso aos serviços da Microsoft

### <a name="no-permissions-to-access-the-key-vault-or-key-doesnt-exist"></a>Nenhuma permissão para acessar o cofre de chaves ou a chave não existe?
- Chave excluída por engano
- APPID SQL excluída por engano
- SQL foi movido para uma assinatura diferente, o que exige uma nova APPID
- Permissões concedidas à APPID para chaves não é suficiente (encapsular, desencapsular, obter)
- As permissões para a APPID SQL revogadas


Na próxima seção, vamos listar as etapas de solução de problemas para os erros mais comuns.


## <a name="how-to-identify-and-resolve-the-most-common-errors"></a>Como identificar e resolver os erros mais comuns

## <a name="missing-server-identity"></a>Identidade de servidor ausente
Mensagem de erro: "401 AzureKeyVaultNoServerIdentity – a identidade do servidor não está configurada corretamente no servidor. Contate o suporte."

Detecção: Use o comando a seguir para garantir que uma identidade tenha sido atribuída ao SQL Server lógico:

- [Azure PowerShell Get-AzureRMSqlServer](https://docs.microsoft.com/powershell/module/AzureRM.Sql/Get-AzureRmSqlServer?view=azurermps-6.13.0) 
- [Azure CLI az-sql-server-show](https://docs.microsoft.com/cli/azure/sql/server?view=azure-cli-latest#az-sql-server-show)

Mitigação: Configurar uma APPID (identidade do Azure AD (Azure Active Directory)) para o SQL Server lógico

Para PowerShell: Use o comando Set-AzureRmSqlServer com a opção [-AssignIdentity](https://docs.microsoft.com/powershell/module/azurerm.sql/set-azurermsqlserver?view=azurermps-6.13.0) 

Para CLI: Use o comando az sql server update com a opção [--assign_identity](https://docs.microsoft.com/cli/azure/sql/server?view=azure-cli-latest#az-sql-server-update) 

No portal do Azure, navegue até o cofre de chaves e vá para as políticas de acesso:  
 - Usando o botão Adicionar Novo, adicione a APPID para o servidor criado na etapa anterior. 
 - Atribua as seguintes permissões de chave: Obter, Encapsular e Desencapsular 

[Saiba mais](https://docs.microsoft.com/azure/sql-database/transparent-data-encryption-byok-azure-sql-configure?view=sql-server-2017&viewFallbackFrom=azuresqldb-current#step-1-assign-an-azure-ad-identity-to-your-server)

> [!IMPORTANT]
> Se o SQL server lógico foi movido para uma nova assinatura após a configuração inicial da TDE com o AKV, a etapa para configurar a identidade do AAD deve ser repetida para criar a APPID.  A nova APPID deve ser adicionada ao cofre de chaves e as permissões corretas devem ser reatribuídas. 
>

## <a name="missing-key-vault"></a>Cofre de chaves ausente
Mensagem de erro: "AzureKeyVaultConnectionFailed 503 – a operação não pôde ser concluída no servidor porque houve falha nas tentativas de conectar-se ao Azure Key Vault"

Detecção: Como identificar o URI da chave e o cofre de chaves 

Etapa 1: Use o comando a seguir para obter o URI da chave de um determinado SQL Server lógico:

-[Azure PowerShell get-azurermsqlserverkeyvaultkey](https://docs.microsoft.com/powershell/module/azurerm.sql/get-azurermsqlserverkeyvaultkey?view=azurermps-6.13.0)

-[Azure CLI az-sql-server-tde-key-show](https://docs.microsoft.com/cli/azure/sql/server/tde-key?view=azure-cli-latest#az-sql-server-tde-key-show) 

Etapa 2: Use o URI da chave para identificar o cofre de chaves

PowerShell: você pode inspecionar as propriedades de $MyServerKeyVaultKey para obter detalhes sobre o cofre de chaves

CLI: inspecione o protetor de criptografia do servidor retornado para obter detalhes sobre o cofre de chaves

Mitigação: Confirme que o cofre de chaves está disponível
- Verifique se o cofre de chaves está disponível e o SQL Server lógico tem acesso
- Se o cofre de chaves estiver protegido por um firewall, verifique se a caixa de seleção para permitir que os serviços da Microsoft acessem o cofre de chaves está marcada
- Se o cofre de chaves tiver sido excluído por engano, a configuração deverá ser concluída desde o início


## <a name="missing-key"></a>Chave ausente 
Mensagem de erro: "ServerKeyNotFound 404 – a chave do servidor solicitada não foi encontrada na assinatura atual."
"409 ServerKeyDoesNotExists – a chave do servidor não existe."

Detecção: Como identificar o URI da chave e o cofre de chaves
- Identifica o URI da chave adicionado ao SQL Server lógico usando os cmdlets da seção do cofre de chaves Ausente acima para retornar a lista de chaves.

Mitigação: Confirme que o protetor de TDE está presente no AKV
- Identificar o cofre de chaves e navegar até ele no portal do Azure
- Verifique se a chave identificada pelo URI da chave está presente

## <a name="missing-permissions"></a>Permissões ausentes 
Mensagem de erro: "401 AzureKeyVaultMissingPermissions – o servidor não tem as permissões necessárias no Azure Key Vault."

Detecção: Como identificar o URI da chave e o cofre de chaves
- Identifique o cofre de chaves usado pelo SQL Server lógico usando os cmdlets da seção do cofre de chaves ausente acima.

Mitigação: Confirme se que o SQL Server lógico tem permissões para o cofre de chaves e as permissões corretas para acessar a chave
- No portal do Azure, navegue até o Cofre de chaves, vá para as políticas de acesso e localize a APPID do SQL Server:  
  - Se o APPID não estiver presente, adicione-o usando o botão Adicionar Novo. 
  - Se a APPID estiver presente, verifique se tem as seguintes permissões de chave: Obter, Encapsular e Desencapsular.
