---
title: Provisionar chaves do Always Encrypted usando o SQL Server Management Studio | Microsoft Docs
ms.custom: ''
ms.date: 10/01/2019
ms.prod: sql
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
f1_keywords:
- SQL13.SWB.COLUMNMASTERKEY.PAGE.F1
- SQL13.SWB.COLUMNENCRYPTIONKEY.PAGE.F1
helpviewer_keywords:
- Always Encrypted, configure with SSMS
ms.assetid: 29816a41-f105-4414-8be1-070675d62e84
author: jaszymas
ms.author: jaszymas
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 13bb5944c5907f3bebc9f01eb969b4b8979f8c97
ms.sourcegitcommit: 312b961cfe3a540d8f304962909cd93d0a9c330b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/05/2019
ms.locfileid: "73595751"
---
# <a name="provision-always-encrypted-keys-using-sql-server-management-studio"></a>Provisionar chaves Always Encrypted usando o SQL Server Management Studio
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

Este artigo fornece as etapas usadas para provisionar chaves mestras de coluna e chaves de criptografia de coluna para o Always Encrypted usando o [SSMS (SQL Server Management Studio)](../../../ssms/download-sql-server-management-studio-ssms.md).

Para obter uma visão geral do gerenciamento de chaves do Always Encrypted, incluindo recomendações de melhor prática e considerações importantes sobre segurança, confira [Visão geral do gerenciamento de chaves do Always Encrypted](../../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md).

<a name="provisioncmk"></a>
## <a name="provision-column-master-keys-with-the-new-column-master-key-dialog"></a>Provisionar chaves mestras de coluna com a caixa de diálogo Nova Chave Mestra de Coluna

A caixa de diálogo **Nova Chave Mestra da Coluna** permite que você gere uma chave mestra da coluna ou escolha uma chave existente em um repositório de chaves e crie metadados de chave mestra da coluna para a chave criada ou selecionada no banco de dados.

1.  Usando o **Pesquisador de Objetos**, navegue até a pasta **Segurança > Chaves Always Encrypted** em seu banco de dados.
2.  Clique com o botão direito do mouse na pasta **Chaves Mestras de Coluna** e selecione **Nova Chave Mestra de Coluna...** . 
3.  Na caixa de diálogo **Nova Chave Mestra de Coluna** , digite o nome do objeto de metadados de chave mestra de coluna.
4.  Selecione um repositório de chaves:
    - **Repositório de Certificados – Usuário atual**: indica a localização do repositório de certificados do usuário atual no Repositório de Certificados do Windows, que é seu repositório pessoal. 
    - **Repositório de Certificados – Computador local**: indica a localização do repositório de certificados do computador local no Repositório de Certificados do Windows. 
    - **Azure Key Vault** – você precisará entrar no Azure (clique em **Entrar**). Depois de entrar, você poderá escolher uma das suas assinaturas do Azure e um cofre de chaves.
    - **Provedor do Repositório de Chaves (KSP)** : indica um repositório de chaves que pode ser acessado pelo KSP (provedor do repositório de chaves) que implementa a API CNG (Cryptography Next Generation). Normalmente, esse tipo de repositório é um HSM (módulo de segurança de hardware). Depois de selecionar essa opção, você precisará escolher um KSP. **Provedor de Armazenamento de Chaves do Software Microsoft** é selecionado por padrão. Se você desejar usar uma chave mestra de coluna armazenada em um HSM, selecione um KSP para seu dispositivo (deve ser instalado e configurado no computador antes de abrir a caixa de diálogo).
    -   **Provedor de Serviços de Criptografia (CSP)** : um repositório de chaves que é acessível por meio de um CSP (provedor de serviços de criptografia) que implementa a CAPI (Cryptography API). Normalmente, esse tipo de repositório é um HSM (módulo de segurança de hardware). Depois de selecionar essa opção, você precisará escolher um CSP.  Se você desejar usar uma chave mestra de coluna armazenada em um HSM, selecione um CSP para seu dispositivo (deve ser instalado e configurado no computador antes de abrir a caixa de diálogo).
    
    > [!NOTE]
    > Como a CAPI é uma API preterida, a opção Provedor de Serviços de Criptografia (CAPI) é desabilitada por padrão. Você pode habilitar criando o valor CAPI Provider Enabled DWORD na chave **[HKEY_CURRENT_USER\Software\Microsoft\Microsoft SQL Server\sql13\Tools\Client\Always Encrypted]** no Registro do Windows e definindo-o como 1. Você deve usar o CNG em vez de CAPI, a menos que seu repositório de chaves não dê suporte ao CNG.
   
    Para obter mais informações sobre os repositórios de chaves acima, confira [Criar e armazenar chaves mestras de coluna do Always Encrypted](../../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md).

