---
title: Permissões GRANT do banco de dados (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/22/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- granting permissions [SQL Server]
- database permissions [SQL Server]
- granting permissions [SQL Server], databases
- permissions [SQL Server], databases
- database permissions [SQL Server], granting
- GRANT statement, databases
ms.assetid: 499e5ed6-945c-4791-ab45-68dec0b9c289
author: VanMSFT
ms.author: vanto
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 7a73c0554c878aea4fa89ffb7170547d55271f15
ms.sourcegitcommit: e37636c275002200cf7b1e7f731cec5709473913
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/13/2019
ms.locfileid: "73982209"
---
# <a name="grant-database-permissions-transact-sql"></a>Permissões de banco de dados GRANT (Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Concede permissões em um banco de dados no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].

![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)

## <a name="syntax"></a>Sintaxe

```

GRANT <permission> [ ,...n ]
    TO <database_principal> [ ,...n ] [ WITH GRANT OPTION ]
    [ AS <database_principal> ]

<permission>::=
permission | ALL [ PRIVILEGES ]

<database_principal> ::=
    Database_user
  | Database_role
  | Application_role
  | Database_user_mapped_to_Windows_User
  | Database_user_mapped_to_Windows_Group
  | Database_user_mapped_to_certificate
  | Database_user_mapped_to_asymmetric_key
  | Database_user_with_no_login
```

## <a name="arguments"></a>Argumentos

*permission* Especifica uma permissão que pode ser concedida em um banco de dados. Para obter uma lista de permissões, consulte a seção Comentários mais adiante neste tópico.

ALL Esta opção não concede todas as permissões possíveis. A concessão ALL é equivalente a conceder as seguintes permissões: BACKUP DATABASE, BACKUP LOG, CREATE DATABASE, CREATE DEFAULT, CREATE FUNCTION, CREATE PROCEDURE, CREATE RULE, CREATE TABLE e CREATE VIEW.

PRIVILEGES Incluídos para conformidade com ISO. Não altera o comportamento de ALL.

WITH GRANT OPTION Indica que a entidade de segurança também terá a capacidade de conceder a permissão especificada a outros principais.

AS \<database_principal> Especifica uma entidade de segurança por meio da qual a entidade de segurança que executa essa consulta obtém seu direito de conceder a permissão.

*Database_user* Especifica um usuário de banco de dados.

*Database_role* Especifica uma função de banco de dados.

*Application_role*
**Aplica-se a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e posterior, [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]

Especifica uma função de aplicativo.

*Database_user_mapped_to_Windows_User*
**Aplica-se a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e posterior

Especifica um usuário do banco de dados mapeado para um usuário do Windows.

*Database_user_mapped_to_Windows_Group*
**Aplica-se a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e posterior

Especifica um usuário do banco de dados mapeado para um grupo do Windows.

*Database_user_mapped_to_certificate*
**Aplica-se a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e posterior

Especifica um usuário do banco de dados mapeado para um certificado.

*Database_user_mapped_to_asymmetric_key*
**Aplica-se a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e posterior

Especifica um usuário do banco de dados mapeado para uma chave assimétrica.

*Database_user_with_no_login* Especifica um usuário de banco de dados sem entidade de segurança no nível do servidor correspondente.

## <a name="remarks"></a>Remarks

> [!IMPORTANT]
> Uma combinação das permissões ALTER e REFERENCE em alguns casos pode permitir ao usuário autorizado exibir dados ou executar funções não autorizadas. Por exemplo: Um usuário com a permissão ALTER em uma tabela e a permissão REFERENCE em uma função pode criar uma coluna computada em uma função e fazer com que ela seja executada. Nesse caso, o usuário também precisará da permissão SELECT na coluna computada.

Um banco de dados é um protegível contido no servidor pai na hierarquia de permissões. As permissões mais específicas e limitadas que podem ser concedidas em um banco de dados são listadas na tabela a seguir, junto com as permissões mais gerais que as incluem implicitamente.

|Permissão de banco de dados|Implícito na permissão de banco de dados|Implícito na permissão de servidor|
|-------------------------|------------------------------------|----------------------------------|
|ADMINISTRAR OPERAÇÕES EM LOTE DO BANCO DE DADOS<br/>**Aplica-se ao:** [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)].|CONTROL|CONTROL SERVER|
|ALTER|CONTROL|ALTER ANY DATABASE|
|ALTER ANY APPLICATION ROLE|ALTER|CONTROL SERVER|
|ALTER ANY ASSEMBLY|ALTER|CONTROL SERVER|
|ALTER ANY ASYMMETRIC KEY|ALTER|CONTROL SERVER|
|ALTER ANY CERTIFICATE|ALTER|CONTROL SERVER|
|ALTER ANY COLUMN ENCRYPTION KEY|ALTER|CONTROL SERVER|
|ALTERAR QUALQUER DEFINIÇÃO DE CHAVE MESTRA DE COLUNA|ALTER|CONTROL SERVER|
|ALTER ANY CONTRACT|ALTER|CONTROL SERVER|
|ALTER ANY DATABASE AUDIT|ALTER|ALTER ANY SERVER AUDIT|
|ALTER ANY DATABASE DDL TRIGGER|ALTER|CONTROL SERVER|
|ALTER ANY DATABASE EVENT NOTIFICATION|ALTER|ALTER ANY EVENT NOTIFICATION|
|ALTER ANY DATABASE EVENT SESSION<br />**Aplica-se a**: [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)].|ALTER|ALTER ANY EVENT SESSION|
|ALTER ANY DATABASE SCOPED CONFIGURATION<br /> **Aplica-se a**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] e posterior, [!INCLUDE[ssSDS](../../includes/sssds-md.md)].|CONTROL|CONTROL SERVER|
|ALTER ANY DATASPACE|ALTER|CONTROL SERVER|
|ALTER ANY EXTERNAL DATA SOURCE|ALTER|CONTROL SERVER|
|ALTER ANY EXTERNAL FILE FORMAT|ALTER|CONTROL SERVER|
|ALTERAR QUALQUER BIBLIOTECA EXTERNA <br /> **Aplica-se a**: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)].|CONTROL|CONTROL SERVER |
|ALTER ANY FULLTEXT CATALOG|ALTER|CONTROL SERVER|
|ALTER ANY MASK|CONTROL|CONTROL SERVER|
|ALTER ANY MESSAGE TYPE|ALTER|CONTROL SERVER|
|ALTER ANY REMOTE SERVICE BINDING|ALTER|CONTROL SERVER|
|ALTER ANY ROLE|ALTER|CONTROL SERVER|
|ALTER ANY ROUTE|ALTER|CONTROL SERVER|
|ALTER ANY SCHEMA|ALTER|CONTROL SERVER|
|ALTER ANY SECURITY POLICY<br /> **Aplica-se a**: [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].|CONTROL|CONTROL SERVER|
|ALTER ANY SERVICE|ALTER|CONTROL SERVER|
|ALTER ANY SYMMETRIC KEY|ALTER|CONTROL SERVER|
|ALTER ANY USER|ALTER|CONTROL SERVER|
|AUTHENTICATE|CONTROL|AUTHENTICATE SERVER|
|BACKUP DATABASE|CONTROL|CONTROL SERVER|
|BACKUP LOG|CONTROL|CONTROL SERVER|
|CHECKPOINT|CONTROL|CONTROL SERVER|
|CONNECT|CONNECT REPLICATION|CONTROL SERVER|
|CONNECT REPLICATION|CONTROL|CONTROL SERVER|
|CONTROL|CONTROL|CONTROL SERVER|
|CREATE AGGREGATE|ALTER|CONTROL SERVER|
|CREATE ANY EXTERNAL LIBRARY <br /> **Aplica-se a**: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)].|CONTROL|CONTROL SERVER |
|CREATE ASSEMBLY|ALTER ANY ASSEMBLY|CONTROL SERVER|
|CREATE ASYMMETRIC KEY|ALTER ANY ASYMMETRIC KEY|CONTROL SERVER|
|CREATE CERTIFICATE|ALTER ANY CERTIFICATE|CONTROL SERVER|
|CREATE CONTRACT|ALTER ANY CONTRACT|CONTROL SERVER|
|CREATE DATABASE|CONTROL|CREATE ANY DATABASE|
|CREATE DATABASE DDL EVENT NOTIFICATION|ALTER ANY DATABASE EVENT NOTIFICATION|CREATE DDL EVENT NOTIFICATION|
|CREATE DEFAULT|ALTER|CONTROL SERVER|
|CREATE FULLTEXT CATALOG|ALTER ANY FULLTEXT CATALOG|CONTROL SERVER|
|CREATE FUNCTION|ALTER|CONTROL SERVER|
|CREATE MESSAGE TYPE|ALTER ANY MESSAGE TYPE|CONTROL SERVER|
|CREATE PROCEDURE|ALTER|CONTROL SERVER|
|CREATE QUEUE|ALTER|CONTROL SERVER|
|CREATE REMOTE SERVICE BINDING|ALTER ANY REMOTE SERVICE BINDING|CONTROL SERVER|
|CREATE ROLE|ALTER ANY ROLE|CONTROL SERVER|
|CREATE ROUTE|ALTER ANY ROUTE|CONTROL SERVER|
|CREATE RULE|ALTER|CONTROL SERVER|
|CREATE SCHEMA|ALTER ANY SCHEMA|CONTROL SERVER|
|CREATE SERVICE|ALTER ANY SERVICE|CONTROL SERVER|
|CREATE SYMMETRIC KEY|ALTER ANY SYMMETRIC KEY|CONTROL SERVER|
|CREATE SYNONYM|ALTER|CONTROL SERVER|
|CREATE TABLE|ALTER|CONTROL SERVER|
|CREATE TYPE|ALTER|CONTROL SERVER|
|CREATE VIEW|ALTER|CONTROL SERVER|
|CREATE XML SCHEMA COLLECTION|ALTER|CONTROL SERVER|
|Delete (excluir)|CONTROL|CONTROL SERVER|
|Execute|CONTROL|CONTROL SERVER|
|EXECUTE ANY EXTERNAL SCRIPT <br /> **Aplica-se a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)].|CONTROL|CONTROL SERVER|
|EXECUTE EXTERNAL SCRIPT <br /> **Aplica-se a**: [!INCLUDE[ssSQL15](../../includes/sssqlv15-md.md)].|EXECUTE ANY EXTERNAL SCRIPT|CONTROL SERVER|
|INSERT|CONTROL|CONTROL SERVER|
|KILL DATABASE CONNECTION<br />**Aplica-se a**: [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].|CONTROL|ALTER ANY CONNECTION|
|REFERENCES|CONTROL|CONTROL SERVER|
|SELECT|CONTROL|CONTROL SERVER|
|SHOWPLAN|CONTROL|ALTER TRACE|
|SUBSCRIBE QUERY NOTIFICATIONS|CONTROL|CONTROL SERVER|
|TAKE OWNERSHIP|CONTROL|CONTROL SERVER|
|UNMASK|CONTROL|CONTROL SERVER|
|UPDATE|CONTROL|CONTROL SERVER|
|VIEW ANY COLUMN ENCRYPTION KEY DEFINITION|CONTROL|VIEW ANY DEFINITION|
|VIEW ANY COLUMN MASTER KEY DEFINITION|CONTROL|VIEW ANY DEFINITION|
|VIEW DATABASE STATE|CONTROL|VIEW SERVER STATE|
|VIEW DEFINITION|CONTROL|VIEW ANY DEFINITION|

