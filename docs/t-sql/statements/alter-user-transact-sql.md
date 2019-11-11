---
title: ALTER USER (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/06/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ALTER_USER_TSQL
- ALTER USER
dev_langs:
- TSQL
helpviewer_keywords:
- modifying database users
- ALTER USER statement
- renaming databases
- schemas [SQL Server], default
- database user names [SQL Server]
- names [SQL Server], database users
- default schemas
- modifying default schemas
ms.assetid: 344fc6ce-a008-47c8-a02e-47fae66cc590
author: VanMSFT
ms.author: vanto
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: edff69f8dfae4047cf935a290c56d1192a03a41e
ms.sourcegitcommit: baa40306cada09e480b4c5ddb44ee8524307a2ab
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/06/2019
ms.locfileid: "73659550"
---
# <a name="alter-user-transact-sql"></a>ALTER USER (Transact-SQL)

Renomeia um usuário de banco de dados ou altera seu esquema padrão.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)

## <a name="click-a-product"></a>Clique em um produto!

Na linha a seguir, clique em qualquer nome de produto de seu interesse. O clique exibe conteúdo diferente aqui nesta página da Web, apropriado para qualquer produto no qual você clicar.

::: moniker range=">=sql-server-2016||>=sql-server-linux-2017||=sqlallproducts-allversions"

||||||
|-|-|-|-|-|
|**_\* SQL Server \*_** &nbsp;|[Banco de dados individual/pool elástico<br />do Banco de Dados SQL](alter-user-transact-sql.md?view=azuresqldb-current)|[Instância gerenciada<br />do Banco de Dados SQL](alter-user-transact-sql.md?view=azuresqldb-mi-current)|[SQL Data<br />Warehouse](alter-user-transact-sql.md?view=azure-sqldw-latest)|[Analytics Platform<br />System (PDW)](alter-user-transact-sql.md?view=aps-pdw-2016)
||||||

&nbsp;

## <a name="sql-server"></a>SQL Server
  
## <a name="syntax"></a>Sintaxe  
  
```
-- Syntax for SQL Server
  
ALTER USER userName
     WITH <set_item> [ ,...n ]  
[;]  
  
<set_item> ::=
      NAME = newUserName
    | DEFAULT_SCHEMA = { schemaName | NULL }  
    | LOGIN = loginName  
    | PASSWORD = 'password' [ OLD_PASSWORD = 'oldpassword' ]  
    | DEFAULT_LANGUAGE = { NONE | <lcid> | <language name> | <language alias> }  
    | ALLOW_ENCRYPTED_VALUE_MODIFICATIONS = [ ON | OFF ]  
```
  
## <a name="arguments"></a>Argumentos

 *userName*  
 Especifica o nome pelo qual o usuário é identificado nesse banco de dados.  
  
 LOGIN **=** _loginName_  
 Mapeia novamente um usuário para outro logon alterando o SID (identificador de segurança) do usuário para corresponder ao SID do logon.  
  
 NAME **=** _newUserName_  
 Especifica o novo nome para o usuário. *newUserName* não deve existir no banco de dados atual.  
  
 DEFAULT_SCHEMA **=** { *schemaName* | NULL }  
 Especifica o primeiro esquema que será pesquisado pelo servidor quando ele resolver os nomes de objetos para este usuário. A configuração do esquema padrão como NULL remove um esquema padrão de um grupo do Windows. A opção NULL não pode ser usada com um usuário do Windows.  
  
 PASSWORD **=** '*password*'  
 **Aplica-se a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)].  
  
 Especifica a senha do logon do usuário que está sendo alterado. As senhas diferenciam maiúsculas de minúsculas.  
  
> [!NOTE]  
> Essa opção está disponível apenas para usuários contidos. Confira mais informações em [Bancos de dados independentes](../../relational-databases/databases/contained-databases.md) e [sp_migrate_user_to_contained &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-migrate-user-to-contained-transact-sql.md).  
  
 OLD_PASSWORD **=** _'oldpassword'_  
 **Aplica-se a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)].  
  
 A senha do usuário atual que será substituída por '*password*'. As senhas diferenciam maiúsculas de minúsculas. *OLD_PASSWORD* é necessária para alterar uma senha, a menos que você tenha a permissão **ALTER ANY USER**. Exigir *OLD_PASSWORD* impede que os usuários com a permissão **IMPERSONATION** alterem a senha.  
  
> [!NOTE]  
> Essa opção está disponível apenas para usuários contidos.
  
 DEFAULT_LANGUAGE **=** _{ NONE | \<lcid> | \<language name> | \<language alias> }_  
 **Aplica-se a**: do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Especifica um idioma padrão a ser atribuído ao usuário. Se essa opção não for definida como NONE, o idioma padrão será definido como o idioma padrão do banco de dados. Se o idioma padrão do banco de dados for alterado mais tarde, o idioma padrão do usuário permanecerá inalterado. *DEFAULT_LANGUAGE* pode ser a lcid (ID local), o nome do idioma ou o alias do idioma.  
  
> [!NOTE]  
> Essa opção pode ser especificada apenas em um banco de dados independente e apenas para usuários contidos.
  
 ALLOW_ENCRYPTED_VALUE_MODIFICATIONS = [ ON | **OFF** ]  
 **Aplica-se a**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
 Suprime as verificações de metadados criptográficos no servidor em operações de cópia em massa. Isso permite que o usuário copie em massa dados criptografados entre tabelas ou bancos de dados sem descriptografá-los. O padrão é OFF.  
  
> [!WARNING]  
> O uso inadequado dessa opção pode resultar em dados corrompidos. Para obter mais informações, veja [Migrar dados confidenciais protegidos por Always Encrypted](../../relational-databases/security/encryption/migrate-sensitive-data-protected-by-always-encrypted.md).
  
## <a name="remarks"></a>Remarks

 O esquema padrão será o primeiro esquema que será pesquisado pelo servidor ao resolver os nomes dos objetos para esse usuário de banco de dados. A não ser quando especificado de outra forma, o esquema padrão será o proprietário dos objetos criados pelo usuário de banco de dados.  
  
 Se o usuário tiver um esquema padrão, esse esquema será usado. Se o usuário não tiver um esquema padrão, mas for um membro de um grupo que tenha um esquema padrão, o esquema do grupo será usado. Se o usuário não tiver um esquema padrão e for membro de mais de um grupo, o esquema padrão do usuário será o do grupo do Windows com o menor principal_id e um esquema padrão definido explicitamente. Se nenhum esquema padrão puder ser determinado para um usuário, o esquema **dbo** será usado.  
  
 DEFAULT_SCHEMA pode ser definido como um esquema que não ocorre atualmente no banco de dados. Portanto, você pode atribuir um DEFAULT_SCHEMA a um usuário antes de o esquema ser criado.  
  
 Não é possível especificar DEFAULT_SCHEMA para um usuário que esteja mapeado para um certificado ou uma chave assimétrica.  
  
