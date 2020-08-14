---
title: Erros comuns com chaves gerenciadas pelo cliente no Azure Key Vault
description: Saiba como identificar e resolver problemas de acesso e erros comuns com a TDE (Transparent Data Encryption) e as chaves gerenciadas pelo cliente no Azure Key Vault.
ms.custom: seo-lt-2019
helpviewer_keywords:
- troublshooting, tde akv
- tde akv configuration, troubleshooting
- tde troubleshooting
author: jaszymas
ms.prod: sql
ms.technology: security
ms.reviewer: vanto
ms.topic: conceptual
ms.date: 11/06/2019
ms.author: jaszymas
monikerRange: = azuresqldb-current || = azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: 16368fe948d2cefeb052d503385c99cedfb097ff
ms.sourcegitcommit: a4ee6957708089f7d0dda15668804e325b8a240c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/06/2020
ms.locfileid: "87899009"
---
# <a name="common-errors-for-transparent-data-encryption-with-customer-managed-keys-in-azure-key-vault"></a>Erros comuns de Transparent Data Encryption com chaves gerenciadas pelo cliente no Azure Key Vault

[!INCLUDE[asdb-asdbmi-asa](../../../includes/applies-to-version/asdb-asdbmi-asa.md)]

Este artigo descreve como identificar e resolver os problemas de acesso de chave do Azure Key Vault que fizeram com que um banco de dados configurado para usar [TDE (Transparent Data Encryption) com chaves gerenciadas pelo cliente no Azure Key Vault](/azure/sql-database/transparent-data-encryption-byok-azure-sql) se torne inacessível.

## <a name="introduction"></a>Introdução
Quando o TDE está configurado para usar uma chave gerenciada pelo cliente no Azure Key Vault, o acesso contínuo a esse Protetor de TDE é necessário para que o banco de dados permaneça online.  Se o servidor SQL lógico perder o acesso ao protetor de TDE gerenciado pelo cliente no Azure Key Vault, um banco de dados começará a negar todas as conexões com a mensagem de erro adequada e alterará seu estado para *Inacessível* no portal do Azure.

Durante as primeiras 8 horas, se o problema subjacente de acesso à chave do Azure Key Vault for resolvido, o banco de dados será reparado e colocado online automaticamente. Isso significa que para todos os cenários de interrupção de rede intermitente e temporário não é necessária ação do usuário, e o banco de dados será colocado online automaticamente. Na maioria dos casos, a ação do usuário é necessária para resolver o problema subjacente de acesso à chave do cofre de chaves. 

Se um banco de dados inacessível não for mais necessário, ele poderá ser excluído imediatamente para interromper os custos. Todas as outras ações no banco de dados não são permitidas até que o acesso à chave do Azure Key Vault tenha sido restaurado e o banco de dados fique novamente online. A alteração da opção de TDE de chaves gerenciadas pelo cliente para chaves gerenciadas pelo servidor também não é possível enquanto um banco de dados criptografado com chaves gerenciadas pelo cliente está inacessível. Isso é necessário para proteger os dados contra o acesso não autorizado, enquanto as permissões para o protetor de TDE foram revogadas. 