## <a name="permissions"></a>Permissões

O concessor (ou a entidade de segurança especificada com a opção AS) deve ter a própria permissão com GRANT OPTION ou uma permissão superior que tenha a permissão que está sendo concedida implícita.

Se você estiver usando a opção AS, os requisitos adicionais a seguir serão aplicáveis.

|AS *granting_principal*|Permissão adicional necessária|
|------------------------------|------------------------------------|
|Usuário de banco de dados|Permissão IMPERSONATE no usuário, associação na função de banco de dados fixa db_securityadmin, associação na função de banco de dados fixa db_owner ou associação na função de servidor fixa sysadmin.|
|Usuário de banco de dados mapeado para um logon do Windows|Permissão IMPERSONATE no usuário, associação na função de banco de dados fixa db_securityadmin, associação na função de banco de dados fixa db_owner ou associação na função de servidor fixa sysadmin.|
|Usuário de banco de dados mapeado para um grupo do Windows|Associação no grupo do Windows, associação na função de banco de dados fixa db_securityadmin, associação na função de banco de dados fixa db_owner ou associação na função de servidor fixa sysadmin.|
|Usuário de banco de dados mapeado para um certificado|Associação na função de banco de dados fixa db_securityadmin, associação na função de banco de dados fixa db_owner ou associação na função de servidor fixa sysadmin.|
|Usuário de banco de dados mapeado para uma chave assimétrica|Associação na função de banco de dados fixa db_securityadmin, associação na função de banco de dados fixa db_owner ou associação na função de servidor fixa sysadmin.|
|Usuário de banco de dados não mapeado para nenhuma entidade de segurança de servidor|Permissão IMPERSONATE no usuário, associação na função de banco de dados fixa db_securityadmin, associação na função de banco de dados fixa db_owner ou associação na função de servidor fixa sysadmin.|
|Função de banco de dados|Permissão ALTER na função, associação na função de banco de dados fixa db_securityadmin, associação na função de banco de dados fixa db_owner ou associação na função de servidor fixa sysadmin.|
|Função de aplicativo|Permissão ALTER na função, associação na função de banco de dados fixa db_securityadmin, associação na função de banco de dados fixa db_owner ou associação na função de servidor fixa sysadmin.|

