---
title: "Criar usuário (Transact-SQL) | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 07/28/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- WITHOUT_LOGIN_TSQL
- CREATE_USER_TSQL
- SQL13.SWB.DATABASEUSER.OWNEDSCHEMAS.F1
- WITHOUT LOGIN
- CREATE USER
- ALLOW_ENCRYPTED_VALUE_MODIFICATIONS
- ALLOW_ENCRYPTED_VALUE_MODIFICATIONS_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- adding users
- WITHOUT LOGIN [SQL Server]
- CREATE USER statement
- database user additions [SQL Server]
- USER WITHOUT LOGIN [SQL Server]
- users [SQL Server], adding
- users [SQL Server]
ms.assetid: 01de7476-4b25-4d58-85b7-1118fe64aa80
caps.latest.revision: 111
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 47004dfe9ec810fec68a63849755021690f98fdb
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="create-user-transact-sql"></a>CREATE USER (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Adiciona um usuário ao banco de dados atual. Os onze tipos de usuários são listados com um exemplo da sintaxe mais básico:  
  
**Usuários com base em logons no mestre** esse é o tipo mais comum do usuário.  
  
-   Usuário baseado em um logon baseado em uma conta do Active Directory do Windows. `CREATE USER [Contoso\Fritz];`     
-   Usuário baseado em um logon baseado em um grupo do Windows. `CREATE USER [Contoso\Sales];`   
-   Usuário baseado em um logon que usa a autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. `CREATE USER Mary;`  
  
**Os usuários que se autenticam no banco de dados** recomendado para ajudar a tornar seu banco de dados mais portáteis.  
 Sempre é permitido em [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]. Só é permitida em um banco de dados independente em [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)].  
  
-   Usuário baseado em um usuário do Windows que não tem logon. `CREATE USER [Contoso\Fritz];`    
-   Usuário baseado em um grupo do Windows que não tem logon. `CREATE USER [Contoso\Sales];`  
-   Usuário em [!INCLUDE[ssSDS](../../includes/sssds-md.md)] ou [!INCLUDE[ssSDW_md](../../includes/sssdw-md.md)] com base em um usuário do Active Directory do Azure. `CREATE USER [Contoso\Fritz] FROM EXTERNAL PROVIDER;`     

-   Usuário de banco de dados contido com senha. (Não disponível em [!INCLUDE[ssSDW_md](../../includes/sssdw-md.md)].)`CREATE USER Mary WITH PASSWORD = '********';`   
  
**Usuários com base em entidades de segurança do Windows que se conectam por meio de logon de grupo do Windows**  
  
-   Usuário baseado em um usuário do Windows que não tem logon, mas pode conectar-se ao [!INCLUDE[ssDE](../../includes/ssde-md.md)] por meio de associação em um grupo do Windows. `CREATE USER [Contoso\Fritz];`  
  
-   Usuário baseado em um grupo do Windows que não tem logon, mas pode conectar-se ao [!INCLUDE[ssDE](../../includes/ssde-md.md)] por meio de associação em um grupo diferente do Windows. `CREATE USER [Contoso\Fritz];`  
  
**Os usuários que não é possível autenticar** esses usuários não podem fazer logon para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
-   Usuário sem um logon. Não pode fazer logon, mas pode receber permissões. `CREATE USER CustomApp WITHOUT LOGIN;`    
-   Usuário baseado em um certificado. Não pode fazer logon, mas pode receber permissões e assinar módulos. `CREATE USER TestProcess FOR CERTIFICATE CarnationProduction50;`  
-   Usuário baseado em uma chave assimétrica. Não pode fazer logon, mas pode receber permissões e assinar módulos. `CREATE User TestProcess FROM ASYMMETRIC KEY PacificSales09;`   
 
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
-- Syntax Users based on logins in master  
CREATE USER user_name   
    [   
        { FOR | FROM } LOGIN login_name   
    ]  
    [ WITH <limited_options_list> [ ,... ] ]   
[ ; ]  
  