5. Se você estiver usando o [!INCLUDE [sssqlv15-md](../../../includes/sssqlv15-md.md)] e a Instância do SQL Server estiver configurada com um enclave seguro, marque a caixa de seleção **Permitir cálculos de enclave** para tornar a chave mestra habilitada para enclave. Confira [Always Encrypted com enclaves seguros](always-encrypted-enclaves.md) para obter detalhes. 

    > [!NOTE]
    > A caixa de seleção **Permitir cálculos de enclave** não é exibida se a Instância do SQL Server não está configurada corretamente com um enclave seguro.

6.  Selecione uma chave existente no seu repositório de chaves ou clique no botão **Gerar Chave** ou **Gerar Certificado** para criar uma chave no repositório de chaves. 
7.  Clique em **OK** e a nova chave aparecerá na lista. 

Depois que você concluir a caixa de diálogo, o SQL Server Management Studio criará metadados para a chave mestra de coluna no banco de dados. A caixa de diálogo consegue isso gerando e emitindo uma instrução [CREATE COLUMN MASTER KEY (Transact-SQL)](../../../t-sql/statements/create-column-master-key-transact-sql.md) .

::: moniker range=">=sql-server-ver15||=sqlallproducts-allversions"

Se você está configurando uma chave mestra de coluna habilitada para enclave, o SSMS também assina os metadados usando a chave mestra de coluna. 

::: moniker-end

### <a name="permissions-for-provisioning-a-column-master-key"></a>Permissões para provisionar uma chave mestra de coluna

Você precisará da permissão de banco de dados *ALTER ANY COLUMN MASTER KEY* no banco de dados para que a caixa de diálogo crie uma chave mestra de coluna. Para usar a caixa de diálogo para criar uma chave mestra de coluna ou usar uma chave existente em uma criação de repositório de chaves, você pode exigir permissões no repositório de chaves e/ou a chave:
- **Repositório de Certificados – Computador local**: você precisa ter acesso de leitura ao certificado que é usado como uma chave mestra da coluna ou ser o administrador do computador.
- **Azure Key Vault** – você precisará das permissões *get* e *list* para selecionar e usar uma chave e da permissão *create* para criar uma chave. Para configurar uma chave mestra de coluna habilitada para enclave, você também precisará da permissão *sign* para gerar uma assinatura dos metadados da chave.
- **Provedor do Repositório de Chaves (CNG)** : a permissão e as credenciais necessárias poderão ser solicitadas quando você usar um repositório de chaves ou uma chave, dependendo do repositório e da configuração do KSP.
- **Provedor de Serviços de Criptografia (CAPI)** : a permissão e as credenciais necessárias poderão ser solicitadas quando você usar um repositório de chaves ou uma chave, dependendo do repositório e da configuração do CSP.

Para obter mais informações, confira [Criar e armazenar chaves mestras de coluna do Always Encrypted](../../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md).

<a name="provisioncek"></a> 
## <a name="provision-column-encryption-keys-with-the-new-column-encryption-key-dialog"></a>Provisionar chaves de criptografia de coluna com a caixa de diálogo Nova Chave de Criptografia de Coluna

A caixa de diálogo **Nova Chave de Criptografia de Coluna** permite gerar uma nova chave de criptografia de coluna, criptografá-la com uma chave mestra da coluna e criar metadados de chave de criptografia de coluna no banco de dados.

1.  Usando o **Pesquisador de Objetos**, navegue até a pasta **Segurança/Chaves Always Encrypted** em seu banco de dados.
2.  Clique com o botão direito do mouse na pasta **Chaves de Criptografia de Coluna** e selecione **Nova Chave de Criptografia de Coluna...** . 
3.  Na caixa de diálogo **Nova Chave de Criptografia da Coluna** , digite o nome do objeto de metadados de chave de criptografia da coluna.
4.  Selecione um objeto de metadados que representa a chave mestra da coluna no banco de dados.
5.  Clique em **OK**. 

Depois que você concluir a caixa de diálogo, o SQL Server Management Studio gerará uma nova chave de criptografia de coluna e, em seguida, recuperará os metadados para a chave mestra de coluna selecionada do banco de dados. Em seguida, o SSMS usará os metadados da chave mestra de coluna para contatar o repositório de chaves que contém a chave mestra de coluna e criptografará a chave de criptografia de coluna. Por fim, o SSMS criará os dados de metadados para a nova criptografia de coluna no banco de dados gerando e emitindo uma instrução [CREATE COLUMN ENCRYPTION KEY (Transact-SQL)](../../../t-sql/statements/create-column-encryption-key-transact-sql.md).

