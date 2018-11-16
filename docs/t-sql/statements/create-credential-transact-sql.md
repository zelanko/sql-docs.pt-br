---
title: CREATE CREDENTIAL (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/07/2018
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- CREDENTIAL_TSQL
- SQL13.SWB.CREDENTIAL.GENERAL.F1
- CREATE CREDENTIAL
- CREATE_CREDENTIAL_TSQL
- CREDENTIAL
dev_langs:
- TSQL
helpviewer_keywords:
- SECRET clause
- authentication [SQL Server], credentials
- CREATE CREDENTIAL statement
- credentials [SQL Server], CREATE CREDENTIAL statement
ms.assetid: d5e9ae69-41d9-4e46-b13d-404b88a32d9d
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: aa3decb1f8abd44dc9e35f75de63ebae24a885e9
ms.sourcegitcommit: 50b60ea99551b688caf0aa2d897029b95e5c01f3
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/15/2018
ms.locfileid: "51704014"
---
# <a name="create-credential-transact-sql"></a>CREATE CREDENTIAL (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md)]

  Cria uma credencial no nível do servidor. Uma credencial é um registro que contém as informações de autenticação necessárias para se conectar a um recurso fora do SQL Server. A maioria das credenciais inclui um usuário e uma senha do Windows. Por exemplo, salvar um backup de banco de dados em um local pode exigir que o SQL Server forneça credenciais especiais para acessar esse local. Para obter mais informações, consulte [Credenciais (Mecanismo de Banco de Dados)](../../relational-databases/security/authentication-access/credentials-database-engine.md).

> [!NOTE]  
>  Para tornar a credencial no nível do banco de dados, use [CREATE DATABASE SCOPED CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/create-database-scoped-credential-transact-sql.md). Use uma credencial no nível do servidor quando precisa usar a mesma credencial para vários bancos de dados no servidor. Use uma credencial no escopo do banco de dados para tornar o banco de dados mais portátil. Quando um banco de dados for movido para um novo servidor, a credencial no escopo do banco de dados será movida com ele. Use as credenciais no escopo do banco de dados no [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
CREATE CREDENTIAL credential_name   
WITH IDENTITY = 'identity_name'  
    [ , SECRET = 'secret' ]  
        [ FOR CRYPTOGRAPHIC PROVIDER cryptographic_provider_name ]  
```  
  
## <a name="arguments"></a>Argumentos  
 *credential_name*  
 Especifica o nome da credencial que está sendo criada. *credential_name* não pode começar com a tecla jogo da velha (#). As credenciais de sistema começam com ##.  Ao usar uma SAS (assinatura de acesso compartilhado), esse nome deve corresponder ao caminho do contêiner, começar com https e não deve conter uma barra "/". Veja o exemplo D abaixo.  
  
 IDENTITY **='**_identity\_name_**'**  
 Especifica o nome da conta a ser usada ao conectar o servidor externamente. Quando a credencial é usada para acessar o Azure Key Vault, o **IDENTITY** é o nome do cofre de chaves. Veja o exemplo C a seguir. Quando a credencial usa uma SAS (assinatura de acesso compartilhado), a **IDENTITY** é *SHARED ACCESS SIGNATURE*. Veja o exemplo D abaixo.  
 
> [!IMPORTANT]
> O Banco de dados SQL do Azure é compatível apenas as identidades do Azure Key Vault e com Assinatura de Acesso Compartilhado. Não há suporte para identidades de usuário do Windows.
 
 SECRET **='**_secret_**'**  
 Especifica o segredo necessário para a autenticação de saída.  
  
 Quando a credencial é usada para acessar o Azure Key Vault, o argumento **SECRET** de **CREATE CREDENTIAL** exige que a *\<Client ID>* (sem hifens) e o *\<Secret>* de uma **Entidade de Serviço** no Azure Active Directory sejam passados juntos sem um espaço entre eles. Veja o exemplo C a seguir. Quando a credencial usa uma assinatura de acesso compartilhado, o **SECRET** é o token de assinatura de acesso compartilhado. Veja o exemplo D abaixo.  Para obter informações sobre como criar uma política de acesso armazenado e uma assinatura de acesso compartilhado em um contêiner do Azure, consulte [Lição 1: Criar uma política de acesso armazenado e uma assinatura de acesso compartilhado em um contêiner do Azure](../../relational-databases/lesson-1-create-stored-access-policy-and-shared-access-signature.md).  
  
 FOR CRYPTOGRAPHIC PROVIDER *cryptographic_provider_name*  
 Especifica o nome de um *Provedor de EKM (Gerenciamento Extensível de Chaves)*. Para obter mais informações sobre o Gerenciamento de Chaves, consulte [EKM &#40;Gerenciamento Extensível de Chaves&#41;](../../relational-databases/security/encryption/extensible-key-management-ekm.md).  
  
## <a name="remarks"></a>Remarks  

 Quando IDENTITY for um usuário do Windows, o segredo poderá ser a senha. O segredo é criptografado com a chave mestre de serviço. Se a chave mestre de serviço for gerada novamente, o segredo será criptografado novamente com a nova chave mestre de serviço.  
  
 Depois de criar uma credencial, mapeie-a para um logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando [CREATE LOGIN](../../t-sql/statements/create-login-transact-sql.md) ou [ALTER LOGIN](../../t-sql/statements/alter-login-transact-sql.md). Um logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pode ser mapeado somente para uma credencial, mas uma única credencial pode ser mapeada para vários logons do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter mais informações, consulte [Credenciais &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/authentication-access/credentials-database-engine.md). Uma credencial no nível do servidor pode ser mapeada apenas para um logon, não para um usuário de banco de dados. 
  
 As informações sobre as credenciais são visíveis na exibição do catálogo [sys.credentials](../../relational-databases/system-catalog-views/sys-credentials-transact-sql.md).  
  
 Se não houver nenhuma credencial mapeada de logon para o provedor, a credencial mapeada para a conta de serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] será usada.  
  
 Um logon pode ter várias credenciais mapeadas, contanto que elas sejam usadas com provedores diferentes. Deve haver só uma credencial mapeada por provedor por logon. A mesma credencial pode ser mapeada para outros logons.  
  
## <a name="permissions"></a>Permissões  
 Exige a permissão **ALTER ANY CREDENTIAL**.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-basic-example"></a>A. Exemplo básico  
 O exemplo a seguir cria a credencial chamada `AlterEgo`. A credencial contém o usuário do Windows `Mary5` e uma senha.  
  
```  
CREATE CREDENTIAL AlterEgo WITH IDENTITY = 'Mary5',   
    SECRET = '<EnterStrongPasswordHere>';  
GO  
```  
  
### <a name="b-creating-a-credential-for-ekm"></a>B. Criando uma credencial para o EKM  
 O exemplo a seguir usa uma conta criada anteriormente chamada `User1OnEKM` em um módulo de EKM através das ferramentas de gerenciamento de EKM, com um tipo de conta e senha básicos. A conta **sysadmin** no servidor cria uma credencial usada para se conectar à conta da EKM e atribui essa credencial à conta `User1`[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
```  
CREATE CREDENTIAL CredentialForEKM  
    WITH IDENTITY='User1OnEKM', SECRET='<EnterStrongPasswordHere>'  
    FOR CRYPTOGRAPHIC PROVIDER MyEKMProvider;  
GO  
  
/* Modify the login to assign the cryptographic provider credential */  
ALTER LOGIN Login1  
ADD CREDENTIAL CredentialForEKM;  
  
/* Modify the login to assign a non cryptographic provider credential */   
ALTER LOGIN Login1  
WITH CREDENTIAL = AlterEgo;  
GO  
```  
  
### <a name="c-creating-a-credential-for-ekm-using-the-azure-key-vault"></a>C. Criando uma credencial de EKM usando a Chave do Cofre do Azure  
 O exemplo a seguir cria uma credencial [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para o [!INCLUDE[ssDE](../../includes/ssde-md.md)] para uso ao acessar o Azure Key Vault com o **Conector do SQL Server para Microsoft Azure Key Vault**. Para obter um exemplo completo de como usar o Conector do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], consulte [Gerenciamento extensível de chaves usando o Azure Key Vault &#40;SQL Server&#41;](../../relational-databases/security/encryption/extensible-key-management-using-azure-key-vault-sql-server.md).  
  
> [!IMPORTANT]  
>  O argumento **IDENTITY** de **CREATE CREDENTIAL** requer o nome da chave de cofre. O argumento **SECRET** de **CREATE CREDENTIAL** exige que a *\<Client ID>* (sem hifens) e o *\<Secret>* sejam passados juntos sem um espaço entre eles.  
  
 No exemplo a seguir, a **ID do cliente** (`EF5C8E09-4D2A-4A76-9998-D93440D8115D`) não tem hifens e foi inserida como a cadeia de caracteres `EF5C8E094D2A4A769998D93440D8115D` , e **Secret** é representado pela cadeia de caracteres *SECRET_DBEngine*.  
  
```  
USE master;  
CREATE CREDENTIAL Azure_EKM_TDE_cred   
    WITH IDENTITY = 'ContosoKeyVault',   
    SECRET = 'EF5C8E094D2A4A769998D93440D8115DSECRET_DBEngine'   
    FOR CRYPTOGRAPHIC PROVIDER AzureKeyVault_EKM_Prov ;  
```  
  
 O exemplo a seguir cria a mesma credencial usando variáveis para as cadeias de caracteres **Client ID** e **Secret**, que, em seguida, são concatenadas para formar o argumento **SECRET**. A função **REPLACE** é usada para remover os hifens da ID do Cliente.  
  
```  
DECLARE @AuthClientId uniqueidentifier = 'EF5C8E09-4D2A-4A76-9998-D93440D8115D';  
DECLARE @AuthClientSecret varchar(200) = 'SECRET_DBEngine';  
DECLARE @pwd varchar(max) = REPLACE(CONVERT(varchar(36), @AuthClientId) , '-', '') + @AuthClientSecret;  
  
EXEC ('CREATE CREDENTIAL Azure_EKM_TDE_cred   
    WITH IDENTITY = 'ContosoKeyVault', SECRET = ''' + @PWD + '''   
    FOR CRYPTOGRAPHIC PROVIDER AzureKeyVault_EKM_Prov ;');  
```  
  
### <a name="d-creating-a-credential-using-a-sas-token"></a>D. Criando uma credencial usando um token SAS  
 **Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] à [versão atual](https://go.microsoft.com/fwlink/p/?LinkId=299658).  
  
 O exemplo a seguir cria uma credencial de assinatura de acesso compartilhado usando um token SAS.  Para obter um tutorial sobre como criar uma política de acesso armazenado e uma assinatura de acesso compartilhado em um contêiner do Azure e, em seguida, criar uma credencial usando a assinatura de acesso compartilhado, consulte [Tutorial: Usando o serviço de armazenamento de Blobs do Microsoft Azure com bancos de dados SQL Server 2016](../../relational-databases/tutorial-use-azure-blob-storage-service-with-sql-server-2016.md).  
  
> [!IMPORTANT]  
>  O argumento **CREDENTIAL NAME** exige que o nome corresponda ao caminho do contêiner, comece com https e não contenha uma barra "/" à direita. O argumento **IDENTITY** exige o nome, *SHARED ACCESS SIGNATURE*. O argumento **SECRET** exige o token de assinatura de acesso compartilhado.  
  
```  
USE master  
CREATE CREDENTIAL [https://<mystorageaccountname>.blob.core.windows.net/<mystorageaccountcontainername>] -- this name must match the container path, start with https and must not contain a trailing forward slash.  
   WITH IDENTITY='SHARED ACCESS SIGNATURE' -- this is a mandatory string and do not change it.   
   , SECRET = 'sharedaccesssignature' –- this is the shared access signature token   
GO    
```  
  
## <a name="see-also"></a>Consulte Também  
 [Credenciais &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/authentication-access/credentials-database-engine.md)   
 [ALTER CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/alter-credential-transact-sql.md)   
 [DROP CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/drop-credential-transact-sql.md)   
 [CREATE DATABASE SCOPED CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/create-database-scoped-credential-transact-sql.md)   
 [CREATE LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/create-login-transact-sql.md)   
 [ALTER LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/alter-login-transact-sql.md)   
 [sys.credentials &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-credentials-transact-sql.md)   
 [Lição 2: Criar uma credencial do SQL Server usando uma assinatura de acesso compartilhado](../../relational-databases/lesson-2-create-a-sql-server-credential-using-a-shared-access-signature.md)   
 [Assinaturas de Acesso Compartilhado](https://azure.microsoft.com/documentation/articles/storage-dotnet-shared-access-signature-part-1/)  
  
  
