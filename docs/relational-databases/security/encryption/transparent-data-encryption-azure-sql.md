---
title: TDE para Data Warehouse e Banco de Dados SQL do Azure | Microsoft Docs
description: "Uma visão geral da Transparent Data Encryption para Data Warehouse e Banco de Dados SQL. O documento aborda seus benefícios e as opções de configuração, incluindo a TDE gerenciada por serviço e Bring Your Own Key."
keywords: 
services: sql-database
documentationcenter: 
author: becczhang
manager: cguyer
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: security
ms.workload: On Demand
ms.tgt_pltfrm: 
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: rebeccaz
ms.openlocfilehash: ac3ea91dc2db3d1cfb22dca2fdc341650c74b95b
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="transparent-data-encryption-for-azure-sql-database-and-data-warehouse"></a>Transparent Data Encryption para Data Warehouse e Banco de Dados SQL do Azure

[!INCLUDE[tsql-appliesto-xxxxxx-asdb-asdw-xxx-md](../../../includes/tsql-appliesto-xxxxxx-asdb-asdw-xxx-md.md)]

A TDE (Transparent Data Encryption) ajuda a proteger O Data Warehouse e o Banco de Dados SQL do Azure contra a ameaça de atividades mal-intencionadas executando criptografia e descriptografia em tempo real do banco de dados, backups associados e arquivos de log de transações em repouso sem exigir alterações no aplicativo.

A TDE criptografa o armazenamento de um banco de dados inteiro usando uma chave simétrica chamada de DEK (chave de criptografia de banco de dados). Essa chave de criptografia do banco de dados é protegida pelo protetor de TDE, que é um certificado gerenciado por serviço (“TDE gerenciada por serviço”) ou uma chave assimétrica armazenada no Azure Key Vault (“Bring Your Own Key”). O protetor de TDE é definido no nível do servidor. 

Na inicialização do banco de dados, a DEK criptografada é descriptografada e, em seguida, usada para descriptografia e para a nova criptografia dos arquivos de banco de dados no processo do SQL Engine. A TDE realiza a criptografia e a descriptografia de E/S em tempo real dos dados no nível da página. Cada página é descriptografada quando lida na memória e criptografada antes de ser gravada em disco. Para obter uma descrição geral do TDE, consulte [TDE (Transparent Data Encryption)](transparent-data-encryption.md).

O SQL Server em execução em uma máquina virtual do Azure também pode usar uma chave assimétrica do Key Vault. As etapas de configuração são diferentes do uso de uma chave assimétrica no Banco de Dados SQL do Azure. Para obter mais informações, veja [Gerenciamento extensível de chaves usando o Azure Key Vault (SQL Server)](extensible-key-management-using-azure-key-vault-sql-server.md).

## <a name="service-managed-tde"></a>TDE Gerenciada por Serviço

No Azure, a configuração padrão para a TDE é a que a chave de criptografia do banco de dados é protegida por um certificado do servidor interno. O certificado do servidor interno é exclusivo para cada servidor. Se um banco de dados estiver em um relacionamento de replicação geográfica, o banco de dados primário e o secundário geográfico serão protegidos pela chave de servidor pai do primário. Se dois bancos de dados estão conectados ao mesmo servidor, eles compartilham o mesmo certificado interno. A Microsoft gira automaticamente esses certificados pelo menos a cada 90 dias.

A Microsoft também move e gerencia diretamente as chaves conforme necessário para restaurações e replicação geográfica. 

> [!IMPORTANT]
> Todos os bancos de dados SQL recém-criados são criptografados por padrão usando a TDE gerenciada por serviço. Bancos de dados existentes antes de maio de 2017 e bancos de dados criados por meio de restauração, replicação geográfica e cópia de banco de dados não são criptografados por padrão.
>

## <a name="bring-your-own-key"></a>Bring Your Own Key