> [!IMPORTANT]  
> O valor de DEFAULT_SCHEMA será ignorado se o usuário for membro da função de servidor fixa **sysadmin**. Todos os membros da função de servidor fixa **sysadmin** têm um esquema padrão de `dbo`.
  
 É possível alterar o nome de um usuário que esteja mapeado para um grupo ou logon do Windows somente quando o SID do novo nome de usuário corresponde ao SID que está registrado no banco de dados. Essa verificação ajuda a prevenir a falsificação de logons do Windows no banco de dados.  
  
 Uma cláusula WITH LOGON habilita o remapeamento de um usuário para um logon diferente. Os usuários sem um logon, mapeados para um certificado ou mapeados para uma chave assimétrica não podem ser remapeados com essa cláusula. Somente os usuários do SQL e do Windows (ou grupos) podem ser remapeados. A cláusula WITH LOGIN não pode ser usada para alterar o tipo de usuário, como alterar uma conta do Windows para um logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 O nome do usuário será renomeado automaticamente para o nome de logon se as condições a seguir forem verdadeiras.  
  
- O usuário é um usuário do Windows.  
  
- O nome é um nome do Windows (contém uma barra invertida).  
  
- Nenhum novo nome foi especificado.  
  
- O nome atual difere do nome de logon.  
  
 Caso contrário, o usuário não será renomeado se o chamador não invocar também a cláusula NAME.  
  
O nome de um usuário mapeado para um logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], um certificado ou uma chave assimétrica não pode conter o caractere de barra invertida (\\).  
  
> [!CAUTION]  
> [!INCLUDE[ssCautionUserSchema](../../includes/sscautionuserschema-md.md)]  
  
## <a name="security"></a>Segurança  
  
> [!NOTE]  
> Um usuário com a permissão **ALTER ANY USER** pode alterar o esquema padrão de qualquer usuário. Um usuário que tenha um esquema alterado pode, sem perceber, selecionar dados da tabela incorreta ou executar código do esquema incorreto.
  
### <a name="permissions"></a>Permissões

 Para alterar o nome de um usuário requer a permissão **ALTER ANY USER**.  
  
 Alterar o logon de um usuário de destino requer a permissão **CONTROL** no banco de dados.  
  
 Para alterar um nome de usuário que tenha a permissão **CONTROL** no banco de dados, é necessário ter a permissão **CONTROL** no banco de dados.  
  
 Para alterar o esquema ou idioma padrão, é necessário ter a permissão **ALTER** no usuário. Os usuários podem alterar seu próprio esquema ou idioma padrão.  
  
## <a name="examples"></a>Exemplos  

Todos os exemplos são executados em um banco de dados do usuário.  

### <a name="a-changing-the-name-of-a-database-user"></a>A. Alterando o nome de um usuário de banco de dados

 O exemplo a seguir altera o nome do usuário do banco de dados `Mary5` para `Mary51`.  
  
```sql
ALTER USER Mary5 WITH NAME = Mary51;  
GO  
```  
  
### <a name="b-changing-the-default-schema-of-a-user"></a>B. Alterando o esquema padrão de um usuário

 O exemplo a seguir altera o esquema padrão do usuário `Mary51` para `Purchasing`.  
  
```sql
ALTER USER Mary51 WITH DEFAULT_SCHEMA = Purchasing;  
GO  
```  
  
### <a name="c-changing-several-options-at-once"></a>C. Alterando vários opções de uma vez

 O exemplo a seguir altera várias opções para um usuário de banco de dados contido em uma instrução.  
  
**Aplica-se a**: do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
```sql
ALTER USER Philip
WITH NAME = Philipe
    , DEFAULT_SCHEMA = Development
    , PASSWORD = 'W1r77TT98%ab@#' OLD_PASSWORD = 'New Devel0per'
    , DEFAULT_LANGUAGE  = French ;  
GO  
```  

## <a name="see-also"></a>Confira também

 - [CREATE USER &#40;Transact-SQL&#41;](../../t-sql/statements/create-user-transact-sql.md)
 - [DROP USER &#40;Transact-SQL&#41;](../../t-sql/statements/drop-user-transact-sql.md)
 - [Bancos de dados independentes](../../relational-databases/databases/contained-databases.md)
 - [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)
 - [sp_migrate_user_to_contained &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-migrate-user-to-contained-transact-sql.md)

::: moniker-end
::: moniker range="=azuresqldb-current||=sqlallproducts-allversions"

> ||||||
> |-|-|-|-|-|
> |[SQL Server](alter-user-transact-sql.md?view=sql-server-2017)|**_\* Banco de dados individual/pool elástico<br />do Banco de Dados SQL \*_**|[Instância gerenciada<br />do Banco de Dados SQL](alter-user-transact-sql.md?view=azuresqldb-mi-current)|[SQL Data<br />Warehouse](alter-user-transact-sql.md?view=azure-sqldw-latest)|[Analytics Platform<br />System (PDW)](alter-user-transact-sql.md?view=aps-pdw-2016)

&nbsp;

## <a name="azure-sql-database-single-databaseelastic-pool"></a>Banco de dados individual/pool elástico do Banco de Dados SQL do Azure

## <a name="syntax"></a>Sintaxe

```
-- Syntax for Azure SQL Database
  
ALTER USER userName
     WITH <set_item> [ ,...n ]  
  
<set_item> ::=
      NAME = newUserName
    | DEFAULT_SCHEMA = schemaName  
    | LOGIN = loginName  
    | ALLOW_ENCRYPTED_VALUE_MODIFICATIONS = [ ON | OFF ]
[;]  
  
-- Azure SQL Database Update Syntax  
ALTER USER userName
     WITH <set_item> [ ,...n ]  
[;]  
  
<set_item> ::=
      NAME = newUserName
    | DEFAULT_SCHEMA = { schemaName | NULL }  
    | LOGIN = loginName  
    | PASSWORD = 'password' [ OLD_PASSWORD = 'oldpassword' ]  
    | ALLOW_ENCRYPTED_VALUE_MODIFICATIONS = [ ON | OFF ]
  
-- SQL Database syntax when connected to a federation member  
ALTER USER userName  
     WITH <set_item> [ ,... n ]
[;]  
  
<set_item> ::=
     NAME = newUserName  
```  

## <a name="arguments"></a>Argumentos

 *userName*  
 Especifica o nome pelo qual o usuário é identificado nesse banco de dados.  
  
 LOGIN **=** _loginName_  
 Mapeia novamente um usuário para outro logon alterando o SID (identificador de segurança) do usuário para corresponder ao SID do logon.  
  
 Se a instrução ALTER USER for a única instrução em um lote SQL, o Banco de Dados SQL do Azure oferecerá suporte à cláusula WITH LOGIN. Se a instrução ALTER USER não for a única instrução em um lote SQL ou for executada no SQL dinâmico, a cláusula WITH LOGIN não terá suporte.  
  
 NAME **=** _newUserName_  
 Especifica o novo nome para o usuário. *newUserName* não deve existir no banco de dados atual.  
  
 DEFAULT_SCHEMA **=** { *schemaName* | NULL }  
 Especifica o primeiro esquema que será pesquisado pelo servidor quando ele resolver os nomes de objetos para este usuário. A configuração do esquema padrão como NULL remove um esquema padrão de um grupo do Windows. A opção NULL não pode ser usada com um usuário do Windows.  
  
 PASSWORD **=** '*password*'  
 **Aplica-se a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)].  
  
 Especifica a senha do logon do usuário que está sendo alterado. As senhas diferenciam maiúsculas de minúsculas.  
  