Os proprietários de objetos podem conceder permissões nos objetos de sua propriedade. As entidades que têm a permissão CONTROL em um protegível podem conceder a permissão nesse protegível.

Os usuários autorizados da permissão CONTROL SERVER, como os membros da função de servidor fixa sysadmin, podem conceder qualquer permissão em qualquer protegível do servidor.

## <a name="examples"></a>Exemplos

### <a name="a-granting-permission-to-create-tables"></a>A. Concedendo permissão para criar tabelas

O exemplo a seguir concede a permissão `CREATE TABLE` no banco de dados `AdventureWorks` ao usuário `MelanieK`.

```sql
USE AdventureWorks;
GRANT CREATE TABLE TO MelanieK;
GO
```

### <a name="b-granting-showplan-permission-to-an-application-role"></a>B. Concedendo a permissão SHOWPLAN a uma função de aplicativo

 O exemplo a seguir concede a permissão `SHOWPLAN` no banco de dados `AdventureWorks2012` à função de aplicativo `AuditMonitor`.

**Aplica-se a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e posterior, [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]

```sql
USE AdventureWorks2012;
GRANT SHOWPLAN TO AuditMonitor;
GO
```

### <a name="c-granting-create-view-with-grant-option"></a>C. Concedendo CREATE VIEW com GRANT OPTION

 O exemplo a seguir concede a permissão `CREATE VIEW` no banco de dados `AdventureWorks2012` ao usuário `CarmineEs` com o direito de conceder `CREATE VIEW` a outras entidades.

```sql
USE AdventureWorks2012;
GRANT CREATE VIEW TO CarmineEs WITH GRANT OPTION;
GO
```

### <a name="d-granting-control-permission-to-a-database-user"></a>D. Concedendo a permissão CONTROL a um usuário de banco de dados

 O exemplo a seguir concede a permissão `CONTROL` no banco de dados `AdventureWorks2012` ao usuário do banco de dados `Sarah`. O usuário deve existir no banco de dados, e o contexto deve ser definido como o banco de dados.

```sql
USE AdventureWorks2012;
GRANT CONTROL ON DATABASE::AdventureWorks2012 TO Sarah;
GO
```

## <a name="see-also"></a>Consulte Também

- [sys.database_permissions](../../relational-databases/system-catalog-views/sys-database-permissions-transact-sql.md)
- [sys.database_principals](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)
- [CREATE DATABASE](../../t-sql/statements/create-database-transact-sql.md?view=sql-server-2017)
- [GRANT](../../t-sql/statements/grant-transact-sql.md)
- [Permissões](../../relational-databases/security/permissions-database-engine.md)
- [Entidades](../../relational-databases/security/authentication-access/principals-database-engine.md)
