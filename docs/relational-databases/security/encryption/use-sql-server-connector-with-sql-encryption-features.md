---
title: Usar o Conector do SQL Server com recursos de criptografia do SQL | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: vanto
ms.suite: sql
ms.technology: security
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Connector, using
- EKM, with SQL Server Connector
ms.assetid: 58fc869e-00f1-4d7c-a49b-c0136c9add89
caps.latest.revision: 14
author: aliceku
ms.author: aliceku
manager: craigg
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: 57294027687687f72fd7ae2841a25c0e668de43a
ms.sourcegitcommit: 3762dd447ca4bb449eda8476e72f393db0851b38
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/18/2018
ms.locfileid: "46013841"
---
# <a name="use-sql-server-connector-with-sql-encryption-features"></a>Use SQL Server Connector with SQL Encryption Features (Usar o Conector do SQL Server com recursos de criptografia do SQL)
[!INCLUDE[appliesto-xx-asdb-xxxx-xxx-md](../../../includes/appliesto-xx-asdb-xxxx-xxx-md.md)]
  As atividades de criptografia do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] comuns do que usam uma chave assimétrica protegidas pelo Cofre de Chaves do Azure incluem três áreas a seguir.  
  
-   Transparent Data Encryption usando uma chave assimétrica do Cofre de Chaves do Azure  
  
-   Criptografia de backups usando uma chave assimétrica do Key Vault  
  
-   Criptografia de nível de coluna usando uma chave assimétrica do Key Vault  
  
 Concluir as partes I a IV do tópico [Setup Steps for Extensible Key Management Using the Azure Key Vault](../../../relational-databases/security/encryption/setup-steps-for-extensible-key-management-using-the-azure-key-vault.md)(Etapas de instalação para o gerenciamento extensível de chaves usando o Cofre de Chaves do Azure), antes continuar com as etapas nesse tópico.  
 