--Users that authenticate at the database  
CREATE USER   
    {  
      windows_principal [ WITH <options_list> [ ,... ] ]  
  
    | user_name WITH PASSWORD = 'password' [ , <options_list> [ ,... ]   
    | Azure_Active_Directory_principal FROM EXTERNAL PROVIDER   
    }  
  
 [ ; ]  
  
--Users based on Windows principals that connect through Windows group logins  
CREATE USER   
    {   
          windows_principal [ { FOR | FROM } LOGIN windows_principal ]  
        | user_name { FOR | FROM } LOGIN windows_principal  
}  
    [ WITH <limited_options_list> [ ,... ] ]   
[ ; ]  
  
--Users that cannot authenticate   
CREATE USER user_name   
    {  
         WITHOUT LOGIN [ WITH <limited_options_list> [ ,... ] ]  
       | { FOR | FROM } CERTIFICATE cert_name   
       | { FOR | FROM } ASYMMETRIC KEY asym_key_name   
    }  
 [ ; ]  
  
<options_list> ::=  
      DEFAULT_SCHEMA = schema_name  
    | DEFAULT_LANGUAGE = { NONE | lcid | language name | language alias }  
    | SID = sid   
    | ALLOW_ENCRYPTED_VALUE_MODIFICATIONS = [ ON | OFF ] ]  
  
<limited_options_list> ::=  
      DEFAULT_SCHEMA = schema_name ]   
    | ALLOW_ENCRYPTED_VALUE_MODIFICATIONS = [ ON | OFF ] ]  
  
-- SQL Database syntax when connected to a federation member  
CREATE USER user_name  
[;]  
```  

```  
-- Syntax for Azure SQL Data Warehouse  
  
