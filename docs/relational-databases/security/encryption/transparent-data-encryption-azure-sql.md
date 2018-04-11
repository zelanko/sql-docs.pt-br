---
title: Transparent Data Encryption para Data Warehouse e Banco de Dados SQL do Azure | Microsoft Docs
description: Uma visão geral sobre a Transparent Data Encryption para Data Warehouse e Banco de Dados SQL. O documento aborda seus benefícios e as opções de configuração, que inclui a Transparent Data Encryption gerenciada por serviço e Bring Your Own Key.
keywords: ''
author: becczhang
manager: craigg
editor: ''
ms.prod: ''
ms.reviewer: ''
ms.suite: sql
ms.prod_service: sql-database, sql-data-warehouse
ms.service: sql-database
ms.component: security
ms.custom: ''
ms.workload: On Demand
ms.tgt_pltfrm: ''
ms.topic: article
ms.date: 08/07/2017
ms.author: rebeccaz
ms.openlocfilehash: 45e4c702e2f08ce6e7c39463ac49c98701646f37
ms.sourcegitcommit: d6b1695c8cbc70279b7d85ec4dfb66a4271cdb10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2018
---
# <a name="transparent-data-encryption-for-sql-database-and-data-warehouse"></a>Transparent Data Encryption para Data Warehouse e Banco de Dados SQL
[!INCLUDE[appliesto-xx-asdb-asdw-xxx-md](../../../includes/appliesto-xx-asdb-asdw-xxx-md.md)]

A Transparent Data Encryption ajuda a proteger o Banco de Dados SQL do Azure e o Data Warehouse do Azure contra a ameaça de atividades mal-intencionadas. Ela executa criptografia e descriptografia em tempo real do banco de dados, backups associados e arquivos de log de transações em repouso sem exigir alterações no aplicativo.

A Transparent Data Encryption criptografa o armazenamento de um banco de dados inteiro usando uma chave simétrica chamada de chave de criptografia do banco de dados. Essa chave de criptografia do banco de dados é protegida pelo protetor da Transparent Data Encryption. O protetor é um certificado gerenciado por serviço (Transparent Data Encryption gerenciada por serviço) ou uma chave assimétrica armazenada no Azure Key Vault (Bring Your Own Key). Você define o protetor da Transparent Data Encryption no nível do servidor. 

Na inicialização do banco de dados, a chave de criptografia do banco de dados criptografada é descriptografada e, em seguida, usada para descriptografia e para a nova criptografia dos arquivos do banco de dados no processo do Mecanismo de Banco de Dados do SQL Server. A Transparent Data Encryption executa criptografia de E/S em tempo real e a descriptografia dos dados no nível de página. Cada página é descriptografada quando lida na memória e, em seguida, criptografada antes de ser gravada em disco. Para obter uma descrição geral da Transparent Data Encryption, consulte [Transparent Data Encryption](transparent-data-encryption.md).

O SQL Server em execução em uma máquina virtual do Azure também pode usar uma chave assimétrica do Key Vault. As etapas de configuração são diferentes do uso de uma chave assimétrica no Banco de Dados SQL. Para obter mais informações, veja [Gerenciamento extensível de chaves usando o Azure Key Vault (SQL Server)](extensible-key-management-using-azure-key-vault-sql-server.md).

## <a name="service-managed-transparent-data-encryption"></a>Transparent Data Encryption gerenciada por serviço

No Azure, a configuração padrão para a Transparent Data Encryption é a que a chave de criptografia do banco de dados é protegida por um certificado do servidor interno. O certificado do servidor interno é exclusivo para cada servidor. Se um banco de dados está em um relacionamento de replicação geográfica, o banco de dados primário e o secundário geográfico são protegidos pela chave de servidor pai do banco de dados primário. Se dois bancos de dados estão conectados ao mesmo servidor, eles compartilham o mesmo certificado interno. A Microsoft gira automaticamente esses certificados pelo menos a cada 90 dias.

A Microsoft também move e gerencia diretamente as chaves conforme necessário para restaurações e replicação geográfica. 