O suporte a BYOK (Bring Your Own Key) permite que o usuário tenha controle sobre suas chaves de criptografia de TDE e controle quem pode acessá-las e quando. O AKV (Azure Key Vault), que é o sistema de gerenciamento de chaves externas baseado em nuvem do Azure, é o primeiro serviço de gerenciamento de chaves integrado com TDE para suporte a BYOK. Com o BYOK, a chave de criptografia do banco de dados é protegida por uma chave assimétrica armazenada no AKV. A chave assimétrica nunca deixa o Key Vault. Depois que o servidor tem permissões para um cofre de chaves, o servidor envia solicitações de operação de chave básica para ele por meio do serviço do Key Vault. A chave assimétrica é definida no nível do servidor e herdada por todos os bancos de dados no servidor. Com suporte a BYOK, os usuários agora podem controlar tarefas de gerenciamento de chaves, incluindo rotações de chave, permissões do cofre de chaves, exclusão de chaves e habilitação de auditoria/relatórios em todas as chaves de criptografia. O Key Vault fornece o gerenciamento de chaves central, aproveita os HSMs (módulos de segurança de hardware) monitorados e promove a separação do gerenciamento de chaves e de dados para ajudar a atender às conformidades regulatórias. Para saber mais sobre o Key Vault, visite o [página de documentação do Key Vault](https://docs.microsoft.com/azure/key-vault/key-vault-secure-your-key-vault).

Para saber mais sobre a TDE com suporte a BYOK para Data Warehouse e Banco de dados SQL do Azure, consulte [Transparent Data Encryption com suporte a Bring Your Own Key](transparent-data-encryption-byok-azure-sql.md).

Para começar a usar a TDE com suporte a BYOK, consulte o guia de instruções [Ativar a Transparent Data Encryption usando sua própria chave do Key Vault usando o PowerShell](transparent-data-encryption-byok-azure-sql-configure.md).

## <a name="moving-a-tde-protected-database"></a>Movendo banco de dados protegido por TDE

Não é necessário descriptografar bancos de dados para operações no Azure. As configurações de TDE no banco de dados de origem ou banco de dados primário são herdadas de forma transparente no destino. Isso inclui operações envolvendo:
- Restauração geográfica
- Recuperação pontual de autoatendimento
- Restaurar um banco de dados excluído
- Replicação geográfica ativa
- Criar uma cópia do banco de dados

Ao exportar um banco de dados protegido por TDE, o conteúdo exportado do banco de dados não é criptografado. Esse conteúdo exportado é armazenado em arquivos BACPAC não criptografados. Certifique-se de proteger os arquivos BACPAC adequadamente e habilitar a TDE após a conclusão da importação do novo banco de dados.

Por exemplo, se o arquivo BACPAC for exportado de um SQL Server local, o conteúdo importado do novo banco de dados não será criptografado automaticamente. Da mesma forma, se o arquivo BACPAC for exportado para um SQL Server local, o novo banco de dados também não será criptografado automaticamente.

A única exceção é ao exportar de e para o Banco de Dados SQL do Azure. A TDE está habilitada no novo banco de dados, mas o próprio arquivo PACPAC ainda não está criptografado.

## <a name="managing-transparent-data-encryption-in-the-azure-portal"></a>Gerenciando a Transparent Data Encryption no Portal do Azure

Para configurar a TDE por meio do Portal do Azure, você deve estar conectado como o proprietário do Azure, o Colaborador ou o Gerenciador de segurança do SQL. 

A Transparent Data Encryption é definida no nível do banco de dados. Para habilitar a TDE em um banco de dados, visite o [Portal do Azure](https://portal.azure.com) e entre com sua conta de Colaborador ou Administrador do Azure. Localize as configurações da TDE em seu banco de dados do usuário. Por padrão, a TDE gerenciada por serviço é usada e um certificado de TDE é gerado automaticamente para o servidor contendo o banco de dados. 

![TDE gerenciada por serviço](./media/transparent-data-encryption-azure-sql/service-managed-tde.png)  

A chave mestra da TDE, também conhecida como o *Protetor da TDE*, é definida no nível do servidor. Para usar a TDE com suporte a Bring Your Own Key e proteger seus bancos de dados com uma chave do Azure Key Vault, visite as configurações da TDE no servidor. 

![TDE com suporte a BYOK](./media/transparent-data-encryption-azure-sql/tde-byok-support.png) 

## <a name="managing-transparent-data-encryption-using-powershell"></a>Gerenciando a Transparent Data Encryption usando o PowerShell

Para configurar a TDE por meio do PowerShell, você deve estar conectado como o proprietário do Azure, o Colaborador ou o Gerenciador de segurança do SQL. 

| Cmdlet | Description |
| --- | --- |
| [Set-AzureRmSqlDatabaseTransparentDataEncryption](/powershell/module/azurerm.sql/set-azurermsqldatabasetransparentdataencryption) |Habilita ou desabilita a TDE para um banco de dados.|
| [Get-AzureRmSqlDatabaseTransparentDataEncryption](/powershell/module/azurerm.sql/get-azurermsqldatabasetransparentdataencryption) |Obtém o estado da TDE para um banco de dados. |
| [Get-AzureRmSqlDatabaseTransparentDataEncryptionActivity](/powershell/module/azurerm.sql/get-azurermsqldatabasetransparentdataencryptionactivity) |Verifica o progresso da criptografia para um banco de dados. |
| [Add-AzureRmSqlServerKeyVaultKey](/powershell/module/azurerm.sql/add-azurermsqlserverkeyvaultkey) |Adiciona uma chave do Key Vault a um SQL Server. |
| [Get-AzureRmSqlServerKeyVaultKey](/powershell/module/azurerm.sql/get-azurermsqlserverkeyvaultkey) |Obtém as chaves do Key Vault do SQL Server. |
| [Set-AzureRmSqlServerTransparentDataEncryptionProtector](/powershell/module/azurerm.sql/set-azurermsqlservertransparentdataencryptionprotector) |Define o protetor de TDE para um SQL Server. |
| [Get-AzureRmSqlServerTransparentDataEncryptionProtector](/powershell/module/azurerm.sql/get-azurermsqlservertransparentdataencryptionprotector) |Obtém o protetor de TDE (Transparent Data Encryption). |
| [Remove-AzureRmSqlServerKeyVaultKey](/powershell/module/azurerm.sql/remove-azurermsqlserverkeyvaultkey) |Remove uma chave do Key Vault de um SQL Server. |
|  | |

## <a name="managing-transparent-data-encryption-using-transact-sql"></a>Gerenciando a Transparent Data Encryption usando o Transact-SQL

Conecte-se ao banco de dados usando um logon que seja um administrador ou um membro da função **dbmanager** no banco de dados mestre.

| Comando | Description |
| --- | --- |
| [ALTER DATABASE (Banco de Dados SQL do Azure)](/sql/t-sql/statements/alter-database-azure-sql-database) | Use SET ENCRYPTION ON/OFF para criptografar ou descriptografar um banco de dados. |
| [sys.dm_database_encryption_keys](/sql/relational-databases/system-dynamic-management-views/sys-dm-database-encryption-keys-transact-sql) |Retorna informações sobre o estado de criptografia de um banco de dados e suas chaves de criptografia de banco de dados associadas. |
| [sys.dm_pdw_nodes_database_encryption_keys](https://docs.microsoft.com/en-us/sql/relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-database-encryption-keys-transact-sql) |Retorna informações sobre o estado de criptografia de cada nó de data warehouse e suas chaves de criptografia de banco de dados associadas. | 
|  | |

O Protetor de TDE não pode ser alternado para uma chave do Azure Key Vault usando o Transact-SQL, use o PowerShell ou o Portal do Azure.

## <a name="managing-transparent-data-encryption-using-rest-api"></a>Gerenciando a Transparent Data Encryption usando a API REST
 
Para configurar a TDE por meio da API REST, você deve estar conectado como o proprietário do Azure, o Colaborador ou o Gerenciador de segurança do SQL. 

| Comando | Description |
| --- | --- |
|[Criar ou atualizar servidor](/rest/api/sql/servers/createorupdate)|Adiciona uma identidade do AAD para o SQL Server (usado para conceder acesso ao Key Vault).|
|[Criar ou atualizar a chave do servidor](/rest/api/sql/serverkeys/createorupdate)|Adiciona uma chave do Key Vault a um SQL Server.|
|[Excluir a chave do servidor](/rest/api/sql/serverkeys/delete)|Remove uma chave do Key Vault de um SQL Server.|
|[Obter a chave do servidor](/rest/api/sql/serverkeys/get)|Obtém uma chave específica do Key Vault de um SQL Server.|
|[Listar chaves de servidor por servidor](/rest/api/sql/serverkeys/listbyserver)|Obtém as chaves do Key Vault do SQL Server.|
|[Criar ou atualizar o protetor de criptografia](/rest/api/sql/encryptionprotectors/createorupdate)|Define o protetor de TDE para um SQL Server.|
|[Obter o protetor de criptografia](/rest/api/sql/encryptionprotectors/get)|Obtém o protetor de TDE para um SQL Server.|
|[Listar os protetores de criptografia por servidor](/rest/api/sql/encryptionprotectors/listbyserver)|Obtém os Protetores de TDE do SQL Server.|
|[Criar ou atualizar a configuração da Transparent Data Encryption](/rest/api/sql/transparentdataencryptions/createorupdate)|Habilita ou desabilita a TDE para um banco de dados.|
|[Obter a configuração da Transparent Data Encryption](/rest/api/sql/transparentdataencryptions/get)|Obtém a configuração de TDE para um banco de dados.|
|[Listar os resultados da configuração da Transparent Data Encryption](/rest/api/sql/transparentdataencryptionactivities/ListByConfiguration)|Obtém o resultado de criptografia para um banco de dados.|

## <a name="next-steps"></a>Próximas etapas

- Para obter uma descrição geral do TDE, consulte [TDE (Transparent Data Encryption)](transparent-data-encryption.md).

- Para saber mais sobre a TDE com suporte a BYOK para Data Warehouse e Banco de dados SQL do Azure, visite [Transparent Data Encryption com suporte a Bring Your Own Key](transparent-data-encryption-byok-azure-sql.md).

- Para começar a usar a TDE com suporte a BYOK, consulte o guia de instruções [Ativar a Transparent Data Encryption usando sua própria chave do Key Vault usando o PowerShell](transparent-data-encryption-byok-azure-sql-configure.md).

- Para obter mais informações sobre o Key Vault, consulte a [página de documentação do Key Vault](https://docs.microsoft.com/azure/key-vault/key-vault-secure-your-key-vault).