CREATE USER user_name   
    [ { { FOR | FROM } { LOGIN login_name }   
      | WITHOUT LOGIN  
    ]   
    [ WITH DEFAULT_SCHEMA = schema_name ]  
[;]

CREATE USER Azure_Active_Directory_principal FROM EXTERNAL PROVIDER  
    [ WITH DEFAULT_SCHEMA = schema_name ]  
[;]
``` 
  
```  
-- Syntax for Parallel Data Warehouse  
  
CREATE USER user_name   
    [ { { FOR | FROM }  
      {   
        LOGIN login_name   
      }   
      | WITHOUT LOGIN  
    ]   
    [ WITH DEFAULT_SCHEMA = schema_name ]  
[;]  
```  
  
## <a name="arguments"></a>Argumentos  
 *user_name*  
 Especifica o nome pelo qual o usuário é identificado nesse banco de dados. *user_name* é um **sysname**. Pode ter até 128 caracteres. Ao criar um usuário baseado em uma entidade de segurança do Windows, o nome da entidade de segurança do Windows se tornará o nome do usuário, a menos que outro nome de usuário seja especificado.  
  
 LOGON *login_name*  
 Especifica o logon para o qual o usuário do banco de dados está sendo criado. *login_name* deve ser um logon válido no servidor. Pode ser um logon baseado em uma entidade de segurança do Windows (usuário ou grupo) ou um logon que usa a autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Quando esse logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] entra no banco de dados, ele adquire o nome e a ID do usuário de banco de dados que está sendo criado. Ao criar um logon mapeado de uma entidade de segurança do Windows, use o formato **[***\<domainName >*  **\\**   *\<loginName >***]**. Para obter exemplos, consulte [Resumo da sintaxe](#SyntaxSummary).  
  
 Se a instrução CREATE USER for a única em um lote SQL, o Banco de Dados SQL do Windows Azure oferecerá suporte à cláusula WITH LOGIN. Se a instrução CREATE USER não for a única em um lote SQL ou for executada na SQL dinâmica, não haverá suporte para a cláusula WITH LOGIN.  
  
 COM DEFAULT_SCHEMA = *schema_name*  
 Especifica o primeiro esquema que será pesquisado pelo servidor quando ele resolver os nomes de objetos para esse usuário de banco de dados.  
  
 '*windows_principal*'  
 Especifica a entidade de segurança do Windows para a qual o usuário de banco de dados está sendo criado. O *windows_principal* pode ser um usuário do Windows ou um grupo do Windows. O usuário será criado mesmo que o *windows_principal* não tem um logon. Ao se conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], se o *windows_principal* não tem um logon, o Windows principal deve ser autenticado no [!INCLUDE[ssDE](../../includes/ssde-md.md)] através da participação em um grupo do Windows que tem um logon ou a cadeia de caracteres de conexão deve Especifique o banco de dados independente como catálogo inicial. Ao criar um usuário de uma entidade de segurança do Windows, use o formato **[***\<domainName >*  **\\**   *\< loginName >***]**. Para obter exemplos, consulte [Resumo da sintaxe](#SyntaxSummary). Usuários com base em usuários do Active Directory, são limitados aos nomes de menos de 21 caracteres.    
  
 '*Azure_Active_Directory_principal*'  
 **Aplica-se a**: [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)], [!INCLUDE[ssSDW_md](../../includes/sssdw-md.md)].  
  
 Especifica a entidade de segurança do Active Directory do Azure para que o usuário de banco de dados está sendo criado. O *Azure_Active_Directory_principal* pode ser um usuário do Active Directory do Azure, ou um grupo do Active Directory do Azure. (Os usuários do Active Directory do azure não podem ter logons de autenticação do Windows em [!INCLUDE[ssSDS](../../includes/sssds-md.md)]; somente os usuários de banco de dados.) A cadeia de caracteres de conexão deve especificar o banco de dados independente como catálogo inicial. 

 Para usuários, você deve usar o alias completo do seu domínio principal.   
 
-   `CREATE USER [bob@contoso.com] FROM EXTERNAL PROVIDER;`  
  
-   `CREATE USER [alice@fabrikam.onmicrosoft.com] FROM EXTERNAL PROVIDER;`

 Para grupos de segurança, você deve usar o *nome de exibição* do grupo de segurança. Para o *enfermeiras* grupo de segurança que você deseja usar:  
  
-   `CREATE USER [Nurses] FROM EXTERNAL PROVIDER;`  
  
 Para obter mais informações, veja [Conectar-se ao Banco de Dados SQL usando a Autenticação do Azure Active Directory](https://azure.microsoft.com/documentation/articles/sql-database-aad-authentication).  
  
COM a senha = '*senha*'  
 **Aplica-se a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] por meio de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)].  
  
 Pode ser usado apenas em um banco de dados independente. Especifica a senha do usuário que está sendo criado. Começando com [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]armazenadas, informações de senha são calculadas usando SHA-512 da senha com valor de sal.  
  
WITHOUT LOGIN  
 Especifica que o usuário não deve ser mapeado para um logon existente.  
  
CERTIFICADO *cert_name*  
 **Aplica-se a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] por meio de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)].  
  
 Especifica o certificado para o qual o usuário do banco de dados está sendo criado.  
  
CHAVE ASSIMÉTRICA *asym_key_name*  
 **Aplica-se a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] por meio de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)].  
  
 Especifica a chave assimétrica para a qual o usuário de banco de dados está sendo criado.  
  
DEFAULT_LANGUAGE = *{NONE | \<lcid > | \<nome de idioma > | \<alias do idioma >}*  
 **Aplica-se a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] por meio de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)].  
  
 Especifica o idioma padrão do novo usuário. Se for especificado um idioma padrão para o usuário e o idioma padrão do banco de dados for alterado posteriormente, o idioma padrão dos usuários permanecerá conforme especificado. Se nenhum idioma padrão for especificado, o idioma padrão do usuário será o idioma padrão do banco de dados. Se o idioma padrão do usuário não for especificado, e o idioma padrão do banco de dados for alterado posteriormente, o idioma padrão do usuário será alterado para o novo idioma padrão do banco de dados.  
  
> [!IMPORTANT]  
>  *DEFAULT_LANGUAGE* é usado apenas para um usuário de banco de dados independente.  
  
SID = *sid*  
 **Aplica-se a**: do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Aplica-se somente a usuários com senhas (autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]) em um banco de dados independente. Especifica o SID do novo usuário de banco de dados. Se esta opção não for selecionada, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nomeará um SID automaticamente. Use o parâmetro do SID para criar usuários em vários bancos de dados que têm a mesma identidade (SID). Isso é útil ao criar usuários em vários bancos de dados para se preparar para failover do AlwaysOn. Para determinar o SID de um usuário, consulte sys. database_principals.  
  
ALLOW_ENCRYPTED_VALUE_MODIFICATIONS = [ON | **OFF** ]]  
 **Aplica-se a**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] por meio de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
 Suprime as verificações de metadados criptográficos no servidor em operações de cópia em massa. Isso permite que o usuário copiar em massa criptografado dados entre tabelas ou bancos de dados, sem descriptografá-los. O padrão é OFF.  
  
> [!WARNING]  
>  O uso inadequado dessa opção pode resultar em dados corrompidos. Para obter mais informações, consulte [migrar dados confidenciais protegidos pelo sempre criptografado](../../relational-databases/security/encryption/migrate-sensitive-data-protected-by-always-encrypted.md).  
  
## <a name="remarks"></a>Comentários  
 Se FOR LOGIN for omitido, o novo usuário de banco de dados será mapeado para o logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] com o mesmo nome.  
  
 O esquema padrão será o primeiro esquema que será pesquisado pelo servidor ao resolver os nomes dos objetos para esse usuário de banco de dados. A não ser quando especificado de outra forma, o esquema padrão será o proprietário dos objetos criados pelo usuário de banco de dados.  
  
 Se o usuário tiver um esquema padrão, esse esquema padrão será usado. Se o usuário não tiver um esquema padrão, mas for um membro de um grupo que tenha um esquema padrão, o esquema padrão do grupo será usado. Se o usuário não tiver um esquema padrão e for membro de mais de um grupo, o esquema padrão do usuário será o do grupo do Windows com o menor principal_id e um esquema padrão definido explicitamente. Não é possível selecionar explicitamente um dos esquemas padrão disponíveis como o esquema preferencial. Se nenhum esquema padrão pode ser determinada para um usuário, o **dbo** esquema será usado.  
  
 DEFAULT_SCHEMA pode ser definido antes de o esquema para o qual ele aponta ser criado.  
  
 DEFAULT_SCHEMA não pode ser especificado ao criar um usuário mapeado para um certificado ou para uma chave assimétrica.  
  
 O valor de DEFAULT_SCHEMA será ignorado se o usuário for um membro da função de servidor fixa sysadmin. Todos os membros da função de servidor fixa sysadmin possuem um esquema padrão do `dbo`.  
  
 A cláusula WITHOUT LOGIN cria um usuário que não é mapeado para um logon do SQL Server. Pode conectar-se a outros bancos de dados como convidado. Podem ser atribuídas permissões a esse usuário sem logon e quando o contexto de segurança for alterado para um usuário sem logon, os usuários originais receberão as permissões do usuário sem logon. Consulte o exemplo [d. criando e usando um usuário sem um logon](#withoutLogin).  
  
 Somente usuários que são mapeados para entidades de segurança do Windows podem conter o caractere de barra invertida (**\\**).  
  
 CREATE USER não pode ser usado para criar um usuário convidado porque o usuário convidado já existe dentro de todo banco de dados. Você pode ativar o usuário convidado concedendo permissão CONNECT, conforme mostrado:  
  
```  
GRANT CONNECT TO guest;  
GO  
```  
  
 Informações sobre usuários de banco de dados são visíveis no [database_principals](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md) exibição do catálogo.  
  
##  <a name="SyntaxSummary"></a>Resumo da sintaxe  
 **Usuários com base em logons no mestre**  
  
 A lista a seguir mostra a sintaxe possível para usuários baseados em logons. As opções de esquema padrão não são listadas.  
  
-   `CREATE USER [Domain1\WindowsUserBarry]`  
-   `CREATE USER [Domain1\WindowsUserBarry] FOR LOGIN Domain1\WindowsUserBarry`  
-   `CREATE USER [Domain1\WindowsUserBarry] FROM LOGIN Domain1\WindowsUserBarry`  
-   `CREATE USER [Domain1\WindowsGroupManagers]`  
-   `CREATE USER [Domain1\WindowsGroupManagers] FOR LOGIN [Domain1\WindowsGroupManagers]`  
-   `CREATE USER [Domain1\WindowsGroupManagers] FROM LOGIN [Domain1\WindowsGroupManagers]`  
-   `CREATE USER SQLAUTHLOGIN`  
-   `CREATE USER SQLAUTHLOGIN FOR LOGIN SQLAUTHLOGIN`  
-   `CREATE USER SQLAUTHLOGIN FROM LOGIN SQLAUTHLOGIN`  
  
**Usuários que se autenticam no banco de dados**  
  
 A lista a seguir mostra a sintaxe possível para usuários que pode ser usada apenas em um banco de dados contido. Os usuários criados não serão relacionados a nenhum logon na **mestre** banco de dados. As opções de esquema e de idioma padrão não estão listadas.  
  
> [!IMPORTANT]  
>  Esta sintaxe concede acesso de usuário ao banco de dados e também concede novo acesso ao [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
-   `CREATE USER [Domain1\WindowsUserBarry]`  
-   `CREATE USER [Domain1\WindowsGroupManagers]`  
-   `CREATE USER Barry WITH PASSWORD = 'sdjklalie8rew8337!$d'`  
  
**Usuários com base em entidades de segurança do Windows sem logons no mestre**  
  
 A lista a seguir mostra a sintaxe possível para usuários que têm acesso para o [!INCLUDE[ssDE](../../includes/ssde-md.md)] por meio de uma janela de grupo, mas não tiver um logon **mestre**. Essa sintaxe pode ser usada em todos os tipos de bancos de dados. As opções de esquema e de idioma padrão não estão listadas.  
  
 Essa sintaxe é semelhante a usuários baseados em logons no mestre, mas essa categoria de usuário não tem um logon no mestre. O usuário deve ter acesso ao [!INCLUDE[ssDE](../../includes/ssde-md.md)] por meio de um logon de grupo do Windows.  
  
 Esta sintaxe é semelhante a usuários de banco de dados contidos baseados em entidades de segurança do Windows, mas essa categoria de usuário não obtém novo acesso ao [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
-   `CREATE USER [Domain1\WindowsUserBarry]`  
-   `CREATE USER [Domain1\WindowsUserBarry] FOR LOGIN Domain1\WindowsUserBarry`  
-   `CREATE USER [Domain1\WindowsUserBarry] FROM LOGIN Domain1\WindowsUserBarry`  
-   `CREATE USER [Domain1\WindowsGroupManagers]`  
-   `CREATE USER [Domain1\WindowsGroupManagers] FOR LOGIN [Domain1\WindowsGroupManagers]`  
-   `CREATE USER [Domain1\WindowsGroupManagers] FROM LOGIN [Domain1\WindowsGroupManagers]`  
  
**Usuários que não é possível autenticar**  
  
 A lista a seguir mostra a sintaxe possível para usuários que não podem fazer logon no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   `CREATE USER RIGHTSHOLDER WITHOUT LOGIN`  
-   `CREATE USER CERTUSER FOR CERTIFICATE SpecialCert`  
-   `CREATE USER CERTUSER FROM CERTIFICATE SpecialCert`  
-   `CREATE USER KEYUSER FOR ASYMMETRIC KEY SecureKey`  
-   `CREATE USER KEYUSER FROM ASYMMETRIC KEY SecureKey`  
  
## <a name="security"></a>Segurança  
 A criação de um usuário concede acesso a um banco de dados, mas não concede automaticamente nenhum acesso aos objetos em um banco de dados. Depois de criar um usuário, as ações comuns são adicionar os usuários às funções de banco de dados que têm permissão para acessar objetos de banco de dados ou conceder permissões de objeto ao usuário. Para obter informações sobre como criar um sistema de permissões, veja [Introdução às permissões do mecanismo de banco de dados](../../relational-databases/security/authentication-access/getting-started-with-database-engine-permissions.md).  
  
### <a name="special-considerations-for-contained-databases"></a>Considerações especiais para bancos de dados contidos  
 Ao se conectar a um banco de dados independente, se o usuário não tem um logon na **mestre** banco de dados, a cadeia de caracteres de conexão deve incluir o nome do banco de dados independente como catálogo inicial. O parâmetro de catálogo inicial sempre é necessário para um usuário com senha de banco de dados contido.  
  
 Em um banco de dados contido, a criação de usuários ajuda a separar o banco de dados da instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)], de forma que o banco de dados possa ser movido facilmente para outra instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter mais informações, consulte [bancos de dados independentes](../../relational-databases/databases/contained-databases.md) e [banco de dados de usuários independentes – tornando seu banco de dados portátil](../../relational-databases/security/contained-database-users-making-your-database-portable.md). Para alterar um usuário de banco de dados de um usuário com base em um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] logon de autenticação para um usuário de banco de dados independente com senha, consulte [sp_migrate_user_to_contained &#40; Transact-SQL &#41; ](../../relational-databases/system-stored-procedures/sp-migrate-user-to-contained-transact-sql.md).  
  
 Em um banco de dados independente, os usuários não precisam ter logons no **mestre** banco de dados. Os administradores do [!INCLUDE[ssDE](../../includes/ssde-md.md)] devem entender que o acesso a um banco de dados independente pode ser concedido no nível do banco de dados e não no nível do [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Para obter mais informações, consulte [Security Best Practices with Contained Databases](../../relational-databases/databases/security-best-practices-with-contained-databases.md).  
  
 Ao usar os usuários do banco de dados independente em [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)], configure o acesso usando uma regra de firewall no nível de banco de dados, em vez de uma regra de firewall de nível de servidor. Para obter mais informações, consulte [sp_set_database_firewall_rule &#40; Banco de dados SQL do Azure &#41; ](../../relational-databases/system-stored-procedures/sp-set-database-firewall-rule-azure-sql-database.md).
 
Para [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] e [!INCLUDE[ssSDW_md](../../includes/sssdw-md.md)] usuários de banco de dados independente, o SSMS podem dar suporte a autenticação multifator. Para obter mais informações, consulte [Suporte ao SSMS para MFA do Azure AD com o banco de dados SQL e o SQL Data Warehouse](https://azure.microsoft.com/documentation/articles/sql-database-ssms-mfa-authentication/).  
  
### <a name="permissions"></a>Permissões  
 Requer a permissão ALTER ANY USER no banco de dados.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-creating-a-database-user-based-on-a-sql-server-login"></a>A. Criando um usuário de banco de dados baseado em um logon do SQL Server  
 O exemplo a seguir cria primeiro um logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] denominado `AbolrousHazem` e, em seguida, cria um usuário de banco de dados correspondente `AbolrousHazem` no `AdventureWorks2012`.  
  
```  
CREATE LOGIN AbolrousHazem   
    WITH PASSWORD = '340$Uuxwp7Mcxo7Khy';  
```   
Alterar um banco de dados do usuário. Por exemplo, em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usar o `USE AdventureWorks2012` instrução. Em [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], você deve fazer uma nova conexão para o banco de dados do usuário.

```   
CREATE USER AbolrousHazem FOR LOGIN AbolrousHazem;  
GO   
```  
  
### <a name="b-creating-a-database-user-with-a-default-schema"></a>B. Criando um usuário de banco de dados com um esquema padrão  
 O exemplo a seguir cria primeiro um logon de servidor denominado `WanidaBenshoof` com uma senha e depois cria um usuário de banco de dados correspondente `Wanida`, com o esquema padrão `Marketing`.  
  
```  
CREATE LOGIN WanidaBenshoof   
    WITH PASSWORD = '8fdKJl3$nlNv3049jsKK';  
USE AdventureWorks2012;  
CREATE USER Wanida FOR LOGIN WanidaBenshoof   
    WITH DEFAULT_SCHEMA = Marketing;  
GO  
```  
  
### <a name="c-creating-a-database-user-from-a-certificate"></a>C. Criando um usuário de banco de dados de um certificado  
 O exemplo a seguir cria um usuário de banco de dados `JinghaoLiu` a partir do certificado `CarnationProduction50`.  
  
**Aplica-se a**: do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
```  
USE AdventureWorks2012;  
CREATE CERTIFICATE CarnationProduction50  
    WITH SUBJECT = 'Carnation Production Facility Supervisors',  
    EXPIRY_DATE = '11/11/2011';  
GO  
CREATE USER JinghaoLiu FOR CERTIFICATE CarnationProduction50;  
GO   
```  
  
###  <a name="withoutLogin"></a> D. Criando e usando um usuário sem um logon  
 O exemplo a seguir cria um usuário de banco de dados `CustomApp` que não mapeia para um logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. O exemplo concede uma permissão de usuário `adventure-works\tengiz0` para representar o usuário `CustomApp`.  
  
```  
USE AdventureWorks2012 ;  
CREATE USER CustomApp WITHOUT LOGIN ;  
GRANT IMPERSONATE ON USER::CustomApp TO [adventure-works\tengiz0] ;  
GO   
```  
  
 Para usar as credenciais `CustomApp`, o usuário `adventure-works\tengiz0` executa a seguinte instrução.  
  
```  
EXECUTE AS USER = 'CustomApp' ;  
GO  
```  
  
 Para reverter para as credenciais de `adventure-works\tengiz0`, o usuário executa a instrução a seguir.  
  
```  
REVERT ;  
GO  
```  
  
### <a name="e-creating-a-contained-database-user-with-password"></a>E. Criando um usuário com senha de banco de dados independente  
 O exemplo a seguir cria um usuário com senha de banco de dados contido. Este exemplo pode ser executado apenas em um banco de dados contido.  
  
**Aplica-se a**: do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Este exemplo funciona em [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)] se DEFAULT_LANGUAGE for removido.  
  
```  
USE AdventureWorks2012 ;  
GO  
CREATE USER Carlo  
WITH PASSWORD='RN92piTCh%$!~3K9844 Bl*'  
    , DEFAULT_LANGUAGE=[Brazilian]  
    , DEFAULT_SCHEMA=[dbo]  
GO   
```  
  
### <a name="f-creating-a-contained-database-user-for-a-domain-login"></a>F. Criando um usuário de banco de dados independente para um logon de domínio  
 O exemplo a seguir cria um usuário de banco de dados contido para um logon denominado Fritz em um domínio denominado Contoso. Este exemplo pode ser executado apenas em um banco de dados contido.  
  
**Aplica-se a**: do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
```  
USE AdventureWorks2012 ;  
GO  
CREATE USER [Contoso\Fritz] ;  
GO   
```  
  
### <a name="g-creating-a-contained-database-user-with-a-specific-sid"></a>G. Criando um usuário de banco de dados independente com uma SID específica  
 O exemplo a seguir cria um usuário de banco de dados independente autenticado do SQLServer chamado CarmenW. Este exemplo pode ser executado apenas em um banco de dados contido.  
  
**Aplica-se a**: do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
```  
USE AdventureWorks2012 ;  
GO  
CREATE USER CarmenW WITH PASSWORD = 'a8ea v*(Rd##+'  
, SID = 0x01050000000000090300000063FF0451A9E7664BA705B10E37DDC4B7;  
  
```  
  
### <a name="h-creating-a-user-to-copy-encrypted-data"></a>H. Criando um usuário para copiar os dados criptografados  
 O exemplo a seguir cria um usuário que pode copiar os dados protegidos pelo recurso sempre criptografado de um conjunto de tabelas, contendo colunas criptografadas, a outro conjunto de tabelas com colunas criptografadas (na mesma ou em outro banco de dados).  Para obter mais informações, consulte [migrar dados confidenciais protegidos pelo sempre criptografado](../../relational-databases/security/encryption/migrate-sensitive-data-protected-by-always-encrypted.md).  
  
**Aplica-se a**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] por meio de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
```  
CREATE USER [Chin]   
WITH   
      DEFAULT_SCHEMA = dbo  
    , ALLOW_ENCRYPTED_VALUE_MODIFICATIONS = ON ;  
```  
  

## <a name="next-steps"></a>Próximas etapas  
Quando o usuário é criado, considere adicionar o usuário a uma função de banco de dados usando o [ALTER ROLE](../../t-sql/statements/alter-role-transact-sql.md) instrução.  
Você talvez também queira [CONCEDER permissões de objeto](../../t-sql/statements/grant-object-permissions-transact-sql.md) para a função para que possam acessar as tabelas. Para obter informações gerais sobre o modelo de segurança do SQL Server, consulte [permissões](../../relational-databases/security/permissions-database-engine.md).   
  
## <a name="see-also"></a>Consulte também  
 [Criar um usuário de banco de dados](../../relational-databases/security/authentication-access/create-a-database-user.md)   
 [sys.database_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)   
 [ALTER USER &#40;Transact-SQL&#41;](../../t-sql/statements/alter-user-transact-sql.md)   
 [Remover usuário &#40; Transact-SQL &#41;](../../t-sql/statements/drop-user-transact-sql.md)   
 [CREATE LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/create-login-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [Bancos de dados independentes](../../relational-databases/databases/contained-databases.md)   
 [Conectar-se ao banco de dados SQL usando a autenticação do Active Directory do Azure](https://azure.microsoft.com/documentation/articles/sql-database-aad-authentication)   
 [Guia de Introdução às permissões do mecanismo de banco de dados](../../relational-databases/security/authentication-access/getting-started-with-database-engine-permissions.md)  
  
  