> [!NOTE]  
>  Versões 1.0.0.440 e anteriores foram substituídas e não têm mais suporte em ambientes de produção. Atualize para a versão 1.0.1.0 ou posterior visitando o [Centro de Download da Microsoft](https://www.microsoft.com/download/details.aspx?id=45344) e usando as instruções da página [Manutenção e solução de problemas do Conector do SQL Server](../../../relational-databases/security/encryption/sql-server-connector-maintenance-troubleshooting.md) em "Atualização do Conector do SQL Server".  
  
## <a name="transparent-data-encryption-by-using-an-asymmetric-key-from-azure-key-vault"></a>Transparent Data Encryption usando uma chave assimétrica do Cofre de Chaves do Azure  
 Depois de concluir as Partes I a IV do tópico Setup Steps for Extensible Key Management Using the Azure Key Vault (Etapas de instalação para o gerenciamento extensível de chaves usando o Cofre de Chaves do Azure), use a chave de Cofre de Chaves do Azure para criptografar a chave de criptografia do banco de dados usando TDE.  
Você precisará criar uma credencial e um logon e criar uma chave de criptografia do banco de dados que fará criptografia dos dados e logs no banco de dados. Para criptografar um banco de dados a permissão **CONTROL** é exigida no banco de dados. O gráfico a seguir mostra a hierarquia da chave de criptografia ao usar o Cofre de Chaves do Azure.  
  
 ![ekm&#45;key&#45;hierarchy&#45;with&#45;akv](../../../relational-databases/security/encryption/media/ekm-key-hierarchy-with-akv.png "ekm-key-hierarchy-with-akv")  
  
1.  **Criar uma credencial do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para uso pelo mecanismo do banco de dados para TDE**  
  
     O mecanismo de banco de dados usa a credencial para acessar o Cofre de Chaves durante o carregamento de banco de dados. É recomendável criar outra **ID do cliente** e **Segredo** do Azure Active Directory na Parte I para o [!INCLUDE[ssDE](../../../includes/ssde-md.md)], para limitar as permissões de Cofre de Chaves que são concedidas.  
  
     Modificar o script [!INCLUDE[tsql](../../../includes/tsql-md.md)] abaixo das seguintes maneiras:  
  
    -   Edite o argumento `IDENTITY` (`ContosoDevKeyVault`) para apontar para o Cofre de Chaves do Azure.
        - Se você estiver usando o **Azure público**, substitua o argumento `IDENTITY` pelo nome do seu Cofre de Chaves do Azure da Parte II.
        - Se você estiver usando uma **nuvem privada do Azure** (por ex:. Azure Governamental, Azure China ou Azure Alemanha), substitua o argumento `IDENTITY` pelo URI do Cofre retornado na Parte II, etapa 3. Não inclua “https://” no URI do Cofre.   
  
    -   Substitua a primeira parte do argumento do `SECRET` pela **ID do Cliente** do Azure Active Directory da Parte I. Neste exemplo, a **ID do Cliente** é `EF5C8E094D2A4A769998D93440D8115D`.  
  
        > [!IMPORTANT]  
        >  É necessário remover os hifens da **ID do Cliente**.  
  
    -   Conclua a segunda parte do argumento `SECRET` com o **Segredo do Cliente** da Parte I. Neste exemplo, o **Segredo do Cliente** da Parte 1 é `Replace-With-AAD-Client-Secret`. A cadeia de caracteres final do argumento `SECRET` será uma sequência longa de letras e números, *sem hifens*.  
  
    ```sql  
    USE master;  
    CREATE CREDENTIAL Azure_EKM_TDE_cred   
        WITH IDENTITY = 'ContosoDevKeyVault', -- for public Azure
        -- WITH IDENTITY = 'ContosoDevKeyVault.vault.usgovcloudapi.net', -- for Azure Government
        -- WITH IDENTITY = 'ContosoDevKeyVault.vault.azure.cn', -- for Azure China
        -- WITH IDENTITY = 'ContosoDevKeyVault.vault.microsoftazure.de', -- for Azure Germany   
        SECRET = 'EF5C8E094D2A4A769998D93440D8115DReplace-With-AAD-Client-Secret'   
    FOR CRYPTOGRAPHIC PROVIDER AzureKeyVault_EKM_Prov;  
    ```  
  
2.  **Criar um logon do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para o [!INCLUDE[ssDE](../../../includes/ssde-md.md)] para TDE**  
  
     Crie um logon do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e adicione a credencial da Etapa 1 para ele. Esse exemplo do [!INCLUDE[tsql](../../../includes/tsql-md.md)] usa a mesma chave que foi importada anteriormente.  
  
    ```sql  
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
  
3.  **Criar a DEK (Chave de Criptografia de Banco de Dados)**  
  
     A DEK criptografará os arquivos de log e de dados na instância do banco de dados e, por sua vez, será criptografada pela chave assimétrica do Cofre de Chaves do Azure. A DEK pode ser criada usando qualquer algoritmo com suporte do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ou o comprimento da chave.  
  
    ```sql  
    USE ContosoDatabase;  
    GO  
  
    CREATE DATABASE ENCRYPTION KEY   
    WITH ALGORITHM = AES_256   
    ENCRYPTION BY SERVER ASYMMETRIC KEY CONTOSO_KEY;  
    GO  
    ```  
  
4.  **Ativar TDE**  
  
    ```sql  
    -- Alter the database to enable transparent data encryption.  
    ALTER DATABASE ContosoDatabase   
    SET ENCRYPTION ON;  
    GO  
    ```  
  
     Usando [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)], verifique se a TDE foi ativada conectando-se ao banco de dados com o Pesquisador de Objetos. Clique com o botão direito do mouse no banco de dados, aponte para **Tarefas**e clique em **Gerenciar Criptografia de Banco de Dados**.  
  
     ![ekm&#45;tde&#45;object&#45;explorer](../../../relational-databases/security/encryption/media/ekm-tde-object-explorer.png "ekm-tde-object-explorer")  
  
     Na caixa de diálogo **Gerenciar Criptografia de Banco de Dados** , confirme se a TDE está ativada e se a chave assimétrica está criptografando a DEK.  
  
     ![ekm&#45;tde&#45;dialog&#45;box](../../../relational-databases/security/encryption/media/ekm-tde-dialog-box.png "ekm-tde-dialog-box")  
  
     Como alternativa, você pode executar o seguinte script [!INCLUDE[tsql](../../../includes/tsql-md.md)] . Um estado de criptografia de 3 indica um banco de dados criptografado.  
  
    ```sql  
    USE MASTER  
    SELECT * FROM sys.asymmetric_keys  
  
    -- Check which databases are encrypted using TDE  
    SELECT d.name, dek.encryption_state   
    FROM sys.dm_database_encryption_keys AS dek  
    JOIN sys.databases AS d  
         ON dek.database_id = d.database_id;  
    ```  
  
    > [!NOTE]  
    >  O banco de dados do `tempdb` é criptografado automaticamente sempre que qualquer banco de dados habilita TDE.  
  
## <a name="encrypting-backups-by-using-an-asymmetric-key-from-the-key-vault"></a>Criptografia de backups usando uma chave assimétrica do Key Vault  
 Há suporte para backups criptografados começando com [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)]. O exemplo a seguir cria e restaura um backup criptografado e uma chave de criptografia de dados protegida pela chave assimétrica no cofre de chave.  
O [!INCLUDE[ssDE](../../../includes/ssde-md.md)] precisa de credenciais ao acessar o Cofre de Chaves durante o carregamento de banco de dados. É recomendável criar outra ID do cliente e Segredo do Azure Active Directory na Parte I para o Mecanismo de Banco de Dados, para limitar as permissões de Cofre de Chaves que são concedidas.  
  
1.  **Criar uma credencial do SQL Server para o Mecanismo de Banco de Dados a ser usado para Criptografia de Backup**  
  
     Modificar o script [!INCLUDE[tsql](../../../includes/tsql-md.md)] abaixo das seguintes maneiras:  
  
    -   Edite o argumento `IDENTITY` (`ContosoDevKeyVault`) para apontar para o Cofre de Chaves do Azure.
        - Se você estiver usando o **Azure público**, substitua o argumento `IDENTITY` pelo nome do seu Cofre de Chaves do Azure da Parte II.
        - Se você estiver usando uma **nuvem privada do Azure** (por ex:. Azure Governamental, Azure China ou Azure Alemanha), substitua o argumento `IDENTITY` pelo URI do Cofre retornado na Parte II, etapa 3. Não inclua “https://” no URI do Cofre.    
  
    -   Substitua a primeira parte do argumento do `SECRET` pela **ID do Cliente** do Azure Active Directory da Parte I. Neste exemplo, a **ID do Cliente** é `EF5C8E094D2A4A769998D93440D8115D`.  
  
        > [!IMPORTANT]  
        >  É necessário remover os hifens da **ID do Cliente**.  
  
    -   Conclua a segunda parte do argumento `SECRET` com o **Segredo do Cliente** da Parte I. Neste exemplo, o **Segredo do Cliente** da Parte I é `Replace-With-AAD-Client-Secret`. A cadeia de caracteres final do argumento `SECRET` será uma sequência longa de letras e números, *sem hifens*.   
  
        ```sql  
        USE master;  
  
        CREATE CREDENTIAL Azure_EKM_Backup_cred   
            WITH IDENTITY = 'ContosoDevKeyVault', -- for public Azure
            -- WITH IDENTITY = 'ContosoDevKeyVault.vault.usgovcloudapi.net', -- for Azure Government
            -- WITH IDENTITY = 'ContosoDevKeyVault.vault.azure.cn', -- for Azure China
            -- WITH IDENTITY = 'ContosoDevKeyVault.vault.microsoftazure.de', -- for Azure Germany   
            SECRET = 'EF5C8E094D2A4A769998D93440D8115DReplace-With-AAD-Client-Secret'   
        FOR CRYPTOGRAPHIC PROVIDER AzureKeyVault_EKM_Prov;    
        ```  
  
2.  **Criar um logon do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para o [!INCLUDE[ssDE](../../../includes/ssde-md.md)] para Criptografia de Backup**  
  
     Crie um logon do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] a ser usado pelo [!INCLUDE[ssDE](../../../includes/ssde-md.md)]e para backups de criptografia e adicione a ele credencial da Etapa 1. Esse exemplo do [!INCLUDE[tsql](../../../includes/tsql-md.md)] usa a mesma chave que foi importada anteriormente.  
  
    > [!IMPORTANT]  
    >  Você não poderá usar a mesma chave assimétrica para criptografia de backup se você já tiver usado essa chave para a TDE (o exemplo acima) ou criptografia de nível de coluna (exemplo abaixo).  
  
     Este exemplo usa a chave assimétrica do `CONTOSO_KEY_BACKUP` armazenada no cofre de chaves, que pode ser importada ou criada anteriormente para o banco de dados mestre, como descrito anteriormente na Parte IV, Etapa 5.  
  
    ```sql  
    USE master;  
  
    -- Create a SQL Server login associated with the asymmetric key   
    -- for the Database engine to use when it is encrypting the backup.  
    CREATE LOGIN Backup_Login   
    FROM ASYMMETRIC KEY CONTOSO_KEY_BACKUP;  
    GO   
  
    -- Alter the Encrypted Backup Login to add the credential for use by   
    -- the Database Engine to access the key vault  
    ALTER LOGIN Backup_Login   
    ADD CREDENTIAL Azure_EKM_Backup_cred ;  
    GO  
    ```  
  
3.  **Backup de banco de dados**  
  
     Faça backup do banco de dados especificando a criptografia com a chave assimétrica armazenada no cofre de chaves.
     
     No exemplo abaixo, observe que, se o banco de dados já foi criptografado com TDE e a chave assimétrica `CONTOSO_KEY_BACKUP` é diferente da chave assimétrica TDE, o backup será criptografado tanto pela chave assimétrica TDE quanto por `CONTOSO_KEY_BACKUP`. A instância de destino [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] precisará das duas chaves para descriptografar o backup.
  
    ```sql  
    USE master;  
  
    BACKUP DATABASE [DATABASE_TO_BACKUP]  
    TO DISK = N'[PATH TO BACKUP FILE]'   
    WITH FORMAT, INIT, SKIP, NOREWIND, NOUNLOAD,   
    ENCRYPTION(ALGORITHM = AES_256,   
    SERVER ASYMMETRIC KEY = [CONTOSO_KEY_BACKUP]);  
    GO  
    ```  
  
4.  **Restaurar o banco de dados**  
    
    Para restaurar um backup de banco de dados criptografado com TDE, a instância de destino [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] primeiro deve ter uma cópia da chave de cofre de chaves assimétrica usada para criptografia. Isso poderia ser feito assim:  
    
    - Se a chave assimétrica original usada para TDE não estiver mais no cofre de chaves, restaure o backup da chave de cofre de chaves ou importe novamente a chave de uma HSM local. **Importante:** para que a impressão digital da chave corresponda a impressão digital registrada no backup do banco de dados, a chave deve ser nomeada com o **mesmo nome de chave do cofre de chaves** que recebeu originalmente.
    
    - Aplique as etapas 1 e 2 na instância de destino [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].
    
    - Uma vez que a instância de destino [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tiver acesso às chaves assimétricas usadas para criptografar o backup, restaure o banco de dados no servidor.
    
     Código de restauração de exemplo:  
  
    ```sql  
    RESTORE DATABASE [DATABASE_TO_BACKUP]  
    FROM DISK = N'[PATH TO BACKUP FILE]'   
        WITH FILE = 1, NOUNLOAD, REPLACE;  
    GO  
    ```  
  
     Para obter mais informações sobre opções de backup, consulte [BACKUP (Transact-SQL)](../../../t-sql/statements/backup-transact-sql.md).  
  
## <a name="column-level-encryption-by-using-an-asymmetric-key-from-the-key-vault"></a>Criptografia de nível de coluna usando uma chave assimétrica do Key Vault  
 O exemplo a seguir cria uma chave simétrica protegida pela chave assimétrica no cofre de chave. Em seguida, a chave simétrica é usada para criptografar dados no banco de dados.  
  
> [!IMPORTANT]  
>  Você não poderá usar a mesma chave assimétrica para criptografia de backup se você já tiver usado essa chave para TDE ou criptografia de backup (nos exemplos anteriores).  
  
 Este exemplo usa a chave assimétrica do `CONTOSO_KEY_COLUMNS` armazenada no cofre de chaves, que pode ser importada ou criada anteriormente, como descrito na Etapa 3, seção 3 do [Setup Steps for Extensible Key Management Using the Azure Key Vault](../../../relational-databases/security/encryption/setup-steps-for-extensible-key-management-using-the-azure-key-vault.md)(Etapas de instalação para o gerenciamento extensível de chaves usando o Cofre de Chaves do Azure). Para usar essa chave assimétrica no banco de dados `ContosoDatabase` , você deve executar a instrução `CREATE ASYMMETRIC KEY` novamente, para fornecer ao banco de dados `ContosoDatabase` uma referência para a chave.  
  
```sql  
USE [ContosoDatabase];  
GO  
  
-- Create a reference to the key in the key vault  
CREATE ASYMMETRIC KEY CONTOSO_KEY_COLUMNS   
FROM PROVIDER [AzureKeyVault_EKM_Prov]  
WITH PROVIDER_KEY_NAME = 'ContosoDevRSAKey2',  
CREATION_DISPOSITION = OPEN_EXISTING;  
  
-- Create the data encryption key.  
-- The data encryption key can be created using any SQL Server   
-- supported algorithm or key length.  
-- The DEK will be protected by the asymmetric key in the key vault  
  
CREATE SYMMETRIC KEY DATA_ENCRYPTION_KEY  
    WITH ALGORITHM=AES_256  
    ENCRYPTION BY ASYMMETRIC KEY CONTOSO_KEY_COLUMNS;  
  
DECLARE @DATA VARBINARY(MAX);  
  
--Open the symmetric key for use in this session  
OPEN SYMMETRIC KEY DATA_ENCRYPTION_KEY   
DECRYPTION BY ASYMMETRIC KEY CONTOSO_KEY_COLUMNS;  
  
--Encrypt syntax  
SELECT @DATA = ENCRYPTBYKEY  
    (  
    KEY_GUID('DATA_ENCRYPTION_KEY'),   
    CONVERT(VARBINARY,'Plain text data to encrypt')  
    );  
  
-- Decrypt syntax  
SELECT CONVERT(VARCHAR, DECRYPTBYKEY(@DATA));  
  
--Close the symmetric key  
CLOSE SYMMETRIC KEY DATA_ENCRYPTION_KEY;  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Setup Steps for Extensible Key Management Using the Azure Key Vault](../../../relational-databases/security/encryption/setup-steps-for-extensible-key-management-using-the-azure-key-vault.md)   
 [Gerenciamento extensível de chaves usando o Azure Key Vault](../../../relational-databases/security/encryption/extensible-key-management-using-azure-key-vault-sql-server.md)  
 [Opção de configuração de servidor EKM provider enabled](../../../database-engine/configure-windows/ekm-provider-enabled-server-configuration-option.md)   
 [Manutenção e solução de problemas do conector do SQL Server](../../../relational-databases/security/encryption/sql-server-connector-maintenance-troubleshooting.md)  
  
  