Depois que um banco de dados ficar inacessível por mais de 8 horas, ele não será mais reparado automaticamente. Se o acesso necessário à chave do cofre de chaves do Azure for restaurado após esse período, você deverá revalidar o acesso à chave manualmente para colocar novamente o banco de dados online. Nesse caso, colocar novamente o banco de dados online pode demorar, dependendo do tamanho do banco de dados. Depois que o banco de dados estiver novamente online, as configurações definidas anteriormente, como o [grupo de failover](https://docs.microsoft.com/azure/sql-database/sql-database-auto-failover-group), histórico de PITR e todas as marcas **serão perdidas**. Portanto, é recomendável implementar um sistema de notificação usando [Grupos de Ações](https://docs.microsoft.com/azure/azure-monitor/platform/action-groups) que permitem estar ciente e tratar os problemas subjacentes do cofre de chaves assim que possível. 

## <a name="common-errors-causing-databases-to-become-inaccessible"></a>Erros comuns que fazem com que os bancos de dados se tornem inacessíveis

A maioria dos problemas que ocorrem ao usar TDE com o Key Vault é causada por um dos erros de configuração a seguir:

### <a name="the-key-vault-is-unavailable-or-doesnt-exist"></a>O cofre de chaves não está disponível ou não existe

- O cofre de chaves foi excluído por engano.
- O firewall foi configurado para o Azure Key Vault, mas não permite o acesso aos serviços da Microsoft.
- Um erro de rede intermitente faz com que o cofre de chaves fique indisponível.

### <a name="no-permissions-to-access-the-key-vault-or-the-key-doesnt-exist"></a>Sem permissão para acessar o cofre de chaves ou a chave não existe

- A chave foi excluída, desabilitada acidentalmente ou expirou.
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

Para saber mais, confira [Atribuir uma identidade do Azure AD ao seu servidor](/azure/sql-database/transparent-data-encryption-byok-azure-sql-configure#assign-an-azure-ad-identity-to-your-server).

> [!IMPORTANT]
> Se a instância lógica do SQL Server for movida para um novo locatário após a configuração inicial da TDE com o Key Vault, repita a etapa para configurar a identidade do Azure AD para criar uma AppId. Em seguida, adicione a AppId ao cofre de chaves e atribua as permissões corretas para a chave. 
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

## <a name="getting-tde-status-from-the-activity-log"></a>Obter o status de TDE do Log de atividades

Para permitir o monitoramento do status do banco de dados devido aos problemas de acesso à chave do Azure Key Vault, os eventos a seguir serão registrados no [Log de atividades](https://docs.microsoft.com/azure/service-health/alerts-activity-log-service-notifications) para a ID de recurso com base na URL do Azure Resource Manager e Assinatura + Resourcegroup + ServerName + DatabseName: 

**Evento quando o serviço perde o acesso à chave do Azure Key Vault**

EventName: MakeDatabaseInaccessible 

Status: Started (iniciado) 

Descrição: O banco de dados perdeu o acesso à chave do Azure Key Vault e agora está inacessível: <error message>   

 

**Evento quando o tempo de espera de 8 horas para a autorrecuperação começa** 

EventName: MakeDatabaseInaccessible 

Status: InProgress 

Descrição: O banco de dados está aguardando o acesso à chave do Azure Key Vault ser restabelecido pelo usuário em até 8 horas.   

 

**Evento quando o banco de dados volta a ficar online automaticamente**

EventName: MakeDatabaseAccessible 

Status: Teve êxito 

Descrição: O acesso ao banco de dados para a chave do Azure Key Vault foi restabelecido e o banco de dados agora está online. 

 

**Evento quando o problema não foi resolvido dentro de 8 horas e o acesso à chave do Azure Key Vault precisa ser validado manualmente** 

EventName: MakeDatabaseInaccessible 

Status: Teve êxito 

Descrição: O banco de dados está inacessível e exige que o usuário resolva os erros do Azure Key Vault e restabeleça o acesso à chave do Azure Key Vault usando a chave de revalidação. 

 

**Evento quando o BD ficar online após a revalidação da chave manual**

EventName: MakeDatabaseAccessible 

Status: Teve êxito 

Descrição: O acesso ao banco de dados para a chave do Azure Key Vault foi restabelecido e o banco de dados agora está online. 

 

**Evento quando a revalidação do acesso à chave de Azure Key Vault foi bem-sucedida e o banco de dados voltar a ficar online**

EventName: MakeDatabaseAccessible 

Status: Started (iniciado) 

Descrição: A restauração do acesso ao banco de dados para a chave do Azure Key Vault foi iniciada. 

 

**Evento ao revalidar o acesso à chave de Azure Key Vault falhou**

EventName: MakeDatabaseAccessible 

Status: Falhou 

Descrição: A restauração do acesso ao banco de dados para a chave do Azure Key Vault falhou. 


## <a name="next-steps"></a>Próximas etapas

- Saiba mais sobre o [Azure Resource Health](https://docs.microsoft.com/azure/service-health/resource-health-overview).
- Configure os [Grupos de ações](https://docs.microsoft.com/azure/azure-monitor/platform/action-groups) para receber notificações e alertas com base em suas preferências, por exemplo, email/SMS/Push/voz, aplicativo lógico, webhook, ITSM ou runbook de automação. 


