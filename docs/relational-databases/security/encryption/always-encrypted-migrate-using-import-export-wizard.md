---
title: Migrar dados bidirecionalmente em colunas usando o Always Encrypted com o Assistente de Importação e Exportação do SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 10/31/2019
ms.prod: sql
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
f1_keywords:
- SQL13.SWB.COLUMNMASTERKEY.PAGE.F1
- SQL13.SWB.COLUMNENCRYPTIONKEY.PAGE.F1
- SQL13.SWB.COLUMNMASTERKEY.ROTATION.F1
helpviewer_keywords:
- Always Encrypted, configure with SSMS
ms.assetid: 29816a41-f105-4414-8be1-070675d62e84
author: jaszymas
ms.author: jaszymas
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: c8e23b3f5f291d120a099cae7f3e3e057db8da95
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "73595781"
---
# <a name="migrate-data-to-or-from-columns-using-always-encrypted-with-sql-server-import-and-export-wizard"></a>Migrar dados para ou de colunas usando Always Encrypted com o Assistente de Importação e Exportação do SQL Server 
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

O [Assistente de Importação e Exportação do SQL Server](../../../integration-services/import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard.md) é uma ferramenta que permite copiar dados de uma origem para um destino. Este documento descreve como usar o Assistente de Importação e Exportação do SQL Server se uma origem e/ou um destino é um banco de dados do SQL Server que contém colunas protegidas com o [Always Encrypted](../../../relational-databases/security/encryption/always-encrypted-database-engine.md).

## <a name="migration-scenarios"></a>Cenários de migração
Com o Assistente de Importação e Exportação do SQL Server, implemente os cenários a seguir para migrar dados bidirecionalmente em colunas criptografadas.

### <a name="encrypt-plaintext-data-on-migration"></a>Criptografar dados de texto não criptografado na migração
Se a fonte de dados contém dados de texto não criptografado e o destino é um banco de dados do SQL Server que contém colunas criptografadas, use o Assistente de Importação e Exportação do SQL Server para recuperar os dados de texto não criptografado da origem, criptografá-los e copiar os dados criptografados (texto cifrado) para as colunas criptografadas no banco de dados de destino. Para esse cenário de migração, a fonte de dados pode ser qualquer armazenamento de dados compatível com o Assistente de Importação e Exportação do SQL Server. Por exemplo, um arquivo, um banco de dados do SQL Server ou um banco de dados em outro sistema de banco de dados.

