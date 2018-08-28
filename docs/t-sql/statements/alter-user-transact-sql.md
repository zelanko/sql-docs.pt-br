---
title: ALTER USER (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/05/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
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
caps.latest.revision: 75
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: b8d97b5d3acebc633c231d7e27dcfa3c12c71209
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43110065"
---
# <a name="alter-user-transact-sql"></a>ALTER USER (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Renomeia um usuário de banco de dados ou altera seu esquema padrão.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
     WITH <set_item> [ ,… n ]   
[;]  
  
<set_item> ::=   
     NAME = newUserName  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
ALTER USER userName    
     WITH <set_item> [ ,...n ]  
  
<set_item> ::=   
     NAME =newUserName   
     | LOGIN =loginName  
     | DEFAULT_SCHEMA = schema_name  
[;]  
```  
  
## <a name="arguments"></a>Argumentos  
 *userName*  
 Especifica o nome pelo qual o usuário é identificado nesse banco de dados.  
  
 LOGIN **=***loginName*  
 Mapeia novamente um usuário para outro logon alterando o SID (identificador de segurança) do usuário para corresponder ao SID do logon.  
  
 Se a instrução ALTER USER for a única instrução em um lote SQL, o banco de dados SQL do Windows Azure oferecerá suporte à cláusula WITH LOGIN. Se a instrução ALTER USER não for a única instrução em um lote SQL ou for executada no SQL dinâmico, a cláusula WITH LOGIN não terá suporte.  
  
 NAME **=***newUserName*  
 Especifica o novo nome para o usuário. *newUserName* não deve existir no banco de dados atual.  
  
 DEFAULT_SCHEMA **=** { *schemaName* | NULL }  
 Especifica o primeiro esquema que será pesquisado pelo servidor quando ele resolver os nomes de objetos para este usuário. A configuração do esquema padrão como NULL remove um esquema padrão de um grupo do Windows.   A opção NULL não pode ser usada com um usuário do Windows.  
  
 PASSWORD **=** '*password*'  
 **Aplica-se a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)].  
  
 Especifica a senha do logon do usuário que está sendo alterado. As senhas diferenciam maiúsculas de minúsculas.  
  
> [!NOTE]  
>  Essa opção está disponível apenas para usuários contidos. Veja [bancos de dados independentes](../../relational-databases/databases/contained-databases.md) e [sp_migrate_user_to_contained &#40;Transact-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-migrate-user-to-contained-transact-sql.md) para obter mais informações.  
  
 OLD_PASSWORD **=***'oldpassword'*  
 **Aplica-se a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)].  
  
 A senha do usuário atual que será substituída por '*password*'. As senhas diferenciam maiúsculas de minúsculas. *OLD_PASSWORD* é necessária para alterar uma senha, a menos que você tenha a permissão **ALTER ANY USER**. Exigir *OLD_PASSWORD* impede que os usuários com a permissão **IMPERSONATION** alterem a senha.  
  
> [!NOTE]  
>  Essa opção está disponível apenas para usuários contidos.  
  
 DEFAULT_LANGUAGE **=***{ NONE | \<lcid> | \<language name> | \<language alias> }*  
 **Aplica-se a**: do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Especifica um idioma padrão a ser atribuído ao usuário. Se essa opção não for definida como NONE, o idioma padrão será definido como o idioma padrão do banco de dados. Se o idioma padrão do banco de dados for alterado mais tarde, o idioma padrão do usuário permanecerá inalterado. *DEFAULT_LANGUAGE* pode ser a lcid (ID local), o nome do idioma ou o alias do idioma.  
  
> [!NOTE]  
>  Essa opção pode ser especificada apenas em um banco de dados independente e apenas para usuários contidos.  
  
 ALLOW_ENCRYPTED_VALUE_MODIFICATIONS = [ ON | **OFF** ] ]  
 **Aplica-se a**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
 Suprime as verificações de metadados criptográficos no servidor em operações de cópia em massa. Isso permite que o usuário copie em massa dados criptografado entre tabelas ou bancos de dados sem descriptografá-los. O padrão é OFF.  
  
> [!WARNING]  
>  O uso inadequado dessa opção pode resultar em dados corrompidos. Para obter mais informações, veja [Migrar dados confidenciais protegidos por Always Encrypted](../../relational-databases/security/encryption/migrate-sensitive-data-protected-by-always-encrypted.md).  
  
## <a name="remarks"></a>Remarks  
 O esquema padrão será o primeiro esquema que será pesquisado pelo servidor ao resolver os nomes dos objetos para esse usuário de banco de dados. A não ser quando especificado de outra forma, o esquema padrão será o proprietário dos objetos criados pelo usuário de banco de dados.  
  
 Se o usuário tiver um esquema padrão, esse esquema padrão será usado. Se o usuário não tiver um esquema padrão, mas for um membro de um grupo que tenha um esquema padrão, o esquema padrão do grupo será usado. Se o usuário não tiver um esquema padrão e for membro de mais de um grupo, o esquema padrão do usuário será o do grupo do Windows com o menor principal_id e um esquema padrão definido explicitamente. Se nenhum esquema padrão puder ser determinado para um usuário, o esquema **dbo** será usado.  
  
 DEFAULT_SCHEMA pode ser definido como um esquema que não ocorre atualmente no banco de dados. Portanto, você pode atribuir um DEFAULT_SCHEMA a um usuário antes de o esquema ser criado.  
  
 Não é possível especificar DEFAULT_SCHEMA para um usuário que esteja mapeado para um certificado ou para uma chave assimétrica.  
  
> [!IMPORTANT]  
>  O valor de DEFAULT_SCHEMA será ignorado se o usuário for membro da função de servidor fixa **sysadmin**. Todos os membros da função de servidor fixa **sysadmin** têm um esquema padrão de `dbo`.  
  
 É possível alterar o nome de um usuário que esteja mapeado para um grupo ou logon do Windows somente quando o SID do novo nome de usuário corresponde ao SID que está registrado no banco de dados. Essa verificação ajuda a prevenir a falsificação de logons do Windows no banco de dados.  
  
 Uma cláusula WITH LOGON habilita o remapeamento de um usuário para um logon diferente. Os usuários sem um logon, mapeados para um certificado ou mapeados para uma chave assimétrica não podem ser remapeados com essa cláusula. Somente os usuários do SQL e do Windows (ou grupos) podem ser remapeados. A cláusula WITH LOGIN não pode ser usada para alterar o tipo de usuário, como alterar uma conta do Windows para um logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 O nome do usuário será renomeado automaticamente para o nome de logon se as condições a seguir forem verdadeiras.  
  
-   O usuário é um usuário do Windows.  
  
-   O nome é um nome do Windows (contém uma barra invertida).  
  
-   Nenhum novo nome foi especificado.  
  
-   O nome atual difere do nome de logon.  
  
 Caso contrário, o usuário não será renomeado se o chamador não invocar também a cláusula NAME.  
  
O nome de um usuário mapeado para um logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], um certificado ou uma chave assimétrica não pode conter o caractere de barra invertida (\\).  
  
> [!CAUTION]  
>  [!INCLUDE[ssCautionUserSchema](../../includes/sscautionuserschema-md.md)]  
  
## <a name="security"></a>Segurança  
  
> [!NOTE]  
>  Um usuário com a permissão **ALTER ANY USER** pode alterar o esquema padrão de qualquer usuário. Um usuário que tenha um esquema alterado pode, sem perceber, selecionar dados da tabela incorreta ou executar código do esquema incorreto.  
  
### <a name="permissions"></a>Permissões  
 Para alterar o nome de um usuário requer a permissão **ALTER ANY USER**.  
  
 Alterar o logon de um usuário de destino requer a permissão **CONTROL** no banco de dados.  
  
 Para alterar um nome de usuário que tenha a permissão **CONTROL** no banco de dados, é necessário ter a permissão **CONTROL** no banco de dados.  
  
 Para alterar o esquema ou idioma padrão, é necessário ter a permissão **ALTER** no usuário. Os usuários podem alterar seu próprio esquema ou idioma padrão.  
  
## <a name="examples"></a>Exemplos  

Todos os exemplos são executados em um banco de dados do usuário.  

### <a name="a-changing-the-name-of-a-database-user"></a>A. Alterando o nome de um usuário de banco de dados  
 O exemplo a seguir altera o nome do usuário do banco de dados `Mary5` para `Mary51`.  
  
```  
ALTER USER Mary5 WITH NAME = Mary51;  
GO  
```  
  
### <a name="b-changing-the-default-schema-of-a-user"></a>B. Alterando o esquema padrão de um usuário  
 O exemplo a seguir altera o esquema padrão do usuário `Mary51` para `Purchasing`.  
  
```  
ALTER USER Mary51 WITH DEFAULT_SCHEMA = Purchasing;  
GO  
```  
  
### <a name="c-changing-several-options-at-once"></a>C. Alterando vários opções de uma vez  
 O exemplo a seguir altera várias opções para um usuário de banco de dados contido em uma instrução.  
  
**Aplica-se a**: do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
```  
ALTER USER Philip   
WITH  NAME = Philipe   
    , DEFAULT_SCHEMA = Development   
    , PASSWORD = 'W1r77TT98%ab@#’ OLD_PASSWORD = 'New Devel0per'   
    , DEFAULT_LANGUAGE  = French ;  
GO  
```  
  
  
## <a name="see-also"></a>Consulte Também  
 [CREATE USER &#40;Transact-SQL&#41;](../../t-sql/statements/create-user-transact-sql.md)   
 [DROP USER &#40;Transact-SQL&#41;](../../t-sql/statements/drop-user-transact-sql.md)   
 [Bancos de dados independentes](../../relational-databases/databases/contained-databases.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [sp_migrate_user_to_contained &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-migrate-user-to-contained-transact-sql.md)  
  
  