> [!NOTE]  
> Essa opção está disponível apenas para usuários contidos. Confira mais informações em [Bancos de dados independentes](../../relational-databases/databases/contained-databases.md) e [sp_migrate_user_to_contained &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-migrate-user-to-contained-transact-sql.md).
  
 OLD_PASSWORD **=** _'oldpassword'_  
 **Aplica-se a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)].  
  
 A senha do usuário atual que será substituída por '*password*'. As senhas diferenciam maiúsculas de minúsculas. *OLD_PASSWORD* é necessária para alterar uma senha, a menos que você tenha a permissão **ALTER ANY USER**. Exigir *OLD_PASSWORD* impede que os usuários com a permissão **IMPERSONATION** alterem a senha.  
  
> [!NOTE]  
> Essa opção está disponível apenas para usuários contidos.
  
 ALLOW_ENCRYPTED_VALUE_MODIFICATIONS = [ ON | **OFF** ]  
 **Aplica-se a**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
 Suprime as verificações de metadados criptográficos no servidor em operações de cópia em massa. Isso permite que o usuário copie em massa dados criptografado entre tabelas ou bancos de dados sem descriptografá-los. O padrão é OFF.  
  
> [!WARNING]  
> O uso inadequado dessa opção pode resultar em dados corrompidos. Para obter mais informações, veja [Migrar dados confidenciais protegidos por Always Encrypted](../../relational-databases/security/encryption/migrate-sensitive-data-protected-by-always-encrypted.md).
  
## <a name="remarks"></a>Remarks

 O esquema padrão será o primeiro esquema que será pesquisado pelo servidor ao resolver os nomes dos objetos para esse usuário de banco de dados. A não ser quando especificado de outra forma, o esquema padrão será o proprietário dos objetos criados pelo usuário de banco de dados.  
  
 Se o usuário tiver um esquema padrão, esse esquema padrão será usado. Se o usuário não tiver um esquema padrão, mas for um membro de um grupo que tenha um esquema padrão, o esquema do grupo será usado. Se o usuário não tiver um esquema padrão e for membro de mais de um grupo, o esquema padrão do usuário será o do grupo do Windows com o menor principal_id e um esquema padrão definido explicitamente. Se nenhum esquema padrão puder ser determinado para um usuário, o esquema **dbo** será usado.  
  
 DEFAULT_SCHEMA pode ser definido como um esquema que não ocorre atualmente no banco de dados. Portanto, você pode atribuir um DEFAULT_SCHEMA a um usuário antes de o esquema ser criado.  
  
 Não é possível especificar DEFAULT_SCHEMA para um usuário que esteja mapeado para um certificado ou uma chave assimétrica.  
  
> [!IMPORTANT]  
> O valor de DEFAULT_SCHEMA será ignorado se o usuário for membro da função de servidor fixa **sysadmin**. Todos os membros da função de servidor fixa **sysadmin** têm um esquema padrão de `dbo`.
  
 É possível alterar o nome de um usuário que esteja mapeado para um grupo ou logon do Windows somente quando o SID do novo nome de usuário corresponde ao SID que está registrado no banco de dados. Essa verificação ajuda a prevenir a falsificação de logons do Windows no banco de dados.  
  
 Uma cláusula WITH LOGON habilita o remapeamento de um usuário para um logon diferente. Os usuários sem um logon, mapeados para um certificado ou mapeados para uma chave assimétrica não podem ser remapeados com essa cláusula. Somente os usuários do SQL e do Windows (ou grupos) podem ser remapeados. A cláusula WITH LOGIN não pode ser usada para alterar o tipo de usuário, como alterar uma conta do Windows para um logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 O nome do usuário será renomeado automaticamente para o nome de logon se as condições a seguir forem verdadeiras.  
  
- O usuário é um usuário do Windows.  
  
- O nome é um nome do Windows (contém uma barra invertida).  
  
- Nenhum novo nome foi especificado.  
  
- O nome atual difere do nome de logon.  
  
 Caso contrário, o usuário não será renomeado se o chamador não invocar também a cláusula NAME.  
  
O nome de um usuário mapeado para um logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], um certificado ou uma chave assimétrica não pode conter o caractere de barra invertida (\\).  
  
> [!CAUTION]  
> [!INCLUDE[ssCautionUserSchema](../../includes/sscautionuserschema-md.md)]  
  
## <a name="security"></a>Segurança
  
> [!NOTE]  
> Um usuário com a permissão **ALTER ANY USER** pode alterar o esquema padrão de qualquer usuário. Um usuário que tenha um esquema alterado pode, sem perceber, selecionar dados da tabela incorreta ou executar código do esquema incorreto.  
  
### <a name="permissions"></a>Permissões

 Para alterar o nome de um usuário requer a permissão **ALTER ANY USER**.  
  
 Alterar o logon de um usuário de destino requer a permissão **CONTROL** no banco de dados.  
  
 Para alterar um nome de usuário que tenha a permissão **CONTROL** no banco de dados, é necessário ter a permissão **CONTROL** no banco de dados.  
  
 Para alterar o esquema ou idioma padrão, é necessário ter a permissão **ALTER** no usuário. Os usuários podem alterar seu próprio esquema ou idioma padrão.  
  