### <a name="permissions-for-provisioning-a-column-encryption-key"></a>Permissões para o provisionamento de uma chave de criptografia de coluna

Você precisará das permissões de banco de dados *ALTER ANY COLUMN ENCRYPTION KEY* e *VIEW ANY COLUMN MASTER KEY DEFINITION* no banco de dados para que a caixa de diálogo crie os metadados da chave de criptografia de coluna e acesse os metadados da chave mestra de coluna.
Para acessar um repositório de chaves e usar a chave mestra da coluna, você pode precisar de permissões no repositório de chaves e/ou na chave:
- **Repositório de Certificados – Computador local**: você precisa ter acesso de leitura ao certificado que é usado como uma chave mestra da coluna ou ser o administrador do computador.
- **Azure Key Vault**: você precisa das permissões *get*, *unwrapKey*, *wrapKey*, *sign* e *verify* no cofre que contém a chave mestra da coluna.
- **Provedor do Repositório de Chaves (CNG)** : a permissão e as credenciais necessárias poderão ser solicitadas quando você usar um repositório de chaves ou uma chave, dependendo do repositório e da configuração do KSP.
- **Provedor de Serviços de Criptografia (CAPI)** : a permissão e as credenciais necessárias poderão ser solicitadas quando você usar um repositório de chaves ou uma chave, dependendo do repositório e da configuração do CSP.

Para obter mais informações, confira [Criar e armazenar chaves mestras de coluna (Always Encrypted)](../../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md).

## <a name="provision-always-encrypted-keys-using-the-always-encrypted-wizard"></a>Provisionar chaves do Always Encrypted usando o Assistente do Always Encrypted

O [Assistente do Always Encrypted](../../../relational-databases/security/encryption/always-encrypted-wizard.md) é uma ferramenta usada para criptografar, descriptografar e criptografar novamente colunas de banco de dados selecionadas. Embora ele possa usar chaves já configuradas, também permite que você gere uma nova chave mestra de coluna e uma nova criptografia de coluna. 

## <a name="next-steps"></a>Next Steps
- [Configurar a criptografia de coluna usando o Assistente do Always Encrypted](always-encrypted-wizard.md)
- [Configurar a criptografia de coluna usando o Always Encrypted com um pacote de DAC](configure-always-encrypted-using-dacpac.md)
- [Girar chaves do Always Encrypted usando o SQL Server Management Studio](rotate-always-encrypted-keys-using-ssms.md)
- [Desenvolver aplicativos usando o Always Encrypted](always-encrypted-client-development.md)
- [Migrar dados para ou de colunas usando Always Encrypted com o Assistente de Importação e Exportação do SQL Server](always-encrypted-migrate-using-import-export-wizard.md)

## <a name="see-also"></a>Consulte Também
- [Always Encrypted](../../../relational-databases/security/encryption/always-encrypted-database-engine.md)
- [Visão geral do gerenciamento de chaves do Always Encrypted](../../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md)
- [Criar e armazenar chaves mestras de coluna para Always Encrypted](../../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md)
- [Configurar o Always Encrypted usando o SQL Server Management Studio](configure-always-encrypted-using-sql-server-management-studio.md)
- [Provisionar chaves do Always Encrypted usando o PowerShell](configure-always-encrypted-keys-using-powershell.md)
- [CREATE COLUMN MASTER KEY (Transact-SQL)](../../../t-sql/statements/create-column-master-key-transact-sql.md)
- [DROP COLUMN MASTER KEY (Transact-SQL)](../../../t-sql/statements/drop-column-master-key-transact-sql.md)
- [CREATE COLUMN ENCRYPTION KEY (Transact-SQL)](../../../t-sql/statements/create-column-encryption-key-transact-sql.md)
- [ALTER COLUMN ENCRYPTION KEY (Transact-SQL)](../../../t-sql/statements/alter-column-encryption-key-transact-sql.md)
- [DROP COLUMN ENCRYPTION KEY (Transact-SQL)](../../../t-sql/statements/drop-column-encryption-key-transact-sql.md) 
- [sys.column_master_keys (Transact-SQL)](../../../relational-databases/system-catalog-views/sys-column-master-keys-transact-sql.md)
- [sys.column_encryption_keys (Transact-SQL)](../../../relational-databases/system-catalog-views/sys-column-encryption-keys-transact-sql.md)
