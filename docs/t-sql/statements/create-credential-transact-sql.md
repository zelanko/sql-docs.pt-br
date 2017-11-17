---
title: Criar CREDENCIAL (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 01/09/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: 51
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 556fa0262696075d63ee549730f2d9824c482dd4
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="create-credential-transact-sql"></a>CREATE CREDENTIAL (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Cria uma credencial de nível de servidor. Uma credencial é um registro que contém as informações de autenticação necessárias para se conectar a um recurso fora do SQL Server. A maioria das credenciais inclui um usuário e uma senha do Windows. Por exemplo, salvar um backup de banco de dados em algum local pode exigir SQL Server para fornecer credenciais especiais para acessar o local. Para obter mais informações, consulte [credenciais (mecanismo de banco de dados)](../../relational-databases/security/authentication-access/credentials-database-engine.md).
  
> [!NOTE]  
>  Para tornar a credencial em, use o nível de banco de dados [CREATE DATABASE SCOPED CREDENTIAL &#40; Transact-SQL &#41; ](../../t-sql/statements/create-database-scoped-credential-transact-sql.md). Use uma credencial de nível de servidor quando você precisa usar a mesma credencial para vários bancos de dados no servidor. Use uma credencial no escopo do banco de dados para tornar o banco de dados mais portáteis. Quando um banco de dados é movido para um novo servidor, a credencial no escopo do banco de dados será movido com ele. As credenciais no escopo de banco de dados de uso em [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
CREATE CREDENTIAL credential_name   
WITH IDENTITY = 'identity_name'  
    [ , SECRET = 'secret' ]  
        [ FOR CRYPTOGRAPHIC PROVIDER cryptographic_provider_name ]  
```  
  
## <a name="arguments"></a>Argumentos  
 *credential_name*  
 Especifica o nome da credencial que está sendo criada. *credential_name* não pode começar com o sinal de número (#). As credenciais de sistema começam com ##.  Ao usar uma assinatura de acesso compartilhado (SAS), esse nome deve corresponder ao caminho do contêiner, inicie com https e não deve conter uma barra invertida. Consulte o exemplo D abaixo.  
  
 IDENTIDADE **='***identity_name***'**  
 Especifica o nome da conta a ser usada ao conectar o servidor externamente. Quando a credencial é usada para acessar o Cofre de chaves do Azure, o **identidade** é o nome do cofre da chave. Veja o exemplo C a seguir. Quando a credencial está usando uma assinatura de acesso compartilhado (SAS), o **identidade** é *assinatura de acesso compartilhado*. Consulte o exemplo D abaixo.  
  
 SEGREDO **='***segredo***'**  
 Especifica o segredo necessário para a autenticação de saída.  
  
 Quando a credencial é usada para acessar o Cofre de chaves do Azure a **segredo** argumento de **CREATE CREDENTIAL** requer o  *\<ID do cliente >* (sem hifens) e  *\<segredo >* de um **entidade de serviço** no Azure Active Directory sejam aprovados juntos sem um espaço entre eles. Veja o exemplo C a seguir. Quando a credencial está usando uma assinatura de acesso compartilhado, o **segredo** é o token de assinatura de acesso compartilhado. Consulte o exemplo D abaixo.  Para obter informações sobre como criar uma política de acesso armazenada e uma assinatura de acesso compartilhado em um contêiner do Azure, consulte [lição 1: criar uma política de acesso armazenada e uma assinatura de acesso compartilhado em um contêiner do Azure](../../relational-databases/lesson-1-create-stored-access-policy-and-shared-access-signature.md).  
  
 PARA o provedor CRIPTOGRÁFICO *cryptographic_provider_name*  
 Especifica o nome de um *provedor de gerenciamento de chave extensível (EKM)*. Para obter mais informações sobre o gerenciamento de chaves, consulte [gerenciamento extensível de chaves &#40; EKM &#41; ](../../relational-databases/security/encryption/extensible-key-management-ekm.md).  
  
## <a name="remarks"></a>Comentários  

 Quando IDENTITY for um usuário do Windows, o segredo poderá ser a senha. O segredo é criptografado com a chave mestre de serviço. Se a chave mestre de serviço for gerada novamente, o segredo será criptografado novamente com a nova chave mestre de serviço.  
  
 Depois de criar uma credencial, mapeie-o para um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] logon usando [CREATE LOGIN](../../t-sql/statements/create-login-transact-sql.md) ou [ALTER LOGIN](../../t-sql/statements/alter-login-transact-sql.md). Um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] logon pode ser mapeado para apenas uma credencial, mas uma única credencial pode ser mapeada para vários [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] logons. Para obter mais informações, consulte [credenciais &#40; mecanismo de banco de dados &#41;](../../relational-databases/security/authentication-access/credentials-database-engine.md). Uma credencial de nível de servidor só pode ser mapeada para um logon, não a um usuário de banco de dados. 
  
 Informações sobre as credenciais são visíveis no [Credentials](../../relational-databases/system-catalog-views/sys-credentials-transact-sql.md) exibição do catálogo.  
  
 Se não houver nenhuma credencial mapeada de logon para o provedor, a credencial mapeada para a conta de serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] será usada.  
  
 Um logon pode ter várias credenciais mapeadas, contanto que elas sejam usadas com provedores diferentes. Deve haver só uma credencial mapeada por provedor por logon. A mesma credencial pode ser mapeada para outros logons.  
  
## <a name="permissions"></a>Permissões  
 Requer **ALTER ANY CREDENTIAL** permissão.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-basic-example"></a>A. Exemplo básico  
 O exemplo a seguir cria a credencial chamada `AlterEgo`. A credencial contém o usuário do Windows `Mary5` e uma senha.  
  
```  
CREATE CREDENTIAL AlterEgo WITH IDENTITY = 'Mary5',   
    SECRET = '<EnterStrongPasswordHere>';  
GO  
```  
  
### <a name="b-creating-a-credential-for-ekm"></a>B. Criando uma credencial para o EKM  
 O exemplo a seguir usa uma conta criada anteriormente chamada `User1OnEKM` em um módulo de EKM através das ferramentas de gerenciamento de EKM, com um tipo de conta e senha básicos. O **sysadmin** conta no servidor cria uma credencial que é usada para conectar-se à conta de EKM e atribui-lo para o `User1` [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] conta:  
  
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
 O exemplo a seguir cria um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de credencial para o [!INCLUDE[ssDE](../../includes/ssde-md.md)] para usar quando acessar o Cofre de chaves do Azure usando o **SQL Server Connector para Cofre de chaves do Microsoft Azure**. Para obter um exemplo completo de como usar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] conector, consulte [Extensible Key Management usando Azure Key Vault &#40; SQL Server &#41; ](../../relational-databases/security/encryption/extensible-key-management-using-azure-key-vault-sql-server.md).  
  
> [!IMPORTANT]  
>  O argumento **IDENTITY** de **CREATE CREDENTIAL** requer o nome da chave de cofre. O **segredo** argumento de **CREATE CREDENTIAL** requer o  *\<ID do cliente >* (sem hifens) e  *\<segredo >*  sejam aprovados juntos sem um espaço entre eles.  
  
 No exemplo a seguir, a **ID do cliente** (`EF5C8E09-4D2A-4A76-9998-D93440D8115D`) não tem hifens e foi inserida como a cadeia de caracteres `EF5C8E094D2A4A769998D93440D8115D` , e **Secret** é representado pela cadeia de caracteres *SECRET_DBEngine*.  
  
```  
USE master;  
CREATE CREDENTIAL Azure_EKM_TDE_cred   
    WITH IDENTITY = 'ContosoKeyVault',   
    SECRET = 'EF5C8E094D2A4A769998D93440D8115DSECRET_DBEngine'   
    FOR CRYPTOGRAPHIC PROVIDER AzureKeyVault_EKM_Prov ;  
```  
  
 O exemplo a seguir cria a mesma credencial usando variáveis para o **ID do cliente** e **segredo** cadeias de caracteres que depois são concatenadas para formar o **segredo** argumento. O **substituir** função é usada para remover os hifens de identificação do cliente.  
  
```  
DECLARE @AuthClientId uniqueidentifier = 'EF5C8E09-4D2A-4A76-9998-D93440D8115D';  
DECLARE @AuthClientSecret varchar(200) = 'SECRET_DBEngine';  
DECLARE @pwd varchar(max) = REPLACE(CONVERT(varchar(36), @AuthClientId) , '-', '') + @AuthClientSecret;  
  
EXEC ('CREATE CREDENTIAL Azure_EKM_TDE_cred   
    WITH IDENTITY = 'ContosoKeyVault', SECRET = ''' + @PWD + '''   
    FOR CRYPTOGRAPHIC PROVIDER AzureKeyVault_EKM_Prov ;');  
```  
  
### <a name="d-creating-a-credential-using-a-sas-token"></a>D. Criando uma credencial usando um Token de SAS  
 **Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] por meio de [versão atual](http://go.microsoft.com/fwlink/p/?LinkId=299658).  
  
 O exemplo a seguir cria uma credencial de assinatura de acesso compartilhado usando um token SAS.  Para um tutorial sobre como criar uma política de acesso armazenada e uma assinatura de acesso compartilhado em um contêiner do Azure e, em seguida, criar uma credencial usando a assinatura de acesso compartilhado, consulte [Tutorial: usando o serviço de armazenamento de BLOBs do Microsoft Azure com o SQL Server 2016 bancos de dados](Tutorial:%20Using%20the%20Microsoft%20Azure%20Blob%20storage%20service%20with%20SQL%20Server%202016%20databases.md).  
  
> [!IMPORTANT]  
>  O **nome da CREDENCIAL** argumento requer que o nome corresponde ao caminho do contêiner, iniciar com https e não conter uma barra invertida. O **identidade** argumento requer o nome, *assinatura de acesso compartilhado*. O **segredo** argumento requer que o token de assinatura de acesso compartilhado.  
  
```  
USE master  
CREATE CREDENTIAL [https://<mystorageaccountname>.blob.core.windows.net/<mystorageaccountcontainername>] -- this name must match the container path, start with https and must not contain a trailing forward slash.  
   WITH IDENTITY='SHARED ACCESS SIGNATURE' -- this is a mandatory string and do not change it.   
   , SECRET = 'sharedaccesssignature' –- this is the shared access signature token   
GO    
```  
  
## <a name="see-also"></a>Consulte também  
 [Credenciais &#40; mecanismo de banco de dados &#41;](../../relational-databases/security/authentication-access/credentials-database-engine.md)   
 [ALTER CREDENTIAL &#40; Transact-SQL &#41;](../../t-sql/statements/alter-credential-transact-sql.md)   
 [DROP CREDENTIAL &#40; Transact-SQL &#41;](../../t-sql/statements/drop-credential-transact-sql.md)   
 [CREATE DATABASE SCOPED CREDENTIAL &#40; Transact-SQL &#41;](../../t-sql/statements/create-database-scoped-credential-transact-sql.md)   
 [CREATE LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/create-login-transact-sql.md)   
 [ALTER LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/alter-login-transact-sql.md)   
 [sys.credentials &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-credentials-transact-sql.md)   
 [Lição 2: Criar uma credencial do SQL Server usando uma assinatura de acesso compartilhado](../../relational-databases/lesson-2-create-a-sql-server-credential-using-a-shared-access-signature.md)   
 [Assinaturas de acesso compartilhado](https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/)  
  
  