Para garantir que o Assistente de Importação e Exportação do SQL Server possa criptografar dados, você precisará habilitar o Always Encrypted para a conexão de banco de dados de destino e ter acesso às chaves que protegem os dados nas colunas do banco de dados de destino. Para obter mais informações, confira [Habilitar e desabilitar o Always Encrypted para uma conexão de banco de dados](#enable-and-disable-always-encrypted-for-a-database-connection) e [Permissões para criptografar ou descriptografar dados durante a migração](#permissions-for-encrypting-or-decrypting-data-during-migration).

### <a name="decrypt-encrypted-data-on-migration"></a>Descriptografar dados criptografados na migração
Se você estiver migrando dados armazenados em colunas de banco de dados criptografadas em um banco de dados do SQL Server, configure o Assistente de Importação e Exportação do SQL Server para descriptografar os dados e copiar os dados descriptografados (texto não criptografado) para um destino, que pode ser qualquer armazenamento de dados compatível com o Assistente de Importação e Exportação do SQL Server, por exemplo, um arquivo, um banco de dados do SQL Server ou um banco de dados em outro sistema de banco de dados.

Para garantir que o Assistente de Importação e Exportação do SQL Server possa descriptografar dados, você precisará habilitar o Always Encrypted para a conexão de banco de dados de origem e ter acesso às chaves que protegem os dados nas colunas do banco de dados de origem. Para obter mais informações, confira [Habilitar e desabilitar o Always Encrypted para uma conexão de banco de dados](#enable-and-disable-always-encrypted-for-a-database-connection) e [Permissões para criptografar ou descriptografar dados durante a migração](#permissions-for-encrypting-or-decrypting-data-during-migration).

### <a name="re-encrypt-data-on-migration"></a>Criptografar dados novamente na migração
Se você estiver copiando os dados de colunas criptografadas em um banco de dados de origem do SQL Server para colunas criptografadas no mesmo ou em outro banco de dados do SQL Server, configure o Assistente de Importação e Exportação do SQL Server para descriptografar os dados depois de recuperá-los da origem e criptografá-los novamente antes de inseri-los nas colunas criptografadas no banco de dados de destino. Use esse método se o esquema das colunas de destino (por exemplo, tipos de dados de coluna, tipos de criptografia e chaves de criptografia de coluna) for diferente do esquema das colunas de origem.

Para garantir que o Assistente de Importação e Exportação do SQL Server possa criptografar e descriptografar dados, você precisará habilitar o Always Encrypted para a conexão de banco de dados de origem e a conexão de banco de dados de destino e ter acesso às chaves que protegem os dados nas colunas de banco de dados de origem e de destino. Para obter mais informações, confira [Habilitar e desabilitar o Always Encrypted para uma conexão de banco de dados](#enable-and-disable-always-encrypted-for-a-database-connection) e [Permissões para criptografar ou descriptografar dados durante a migração](#permissions-for-encrypting-or-decrypting-data-during-migration).

### <a name="keep-data-encrypted-during-migration"></a>Manter os dados criptografados durante a migração
Se você estiver copiando os dados de colunas criptografadas em um banco de dados de origem do SQL Server para colunas criptografadas no mesmo ou em outro banco de dados do SQL Server e as colunas de destino usarem **exatamente** o esquema (incluindo os mesmos tipos de dados, tipos de criptografia e chaves de criptografia de coluna) das colunas de origem, configure o Assistente de Importação e Exportação do SQL Server para recuperar o texto cifrado das colunas de origem e inserir os dados criptografados (texto cifrado) na coluna criptografada no banco de dados de destino do SQL Server. 

Para esse cenário, use qualquer provedor de dados que dê suporte ao SQL Server para se conectar ao banco de dados de origem ou destino do SQL Server. Se você estiver usando um provedor que dê suporte ao Always Encrypted para se conectar ao banco de dados de destino, verifique se o Always Encrypted está desabilitado para a conexão de banco de dados. Para obter mais informações, confira [Habilitar e desabilitar o Always Encrypted para uma conexão de banco de dados](#enable-and-disable-always-encrypted-for-a-database-connection).

Você também precisa garantir que a entidade de segurança do banco de dados (usuário) usada pelo Assistente de Importação e Exportação do SQL Server para se conectar ao banco de dados de destino está configurada com a opção `ALLOW_ENCRYPTED_VALUE_MODIFICATIONS` definida como `ON`. Essa opção suprime as verificações de metadados criptográficos no servidor em operações de cópia em massa, o que permite ao assistente inserir em massa os dados criptografados no banco de dados de destino sem descriptografá-los. Para obter mais informações, confira [Carregar em massa dados criptografados em colunas protegidas pelo Always Encrypted](migrate-sensitive-data-protected-by-always-encrypted.md).

## <a name="enable-and-disable-always-encrypted-for-a-database-connection"></a>Habilitar e desabilitar o Always Encrypted para uma conexão de banco de dados
Se o cenário de migração exige que o Assistente de Importação e Exportação do SQL Server possa criptografar e/ou descriptografar dados, você precisa configurar a conexão de banco de dados de origem do SQL Server e/ou a conexão de banco de dados de destino do SQL Server usando um provedor de dados que dê suporte ao Always Encrypted. Você também precisa habilitar o Always Encrypted para a conexão de banco de dados de origem e/ou destino.

Use qualquer provedor de dados para uma conexão se não precisar que o assistente criptografe ou descriptografe dados nessa conexão.

Os provedores de dados a seguir no Assistente de Importação e Exportação do SQL Server dão suporte ao Always Encrypted.

- Provedor de dados do .NET Framework para SQL Server
  - Verifique se o computador no qual o assistente é executado usa o .NET Framework 4.6.1 ou posterior.
  - Para habilitar o Always Encrypted para uma conexão, defina `Column Encryption Setting` como `Enabled` nas propriedades de conexão. Para desabilitar o Always Encrypted, defina `Column Encryption Setting` como `Disabled`. Para obter mais informações, confira [Conectar-se ao SQL Server com o provedor de dados .NET Framework para SQL Server](../../../integration-services/import-export-data/connect-to-a-sql-server-data-source-sql-server-import-and-export-wizard.md#connect-to-sql-server-with-the-net-framework-data-provider-for-sql-server) e [Como habilitar o Always Encrypted para consultas de aplicativo](develop-using-always-encrypted-with-net-framework-data-provider.md#enabling-always-encrypted-for-application-queries).
- Provedor de dados .NET Framework para ODBC.
  - Instale o Microsoft ODBC Driver 13.1 ou posterior.
    - Para habilitar o Always Encrypted para uma conexão, defina `Column Encryption` como `Enabled` nas propriedades de conexão. Para desabilitar o Always Encrypted, defina `Column Encryption` como `Disabled`. Para obter mais informações, confira [Conectar-se ao SQL Server com o driver ODBC para SQL Server](../../../integration-services/import-export-data/connect-to-a-sql-server-data-source-sql-server-import-and-export-wizard.md#connect-to-sql-server-with-the-odbc-driver-for-sql-server) e [Como habilitar o Always Encrypted em um aplicativo ODBC](../../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md#enabling-always-encrypted-in-an-odbc-application).

## <a name="permissions-for-encrypting-or-decrypting-data-during-migration"></a>Permissões para criptografar ou descriptografar dados durante a migração

Para criptografar ou descriptografar os dados armazenados em um banco de dados de origem ou destino do SQL Server, você precisará das permissões *VIEW ANY COLUMN MASTER KEY DEFINITION* e *VIEW ANY COLUMN ENCRYPTION KEY DEFINITION* no banco de dados de origem.

Você também precisará acessar as chaves mestras de coluna, configuradas para as colunas que armazenam os dados que estão sendo criptografados ou descriptografados:

- **Repositório de Certificados – Computador local**: você precisa ter acesso de leitura ao certificado que é usado como chave mestra da coluna ou ser o administrador do computador.
- **Azure Key Vault** – você precisará das permissões _get_, _unwrapKey_ e _verify_ no cofre que contém a chave mestra de coluna.
- **Provedor do Repositório de Chaves (CNG)** – a permissão e as credenciais necessárias que poderão ser solicitadas quando você usar um repositório de chaves ou uma chave, dependendo do repositório e da configuração do KSP.
- **Provedor de Serviços de Criptografia (CAPI)** – a permissão e as credenciais necessárias que poderão ser solicitadas quando você usar um repositório de chaves ou uma chave, dependendo do repositório e da configuração do CSP.
Para obter mais informações, consulte [Create and Store Column Master Keys (Always Encrypted)](../../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md)Criar e armazenar chaves mestras de coluna (Always Encrypted).

## <a name="next-steps"></a>Próximas etapas
- [Consultar colunas usando o Always Encrypted com o SQL Server Management Studio](always-encrypted-query-columns-ssms.md)
- [Desenvolver aplicativos usando o Always Encrypted](always-encrypted-client-development.md)

## <a name="see-also"></a>Consulte Também
- [Always Encrypted](always-encrypted-database-engine.md)
- [Exportar e importar bancos de dados usando o Always Encrypted](always-encrypted-migrate-using-bacpac.md)
- [Fazer backup de bancos de dados e restaurá-los usando o Always Encrypted](always-encrypted-migrate-using-backup-restore.md)
- [Carregar em massa dados criptografados em colunas usando o Always Encrypted](migrate-sensitive-data-protected-by-always-encrypted.md)