> [!IMPORTANT]
> Todos os bancos de dados SQL recém-criados são criptografados por padrão usando a Transparent Data Encryption gerenciada por serviço. Os bancos de dados existentes antes de maio de 2017 e bancos de dados criados por meio de restauração, de replicação geográfica e de cópia de banco de dados, não são criptografados por padrão.
>

## <a name="bring-your-own-key-preview"></a>Bring Your Own Key (versão prévia)

Com o suporte do Bring Your Own Key (versão prévia), você obtém o controle das suas chaves de Transparent Data Encryption e controla quem pode acessá-las e quando. O Key Vault, que é o sistema de gerenciamento de chave externa baseado em nuvem do Azure, é o primeiro serviço de gerenciamento de chaves que a Transparent Data Encryption integrou com o suporte do Bring Your Own Key. Com o suporte do Bring Your Own Key, a chave de criptografia do banco de dados é protegida por uma chave assimétrica armazenada no Key Vault. A chave assimétrica nunca deixa o Key Vault. Depois que o servidor tem permissões para um cofre de chaves, o servidor envia solicitações básicas de operação de chave para ele por meio do Key Vault. Você define a chave assimétrica no nível do servidor e todos os bancos de dados nesse servidor a herdam.

Com o suporte do Bring Your Own Key, agora você pode controlar tarefas de gerenciamento de chaves, como rotações de chave e permissões do cofre de chaves. Você também pode excluir chaves e habilitar auditoria/relatórios em todas as chaves de criptografia. O Key Vault oferece gerenciamento de chaves central e usa módulos de segurança de hardware rigorosamente monitorados. O Key Vault promove a separação do gerenciamento de chaves e dados para ajudar a atender à conformidade regulatória. Para saber mais sobre o Key Vault, veja a [página de documentação do Key Vault](https://docs.microsoft.com/azure/key-vault/key-vault-secure-your-key-vault).

Para saber mais sobre a Transparent Data Encryption com suporte a Bring Your Own Key para Data Warehouse e Banco de Dados SQL, consulte [Transparent Data Encryption com suporte a Bring Your Own Key](transparent-data-encryption-byok-azure-sql.md).

Para começar a usar a Transparent Data Encryption com suporte a Bring Your Own Key, veja o guia de instruções [Ativar a Transparent Data Encryption com sua própria chave do Key Vault usando o PowerShell](transparent-data-encryption-byok-azure-sql-configure.md).

## <a name="move-a-transparent-data-encryption-protected-database"></a>Mover um banco de dados protegido por Transparent Data Encryption

Não é necessário descriptografar bancos de dados para operações no Azure. As configurações de Transparent Data Encryption no banco de dados de origem ou banco de dados primário são herdadas de forma transparente no destino. As operações que estão incluídas envolvem:
- Restauração geográfica.
- Recuperação pontual de autoatendimento.
- Restauração de um banco de dados excluído.
- Replicação geográfica ativa.
- Criação de uma cópia do banco de dados.

Quando você exporta um banco de dados protegido por Transparent Data Encryption, o conteúdo exportado do banco de dados não é criptografado. Esse conteúdo exportado é armazenado em arquivos BACPAC não criptografados. Certifique-se de proteger os arquivos BACPAC adequadamente e habilitar a Transparent Data Encryption após terminar a importação do novo banco de dados.

Por exemplo, se o arquivo BACPAC for exportado de uma instância local do SQL Server, o conteúdo importado do novo banco de dados não será criptografado automaticamente. Da mesma forma, se o arquivo BACPAC for exportado para uma instância local do SQL Server, o novo banco de dados também não será criptografado automaticamente.

A única exceção é ao exportar de e para um Banco de Dados SQL. A Transparent Data Encryption está habilitada no novo banco de dados, mas o próprio arquivo PACPAC ainda não está criptografado.

## <a name="manage-transparent-data-encryption-in-the-azure-portal"></a>Gerenciar a Transparent Data Encryption no Portal do Azure

Para configurar a Transparent Data Encryption por meio do Portal do Azure, você deve estar conectado como Proprietário ou Colaborador do Azure, ou Gerenciador de Segurança do SQL. 

A Transparent Data Encryption é definida no nível do banco de dados. Para habilitar a Transparent Data Encryption em um banco de dados, acesse o [Portal do Azure](https://portal.azure.com) e entre com sua conta de Colaborador ou Administrador do Azure. Localize as configurações de Transparent Data Encryption em seu banco de dados do usuário. Por padrão, a Transparent Data Encryption gerenciada por serviço é usada. Um certificado de Transparent Data Encryption é gerado automaticamente para o servidor que contém o banco de dados. 

![Transparent Data Encryption gerenciada por serviço](./media/transparent-data-encryption-azure-sql/service-managed-tde.png)  

Você define a chave mestra de Transparent Data Encryption, também conhecida como a protetora da Transparent Data Encryption, no nível do servidor. Para usar a Transparent Data Encryption com suporte de Bring Your Own Key e proteger seus bancos de dados com uma chave do Key Vault, consulte as configurações da Transparent Data Encryption em seu servidor. 

![Transparent Data Encryption com suporte de Bring Your Own Key](./media/transparent-data-encryption-azure-sql/tde-byok-support.png) 

## <a name="manage-transparent-data-encryption-by-using-powershell"></a>Gerenciar a Transparent Data Encryption usando o PowerShell

Para configurar a Transparent Data Encryption por meio do PowerShell, você deve estar conectado como Proprietário ou Colaborador do Azure, ou Gerenciador de Segurança do SQL. 

| Cmdlet | Description |
| --- | --- |
| [Set-AzureRmSqlDatabaseTransparentDataEncryption](/powershell/module/azurerm.sql/set-azurermsqldatabasetransparentdataencryption) |Habilita ou desabilita a Transparent Data Encryption em um banco de dados|
| [Get-Azure-Rm-Sql-Database-Transparent-Data-Encryption](/powershell/module/azurerm.sql/get-azurermsqldatabasetransparentdataencryption) |Obtém o estado da Transparent Data Encryption de um banco de dados |
| [Get-Azure-Rm-Sql-Database-Transparent-Data-Encryption-Activity](/powershell/module/azurerm.sql/get-azurermsqldatabasetransparentdataencryptionactivity) |Verifica o progresso da criptografia em um banco de dados |
| [Add-AzureRmSqlServerKeyVaultKey](/powershell/module/azurerm.sql/add-azurermsqlserverkeyvaultkey) |Adiciona uma chave do Key Vault a uma Instância do SQL Server |
| [Get-AzureRmSqlServerKeyVaultKey](/powershell/module/azurerm.sql/get-azurermsqlserverkeyvaultkey) |Obtém as chaves do Key Vault para uma Instância do SQL Server  |
| [Set-AzureRmSqlServerTransparentDataEncryptionProtector](/powershell/module/azurerm.sql/set-azurermsqlservertransparentdataencryptionprotector) |Define o protetor da Transparent Data Encryption para uma instância do SQL Server |
| [Get-AzureRmSqlServerTransparentDataEncryptionProtector](/powershell/module/azurerm.sql/get-azurermsqlservertransparentdataencryptionprotector) |Obtém o protetor da Transparent Data Encryption |
| [Remove-AzureRmSqlServerKeyVaultKey](/powershell/module/azurerm.sql/remove-azurermsqlserverkeyvaultkey) |Remove uma chave do Key Vault de uma Instância do SQL Server |
|  | |

## <a name="manage-transparent-data-encryption-by-using-transact-sql"></a>Gerenciar a Transparent Data Encryption usando o Transact-SQL

Conecte-se ao banco de dados usando um logon que seja um administrador ou um membro da função **dbmanager** no banco de dados mestre.

| Comando | Description |
| --- | --- |
| [ALTER DATABASE (Banco de Dados SQL do Azure)](/sql/t-sql/statements/alter-database-azure-sql-database) | SET ENCRYPTION ON/OFF criptografa ou descriptografa um banco de dados |
| [sys.dm_database_encryption_keys](/sql/relational-databases/system-dynamic-management-views/sys-dm-database-encryption-keys-transact-sql) |Retorna informações sobre o estado da criptografia de um banco de dados e suas chaves de criptografia de banco de dados associadas |
| [sys.dm_pdw_nodes_database_encryption_keys](https://docs.microsoft.com/sql/relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-database-encryption-keys-transact-sql) |Retorna informações sobre o estado de criptografia de cada nó de data warehouse e suas chaves de criptografia de banco de dados associadas | 
|  | |

Você não pode mudar o protetor da Transparent Data Encryption para uma chave do Key Vault usando o Transact-SQL. Use o PowerShell ou o Portal do Azure.

## <a name="manage-transparent-data-encryption-by-using-the-rest-api"></a>Gerenciar a Transparent Data Encryption usando a API REST
 
Para configurar a Transparent Data Encryption por meio da API REST, você deve estar conectado como Proprietário ou Colaborador do Azure, ou Gerenciador de Segurança do SQL. 

| Comando | Description |
| --- | --- |
|[Criar ou atualizar servidor](/rest/api/sql/servers/createorupdate)|Adiciona uma identidade do Azure Active Directory a uma instância do SQL Server (usada para conceder acesso ao Key Vault)|
|[Criar ou atualizar a chave do servidor](/rest/api/sql/serverkeys/createorupdate)|Adiciona uma chave do Key Vault a uma Instância do SQL Server|
|[Excluir a chave do servidor](/rest/api/sql/serverkeys/delete)|Remove uma chave do Key Vault de uma Instância do SQL Server|
|[Obter a chave do servidor](/rest/api/sql/serverkeys/get)|Obtém uma chave específica do Key Vault de uma Instância do SQL Server|
|[Listar chaves de servidor por servidor](/rest/api/sql/serverkeys/listbyserver)|Obtém as chaves do Key Vault para uma Instância do SQL Server |
|[Criar ou atualizar o protetor de criptografia](/rest/api/sql/encryptionprotectors/createorupdate)|Define o protetor da Transparent Data Encryption para uma instância do SQL Server|
|[Obter o protetor de criptografia](/rest/api/sql/encryptionprotectors/get)|Obtém o protetor da Transparent Data Encryption para uma Instância do SQL Server|
|[Listar os protetores de criptografia por servidor](/rest/api/sql/encryptionprotectors/listbyserver)|Obtém os protetores da Transparent Data Encryption para uma Instância do SQL Server |
|[Criar ou atualizar a configuração da Transparent Data Encryption](/rest/api/sql/transparentdataencryptions/createorupdate)|Habilita ou desabilita a Transparent Data Encryption em um banco de dados|
|[Obter a configuração da Transparent Data Encryption](/rest/api/sql/transparentdataencryptions/get)|Obtém a configuração da Transparent Data Encryption de um banco de dados|
|[Listar os resultados da configuração da Transparent Data Encryption](/rest/api/sql/transparentdataencryptionactivities/ListByConfiguration)|Obtém o resultado da criptografia de um banco de dados|

## <a name="next-steps"></a>Próximas etapas

- Para obter uma descrição geral da Transparent Data Encryption, consulte [Transparent Data Encryption](transparent-data-encryption.md).
- Para saber mais sobre a Transparent Data Encryption com suporte a Bring Your Own Key para Data Warehouse e Banco de Dados SQL, consulte [Transparent Data Encryption com suporte a Bring Your Own Key](transparent-data-encryption-byok-azure-sql.md).
- Para começar a usar a Transparent Data Encryption com suporte a Bring Your Own Key, veja o guia de instruções [Ativar a Transparent Data Encryption com sua própria chave do Key Vault usando o PowerShell](transparent-data-encryption-byok-azure-sql-configure.md).
- Para obter mais informações sobre o Key Vault, consulte a [página de documentação do Key Vault](https://docs.microsoft.com/azure/key-vault/key-vault-secure-your-key-vault).
