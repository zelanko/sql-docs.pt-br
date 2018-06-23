---
title: Gerenciamento extensível de chaves usando o Azure Key Vault (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-security
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- EKM, with key vault
- TDE, EKM and key vault
- Extensible Key Management with key vault
- Key Management with key vault
- Transparent Data Encryption, using EKM and key vault
ms.assetid: 3efdc48a-8064-4ea6-a828-3fbf758ef97c
caps.latest.revision: 37
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 41124ce445bf6f008c7aa473d12853a551aa36b2
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36122588"
---
# <a name="extensible-key-management-using-azure-key-vault-sql-server"></a>Gerenciamento extensível de chaves usando o Azure Key Vault (SQL Server)
  O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Connector para [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Cofre de chaves do Azure permite [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] criptografia Aproveite o serviço de Cofre de chaves do Azure como um [gerenciamento extensível de chaves &#40;EKM&#41; ](extensible-key-management-ekm.md) provedor para proteger seu chaves de criptografia.  
  
 Incluso neste tópico:  
  
-   [Usos de EKM](#Uses)  
  
-   [Etapa 1: Configuração do Key Vault para uso pelo SQL Server](#Step1)  
  
-   [Etapa 2: Instalar o conector do SQL Server](#Step2)  
  
-   [Etapa 3: Configurar o SQL Server para usar um provedor EKM para o Cofre de chaves](#Step3)  
  
-   [Exemplo a: criptografia transparente de dados usando uma chave assimétrica do Key Vault](#ExampleA)  
  
-   [Exemplo b: criptografia de Backups usando uma chave assimétrica do Key Vault](#ExampleB)  
  
-   [Exemplo c: criptografia de nível de coluna usando uma chave assimétrica do Key Vault](#ExampleC)  
  
##  <a name="Uses"></a> Usos de EKM  
 Uma organização pode usar criptografia [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para proteger dados confidenciais. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] a criptografia inclui [Transparent Data Encryption &#40;TDE&#41;](transparent-data-encryption.md), [criptografia em nível de coluna](/sql/t-sql/functions/cryptographic-functions-transact-sql) (CLE) e [criptografia de Backup](../../backup-restore/backup-encryption.md). Em todos esses casos, os dados são criptografados usando uma chave de criptografia simétrica de dados. A chave de criptografia simétrica de dados é ainda mais protegida ao criptografar com uma hierarquia de chaves armazenadas em [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Como alternativa, a arquitetura de provedor EKM permite que [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para proteger as chaves de criptografia de dados usando uma chave assimétrica armazenada fora do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] em um provedor criptográfico externo. Usar a arquitetura de provedor EKM acrescenta uma camada adicional de segurança e permite que as organizações separem o gerenciamento de chaves e dados.  
  
 O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Connector para Cofre de chaves do Azure permite que [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Aproveite o serviço de Cofre de chave altamente disponível e a escalonável e de alto desempenho como um provedor EKM para proteção de chave de criptografia. O serviço de Cofre de chaves pode ser usado com [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] instalações em [!INCLUDE[msCoName](../../../includes/msconame-md.md)] máquinas virtuais do Azure e para servidores locais. O serviço de chave de cofre também fornece a opção de usar rigidamente módulos de segurança de hardware (HSM) monitorados e controlados para um nível mais alto de proteção para as chaves de criptografia assimétrica. Para obter mais informações sobre o cofre de chaves, consulte [Cofre de Chaves do Azure](http://go.microsoft.com/fwlink/?LinkId=521401).  
  
 A imagem a seguir resume o fluxo do processo de EKM usando o cofre da chave. Os números de etapa do processo na imagem não devem corresponder aos números de etapa de instalação que seguem a imagem.  
  
 ![EKM do SQL Server usando o Azure Key Vault](../../../database-engine/media/ekm-using-azure-key-vault.png "EKM do SQL Server usando o Azure Key Vault")  
  
##  <a name="Step1"></a> Etapa 1: Configurar o Cofre de chaves para uso pelo SQL Server  
 Use as seguintes etapas para configurar uma chave de cofre para uso com o [!INCLUDE[ssDEnoversion](../../../includes/ssdenoversion-md.md)] para proteção de chave de criptografia. Um cofre já pode estar em uso para a organização. Quando um cofre não existir, o administrador do Azure em sua organização designado para gerenciar chaves de criptografia pode criar um cofre, gerar uma chave assimétrica no cofre e, então, autorizar [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para usar a chave. Familiarize-se com o serviço de cofre de chave consultando [Introdução ao Azure Key Vault](http://go.microsoft.com/fwlink/?LinkId=521402)e a referência de [Cmdlets do PowerShell do Azure Key Vault](http://go.microsoft.com/fwlink/?LinkId=521403) .  
  
> [!IMPORTANT]  
>  Se você tiver várias assinaturas do Azure, você deve usar a assinatura que contém [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
1.  **Crie um cofre:** Crie um cofre usando as instruções na seção **Criar um cofre da chave** da [Introdução ao Azure Key Vault](http://go.microsoft.com/fwlink/?LinkId=521402). Registre o nome do cofre. Este tópico usa **ContosoKeyVault** como o nome da chave de cofre.  
  
2.  **Gere uma chave assimétrica no cofre:** a chave assimétrica no cofre de chave é usada para proteger [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] chaves de criptografia. Somente a parte pública da chave assimétrica nunca deixa o cofre, a parte particular nunca é exportada pelo cofre. Todas as operações de criptografia usando a chave assimétrica são delegadas ao Azure Key Vault e são protegidas pela segurança de chave de cofre.  
  
     Há várias maneiras de gerar uma chave assimétrica e armazená-la no cofre. Externamente, você pode gerar uma chave e importá-la para o cofre como um arquivo .pfx. Ou criar a chave diretamente no cofre usando as APIs do cofre da chave.  
  
     O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] conector requer que as chaves assimétricas sejam RSA de 2048 bits e o nome da chave só pode usar os caracteres "a-z", "A-Z", "0-9", e "-". Neste documento, o nome da chave assimétrica é conhecido como **ContosoMasterKey**. Substitua isso pelo nome exclusivo usado para a chave.  
  
    > [!IMPORTANT]  
    >  Importar a chave assimétrica é altamente recomendável para cenários de produção, pois ela permite que o administrador garanta a chave em um sistema de caução de chaves. Se a chave assimétrica for criada no cofre, ela não pode ser mantida em garantia porque a chave privada nunca pode deixar o cofre. As chaves usadas para proteger dados críticos devem ser mantidas em garantia. A perda de uma chave assimétrica resultará em dados irrecuperáveis permanentemente.  
  
    > [!IMPORTANT]  
    >  O cofre da chave dá suporte a várias versões da mesma chave nomeada. As chaves usadas pelo [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] conector não deve estar com controle de versão ou revertidas. Se o administrador deseja distribuir a chave usada para criptografia [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , uma nova chave com um nome diferente deve ser criada no cofre e usada para criptografar DEK.  
  
     Para obter mais informações sobre como importar uma chave no cofre de chave ou criar uma chave no cofre de chave (não recomendado para um ambiente de produção), consulte a seção **Adicionar uma chave ou um segredo no cofre chave** em [Introdução ao Azure Key Vault](http://go.microsoft.com/fwlink/?LinkId=521402).  
  
3.  **Obtenha as Entidades de Serviço do Active Directory do Azure para uso com o SQL Server:** Quando a empresa se inscreve para um serviço de nuvem da Microsoft, ela recebe um Active Directory do Azure. Criar **entidades de serviço** no Active Directory do Azure para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para uso (para se autenticar para o Azure Active Directory) ao acessar o Cofre de chaves.  
  
    -   Um **entidade de serviço** será necessária para um [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] administrador acesse o cofre durante a configuração de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para usar a criptografia.  
  
    -   Outro **entidade de serviço** será necessária para o [!INCLUDE[ssDEnoversion](../../../includes/ssdenoversion-md.md)] para acessar o cofre para descodificar chaves usadas na [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] criptografia.  
  
     Para obter mais informações sobre como registrar um aplicativo e gerar uma entidade de serviço, consulte a seção **Registrar um aplicativo com o Active Directory do Azure** em [Introdução ao Azure Key Vault](http://go.microsoft.com/fwlink/?LinkId=521402). O processo de registro retorna uma **ID do aplicativo** (também conhecida como uma **ID DO CLIENTE**) e uma **Chave de autenticação** (também conhecida como um **Segredo**) para cada **Entidade de serviço**do Active Directory do Azure. Quando usado na `CREATE CREDENTIAL` instrução, o hífen deve ser removido do **ID do cliente**. Registre isso para uso nos scripts abaixo:  
  
    -   **Entidade de serviço** para um logon **sysadmin** : **CLIENTID_sysadmin_login** e **SECRET_sysadmin_login**  
  
    -   **Entidade de serviço** para o [!INCLUDE[ssDEnoversion](../../../includes/ssdenoversion-md.md)]: **CLIENTID_DBEngine** e **SECRET_DBEngine**.  
  
4.  **Conceder permissão para as entidades de serviço acessar o Cofre de chaves:** ambos o **CLIENTID_sysadmin_login** e **CLIENTID_DBEngineService entidades** exigem o **obter** , **lista**, **wrapKey**, e **unwrapKey** permissões no cofre de chaves. Se você pretende criar chaves por meio de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] também precisará conceder a **criar** permissão no cofre de chaves.  
  
    > [!IMPORTANT]  
    >  Os usuários devem ter pelo menos as operações **wrapKey** e **unwrapKey** para o cofre da chave.  
  
     Para obter mais informações sobre como conceder permissões para o cofre, consulte a seção **Autorizar o uso pelo aplicativo da chave ou segredo** em [Introdução ao Azure Key Vault](http://go.microsoft.com/fwlink/?LinkId=521402).  
  
     Links para a documentação do Azure Key Vault  
  
    -   [O que é o Azure Key Vault?](http://go.microsoft.com/fwlink/?LinkId=521401)  
  
    -   [Introdução ao Azure Key Vault](http://go.microsoft.com/fwlink/?LinkId=521402)  
  
    -   Referência dos [Cmdlets do Cofre de Chaves do Azure](http://go.microsoft.com/fwlink/?LinkId=521403) do PowerShell  
  
##  <a name="Step2"></a> Etapa 2: Instalar o conector do SQL Server  
 O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] conector é baixado e instalado pelo administrador do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] computador. O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] está disponível como um download do conector de [Microsoft Download Center](http://go.microsoft.com/fwlink/p/?LinkId=521700).  Procure **SQL Server Connector para Microsoft Azure Key Vault**, examine os detalhes, requisitos de sistema e instruções de instalação e escolha baixar o conector e iniciar a instalação usando **Executar**. Examine e aceite a licença e continue.  
  
 Por padrão, o conector é instalado em **C:\Program Files\SQL Server Connector for Microsoft Azure Key Vault**. Esse local pode ser alterado durante a instalação. (Se alterado, ajuste os scripts a seguir).  
  
 Ao concluir a instalação, os seguintes itens são instalados no computador:  
  
-   **Microsoft.AzureKeyVaultService.EKM.dll**: Este é o provedor EKM criptográfico que precisa ser registrado com DLL [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] usando a instrução CREATE CRYPTOGRAPHIC PROVIDER.  
  
-   **Azure Key Vault SQL Server Connector**: Isso é um serviço Windows que permite que o provedor EKM criptográfico se comunique com o cofre de chave.  
  
 O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] instalação do Connector também permite que você baixe opcionalmente os scripts de exemplo para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] criptografia.  
  
##  <a name="Step3"></a> Etapa 3: Configurar o SQL Server para usar um provedor EKM para o Cofre de chaves  
  
###  <a name="Permissions"></a> Permissões  
 Para concluir esse processo todo é necessária a permissão CONTROL SERVER ou associação na função de servidor fixa **sysadmin** . Ações específicas requerem as seguintes permissões:  
  
-   Para criar um provedor criptográfico, é necessária a permissão CONTROL SERVER ou associação na função de servidor fixa **sysadmin** .  
  
-   Para alterar uma opção de configuração e executar a instrução RECONFIGURE, você deve ter a permissão em nível de servidor ALTER SETTINGS. A permissão ALTER SETTINGS é implicitamente mantida pelas funções de servidor fixas **sysadmin** e **serveradmin** .  
  
-   Para criar uma credencial, é necessária a permissão ALTER ANY CREDENTIAL.  
  
-   Para adicionar uma credencial para um logon, é necessária a permissão ALTER ANY LOGIN.  
  
-   Para criar uma chave assimétrica, é necessária a permissão CREATE ASYMMETRIC KEY.  
  
###  <a name="TsqlProcedure"></a> Para configurar o SQL Server para usar um provedor criptográfico  
  
1.  Configurar o [!INCLUDE[ssDE](../../../includes/ssde-md.md)] para usar EKM e registrar (criar) o provedor criptográfico com [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
    ```  
    -- Enable advanced options.  
    USE master;  
    GO  
  
    sp_configure 'show advanced options', 1 ;  
    GO  
    RECONFIGURE ;  
    GO  
    -- Enable EKM provider  
    sp_configure 'EKM provider enabled', 1 ;  
    GO  
    RECONFIGURE ;  
    GO  
  
    -- Create a cryptographic provider, using the SQL Server Connector  
    -- which is an EKM provider for the Azure Key Vault. This example uses   
    -- the name AzureKeyVault_EKM_Prov.  
  
    CREATE CRYPTOGRAPHIC PROVIDER AzureKeyVault_EKM_Prov   
    FROM FILE = 'C:\Program Files\SQL Server Connector for Microsoft Azure Key Vault\Microsoft.AzureKeyVaultService.EKM.dll';  
    GO   
    ```  
  
2.  Instalação uma [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] de credencial para um [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] logon de administrador para usar o Cofre de chaves para instalar e gerenciar [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] cenários de criptografia.  
  
    > [!IMPORTANT]  
    >  O **identidade** argumento de `CREATE CREDENTIAL` requer o nome do Cofre de chaves. O **segredo** argumento de `CREATE CREDENTIAL` requer o  *\<ID do cliente >* (sem hifens) e  *\<segredo >* a serem passados juntos sem um espaço entre eles.  
  
     No exemplo a seguir, a **ID do cliente** (`EF5C8E09-4D2A-4A76-9998-D93440D8115D`) não tem hifens e foi inserida como a cadeia de caracteres `EF5C8E094D2A4A769998D93440D8115D` , e **Secret** é representado pela cadeia de caracteres *SECRET_sysadmin_login*.  
  
    ```  
    USE master;  
    CREATE CREDENTIAL sysadmin_ekm_cred   
        WITH IDENTITY = 'ContosoKeyVault',   
        SECRET = 'EF5C8E094D2A4A769998D93440D8115DSECRET_sysadmin_login'   
    FOR CRYPTOGRAPHIC PROVIDER AzureKeyVault_EKM_Prov ;  
  
    -- Add the credential to the SQL Server administrators domain login   
    ALTER LOGIN [<domain>/<login>]  
    ADD CREDENTIAL sysadmin_ekm_cred;  
    ```  
  
     Para obter um exemplo de uso de variáveis para o `CREATE CREDENTIAL` argumentos e remover programaticamente os hifens da ID do cliente, consulte [CREATE CREDENTIAL &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-credential-transact-sql).  
  
3.  Se você importou uma chave assimétrica, conforme descrito anteriormente na etapa 1, seção 3, abra a chave fornecendo o nome da chave no exemplo a seguir.  
  
    ```  
    CREATE ASYMMETRIC KEY CONTOSO_KEY   
    FROM PROVIDER [AzureKeyVault_EKM_Prov]  
    WITH PROVIDER_KEY_NAME = 'ContosoMasterKey',  
    CREATION_DISPOSITION = OPEN_EXISTING;  
    ```  
  
     Embora não seja recomendado para produção (porque não é possível exportar a chave), é possível criar uma chave assimétrica diretamente no cofre do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Se uma chave não foi importada anteriormente, crie uma chave assimétrica no cofre de chave para teste usando o script a seguir. Execute o script usando um logon fornecido com a credencial **sysadmin_ekm_cred** .  
  
    ```  
    CREATE ASYMMETRIC KEY CONTOSO_KEY   
    FROM PROVIDER [AzureKeyVault_EKM_Prov]  
    WITH ALGORITHM = RSA_2048,  
    PROVIDER_KEY_NAME = 'ContosoMasterKey';  
    ```  
  
> [!TIP]  
>  Os usuários receberão o erro **não é possível exportar a chave pública do provedor. Código de erro do provedor: 2053.** deve verificar suas permissões **get**, **list**, **wrapKey**e **unwrapKey** no cofre da chave.  
  
 Para obter mais informações, consulte o seguinte:  
  
-   [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)  
  
-   [CREATE CRYPTOGRAPHIC PROVIDER &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-cryptographic-provider-transact-sql)  
  
-   [CREATE CREDENTIAL &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-credential-transact-sql)  
  
-   [CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-asymmetric-key-transact-sql)  
  
-   [CREATE LOGIN &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-login-transact-sql)  
  
-   [ALTER LOGIN &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-login-transact-sql)  
  
## <a name="examples"></a>Exemplos  
  
###  <a name="ExampleA"></a> Exemplo a: criptografia transparente de dados usando uma chave assimétrica do Key Vault  
 Depois de concluir as etapas acima, crie uma credencial e um logon, crie uma chave de criptografia do banco de dados protegida pela chave assimétrica no cofre de chave. Use a chave de criptografia do banco de dados para criptografar um banco de dados com TDE.  
  
 Criptografar um banco de dados requer permissão CONTROL no banco de dados.  
  
##### <a name="to-enable-tde-using-ekm-and-the-key-vault"></a>Habilitar TDE usando EKM e a chave de cofre  
  
1.  Crie uma credencial [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para o [!INCLUDE[ssDE](../../../includes/ssde-md.md)] para usar quando acessar o cofre chave EKM durante o carregamento de banco de dados.  
  
    > [!IMPORTANT]  
    >  O **identidade** argumento de `CREATE CREDENTIAL` requer o nome do Cofre de chaves. O **segredo** argumento de `CREATE CREDENTIAL` requer o  *\<ID do cliente >* (sem hifens) e  *\<segredo >* a serem passados juntos sem um espaço entre eles.  
  
     No exemplo a seguir, a **ID do cliente** (`EF5C8E09-4D2A-4A76-9998-D93440D8115D`) não tem hifens e foi inserida como a cadeia de caracteres `EF5C8E094D2A4A769998D93440D8115D` , e **Secret** é representado pela cadeia de caracteres *SECRET_DBEngine*.  
  
    ```  
    USE master;  
    CREATE CREDENTIAL Azure_EKM_TDE_cred   
        WITH IDENTITY = 'ContosoKeyVault',   
        SECRET = 'EF5C8E094D2A4A769998D93440D8115DSECRET_DBEngine'   
        FOR CRYPTOGRAPHIC PROVIDER AzureKeyVault_EKM_Prov ;  
    ```  
  
2.  Criar um logon [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] a ser usado pelo [!INCLUDE[ssDE](../../../includes/ssde-md.md)] para TDE e adicione a credencial a ele. Este exemplo usa a chave assimétrica CONTOSO_KEY armazenada no cofre de chave, que foi importada ou criada anteriormente para o banco de dados mestre, como descrito na [Etapa 3, seção 3](#Step3) acima.  
  
    ```  
    USE master;  
    -- Create a SQL Server login associated with the asymmetric key   
    -- for the Database engine to use when it loads a database   
    -- encrypted by TDE.  
    CREATE LOGIN TDE_Login   
    FROM ASYMMETRIC KEY CONTOSO_KEY;  
    GO   
  
    -- Alter the TDE Login to add the credential for use by the   
    -- Database Engine to access the key vault  
    ALTER LOGIN TDE_Login   
    ADD CREDENTIAL Azure_EKM_TDE_cred ;  
    GO  
    ```  
  
3.  Crie a chave de criptografia do banco de dados (DEK) que será usada para a TDE. A DEK pode ser criada usando qualquer algoritmo com suporte do SQL Server ou o comprimento da chave. A DEK estará protegida pela chave assimétrica no cofre de chave.  
  
     Este exemplo usa a chave assimétrica CONTOSO_KEY armazenada no cofre de chave, que foi importada ou criada anteriormente, como descrito na [Etapa 3, seção 3](#Step3) acima.  
  
    ```  
    USE ContosoDatabase;  
    GO  
  
    CREATE DATABASE ENCRYPTION KEY   
    WITH ALGORITHM = AES_128   
    ENCRYPTION BY SERVER ASYMMETRIC KEY CONTOSO_KEY;  
    GO  
  
    -- Alter the database to enable transparent data encryption.  
    ALTER DATABASE ContosoDatabase   
    SET ENCRYPTION ON ;  
    GO  
    ```  
  
     Para obter mais informações, consulte o seguinte:  
  
    -   [CREATE DATABASE ENCRYPTION KEY &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-database-encryption-key-transact-sql)  
  
    -   [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql)  
  
###  <a name="ExampleB"></a> Exemplo b: criptografia de Backups usando uma chave assimétrica do Key Vault  
 Há suporte para backups criptografados começando com [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)]. O exemplo a seguir cria e restaura um backup criptografado e uma chave de criptografia de dados protegida pela chave assimétrica no cofre de chave.  
  
```  
USE master;  
BACKUP DATABASE [DATABASE_TO_BACKUP]  
TO DISK = N'[PATH TO BACKUP FILE]'   
WITH FORMAT, INIT, SKIP, NOREWIND, NOUNLOAD,   
ENCRYPTION(ALGORITHM = AES_256, SERVER ASYMMETRIC KEY = [CONTOSO_KEY]);  
GO  
```  
  
 Código de restauração de exemplo.  
  
```  
RESTORE DATABASE [DATABASE_TO_BACKUP]  
FROM DISK = N'[PATH TO BACKUP FILE]' WITH FILE = 1, NOUNLOAD, REPLACE;  
GO  
```  
  
 Para obter mais informações sobre opções de backup, consulte [BACKUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-transact-sql).  
  
###  <a name="ExampleC"></a> Exemplo c: criptografia de nível de coluna usando uma chave assimétrica do Key Vault  
 O exemplo a seguir cria uma chave simétrica protegida pela chave assimétrica no cofre de chave. Em seguida, a chave simétrica é usada para criptografar dados no banco de dados.  
  
 Este exemplo usa a chave assimétrica CONTOSO_KEY armazenada no cofre de chave, que foi importada ou criada anteriormente, como descrito na [Etapa 3, seção 3](#Step3) acima. Para usar essa chave assimétrica no banco de dados `ContosoDatabase` , você deve executar a instrução CREATE ASYMMETRIC KEY novamente, para fornecer ao banco de dados `ContosoDatabase` uma referência para a chave.  
  
```  
USE [ContosoDatabase];  
GO  
  
-- Create a reference to the key in the key vault  
CREATE ASYMMETRIC KEY CONTOSO_KEY   
FROM PROVIDER [AzureKeyVault_EKM_Prov]  
WITH PROVIDER_KEY_NAME = 'ContosoMasterKey',  
CREATION_DISPOSITION = OPEN_EXISTING;  
  
-- Create the data encryption key.  
-- The data encryption key can be created using any SQL Server   
-- supported algorithm or key length.  
-- The DEK will be protected by the asymmetric key in the key vault  
  
CREATE SYMMETRIC KEY DATA_ENCRYPTION_KEY  
    WITH ALGORITHM=AES_256  
    ENCRYPTION BY ASYMMETRIC KEY CONTOSO_KEY;  
  
DECLARE @DATA VARBINARY(MAX);  
  
--Open the symmetric key for use in this session  
OPEN SYMMETRIC KEY DATA_ENCRYPTION_KEY   
DECRYPTION BY ASYMMETRIC KEY CONTOSO_KEY;  
  
--Encrypt syntax  
SELECT @DATA = ENCRYPTBYKEY(KEY_GUID('DATA_ENCRYPTION_KEY'), CONVERT(VARBINARY,'Plain text data to encrypt'));  
  
-- Decrypt syntax  
SELECT CONVERT(VARCHAR, DECRYPTBYKEY(@DATA));  
  
--Close the symmetric key  
CLOSE SYMMETRIC KEY DATA_ENCRYPTION_KEY;  
```  
  
## <a name="see-also"></a>Consulte também  
 [CREATE CRYPTOGRAPHIC PROVIDER &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-cryptographic-provider-transact-sql)   
 [CREATE CREDENTIAL &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-credential-transact-sql)   
 [CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-asymmetric-key-transact-sql)   
 [CREATE SYMMETRIC KEY &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-symmetric-key-transact-sql)   
 [Gerenciamento Extensível de Chaves &#40;EKM&#41;](extensible-key-management-ekm.md)   
 [Habilitar TDE usando EKM](enable-tde-on-sql-server-using-ekm.md)   
 [Criptografia de backup](../../backup-restore/backup-encryption.md)   
 [Criar um backup criptografado](../../backup-restore/create-an-encrypted-backup.md)  
  
  
