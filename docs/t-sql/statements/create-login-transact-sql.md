---
description: CREATE LOGIN (Transact-SQL)
title: CREATE LOGIN (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/29/2020
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- CREATE_LOGIN_TSQL
- CREATE LOGIN
- LOGIN_TSQL
- LOGIN
dev_langs:
- TSQL
helpviewer_keywords:
- passwords [SQL Server], logins
- mapping logins [SQL Server]
- logins [SQL Server], creating
- CREATE LOGIN statement
- permissions [SQL Server], logins
- Windows domain accounts [SQL Server]
- re-hashing passwords
- certificates [SQL Server], logins
ms.assetid: eb737149-7c92-4552-946b-91085d8b1b01
author: VanMSFT
ms.author: vanto
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 26284d43476c4d0777a6adcefc5b39d6a5a1ae75
ms.sourcegitcommit: 3bd188e652102f3703812af53ba877cce94b44a9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/15/2020
ms.locfileid: "97488856"
---
# <a name="create-login-transact-sql"></a>CREATE LOGIN (Transact-SQL)

Cria um logon para bancos de dados SQL Server, Banco de Dados SQL, Azure Synapse Analytics ou Analytics Platform System. Clique em uma das guias a seguir para a sintaxe, argumentos, comentários, permissões e exemplos de uma versão específica.

CREATE LOGIN participa de transações. Se CREATE LOGIN for executado em uma transação e a transação for revertida, criação do logon será revertida. Se executado em uma transação, o logon criado não poderá ser usado até a transação ser confirmada.

Para obter mais informações sobre as convenções de sintaxe, consulte [Convenções de sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md).

[!INCLUDE[select-product](../../includes/select-product.md)]

::: moniker range=">=sql-server-2016||>=sql-server-linux-2017"

:::row:::
    :::column:::
        **_\* SQL Server \*_** &nbsp;
    :::column-end:::
    :::column:::
        [Banco de Dados SQL do Azure](create-login-transact-sql.md?view=azuresqldb-current)
    :::column-end:::
    :::column:::
        [Instância Gerenciada<br />de SQL do Azure](create-login-transact-sql.md?view=azuresqldb-mi-current)
    :::column-end:::
    :::column:::
        [Azure Synapse<br />Analytics](create-login-transact-sql.md?view=azure-sqldw-latest)
    :::column-end:::
    :::column:::
        [Analytics Platform<br />System (PDW)](create-login-transact-sql.md?view=aps-pdw-2016&preserve-view=true)
    :::column-end:::
:::row-end:::

&nbsp;

## <a name="sql-server"></a>SQL Server

## <a name="syntax"></a>Sintaxe

```syntaxsql
-- Syntax for SQL Server
CREATE LOGIN login_name { WITH <option_list1> | FROM <sources> }

<option_list1> ::=
    PASSWORD = { 'password' | hashed_password HASHED } [ MUST_CHANGE ]
    [ , <option_list2> [ ,... ] ]

<option_list2> ::=
    SID = sid
    | DEFAULT_DATABASE = database
    | DEFAULT_LANGUAGE = language
    | CHECK_EXPIRATION = { ON | OFF}
    | CHECK_POLICY = { ON | OFF}
    | CREDENTIAL = credential_name

<sources> ::=
    WINDOWS [ WITH <windows_options>[ ,... ] ]
    | CERTIFICATE certname
    | ASYMMETRIC KEY asym_key_name
  
<windows_options> ::=
    DEFAULT_DATABASE = database
    | DEFAULT_LANGUAGE = language
```

## <a name="arguments"></a>Argumentos

*login_name* Especifica o nome do logon criado. Há quatro tipos de logons: logons do SQL Server, logons do Windows, logons mapeados por certificado e logons mapeados por chave assimétrica. Ao criar logons mapeados de uma conta de domínio do Windows, você deve usar o nome de logon de usuário de versões anteriores ao Windows 2000 no formato [\<domainName>\\<nome_de_logon>]. Você não pode usar um UPN no formato login_name@DomainName. Para obter um exemplo, consulte o exemplo D posteriormente neste artigo. Os logons de autenticação são do tipo **sysname** e devem estar em conformidade com as regras para [Identificadores](../../relational-databases/databases/database-identifiers.md) e não podem conter um ' **\\** '. Os logons do Windows podem conter um ' **\\** '. Os logons baseados em usuários do Active Directory estão limitados a nomes com menos de 21 caracteres.

PASSWORD **=** '*password*' Aplica-se apenas a logons do SQL Server. Especifica a senha do logon que está sendo criado. Use uma senha forte. Para obter mais informações, consulte [Senhas fortes](../../relational-databases/security/strong-passwords.md) e [Política de senha](../../relational-databases/security/password-policy.md). Começando pelo SQL Server 2012 (11.x), informações de senha armazenadas são calculadas usando SHA-512 da senha com valor de sal.

As senhas diferenciam maiúsculas de minúsculas. As senhas sempre devem ter pelo menos oito caracteres e não podem exceder 128 caracteres. Elas podem incluir caracteres de a-z, A-Z, 0-9, e a maioria dos caracteres não alfanuméricos. As senhas não podem conter aspas simples nem o *login_name*.

PASSWORD **=** *hashed\_password* Aplica-se somente à palavra-chave HASHED. Especifica o valor com hash da senha para o logon que está sendo criado.

HASHED Aplica-se apenas a logons do SQL Server. Especifica que a senha digitada depois do argumento PASSWORD já esteja com hash. Se esta opção não for selecionada, a cadeia de caracteres inserida como senha terá hash antes de ser armazenada no banco de dados. Essa opção deve ser usada somente para migrar bancos de dados de um servidor para outro. Não use a opção HASHED para criar novos logons. A opção HASHED não pode ser usada com os hashes criados pelo SQL 7 ou anterior.

MUST_CHANGE Aplica-se apenas a logons do SQL Server. Se esta opção estiver incluída, o SQL Server solicitará ao usuário uma nova senha quando o novo logon for usado pela primeira vez.

CREDENTIAL **=** _credential\_name_ O nome de uma credencial a ser mapeada para o novo logon do SQL Server. A credencial já deve existir no servidor. Atualmente, esta opção vincula apenas a credencial a um logon. Uma credencial não pode ser mapeada para o logon de Administrador do Sistema (sa).

SID = *sid* Usado para recriar um logon. Aplica-se apenas aos logons de autenticação do SQL Server, e não aos logons de autenticação do Windows. Especifica o SID do novo logon de autenticação do SQL Server. Se essa opção não for usada, o SQL Server atribuirá um SID automaticamente. A estrutura do SID depende da versão do SQL Server. SID de logon do SQL Server: um valor literal de 16 bytes (**binary(16)** ) baseado em um GUID. Por exemplo, `SID = 0x14585E90117152449347750164BA00A7`.

DEFAULT_DATABASE **=** _database_ Especifica o banco de dados padrão a ser atribuído ao logon. Se esta opção não for incluída, o banco de dados padrão será definido como master.

DEFAULT_LANGUAGE **=** _language_ Especifica o idioma padrão a ser atribuído ao logon. Se esta opção não for incluída, o idioma padrão será definido como o idioma padrão atual do servidor. Se o idioma padrão do servidor for alterado posteriormente, o idioma padrão do logon permanecerá inalterado.

CHECK_EXPIRATION **=** { ON | **OFF** } Aplica-se somente a logons do SQL Server. Especifica se a política de expiração de senha deve ser aplicada neste logon. O valor padrão é OFF.

CHECK_POLICY **=** { **ON** | OFF } Aplica-se somente a logons do SQL Server. Especifica se as políticas de senha do Windows do computador em que o SQL Server está em execução devem ser aplicadas neste logon. O valor padrão é ON.

Se a diretiva de Windows exigir senhas fortes, as senhas deverão conter pelo menos três das quatro características a seguir:

- Um caractere maiúsculo (A-Z).
- Um caractere minúsculo (a-z).
- Um dígito (0-9).
- Um dos caracteres não alfanuméricos, como um espaço, _, @, *, ^, %, !, $, # ou &.

WINDOWS Especifica que o logon seja mapeado para um logon do Windows.

CERTIFICATE *certname* Especifica o nome de um certificado a ser associado a este logon. Este certificado já deve ocorrer no banco de dados mestre.

ASYMMETRIC KEY *asym_key_name* Especifica o nome de uma chave assimétrica a ser associada este logon. Esta chave já deve ocorrer no banco de dados mestre.

## <a name="remarks"></a>Comentários

- As senhas diferenciam maiúsculas de minúsculas.
- O hash prévio de senhas tem suporte somente durante a criação de logons do SQL Server.
- Se MUST_CHANGE for especificado, CHECK_EXPIRATION e CHECK_POLICY deverão ser definidos como ON. Caso contrário, a instrução falhará.
- Não há suporte para uma combinação de CHECK_POLICY = OFF e CHECK_EXPIRATION = ON.
- Quando CHECK_POLICY é definida como OFF, *lockout_time* é redefinido e CHECK_EXPIRATION é definido como OFF.

> [!IMPORTANT]
> CHECK_EXPIRATION e CHECK_POLICY serão aplicados apenas no Windows Server 2003 e posteriores. Para obter mais informações, consulte [Password Policy](../../relational-databases/security/password-policy.md).

- Os logons criados a partir de certificados ou chaves assimétricas só são usados para assinatura de código. Eles não podem ser usados para a conexão com o SQL Server. Você pode criar um logon a partir de um certificado ou chave assimétrica somente quando o certificado ou a chave já existirem em master.
- Para um script transferir logons, consulte [Como transferir os logons e senhas entre instâncias do SQL Server 2005 e SQL Server 2008](https://support.microsoft.com/kb/918992).
- Criar um logon automaticamente habilita o novo logon e concede a ele a permissão **CONNECT SQL** de nível de servidor.
- O [modo de autenticação](../../relational-databases/security/choose-an-authentication-mode.md) do servidor deve corresponder ao tipo de logon para permitir o acesso.
- Para obter informações sobre como criar um sistema de permissões, veja [Introdução às permissões do mecanismo de banco de dados](../../relational-databases/security/authentication-access/getting-started-with-database-engine-permissions.md).

## <a name="permissions"></a>Permissões

- Apenas usuários com a permissão **ALTER ANY LOGIN** no servidor ou com associação na função de servidor fixa **securityadmin** podem criar logons. Para obter mais informações, confira [Funções de nível de servidor](/azure/sql-database/sql-database-manage-logins#groups-and-roles) e [ALTER SERVER ROLE](../../t-sql/statements/alter-server-role-transact-sql.md).
- Se a opção **CREDENTIAL** for usada, também será necessária a permissão **ALTER ANY CREDENTIAL** no servidor.

## <a name="after-creating-a-login"></a>Após criar um logon

Depois de criar um logon, ele poderá se conectar ao SQL Server, mas terá as permissões concedidas apenas à função **pública**. Execute algumas das atividades a seguir.

- Para conectar-se a um banco de dados, crie um usuário de banco de dados para o logon. Para obter mais informações, confira [CREATE USER](../../t-sql/statements/create-user-transact-sql.md).
- Crie uma função de servidor definida pelo usuário usando [CREATE SERVER ROLE](../../t-sql/statements/create-server-role-transact-sql.md). Use **ALTER SERVER ROLE** ... **ADD MEMBER** para adicionar o novo logon á função de servidor definida pelo usuário. Para obter mais informações, consulte [CREATE SERVER ROLE](../../t-sql/statements/create-server-role-transact-sql.md) e [ALTER SERVER ROLE](../../t-sql/statements/alter-server-role-transact-sql.md).
- Use **sp_addsrvrolemember** para adicionar o logon a uma função de servidor fixa. Para obter mais informações, consulte [Funções de nível de servidor](../../relational-databases/security/authentication-access/server-level-roles.md) e [sp_addsrvrolemember](../../relational-databases/system-stored-procedures/sp-addsrvrolemember-transact-sql.md).
- Use a instrução **GRANT** para conceder permissões do nível de servidor para o novo logon ou para uma função que contém o logon. Para obter mais informações, consulte [GRANT](../../t-sql/statements/grant-transact-sql.md).

## <a name="examples"></a>Exemplos

### <a name="a-creating-a-login-with-a-password"></a>a. Criando um logon com uma senha

O exemplo a seguir cria um logon para um usuário específico e atribui uma senha.

```sql
CREATE LOGIN <login_name> WITH PASSWORD = '<enterStrongPasswordHere>';
GO
```

### <a name="b-creating-a-login-with-a-password-that-must-be-changed"></a>B. Criando um logon com uma senha que precisa ser alterada

O exemplo a seguir cria um logon para um usuário específico e atribui uma senha. A opção `MUST_CHANGE` requer que os usuários alterem essa senha na primeira vez em que eles conectam ao servidor.

**Aplica-se a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e posterior.

```sql
CREATE LOGIN <login_name> WITH PASSWORD = '<enterStrongPasswordHere>'
    MUST_CHANGE, CHECK_EXPIRATION = ON;
GO
```

> [!NOTE]
> A opção MUST_CHANGE não pode ser usada quando CHECK_EXPIRATION estiver OFF.

### <a name="c-creating-a-login-mapped-to-a-credential"></a>C. Criando um logon mapeado para uma credencial

O exemplo a seguir cria o logon para um usuário específico usando o usuário. Esse logon é mapeado para a credencial.

**Aplica-se a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e posterior.

```sql
CREATE LOGIN <login_name> WITH PASSWORD = '<enterStrongPasswordHere>',
    CREDENTIAL = <credentialName>;
GO
```

### <a name="d-creating-a-login-from-a-certificate"></a>D. Criando um logon a partir de um certificado

O exemplo a seguir cria um logon para um usuário específico de um certificado em mestre.

**Aplica-se a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e posterior.

```sql
USE MASTER;
CREATE CERTIFICATE <certificateName>
    WITH SUBJECT = '<login_name> certificate in master database',
    EXPIRY_DATE = '12/05/2025';
GO
CREATE LOGIN <login_name> FROM CERTIFICATE <certificateName>;
GO
```

### <a name="e-creating-a-login-from-a-windows-domain-account"></a>E. Criando um logon a partir de uma conta de domínio do Windows

O exemplo a seguir cria um logon a partir de uma conta de domínio do Windows.

**Aplica-se a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e posterior.

```sql
CREATE LOGIN [<domainName>\<login_name>] FROM WINDOWS;
GO
```

### <a name="f-creating-a-login-from-a-sid"></a>F. Criando um logon por meio de um SID

O exemplo a seguir cria primeiro um logon de autenticação do SQL Server e determina seu SID.

```sql
CREATE LOGIN TestLogin WITH PASSWORD = 'SuperSecret52&&';
SELECT name, sid FROM sys.sql_logins WHERE name = 'TestLogin';
GO
```

Minha consulta retorna 0x241C11948AEEB749B0D22646DB1A19F2 como o SID. Sua consulta retornará um valor diferente. As instruções a seguir excluem o logon e depois o recriam. Use o SID da consulta anterior.

```sql
DROP LOGIN TestLogin;
GO

CREATE LOGIN TestLogin
WITH PASSWORD = 'SuperSecret52&&', SID = 0x241C11948AEEB749B0D22646DB1A19F2;

SELECT * FROM sys.sql_logins WHERE name = 'TestLogin';
GO
```

### <a name="g-creating-a-login-with-multiple-arguments"></a>G. Como criar um logon com vários argumentos

O exemplo a seguir mostra como encadear vários argumentos usando vírgulas entre cada argumento.

```sql
CREATE LOGIN [MyUser]
WITH PASSWORD = 'MyPassword',
DEFAULT_DATABASE = MyDatabase,
CHECK_POLICY = OFF,
CHECK_EXPIRATION = OFF ;
```

## <a name="see-also"></a>Consulte Também

- [Guia de Introdução às permissões do mecanismo de banco de dados](../../relational-databases/security/authentication-access/getting-started-with-database-engine-permissions.md)
- [Entidades](../../relational-databases/security/authentication-access/principals-database-engine.md)
- [Política de senha](../../relational-databases/security/password-policy.md)
- [ALTER LOGIN](../../t-sql/statements/alter-login-transact-sql.md)
- [DROP LOGIN](../../t-sql/statements/drop-login-transact-sql.md)
- [EVENTDATA](../../t-sql/functions/eventdata-transact-sql.md)
- [Criar um logon](../../relational-databases/security/authentication-access/create-a-login.md)

::: moniker-end
::: moniker range="=azuresqldb-current"

:::row:::
    :::column:::
        [SQL Server](create-login-transact-sql.md?view=sql-server-ver15&preserve-view=true)
    :::column-end:::
    :::column:::
        **_\* Banco de Dados SQL do Azure \*_**
    :::column-end:::
    :::column:::
        [Instância Gerenciada<br />de SQL do Azure](create-login-transact-sql.md?view=azuresqldb-mi-current)
    :::column-end:::
    :::column:::
        [Azure Synapse<br />Analytics](create-login-transact-sql.md?view=azure-sqldw-latest)
    :::column-end:::
    :::column:::
        [Analytics Platform<br />System (PDW)](create-login-transact-sql.md?view=aps-pdw-2016&preserve-view=true)
    :::column-end:::
:::row-end:::

&nbsp;

## <a name="sql-database"></a>Banco de Dados SQL

## <a name="syntax"></a>Sintaxe

```syntaxsql
-- Syntax for Azure SQL Database
CREATE LOGIN login_name
 { WITH <option_list> }

<option_list> ::=
    PASSWORD = { 'password' }
    [ , SID = sid ]
```

## <a name="arguments"></a>Argumentos

*login_name* Especifica o nome do logon criado. Os bancos de dados individuais e em pool no Banco de Dados SQL do Azure e os bancos de dados no [!INCLUDE[ssSDW](../../includes/sssdwfull-md.md)] dão suporte apenas para logons do SQL. Para criar contas para usuários do Azure Active Directory ou para criar contas de usuário não associadas a um logon, use a instrução [CREATE USER](create-user-transact-sql.md). Para obter mais informações, confira [Gerenciar logons no Banco de Dados SQL do Azure](/azure/sql-database/sql-database-manage-logins).

PASSWORD **='** password* *'* Especifica a senha do logon do SQL que está sendo criado. Use uma senha forte. Para obter mais informações, consulte [Senhas fortes](../../relational-databases/security/strong-passwords.md) e [Política de senha](../../relational-databases/security/password-policy.md). Começando com [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]armazenadas, informações de senha armazenadas são calculadas usando SHA-512 da senha com valor de sal.

As senhas diferenciam maiúsculas de minúsculas. As senhas sempre devem ter pelo menos oito caracteres e não podem exceder 128 caracteres. Elas podem incluir caracteres de a-z, A-Z, 0-9, e a maioria dos caracteres não alfanuméricos. As senhas não podem conter aspas simples nem o *login_name*.

SID = *sid* Usado para recriar um logon. Aplica-se apenas aos logons de autenticação do SQL Server, e não aos logons de autenticação do Windows. Especifica o SID do novo logon de autenticação do SQL Server. Se essa opção não for usada, o SQL Server atribuirá um SID automaticamente. A estrutura do SID depende da versão do SQL Server. Para o Banco de Dados SQL, trata-se de um literal de 32 bytes (**binary(32)** ) que consiste em `0x01060000000000640000000000000000`, além de 16 bytes que representam um GUID. Por exemplo, `SID = 0x0106000000000064000000000000000014585E90117152449347750164BA00A7`.

## <a name="remarks"></a>Comentários

- As senhas diferenciam maiúsculas de minúsculas.
- Criar um logon automaticamente habilita o novo logon e concede a ele a permissão **CONNECT SQL** de nível de servidor.

> [!IMPORTANT]
> Confira [Gerenciar logons no Banco de Dados SQL do Azure](/azure/sql-database/sql-database-manage-logins) para obter informações sobre como trabalhar com logons e usuários no Banco de Dados SQL do Azure.

## <a name="login"></a>Logon

### <a name="sql-database-logins"></a>Logons de banco de dados SQL

A instrução **CREATE LOGIN** deve ser a única instrução em um lote.

Em alguns métodos de conexão com o Banco de Dados SQL, como **sqlcmd**, é necessário acrescentar o nome do servidor do Banco de Dados SQL ao nome do logon na cadeia de conexão usando a notação *\<login>* @ *\<server>* . Por exemplo, se o seu logon for `login1` e o nome totalmente qualificado do servidor do Banco de Dados SQL for `servername.database.windows.net`, o parâmetro *username* da cadeia de conexão deverá ser `login1@servername`. Como o comprimento total do parâmetro *username* é 128 caracteres, *login_name* é limitado a 127 caracteres menos o comprimento do nome de servidor. No exemplo, `login_name` pode ter apenas 117 caracteres porque `servername` tem 10 caracteres.

No Banco de Dados SQL, você deve estar conectado ao banco de dados mestre com as permissões apropriadas para criar um logon. Para obter mais informações, confira [Criar logons e usuários adicionais com permissões administrativas](/azure/sql-database/sql-database-manage-logins#create-additional-logins-and-users-having-administrative-permissions).

As regras do SQL Server permitem criar um logon de autenticação do SQL Server no formato \<loginname>@\<servername>. Se seu servidor do [!INCLUDE[ssSDS](../../includes/sssds-md.md)] for **myazureserver** e o logon for **myemail@live.com** , você deverá fornecer seu logon como **myemail@live.com@myazureserver** .

No Banco de Dados SQL, os dados de logon necessários para autenticar uma conexão e as regras de firewall no nível de servidor são armazenados em cache temporariamente em cada banco de dados. Esse cache é atualizado periodicamente. Para forçar uma atualização do cache de autenticação e garantir que um banco de dados tenha a versão mais recente da tabela de logons, execute [DBCC FLUSHAUTHCACHE](../../t-sql/database-console-commands/dbcc-flushauthcache-transact-sql.md).

## <a name="permissions"></a>Permissões

Somente o logon da entidade de segurança no nível do servidor (criado pelo processo de provisionamento) ou membros da função de banco de dados `loginmanager` no banco de dados mestre podem criar novos logons. Para obter mais informações, confira [Criar logons e usuários adicionais com permissões administrativas](/azure/sql-database/sql-database-manage-logins#create-additional-logins-and-users-having-administrative-permissions).

## <a name="examples"></a>Exemplos

### <a name="a-creating-a-login-with-a-password"></a>a. Criando um logon com uma senha

O exemplo a seguir cria um logon para um usuário específico e atribui uma senha.

```sql
CREATE LOGIN <login_name> WITH PASSWORD = '<enterStrongPasswordHere>';
GO
```

### <a name="b-creating-a-login-from-a-sid"></a>B. Criando um logon por meio de um SID

O exemplo a seguir cria primeiro um logon de autenticação do SQL Server e determina seu SID.

```sql
CREATE LOGIN TestLogin WITH PASSWORD = 'SuperSecret52&&';

SELECT name, sid FROM sys.sql_logins WHERE name = 'TestLogin';
GO
```

Minha consulta retorna 0x241C11948AEEB749B0D22646DB1A19F2 como o SID. Sua consulta retornará um valor diferente. As instruções a seguir excluem o logon e depois o recriam. Use o SID da consulta anterior.

```sql
DROP LOGIN TestLogin;
GO

CREATE LOGIN TestLogin
WITH PASSWORD = 'SuperSecret52&&', SID = 0x241C11948AEEB749B0D22646DB1A19F2;

SELECT * FROM sys.sql_logins WHERE name = 'TestLogin';
GO
```

## <a name="see-also"></a>Consulte Também

- [Guia de Introdução às permissões do mecanismo de banco de dados](../../relational-databases/security/authentication-access/getting-started-with-database-engine-permissions.md)
- [Entidades](../../relational-databases/security/authentication-access/principals-database-engine.md)
- [Política de senha](../../relational-databases/security/password-policy.md)
- [ALTER LOGIN](../../t-sql/statements/alter-login-transact-sql.md)
- [DROP LOGIN](../../t-sql/statements/drop-login-transact-sql.md)
- [EVENTDATA](../../t-sql/functions/eventdata-transact-sql.md)
- [Criar um logon](../../relational-databases/security/authentication-access/create-a-login.md)

::: moniker-end
::: moniker range="=azuresqldb-mi-current"

:::row:::
    :::column:::
        [SQL Server](create-login-transact-sql.md?view=sql-server-ver15&preserve-view=true)
    :::column-end:::
    :::column:::
        [Banco de Dados SQL do Azure](create-login-transact-sql.md?view=azuresqldb-current)
    :::column-end:::
    :::column:::
        **_\* Instância Gerenciada<br />de SQL do Azure \*_**
    :::column-end:::
    :::column:::
        [Azure Synapse<br />Analytics](create-login-transact-sql.md?view=azure-sqldw-latest)
    :::column-end:::
    :::column:::
        [Analytics Platform<br />System (PDW)](create-login-transact-sql.md?view=aps-pdw-2016&preserve-view=true)
    :::column-end:::
:::row-end:::

&nbsp;

## <a name="azure-sql-managed-instance"></a>Instância Gerenciada do Azure SQL

## <a name="syntax"></a>Sintaxe

```syntaxsql
-- Syntax for Azure SQL Managed Instance
CREATE LOGIN login_name [FROM EXTERNAL PROVIDER] { WITH <option_list> [,..]}

<option_list> ::=
    PASSWORD = {'password'}
    | SID = sid
    | DEFAULT_DATABASE = database
    | DEFAULT_LANGUAGE = language
```

## <a name="arguments"></a>Argumentos

*login_name* Quando usado com a cláusula **FROM EXTERNAL PROVIDER**, o logon especifica a Entidade de Segurança do Azure AD (Active Directory), que é um usuário, um grupo ou um aplicativo do Azure AD. Caso contrário, o logon representa o nome do logon SQL que foi criado.

FROM EXTERNAL PROVIDER </br>
Especifica que o logon é para Autenticação do Azure AD.

PASSWORD **=** '*password*' Especifica a senha do logon do SQL que está sendo criado. Use uma senha forte. Para obter mais informações, consulte [Senhas fortes](../../relational-databases/security/strong-passwords.md) e [Política de senha](../../relational-databases/security/password-policy.md). Começando com [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]armazenadas, informações de senha armazenadas são calculadas usando SHA-512 da senha com valor de sal.

As senhas diferenciam maiúsculas de minúsculas. As senhas devem ter sempre no mínimo dez caracteres e não podem exceder 128 caracteres. Elas podem incluir caracteres de a-z, A-Z, 0-9, e a maioria dos caracteres não alfanuméricos. As senhas não podem conter aspas simples nem o *login_name*.

SID **=** *sid* Usado para recriar um logon. Aplica-se apenas a logons de autenticação do SQL Server. Especifica o SID do novo logon de autenticação do SQL Server. Se essa opção não for usada, o SQL Server atribuirá um SID automaticamente. A estrutura do SID depende da versão do SQL Server. Para o Banco de Dados SQL, trata-se de um literal de 32 bytes (**binary(32)** ) que consiste em `0x01060000000000640000000000000000`, além de 16 bytes que representam um GUID. Por exemplo, `SID = 0x0106000000000064000000000000000014585E90117152449347750164BA00A7`.

## <a name="remarks"></a>Comentários

- As senhas diferenciam maiúsculas de minúsculas.
- A nova sintaxe é introduzida para a criação de entidades de segurança no nível de servidor mapeadas para contas do Azure AD (**FROM EXTERNAL PROVIDER**)
- Quando **FROM EXTERNAL PROVIDER** é especificado:

  - O login_name deve representar uma conta existente do Azure AD (usuário, grupo ou aplicativo) acessível no Azure AD pela atual instância gerenciada do SQL. Para entidades de segurança do Azure Active Directory, a sintaxe de CREATE LOGIN exige:
    - UserPrincipalName do objeto do Azure AD para usuários do Azure AD.
    - DisplayName do objeto do Azure Active Directory para Grupos e Aplicativos do Azure AD.
  - A opção **PASSWORD** não pode ser usada.
- Por padrão, quando a cláusula **FROM EXTERNAL PROVIDER** é omitida, um logon SQL regular é criado.
- Logons do Azure AD são visíveis em sys.server_principals, com valor de coluna de tipo definido como **E** e type_desc definido como **EXTERNAL_LOGIN** para logons mapeados para os usuários do Azure AD ou o valor de coluna de tipo definido como **X** e o valor type_desc definido como **EXTERNAL_GROUP** para logons mapeados para grupos do Azure AD.
- Para um script transferir logons, consulte [Como transferir os logons e senhas entre instâncias do SQL Server 2005 e SQL Server 2008](https://support.microsoft.com/kb/918992).
- Criar um logon automaticamente habilita o novo logon e concede a ele a permissão **CONNECT SQL** de nível de servidor.

> [!IMPORTANT]
> Confira [Gerenciar logons no Banco de Dados SQL do Azure](/azure/sql-database/sql-database-manage-logins) para obter informações sobre como trabalhar com logons e usuários no Banco de Dados SQL do Azure.

## <a name="logins-and-permissions"></a>Logons e permissões

Somente o logon da entidade de segurança no nível do servidor (criado pelo processo de provisionamento) ou membros da função de banco de dados `securityadmin` ou `sysadmin` no banco de dados mestre podem criar novos logons. Para obter mais informações, confira [Funções de nível de servidor](/azure/sql-database/sql-database-manage-logins#groups-and-roles) e [ALTER SERVER ROLE](../../t-sql/statements/alter-server-role-transact-sql.md).

Por padrão, a permissão padrão concedida para um logon do Azure AD recém-criado no mestre é: **CONNECT SQL** e **VIEW ANY DATABASE**.

### <a name="sql-managed-instance-logins"></a>Logons da Instância Gerenciada de SQL

- Devem ter a permissão **ALTER ANY LOGIN** no servidor ou associação naquela das funções de servidor fixadas `securityadmin` ou `sysadmin`. Somente uma conta do Azure AD (Azure Active Directory) com a permissão **ALTER ANY LOGIN** no servidor ou associação em uma dessas funções pode executar o comando create.
- Se o logon for uma Entidade de Segurança SQL, somente os logons que fizerem parte da função `sysadmin` poderão usar o comando create para criar logons para uma conta do Azure AD.
- Devem ser um membro do Azure AD dentro do mesmo diretório usado para a Instância Gerenciada do SQL do Azure.

## <a name="after-creating-a-login"></a>Após criar um logon

> [!NOTE]
> A funcionalidade de administrador do Azure AD para a Instância Gerenciada de SQL do Azure após a criação foi alterada. Para obter mais informações, confira [Nova funcionalidade de administrador do Azure AD para MI](/azure/sql-database/sql-database-aad-authentication-configure#new-azure-ad-admin-functionality-for-mi).

Após a criação de um logon, ele poderá se conectar a uma instância gerenciada, mas só terá as permissões concedidas à função **pública**. Execute algumas das atividades a seguir.

- Para criar um usuário do Azure AD de um logon do Azure AD, confira [CREATE USER](../../t-sql/statements/create-user-transact-sql.md).
- Para conceder permissões a um usuário em um banco de dados, use o **ALTER SERVER ROLE** ... Instrução **ADD MEMBER** para adicionar o usuário a uma das funções de banco de dados internas ou a uma função personalizada ou conceder permissões ao usuário diretamente usando a instrução [GRANT](../../t-sql/statements/grant-transact-sql.md). Para saber mais, confira [Funções não de administrador](/azure/sql-database/sql-database-manage-logins#non-administrator-users), [Funções administrativas adicionais de nível do servidor](/azure/sql-database/sql-database-manage-logins#additional-server-level-administrative-roles), [ALTER SERVER ROLE](../../t-sql/statements/alter-server-role-transact-sql.md) e instrução [GRANT](grant-transact-sql.md).
- Para conceder permissões em todo o servidor, crie um usuário de banco de dados no banco de dados mestre e use **ALTER SERVER ROLE** ... Instrução **ADD MEMBER** para adicionar o usuário a uma das funções administrativas do servidor. Para obter mais informações, consulte [Funções de nível de servidor](/azure/sql-database/sql-database-manage-logins#groups-and-roles), [ALTER SERVER ROLE](../../t-sql/statements/alter-server-role-transact-sql.md) e [Funções de servidor](/azure/sql-database/sql-database-manage-logins#additional-server-level-administrative-roles).
  - Use o comando a seguir para adicionar a função `sysadmin` a um logon do Azure AD: `ALTER SERVER ROLE sysadmin ADD MEMBER [AzureAD_Login_name]`
- Use a instrução **GRANT** para conceder permissões do nível de servidor para o novo logon ou para uma função que contém o logon. Para obter mais informações, consulte [GRANT](../../t-sql/statements/grant-transact-sql.md).

## <a name="limitations"></a>Limitações

- Não há suporte para definir um logon do Azure AD mapeado para um grupo do Azure AD como o proprietário do banco de dados.
- Não há suporte para a representação de entidades de segurança no nível do servidor do Azure AD usando outras entidades de segurança do Azure AD, como a cláusula [EXECUTE AS](execute-as-transact-sql.md).
- Somente entidades de segurança no nível do SQL Server (logons) que fazem parte do `sysadmin` podem executar as seguintes operações direcionadas a entidades de segurança do Azure AD:
  - EXECUTE AS USER
  - EXECUTE AS LOGIN
- Usuários externos (convidados) importados de outro diretório do Azure AD não podem ser configurados diretamente como um administrador do Azure AD para a Instância Gerenciada de SQL usando o portal do Azure. Em vez disso, ingresse o usuário externo em um grupo habilitado para segurança do Azure AD e configure o grupo como o administrador da instância. É possível usar o PowerShell ou CLI do Azure para definir usuários convidados individuais como o administrador da instância.
- O logon não é replicado para a instância secundária em um grupo de failover. O logon é salvo no banco de dados mestre, que é um banco de dados do sistema e, dessa forma, não é replicado geograficamente. Para resolver isso, o usuário deve criar um logon com o mesma SID na instância secundária.

```SQL
-- Code to create login on the secondary instance
CREATE LOGIN foo WITH PASSWORD = '<enterStrongPasswordHere>', SID = <login_sid>;
```

## <a name="examples"></a>Exemplos

### <a name="a-creating-a-login-with-a-password"></a>a. Criando um logon com uma senha

O exemplo a seguir cria um logon para um usuário específico e atribui uma senha.

 ```sql
 CREATE LOGIN <login_name> WITH PASSWORD = '<enterStrongPasswordHere>';
 GO
 ```

### <a name="b-creating-a-login-from-a-sid"></a>B. Criando um logon por meio de um SID

 O exemplo a seguir cria primeiro um logon de autenticação do SQL Server e determina seu SID.

 ```sql
 CREATE LOGIN TestLogin WITH PASSWORD = 'SuperSecret52&&';

 SELECT name, sid FROM sys.sql_logins WHERE name = 'TestLogin';
 GO
 ```

Minha consulta retorna 0x241C11948AEEB749B0D22646DB1A19F2 como o SID. Sua consulta retornará um valor diferente. As instruções a seguir excluem o logon e depois o recriam. Use o SID da consulta anterior.

 ```sql
 DROP LOGIN TestLogin;
 GO

 CREATE LOGIN TestLogin
 WITH PASSWORD = 'SuperSecret52&&', SID = 0x241C11948AEEB749B0D22646DB1A19F2;

 SELECT * FROM sys.sql_logins WHERE name = 'TestLogin';
 GO
 ```

### <a name="c-creating-a-login-for-a-local-azure-ad-account"></a>C. Criando um logon para uma conta local do Azure AD

 O exemplo a seguir cria um logon para conta do Azure AD joe@myaad.onmicrosoft.com que existe no Azure AD do *myaad*.

```sql
CREATE LOGIN [joe@myaad.onmicrosoft.com] FROM EXTERNAL PROVIDER
GO
```

### <a name="d-creating-a-login-for-a-federated-azure-ad-account"></a>D. Criando um logon para uma conta federada do Azure AD

 O exemplo a seguir cria um logon para uma conta federada do Azure AD bob@contoso.com que existe no Azure AD chamada *contoso*. O usuário Bob também pode ser um usuário convidado.

```sql
CREATE LOGIN [bob@contoso.com] FROM EXTERNAL PROVIDER
GO
```

### <a name="e-creating-a-login-for-an-azure-ad-group"></a>E. Criando um logon para um grupo do Azure AD

 O exemplo a seguir cria um logon para o grupo do Azure AD *mygroup* que existe no Azure AD do *myaad*

```sql
CREATE LOGIN [mygroup] FROM EXTERNAL PROVIDER
GO
```

### <a name="f-creating-a-login-for-an-azure-ad-application"></a>F. Criando um logon para um aplicativo do Azure AD

O exemplo a seguir cria um logon para o aplicativo do Azure AD *myapp* que existe no Azure AD do *myaad*

```sql
CREATE LOGIN [myapp] FROM EXTERNAL PROVIDER
```

### <a name="g-check-newly-added-logins"></a>G. Verificar logons adicionados recentemente

Para verificar o logon adicionado recentemente, execute o seguinte comando T-SQL:

```sql
SELECT *
FROM sys.server_principals;
GO
```

## <a name="see-also"></a>Consulte Também

- [Guia de Introdução às permissões do mecanismo de banco de dados](../../relational-databases/security/authentication-access/getting-started-with-database-engine-permissions.md)
- [Entidades](../../relational-databases/security/authentication-access/principals-database-engine.md)
- [Política de senha](../../relational-databases/security/password-policy.md)
- [ALTER LOGIN](../../t-sql/statements/alter-login-transact-sql.md)
- [DROP LOGIN](../../t-sql/statements/drop-login-transact-sql.md)
- [EVENTDATA](../../t-sql/functions/eventdata-transact-sql.md)
- [Criar um logon](../../relational-databases/security/authentication-access/create-a-login.md)

::: moniker-end
::: moniker range="=azure-sqldw-latest"

:::row:::
    :::column:::
        [SQL Server](create-login-transact-sql.md?view=sql-server-ver15&preserve-view=true)
    :::column-end:::
    :::column:::
        [Banco de Dados SQL do Azure](create-login-transact-sql.md?view=azuresqldb-current)
    :::column-end:::
    :::column:::
        [Instância Gerenciada<br />de SQL do Azure](create-login-transact-sql.md?view=azuresqldb-mi-current)
    :::column-end:::
    :::column:::
        **_\* Azure Synapse<br />Analytics \*_**
    :::column-end:::
    :::column:::
        [Analytics Platform<br />System (PDW)](create-login-transact-sql.md?view=aps-pdw-2016&preserve-view=true)
    :::column-end:::
:::row-end:::

&nbsp;

## <a name="azure-synapse-analytics"></a>Azure Synapse Analytics

## <a name="syntax"></a>Sintaxe

```syntaxsql
-- Syntax for Azure Synapse Analytics
CREATE LOGIN login_name
 { WITH <option_list> }

<option_list> ::=
    PASSWORD = { 'password' }
    [ , SID = sid ]
```

## <a name="arguments"></a>Argumentos

*login_name* Especifica o nome do logon criado. A Análise do SQL no Azure Synapse dá suporte apenas a logons do SQL. Para criar contas para usuários do Azure Active Directory, use a instrução [CREATE USER](create-user-transact-sql.md).

PASSWORD **='** password* *'* Especifica a senha do logon do SQL que está sendo criado. Use uma senha forte. Para obter mais informações, consulte [Senhas fortes](../../relational-databases/security/strong-passwords.md) e [Política de senha](../../relational-databases/security/password-policy.md). Começando com [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]armazenadas, informações de senha armazenadas são calculadas usando SHA-512 da senha com valor de sal.

As senhas diferenciam maiúsculas de minúsculas. As senhas sempre devem ter pelo menos oito caracteres e não podem exceder 128 caracteres. Elas podem incluir caracteres de a-z, A-Z, 0-9, e a maioria dos caracteres não alfanuméricos. As senhas não podem conter aspas simples nem o *login_name*.

 SID = *sid* Usado para recriar um logon. Aplica-se apenas aos logons de autenticação do SQL Server, e não aos logons de autenticação do Windows. Especifica o SID do novo logon de autenticação do SQL Server. Se essa opção não for usada, o SQL Server atribuirá um SID automaticamente. A estrutura do SID depende da versão do SQL Server. Para Análise de SQL, trata-se de um literal de 32 bytes (**binary(32)** ) que consiste em `0x01060000000000640000000000000000`, além de 16 bytes que representam um GUID. Por exemplo, `SID = 0x0106000000000064000000000000000014585E90117152449347750164BA00A7`.

## <a name="remarks"></a>Comentários

- As senhas diferenciam maiúsculas de minúsculas.
- Para um script transferir logons, consulte [Como transferir os logons e senhas entre instâncias do SQL Server 2005 e SQL Server 2008](https://support.microsoft.com/kb/918992).
- Criar um logon automaticamente habilita o novo logon e concede a ele a permissão **CONNECT SQL** de nível de servidor.
- O [modo de autenticação](../../relational-databases/security/choose-an-authentication-mode.md) do servidor deve corresponder ao tipo de logon para permitir o acesso.
- Para obter informações sobre como criar um sistema de permissões, veja [Introdução às permissões do mecanismo de banco de dados](../../relational-databases/security/authentication-access/getting-started-with-database-engine-permissions.md).

## <a name="logins"></a>Logons

A instrução **CREATE LOGIN** deve ser a única instrução em um lote.

Ao se conectar ao Azure Synapse usando ferramentas, como o **sqlcmd**, é necessário acrescentar o nome do servidor da Análise de SQL à ID de logon na cadeia de conexão usando a notação *\<login>* @ *\<server>* . Por exemplo, se o seu logon for `login1` e o nome totalmente qualificado do servidor da Análise de SQL for `servername.database.windows.net`, o parâmetro *username* da cadeia de conexão deverá ser `login1@servername`. Como o comprimento total do parâmetro *username* é 128 caracteres, *login_name* é limitado a 127 caracteres menos o comprimento do nome de servidor. No exemplo, `login_name` pode ter apenas 117 caracteres porque `servername` tem 10 caracteres.

Para criar um logon, você deve estar conectado ao banco de dados mestre.

As regras do SQL Server permitem criar um logon de autenticação do SQL Server no formato \<loginname>@\<servername>. Se seu servidor do [!INCLUDE[ssSDS](../../includes/sssds-md.md)] for **myazureserver** e o logon for **myemail@live.com** , você deverá fornecer seu logon como **myemail@live.com@myazureserver** .

Os dados de logon necessários para autenticar uma conexão e as regras de firewall no nível do servidor são armazenados em cache temporariamente em cada banco de dados. Esse cache é atualizado periodicamente. Para forçar uma atualização do cache de autenticação e garantir que um banco de dados tenha a versão mais recente da tabela de logons, execute [DBCC FLUSHAUTHCACHE](../../t-sql/database-console-commands/dbcc-flushauthcache-transact-sql.md).

Para saber mais sobre logons, confira [Gerenciar bancos de dados e logons](/azure/sql-database/sql-database-manage-logins).

## <a name="permissions"></a>Permissões

Somente o logon da entidade de segurança no nível do servidor (criado pelo processo de provisionamento) ou membros da função de banco de dados `loginmanager` no banco de dados mestre podem criar novos logons. Para obter mais informações, confira [Funções de nível de servidor](/azure/sql-database/sql-database-manage-logins#groups-and-roles) e [ALTER SERVER ROLE](../../t-sql/statements/alter-server-role-transact-sql.md).

## <a name="after-creating-a-login"></a>Após criar um logon

Depois de criar um logon, ele poderá se conectar ao Azure Synapse, mas terá as permissões concedidas apenas à função **pública**. Execute algumas das atividades a seguir.

- Para conectar-se a um banco de dados, crie um usuário de banco de dados para o logon. Para obter mais informações, confira [CREATE USER](../../t-sql/statements/create-user-transact-sql.md).
- Para conceder permissões a um usuário em um banco de dados, use o **ALTER SERVER ROLE** ... Instrução **ADD MEMBER** para adicionar o usuário a uma das funções de banco de dados internas ou a uma função personalizada ou conceder permissões ao usuário diretamente usando a instrução [GRANT](grant-transact-sql.md). Para saber mais, confira [Funções não de administrador](/azure/sql-database/sql-database-manage-logins#non-administrator-users), [Funções administrativas adicionais de nível do servidor](/azure/sql-database/sql-database-manage-logins#additional-server-level-administrative-roles), [ALTER SERVER ROLE](../../t-sql/statements/alter-server-role-transact-sql.md) e instrução [GRANT](grant-transact-sql.md).
- Para conceder permissões em todo o servidor, crie um usuário de banco de dados no banco de dados mestre e use **ALTER SERVER ROLE** ... Instrução **ADD MEMBER** para adicionar o usuário a uma das funções administrativas do servidor. Para obter mais informações, consulte [Funções de nível de servidor](/azure/sql-database/sql-database-manage-logins#groups-and-roles), [ALTER SERVER ROLE](../../t-sql/statements/alter-server-role-transact-sql.md) e [Funções de servidor](/azure/sql-database/sql-database-manage-logins#additional-server-level-administrative-roles).

- Use a instrução **GRANT** para conceder permissões do nível de servidor para o novo logon ou para uma função que contém o logon. Para obter mais informações, consulte [GRANT](../../t-sql/statements/grant-transact-sql.md).

## <a name="examples"></a>Exemplos

### <a name="a-creating-a-login-with-a-password"></a>a. Criando um logon com uma senha

O exemplo a seguir cria um logon para um usuário específico e atribui uma senha.

```sql
CREATE LOGIN <login_name> WITH PASSWORD = '<enterStrongPasswordHere>';
GO
```

### <a name="b-creating-a-login-from-a-sid"></a>B. Criando um logon por meio de um SID

 O exemplo a seguir cria primeiro um logon de autenticação do SQL Server e determina seu SID.

```sql
CREATE LOGIN TestLogin WITH PASSWORD = 'SuperSecret52&&';

SELECT name, sid FROM sys.sql_logins WHERE name = 'TestLogin';
GO
```

Minha consulta retorna 0x241C11948AEEB749B0D22646DB1A19F2 como o SID. Sua consulta retornará um valor diferente. As instruções a seguir excluem o logon e depois o recriam. Use o SID da consulta anterior.

```sql
DROP LOGIN TestLogin;
GO

CREATE LOGIN TestLogin
WITH PASSWORD = 'SuperSecret52&&', SID = 0x241C11948AEEB749B0D22646DB1A19F2;

SELECT * FROM sys.sql_logins WHERE name = 'TestLogin';
GO
```

## <a name="see-also"></a>Consulte Também

- [Guia de Introdução às permissões do mecanismo de banco de dados](../../relational-databases/security/authentication-access/getting-started-with-database-engine-permissions.md)
- [Entidades](../../relational-databases/security/authentication-access/principals-database-engine.md)
- [Política de senha](../../relational-databases/security/password-policy.md)
- [ALTER LOGIN](../../t-sql/statements/alter-login-transact-sql.md)
- [DROP LOGIN](../../t-sql/statements/drop-login-transact-sql.md)
- [EVENTDATA](../../t-sql/functions/eventdata-transact-sql.md)
- [Criar um logon](../../relational-databases/security/authentication-access/create-a-login.md)

::: moniker-end
::: moniker range=">=aps-pdw-2016"

:::row:::
    :::column:::
        [SQL Server](create-login-transact-sql.md?view=sql-server-ver15&preserve-view=true)
    :::column-end:::
    :::column:::
        [Banco de Dados SQL do Azure](create-login-transact-sql.md?view=azuresqldb-current)
    :::column-end:::
    :::column:::
        [Instância Gerenciada<br />de SQL do Azure](create-login-transact-sql.md?view=azuresqldb-mi-current)
    :::column-end:::
    :::column:::
        [Azure Synapse<br />Analytics](create-login-transact-sql.md?view=azure-sqldw-latest)
    :::column-end:::
    :::column:::
        **_\* Analytics<br />Platform System (PDW) \*_**
    :::column-end:::
:::row-end:::

&nbsp;

## <a name="analytics-platform-system"></a>Sistema de plataforma de análise

## <a name="syntax"></a>Sintaxe

```syntaxsql
-- Syntax for Analytics Platform System
CREATE LOGIN loginName { WITH <option_list1> | FROM WINDOWS }

<option_list1> ::=
    PASSWORD = { 'password' } [ MUST_CHANGE ]
    [ , <option_list> [ ,... ] ]
  
<option_list> ::=
      CHECK_EXPIRATION = { ON | OFF}
    | CHECK_POLICY = { ON | OFF}
```

## <a name="arguments"></a>Argumentos

*login_name* Especifica o nome do logon criado. Há quatro tipos de logons: logons do SQL Server, logons do Windows, logons mapeados por certificado e logons mapeados por chave assimétrica. Ao criar logons mapeados de uma conta de domínio do Windows, você deve usar o nome de logon de usuário de versões anteriores ao Windows 2000 no formato [\<domainName>\\<nome_de_logon>]. Você não pode usar um UPN no formato login_name@DomainName. Para obter um exemplo, consulte o exemplo D posteriormente neste artigo. Os logons de autenticação são do tipo **sysname** e devem estar em conformidade com as regras para [Identificadores](../../relational-databases/databases/database-identifiers.md) e não podem conter um ' **\\** '. Os logons do Windows podem conter um ' **\\** '. Os logons baseados em usuários do Active Directory estão limitados a nomes com menos de 21 caracteres.

PASSWORD **='** _password_' Aplica-se apenas a logons do SQL Server. Especifica a senha do logon que está sendo criado. Use uma senha forte. Para obter mais informações, consulte [Senhas fortes](../../relational-databases/security/strong-passwords.md) e [Política de senha](../../relational-databases/security/password-policy.md). Começando pelo SQL Server 2012 (11.x), informações de senha armazenadas são calculadas usando SHA-512 da senha com valor de sal.

As senhas diferenciam maiúsculas de minúsculas. As senhas sempre devem ter pelo menos oito caracteres e não podem exceder 128 caracteres. Elas podem incluir caracteres de a-z, A-Z, 0-9, e a maioria dos caracteres não alfanuméricos. As senhas não podem conter aspas simples nem o *login_name*.

MUST_CHANGE Aplica-se apenas a logons do SQL Server. Se esta opção estiver incluída, o SQL Server solicitará ao usuário uma nova senha quando o novo logon for usado pela primeira vez.

CHECK_EXPIRATION **=** { ON | **OFF** } Aplica-se somente a logons do SQL Server. Especifica se a política de expiração de senha deve ser aplicada neste logon. O valor padrão é OFF.

CHECK_POLICY **=** { **ON** | OFF } Aplica-se somente a logons do SQL Server. Especifica se as políticas de senha do Windows do computador em que o SQL Server está em execução devem ser aplicadas neste logon. O valor padrão é ON.

Se a diretiva de Windows exigir senhas fortes, as senhas deverão conter pelo menos três das quatro características a seguir:

- Um caractere maiúsculo (A-Z).
- Um caractere minúsculo (a-z).
- Um dígito (0-9).
- Um dos caracteres não alfanuméricos, como um espaço, _, @, *, ^, %, !, $, # ou &.

WINDOWS Especifica que o logon seja mapeado para um logon do Windows.

## <a name="remarks"></a>Comentários

- As senhas diferenciam maiúsculas de minúsculas.
- Se MUST_CHANGE for especificado, CHECK_EXPIRATION e CHECK_POLICY deverão ser definidos como ON. Caso contrário, a instrução falhará.
- Não há suporte para uma combinação de CHECK_POLICY = OFF e CHECK_EXPIRATION = ON.
- Quando CHECK_POLICY é definida como OFF, *lockout_time* é redefinido e CHECK_EXPIRATION é definido como OFF.

> [!IMPORTANT]
> CHECK_EXPIRATION e CHECK_POLICY serão aplicados apenas no Windows Server 2003 e posteriores. Para obter mais informações, consulte [Password Policy](../../relational-databases/security/password-policy.md).

- Para um script transferir logons, consulte [Como transferir os logons e senhas entre instâncias do SQL Server 2005 e SQL Server 2008](https://support.microsoft.com/kb/918992).
- Criar um logon automaticamente habilita o novo logon e concede a ele a permissão **CONNECT SQL** de nível de servidor.
- Para obter informações sobre como criar um sistema de permissões, veja [Introdução às permissões do mecanismo de banco de dados](../../relational-databases/security/authentication-access/getting-started-with-database-engine-permissions.md).

## <a name="permissions"></a>Permissões

Apenas usuários com a permissão **ALTER ANY LOGIN** no servidor ou com associação na função de servidor fixa **securityadmin** podem criar logons. Para obter mais informações, confira [Funções de nível de servidor](/azure/sql-database/sql-database-manage-logins#groups-and-roles) e [ALTER SERVER ROLE](../../t-sql/statements/alter-server-role-transact-sql.md).

## <a name="after-creating-a-login"></a>Após criar um logon

Depois de criar um logon, ele poderá se conectar ao Azure Synapse Analytics, mas terá as permissões concedidas apenas à função **pública**. Execute algumas das atividades a seguir.

- Para conectar-se a um banco de dados, crie um usuário de banco de dados para o logon. Para obter mais informações, confira [CREATE USER](../../t-sql/statements/create-user-transact-sql.md).
- Crie uma função de servidor definida pelo usuário usando [CREATE SERVER ROLE](../../t-sql/statements/create-server-role-transact-sql.md). Use **ALTER SERVER ROLE** ... **ADD MEMBER** para adicionar o novo logon á função de servidor definida pelo usuário. Para obter mais informações, consulte [CREATE SERVER ROLE](../../t-sql/statements/create-server-role-transact-sql.md) e [ALTER SERVER ROLE](../../t-sql/statements/alter-server-role-transact-sql.md).
- Use **sp_addsrvrolemember** para adicionar o logon a uma função de servidor fixa. Para obter mais informações, consulte [Funções de nível de servidor](../../relational-databases/security/authentication-access/server-level-roles.md) e [sp_addsrvrolemember](../../relational-databases/system-stored-procedures/sp-addsrvrolemember-transact-sql.md).
- Use a instrução **GRANT** para conceder permissões do nível de servidor para o novo logon ou para uma função que contém o logon. Para obter mais informações, consulte [GRANT](../../t-sql/statements/grant-transact-sql.md).

## <a name="examples"></a>Exemplos

### <a name="g-creating-a-sql-server-authentication-login-with-a-password"></a>G. Criando um logon de autenticação do SQL Server com uma senha

O exemplo a seguir cria o logon `Mary7` com senha `A2c3456`.

```sql
CREATE LOGIN Mary7 WITH PASSWORD = 'A2c3456$#' ;
```

### <a name="h-using-options"></a>H. Usando opções

O exemplo a seguir cria o logon `Mary8` com senha e alguns argumentos opcionais.

```sql
CREATE LOGIN Mary8 WITH PASSWORD = 'A2c3456$#' MUST_CHANGE,
CHECK_EXPIRATION = ON,
CHECK_POLICY = ON;
```

### <a name="i-creating-a-login-from-a-windows-domain-account"></a>I. Criando um logon a partir de uma conta de domínio do Windows

O exemplo a seguir cria um logon usando uma conta de domínio do Windows chamada `Mary` no domínio `Contoso`.

```sql
CREATE LOGIN [Contoso\Mary] FROM WINDOWS;
GO
```

## <a name="see-also"></a>Consulte Também

- [Guia de Introdução às permissões do mecanismo de banco de dados](../../relational-databases/security/authentication-access/getting-started-with-database-engine-permissions.md)
- [Entidades](../../relational-databases/security/authentication-access/principals-database-engine.md)
- [Política de senha](../../relational-databases/security/password-policy.md)
- [ALTER LOGIN](../../t-sql/statements/alter-login-transact-sql.md)
- [DROP LOGIN](../../t-sql/statements/drop-login-transact-sql.md)
- [EVENTDATA](../../t-sql/functions/eventdata-transact-sql.md)
- [Criar um logon](../../relational-databases/security/authentication-access/create-a-login.md)

---

::: moniker-end