## <a name="examples"></a>Exemplos

Todos os exemplos são executados em um banco de dados do usuário.  

### <a name="a-changing-the-name-of-a-database-user"></a>A. Alterando o nome de um usuário de banco de dados

 O exemplo a seguir altera o nome do usuário do banco de dados `Mary5` para `Mary51`.  
  
```sql
ALTER USER Mary5 WITH NAME = Mary51;  
GO  
```  
  
### <a name="b-changing-the-default-schema-of-a-user"></a>B. Alterando o esquema padrão de um usuário

 O exemplo a seguir altera o esquema padrão do usuário `Mary51` para `Purchasing`.  
  
```sql
ALTER USER Mary51 WITH DEFAULT_SCHEMA = Purchasing;  
GO  
```  
  
### <a name="c-changing-several-options-at-once"></a>C. Alterando vários opções de uma vez

 O exemplo a seguir altera várias opções para um usuário de banco de dados contido em uma instrução.
  
```sql
ALTER USER Philip
WITH  NAME = Philipe
    , DEFAULT_SCHEMA = Development
    , PASSWORD = 'W1r77TT98%ab@#' OLD_PASSWORD = 'New Devel0per';
GO  
```  

## <a name="see-also"></a>Confira também

 - [CREATE USER &#40;Transact-SQL&#41;](../../t-sql/statements/create-user-transact-sql.md)
 - [DROP USER &#40;Transact-SQL&#41;](../../t-sql/statements/drop-user-transact-sql.md)
 - [Bancos de dados independentes](../../relational-databases/databases/contained-databases.md)
 - [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)
 - [sp_migrate_user_to_contained &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-migrate-user-to-contained-transact-sql.md)

::: moniker-end
::: moniker range="=azuresqldb-mi-current||=sqlallproducts-allversions"

> ||||||
> |-|-|-|-|-|
> |[SQL Server](alter-user-transact-sql.md?view=sql-server-2017)|[Banco de dados individual/pool elástico<br />do Banco de Dados SQL](alter-user-transact-sql.md?view=azuresqldb-current)|**_\* Instância gerenciada<br />do Banco de Dados SQL \*_**|[SQL Data<br />Warehouse](alter-user-transact-sql.md?view=azure-sqldw-latest)|[Analytics Platform<br />System (PDW)](alter-user-transact-sql.md?view=aps-pdw-2016)

&nbsp;

## <a name="azure-sql-database-managed-instance"></a>Instância gerenciada do Banco de Dados SQL do Azure

## <a name="syntax"></a>Sintaxe

> [!IMPORTANT]
> Há suporte apenas para as seguintes opções na instância gerenciada do Banco de Dados SQL do Azure ao aplicar aos usuários com logons do Azure AD: `DEFAULT_SCHEMA = { schemaName | NULL }` e `DEFAULT_LANGUAGE = { NONE | lcid | language name | language alias }`
> </br> </br> Há uma nova extensão de sintaxe que foi adicionada para ajudar a remapear os usuários em um banco de dados que foi migrado para a instância gerenciada. A sintaxe ALTER USER ajuda a mapear usuários de banco de dados em um domínio federado e sincronizado com o Azure AD, para logons do Azure AD.

```
-- Syntax for Azure SQL Database managed instance
ALTER USER userName
     { WITH <set_item> [ ,...n ] | FROM EXTERNAL PROVIDER }
[;]  
  
<set_item> ::=
      NAME = newUserName
    | DEFAULT_SCHEMA = { schemaName | NULL }  
    | LOGIN = loginName  
    | PASSWORD = 'password' [ OLD_PASSWORD = 'oldpassword' ]
    | DEFAULT_LANGUAGE = { NONE | <lcid> | <language name> | <language alias> }
    | ALLOW_ENCRYPTED_VALUE_MODIFICATIONS = [ ON | OFF ]
  
-- Users or groups that are migrated as federated and synchronized with Azure AD have the following syntax:

    /** Applies to Windows users that were migrated and have the following user names:
    - Windows user <domain\user>
    - Windows group <domain\MyWindowsGroup>
    - Windows alias <MyWindowsAlias>
    **/

ALTER USER userName  
     { WITH <set_item> [ ,...n ] | FROM EXTERNAL PROVIDER }
[;]  
  
<set_item> ::=
     NAME = newUserName
    | DEFAULT_SCHEMA = { schemaName | NULL }
    | LOGIN = loginName
    | DEFAULT_LANGUAGE = { NONE | <lcid> | <language name> | <language alias> }
```
  
## <a name="arguments"></a>Argumentos

 *userName*  
 Especifica o nome pelo qual o usuário é identificado nesse banco de dados.  
  
 LOGIN **=** _loginName_  
 Mapeia novamente um usuário para outro logon alterando o SID (identificador de segurança) do usuário para corresponder ao SID do logon.  
  
 Se a instrução ALTER USER for a única instrução em um lote SQL, o Banco de Dados SQL do Azure oferecerá suporte à cláusula WITH LOGIN. Se a instrução ALTER USER não for a única instrução em um lote SQL ou for executada no SQL dinâmico, a cláusula WITH LOGIN não terá suporte.  
  
 NAME **=** _newUserName_  
 Especifica o novo nome para o usuário. *newUserName* não deve existir no banco de dados atual.  
  
 DEFAULT_SCHEMA **=** { *schemaName* | NULL }  
 Especifica o primeiro esquema que será pesquisado pelo servidor quando ele resolver os nomes de objetos para este usuário. A configuração do esquema padrão como NULL remove um esquema padrão de um grupo do Windows. A opção NULL não pode ser usada com um usuário do Windows.  
  
 PASSWORD **=** '*password*' 
  
 Especifica a senha do logon do usuário que está sendo alterado. As senhas diferenciam maiúsculas de minúsculas.  
  
> [!NOTE]  
> Essa opção está disponível apenas para usuários contidos. Confira mais informações em [Bancos de dados independentes](../../relational-databases/databases/contained-databases.md) e [sp_migrate_user_to_contained &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-migrate-user-to-contained-transact-sql.md).
  
 OLD_PASSWORD **=** _'oldpassword'_
  
 A senha do usuário atual que será substituída por '*password*'. As senhas diferenciam maiúsculas de minúsculas. *OLD_PASSWORD* é necessária para alterar uma senha, a menos que você tenha a permissão **ALTER ANY USER**. Exigir *OLD_PASSWORD* impede que os usuários com a permissão **IMPERSONATION** alterem a senha.  
  
> [!NOTE]  
> Essa opção está disponível apenas para usuários contidos.
  
 DEFAULT_LANGUAGE **=** _{ NONE | \<lcid> | \<language name> | \<language alias> }_  
  
 Especifica um idioma padrão a ser atribuído ao usuário. Se essa opção não for definida como NONE, o idioma padrão será definido como o idioma padrão do banco de dados. Se o idioma padrão do banco de dados for alterado mais tarde, o idioma padrão do usuário permanecerá inalterado. *DEFAULT_LANGUAGE* pode ser a lcid (ID local), o nome do idioma ou o alias do idioma.  
  
> [!NOTE]  
> Essa opção pode ser especificada apenas em um banco de dados independente e apenas para usuários contidos.
  
 ALLOW_ENCRYPTED_VALUE_MODIFICATIONS = [ ON | **OFF** ]  
  
 Suprime as verificações de metadados criptográficos no servidor em operações de cópia em massa. Isso permite que o usuário copie em massa dados criptografados entre tabelas ou bancos de dados sem descriptografá-los. O padrão é OFF.  
  
> [!WARNING]  
> O uso inadequado dessa opção pode resultar em dados corrompidos. Para obter mais informações, veja [Migrar dados confidenciais protegidos por Always Encrypted](../../relational-databases/security/encryption/migrate-sensitive-data-protected-by-always-encrypted.md).
  
## <a name="remarks"></a>Remarks

 O esquema padrão será o primeiro esquema que será pesquisado pelo servidor ao resolver os nomes dos objetos para esse usuário de banco de dados. A não ser quando especificado de outra forma, o esquema padrão será o proprietário dos objetos criados pelo usuário de banco de dados.  
  
 Se o usuário tiver um esquema padrão, esse esquema padrão será usado. Se o usuário não tiver um esquema padrão, mas for um membro de um grupo que tenha um esquema padrão, o esquema do grupo será usado. Se o usuário não tiver um esquema padrão e for membro de mais de um grupo, o esquema padrão do usuário será o do grupo do Windows com o menor principal_id e um esquema padrão definido explicitamente. Se nenhum esquema padrão puder ser determinado para um usuário, o esquema **dbo** será usado.  
  
 DEFAULT_SCHEMA pode ser definido como um esquema que não ocorre atualmente no banco de dados. Portanto, você pode atribuir um DEFAULT_SCHEMA a um usuário antes de o esquema ser criado.  
  
 Não é possível especificar DEFAULT_SCHEMA para um usuário que esteja mapeado para um certificado ou uma chave assimétrica.  
  
> [!IMPORTANT]  
> O valor de DEFAULT_SCHEMA será ignorado se o usuário for membro da função de servidor fixa **sysadmin**. Todos os membros da função de servidor fixa **sysadmin** têm um esquema padrão de `dbo`.
  
 É possível alterar o nome de um usuário que esteja mapeado para um grupo ou logon do Windows somente quando o SID do novo nome de usuário corresponde ao SID que está registrado no banco de dados. Essa verificação ajuda a prevenir a falsificação de logons do Windows no banco de dados.  
  
 Uma cláusula WITH LOGON habilita o remapeamento de um usuário para um logon diferente. Os usuários sem um logon, mapeados para um certificado ou mapeados para uma chave assimétrica não podem ser remapeados com essa cláusula. Somente os usuários do SQL e do Windows (ou grupos) podem ser remapeados. A cláusula WITH LOGIN não pode ser usada para alterar o tipo de usuário, como alterar uma conta do Windows para um logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. A única exceção é ao alterar um usuário do Windows para um usuário do Azure AD.

> [!NOTE]
> As regras a seguir não se aplicam a usuários do Windows na instância gerenciada, pois não há suporte para a criação de logons do Windows na instância gerenciada. A opção WITH LOGIN só poderá ser usada se os logons do Azure AD estiverem presentes.
  
 O nome do usuário será renomeado automaticamente para o nome de logon se as condições a seguir forem verdadeiras.  
  
- O usuário é um usuário do Windows.  
  
- O nome é um nome do Windows (contém uma barra invertida).  
  
- Nenhum novo nome foi especificado.  
  
- O nome atual difere do nome de logon.  
  
 Caso contrário, o usuário não será renomeado se o chamador não invocar também a cláusula NAME.  
  
O nome de um usuário mapeado para um logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], um certificado ou uma chave assimétrica não pode conter o caractere de barra invertida (\\).  
  
> [!CAUTION]  
> [!INCLUDE[ssCautionUserSchema](../../includes/sscautionuserschema-md.md)]

### <a name="remarks-for-windows-users-in-sql-on-premises-migrated-to-managed-instance"></a>Comentários para usuários do Windows no SQL no local migrados para a instância gerenciada

Esses comentários se aplicam a autenticações como usuários do Windows que foram federados e sincronizados com o Azure AD.

> [!NOTE]
> O administrador do Azure AD para a funcionalidade de instância gerenciada após a criação ter sido alterada. Para obter mais informações, confira [Nova funcionalidade de Administrador do Azure AD para MI](/azure/sql-database/sql-database-aad-authentication-configure#new-azure-ad-admin-functionality-for-mi).

- A validação de usuários ou de grupos do Windows que são mapeados para o Azure AD é feita por padrão por meio da API do Graph em todas as versões da sintaxe ALTER USER usadas para fins de migração.
- Os usuários locais que receberam um alias (um nome diferente da conta original do Windows) manterão o nome com alias.
- Para a autenticação do Azure AD, o parâmetro LOGIN se aplica somente à instância gerenciada e não pode ser usada com o banco de dados SQL.
- Para exibir os logins de Entidades do Azure AD, use o seguinte comando: `select * from sys.server_principals`
    - Verifique se o tipo indicado do logon é `E` ou `X`.
- A opção PASSWORD não pode ser usada para usuários do Azure AD.
- Em todos os casos de migração, as funções e permissões de usuários ou grupos do Windows serão automaticamente transferidas para os novos usuários ou grupos do Azure AD.
- Uma nova extensão de sintaxe, **FROM EXTERNAL PROVIDER**, está disponível para alterar usuários e grupos do SQL local para usuários e grupos do Azure AD. O domínio do Windows deve ser federado com o Azure AD, e todos os membros do domínio do Windows devem existir no Azure AD ao usar essa extensão. A sintaxe **FROM EXTERNAL PROVIDER** se aplica à instância gerenciada e deve ser usada caso os usuários do Windows não tenham logons na instância do SQL original e precisem ser mapeados para usuários autônomos do banco de dados do Azure AD.
  - Nesse caso, o userName permitido pode ser:
    - Um usuário do Windows (_domain\user_).
    - Um grupo do Windows (_MyWidnowsGroup_).
    - Um alias do Windows (_MyWindowsAlias_).
  - O resultado do comando ALTER substitui o antigo nome de usuário pelo nome correspondente encontrado no Azure AD com base no SID original do userName antigo. O nome alterado é substituído e armazenado nos metadados do banco de dados:
    - (_domain\user_) será substituído por Azure AD user@domain.com.
    - (_domain\\MyWidnowsGroup_) será substituído pelo grupo do Azure AD.
    - (_MyWindowsAlias_) permanecerá inalterado, mas o SID desse usuário será verificado no Azure AD.

> [!NOTE]
> Se o SID do usuário original convertido para objectID não puder ser encontrado no Azure AD, o comando ALTER USER falhará.

- Para exibir usuários alterados, use o seguinte comando: `select * from sys.database_principals`
  - Verifique o tipo indicado de usuário `E` ou `X`.
- Quando NAME for usado para migrar usuários do Windows para usuários do Azure AD, as seguintes restrições se aplicarão:
  - Um LOGIN válido deve ser especificado.
  - O NAME será verificado no Azure AD e só poderá ser:
    - O nome do LOGIN.
    - Um alias – o nome não pode existir no Azure AD.
  - Em todos os outros casos, a sintaxe falhará.
  
## <a name="security"></a>Segurança
  
> [!NOTE]  
> Um usuário com a permissão **ALTER ANY USER** pode alterar o esquema padrão de qualquer usuário. Um usuário que tenha um esquema alterado pode, sem perceber, selecionar dados da tabela incorreta ou executar código do esquema incorreto.  
  
### <a name="permissions"></a>Permissões

 Para alterar o nome de um usuário requer a permissão **ALTER ANY USER**.  
  
 Alterar o logon de um usuário de destino requer a permissão **CONTROL** no banco de dados.  
  
 Para alterar um nome de usuário que tenha a permissão **CONTROL** no banco de dados, é necessário ter a permissão **CONTROL** no banco de dados.  
  
 Para alterar o esquema ou idioma padrão, é necessário ter a permissão **ALTER** no usuário. Os usuários podem alterar seu próprio esquema ou idioma padrão.  
  
## <a name="examples"></a>Exemplos

Todos os exemplos são executados em um banco de dados do usuário.  

### <a name="a-changing-the-name-of-a-database-user"></a>A. Alterando o nome de um usuário de banco de dados

 O exemplo a seguir altera o nome do usuário do banco de dados `Mary5` para `Mary51`.  
  
```sql
ALTER USER Mary5 WITH NAME = Mary51;  
GO  
```  
  
### <a name="b-changing-the-default-schema-of-a-user"></a>B. Alterando o esquema padrão de um usuário

 O exemplo a seguir altera o esquema padrão do usuário `Mary51` para `Purchasing`.  
  
```sql
ALTER USER Mary51 WITH DEFAULT_SCHEMA = Purchasing;  
GO  
```  
  
### <a name="c-changing-several-options-at-once"></a>C. Alterando vários opções de uma vez

 O exemplo a seguir altera várias opções para um usuário de banco de dados contido em uma instrução.  
  
```sql
ALTER USER Philip
WITH NAME = Philipe
    , DEFAULT_SCHEMA = Development
    , PASSWORD = 'W1r77TT98%ab@#' OLD_PASSWORD = 'New Devel0per'
    , DEFAULT_LANGUAGE  = French ;  
GO  
```

### <a name="d-map-the-user-in-the-database-to-an-azure-ad-login-after-migration"></a>D. Mapear o usuário no banco de dados para um logon do Azure AD após a migração

O exemplo a seguir remapeia o usuário, `westus/joe`, para um usuário do Azure AD, `joe@westus.com`. Este exemplo é para logons que já existem na instância gerenciada. Isso precisará ser executado depois que você concluir uma migração do banco de dados para a instância gerenciada e quiser usar o logon do Azure AD para autenticar.

```sql
ALTER USER [westus/joe] WITH LOGIN = joe@westus.com
```

### <a name="e-map-an-old-windows-user-in-the-database-without-a-login-in-managed-instance-to-an-azure-ad-user"></a>E. Mapear um antigo usuário do Windows no banco de dados sem um logon na instância gerenciada para um usuário do Azure AD

O exemplo a seguir remapeia o usuário, `westus/joe`, sem um logon, para um usuário do Azure AD, `joe@westus.com`. O usuário federado deve existir no Azure AD.

```sql
ALTER USER [westus/joe] FROM EXTERNAL PROVIDER
```

### <a name="f-map-the-user-alias-to-an-existing-azure-ad-login"></a>F. Mapear o alias de usuário para um logon existente do Azure AD

O exemplo a seguir remapeia o nome do usuário, de `westus\joe` para `joe_alias`. O logon do Azure AD correspondente neste caso é `joe@westus.com`.

```sql
ALTER USER [westus/joe] WITH LOGIN = joe@westus.com, name= joe_alias  
```

### <a name="g-map-a-windows-group-that-was-migrated-in-managed-instance-to-an-azure-ad-group"></a>G. Mapear um grupo do Windows que foi migrado na instância gerenciada para um grupo do Azure AD

O exemplo a seguir remapeia o grupo local antigo `westus\mygroup` para um grupo do Azure AD `mygroup` na instância gerenciada. O grupo deve existir no Azure AD.

```sql
ALTER USER [westus\mygroup] WITH LOGIN = mygroup
```

## <a name="see-also"></a>Confira também

 - [CREATE USER &#40;Transact-SQL&#41;](../../t-sql/statements/create-user-transact-sql.md)
 - [DROP USER &#40;Transact-SQL&#41;](../../t-sql/statements/drop-user-transact-sql.md)
 - [Bancos de dados independentes](../../relational-databases/databases/contained-databases.md)
 - [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)
 - [sp_migrate_user_to_contained &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-migrate-user-to-contained-transact-sql.md)
 - [Tutorial: Como migrar usuários e grupos locais do Windows no SQL Server para a instância gerenciada do Banco de Dados SQL do Azure usando a sintaxe T-SQL DDL](/azure/sql-database/tutorial-managed-instance-azure-active-directory-migration)

::: moniker-end
::: moniker range="=azure-sqldw-latest||=sqlallproducts-allversions"

> ||||||
> |-|-|-|-|-|
> |[SQL Server](alter-user-transact-sql.md?view=sql-server-2017)|[Banco de dados individual/pool elástico<br />do Banco de Dados SQL](alter-user-transact-sql.md?view=azuresqldb-current)|[Instância gerenciada<br />do Banco de Dados SQL](alter-user-transact-sql.md?view=azuresqldb-mi-current)|**_\* SQL Data<br />Warehouse \*_**|[Analytics Platform<br />System (PDW)](alter-user-transact-sql.md?view=aps-pdw-2016)

&nbsp;

## <a name="azure-sql-data-warehouse"></a>Azure SQL Data Warehouse

## <a name="syntax"></a>Sintaxe
  
```
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
ALTER USER userName
     WITH <set_item> [ ,...n ]  
  
<set_item> ::=
     NAME = newUserName
     | LOGIN = loginName  
     | DEFAULT_SCHEMA = schema_name  
[;]  
```  
  
## <a name="arguments"></a>Argumentos

 *userName*  
 Especifica o nome pelo qual o usuário é identificado nesse banco de dados.  
  
 LOGIN **=** _loginName_  
 Mapeia novamente um usuário para outro logon alterando o SID (identificador de segurança) do usuário para corresponder ao SID do logon.  
  
 Se a instrução ALTER USER for a única instrução em um lote SQL, o Banco de Dados SQL do Azure oferecerá suporte à cláusula WITH LOGIN. Se a instrução ALTER USER não for a única instrução em um lote SQL ou for executada no SQL dinâmico, a cláusula WITH LOGIN não terá suporte.  
  
 NAME **=** _newUserName_  
 Especifica o novo nome para o usuário. *newUserName* não deve existir no banco de dados atual.  
  
 DEFAULT_SCHEMA **=** { *schemaName* | NULL }  
 Especifica o primeiro esquema que será pesquisado pelo servidor quando ele resolver os nomes de objetos para este usuário. A configuração do esquema padrão como NULL remove um esquema padrão de um grupo do Windows.   A opção NULL não pode ser usada com um usuário do Windows.  
  
## <a name="remarks"></a>Remarks

 O esquema padrão será o primeiro esquema que será pesquisado pelo servidor ao resolver os nomes dos objetos para esse usuário de banco de dados. A não ser quando especificado de outra forma, o esquema padrão será o proprietário dos objetos criados pelo usuário de banco de dados.  
  
 Se o usuário tiver um esquema padrão, esse esquema padrão será usado. Se o usuário não tiver um esquema padrão, mas for um membro de um grupo que tenha um esquema padrão, o esquema do grupo será usado. Se o usuário não tiver um esquema padrão e for membro de mais de um grupo, o esquema padrão do usuário será o do grupo do Windows com o menor principal_id e um esquema padrão definido explicitamente. Se nenhum esquema padrão puder ser determinado para um usuário, o esquema **dbo** será usado.  
  
 DEFAULT_SCHEMA pode ser definido como um esquema que não ocorre atualmente no banco de dados. Portanto, você pode atribuir um DEFAULT_SCHEMA a um usuário antes de o esquema ser criado.  
  
 Não é possível especificar DEFAULT_SCHEMA para um usuário que esteja mapeado para um certificado ou uma chave assimétrica.  
  
> [!IMPORTANT]  
> O valor de DEFAULT_SCHEMA será ignorado se o usuário for membro da função de servidor fixa **sysadmin**. Todos os membros da função de servidor fixa **sysadmin** têm um esquema padrão de `dbo`.

 Uma cláusula WITH LOGON habilita o remapeamento de um usuário para um logon diferente. Os usuários sem um logon, mapeados para um certificado ou mapeados para uma chave assimétrica não podem ser remapeados com essa cláusula. Somente os usuários do SQL e do Windows (ou grupos) podem ser remapeados. A cláusula WITH LOGIN não pode ser usada para alterar o tipo de usuário, como alterar uma conta do Windows para um logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 O nome do usuário será renomeado automaticamente para o nome de logon se as condições a seguir forem verdadeiras.  

- Nenhum novo nome foi especificado.  
  
- O nome atual difere do nome de logon.  
  
 Caso contrário, o usuário não será renomeado se o chamador não invocar também a cláusula NAME.  
  
O nome de um usuário mapeado para um logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], um certificado ou uma chave assimétrica não pode conter o caractere de barra invertida (\\).  
  
> [!CAUTION]  
> [!INCLUDE[ssCautionUserSchema](../../includes/sscautionuserschema-md.md)]
  
## <a name="security"></a>Segurança
  
> [!NOTE]  
> Um usuário com a permissão **ALTER ANY USER** pode alterar o esquema padrão de qualquer usuário. Um usuário que tenha um esquema alterado pode, sem perceber, selecionar dados da tabela incorreta ou executar código do esquema incorreto.  
  
### <a name="permissions"></a>Permissões

 Para alterar o nome de um usuário requer a permissão **ALTER ANY USER**.  
  
 Alterar o logon de um usuário de destino requer a permissão **CONTROL** no banco de dados.  
  
 Para alterar um nome de usuário que tenha a permissão **CONTROL** no banco de dados, é necessário ter a permissão **CONTROL** no banco de dados.  
  
 Para alterar o esquema ou idioma padrão, é necessário ter a permissão **ALTER** no usuário. Os usuários podem alterar seu próprio esquema ou idioma padrão.  
  
## <a name="examples"></a>Exemplos

Todos os exemplos são executados em um banco de dados do usuário.  

### <a name="a-changing-the-name-of-a-database-user"></a>A. Alterando o nome de um usuário de banco de dados

 O exemplo a seguir altera o nome do usuário do banco de dados `Mary5` para `Mary51`.  
  
```sql
ALTER USER Mary5 WITH NAME = Mary51;  
GO  
```  
  
### <a name="b-changing-the-default-schema-of-a-user"></a>B. Alterando o esquema padrão de um usuário  
 O exemplo a seguir altera o esquema padrão do usuário `Mary51` para `Purchasing`.  
  
```sql
ALTER USER Mary51 WITH DEFAULT_SCHEMA = Purchasing;  
GO  
```

## <a name="see-also"></a>Confira também

 - [CREATE USER &#40;Transact-SQL&#41;](../../t-sql/statements/create-user-transact-sql.md)
 - [DROP USER &#40;Transact-SQL&#41;](../../t-sql/statements/drop-user-transact-sql.md)
 - [Bancos de dados independentes](../../relational-databases/databases/contained-databases.md)
 - [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)
 - [sp_migrate_user_to_contained &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-migrate-user-to-contained-transact-sql.md)

::: moniker-end
::: moniker range=">=aps-pdw-2016||=sqlallproducts-allversions"

> ||||||
> |-|-|-|-|-|
> |[SQL Server](alter-user-transact-sql.md?view=sql-server-2017)|[Banco de dados individual/pool elástico<br />do Banco de Dados SQL](alter-user-transact-sql.md?view=azuresqldb-current)|[Instância gerenciada<br />do Banco de Dados SQL](alter-user-transact-sql.md?view=azuresqldb-mi-current)|[SQL Data<br />Warehouse](alter-user-transact-sql.md?view=azure-sqldw-latest)|**_\* Analytics<br />Platform System (PDW) \*_**

&nbsp;

## <a name="analytics-platform-system"></a>Sistema de plataforma de análise

## <a name="syntax"></a>Sintaxe

```
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
ALTER USER userName
     WITH <set_item> [ ,...n ]  
  
<set_item> ::=
     NAME = newUserName
     | LOGIN = loginName  
     | DEFAULT_SCHEMA = schema_name  
[;]  
```  
  
## <a name="arguments"></a>Argumentos

 *userName*  
 Especifica o nome pelo qual o usuário é identificado nesse banco de dados.  
  
 LOGIN **=** _loginName_  
 Mapeia novamente um usuário para outro logon alterando o SID (identificador de segurança) do usuário para corresponder ao SID do logon.  
  
 Se a instrução ALTER USER for a única instrução em um lote SQL, o Banco de Dados SQL do Azure oferecerá suporte à cláusula WITH LOGIN. Se a instrução ALTER USER não for a única instrução em um lote SQL ou for executada no SQL dinâmico, a cláusula WITH LOGIN não terá suporte.  
  
 NAME **=** _newUserName_  
 Especifica o novo nome para o usuário. *newUserName* não deve existir no banco de dados atual.  
  
 DEFAULT_SCHEMA **=** { *schemaName* | NULL }  
 Especifica o primeiro esquema que será pesquisado pelo servidor quando ele resolver os nomes de objetos para este usuário. A configuração do esquema padrão como NULL remove um esquema padrão de um grupo do Windows.   A opção NULL não pode ser usada com um usuário do Windows.  
  
## <a name="remarks"></a>Remarks

 O esquema padrão será o primeiro esquema que será pesquisado pelo servidor ao resolver os nomes dos objetos para esse usuário de banco de dados. A não ser quando especificado de outra forma, o esquema padrão será o proprietário dos objetos criados pelo usuário de banco de dados.  
  
 Se o usuário tiver um esquema padrão, esse esquema padrão será usado. Se o usuário não tiver um esquema padrão, mas for um membro de um grupo que tenha um esquema padrão, o esquema do grupo será usado. Se o usuário não tiver um esquema padrão e for membro de mais de um grupo, o esquema padrão do usuário será o do grupo do Windows com o menor principal_id e um esquema padrão definido explicitamente. Se nenhum esquema padrão puder ser determinado para um usuário, o esquema **dbo** será usado.  
  
 DEFAULT_SCHEMA pode ser definido como um esquema que não ocorre atualmente no banco de dados. Portanto, você pode atribuir um DEFAULT_SCHEMA a um usuário antes de o esquema ser criado.  
  
 Não é possível especificar DEFAULT_SCHEMA para um usuário que esteja mapeado para um certificado ou uma chave assimétrica.  
  
> [!IMPORTANT]  
> O valor de DEFAULT_SCHEMA será ignorado se o usuário for membro da função de servidor fixa **sysadmin**. Todos os membros da função de servidor fixa **sysadmin** têm um esquema padrão de `dbo`.

 Uma cláusula WITH LOGON habilita o remapeamento de um usuário para um logon diferente. Os usuários sem um logon, mapeados para um certificado ou mapeados para uma chave assimétrica não podem ser remapeados com essa cláusula. Somente os usuários do SQL e do Windows (ou grupos) podem ser remapeados. A cláusula WITH LOGIN não pode ser usada para alterar o tipo de usuário, como alterar uma conta do Windows para um logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 O nome do usuário será renomeado automaticamente para o nome de logon se as condições a seguir forem verdadeiras.  

- Nenhum novo nome foi especificado.  
  
- O nome atual difere do nome de logon.  
  
 Caso contrário, o usuário não será renomeado se o chamador não invocar também a cláusula NAME.  
  
O nome de um usuário mapeado para um logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], um certificado ou uma chave assimétrica não pode conter o caractere de barra invertida (\\).  
  
> [!CAUTION]  
> [!INCLUDE[ssCautionUserSchema](../../includes/sscautionuserschema-md.md)]
  
## <a name="security"></a>Segurança
  
> [!NOTE]  
> Um usuário com a permissão **ALTER ANY USER** pode alterar o esquema padrão de qualquer usuário. Um usuário que tenha um esquema alterado pode, sem perceber, selecionar dados da tabela incorreta ou executar código do esquema incorreto.  
  
### <a name="permissions"></a>Permissões

 Para alterar o nome de um usuário requer a permissão **ALTER ANY USER**.  
  
 Alterar o logon de um usuário de destino requer a permissão **CONTROL** no banco de dados.  
  
 Para alterar um nome de usuário que tenha a permissão **CONTROL** no banco de dados, é necessário ter a permissão **CONTROL** no banco de dados.  
  
 Para alterar o esquema ou idioma padrão, é necessário ter a permissão **ALTER** no usuário. Os usuários podem alterar seu próprio esquema ou idioma padrão.  
  
## <a name="examples"></a>Exemplos

Todos os exemplos são executados em um banco de dados do usuário.  

### <a name="a-changing-the-name-of-a-database-user"></a>A. Alterando o nome de um usuário de banco de dados

 O exemplo a seguir altera o nome do usuário do banco de dados `Mary5` para `Mary51`.  
  
```sql
ALTER USER Mary5 WITH NAME = Mary51;  
GO  
```  
  
### <a name="b-changing-the-default-schema-of-a-user"></a>B. Alterando o esquema padrão de um usuário
 O exemplo a seguir altera o esquema padrão do usuário `Mary51` para `Purchasing`.  
  
```sql
ALTER USER Mary51 WITH DEFAULT_SCHEMA = Purchasing;  
GO  
```

## <a name="see-also"></a>Confira também

 - [CREATE USER &#40;Transact-SQL&#41;](../../t-sql/statements/create-user-transact-sql.md)
 - [DROP USER &#40;Transact-SQL&#41;](../../t-sql/statements/drop-user-transact-sql.md)
 - [Bancos de dados independentes](../../relational-databases/databases/contained-databases.md)
 - [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)
 - [sp_migrate_user_to_contained &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-migrate-user-to-contained-transact-sql.md)

::: moniker-end