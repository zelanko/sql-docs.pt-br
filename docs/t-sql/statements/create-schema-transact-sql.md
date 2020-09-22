---
description: CREATE SCHEMA (Transact-SQL)
title: CREATE SCHEMA (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 12/01/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- CREATE_SCHEMA_TSQL
- SCHEMA
- CREATE SCHEMA
- SCHEMA_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- owners [SQL Server], schemas
- table creation [SQL Server], CREATE SCHEMA statement
- permissions [SQL Server], schemas
- schemas [SQL Server], creating
- CREATE SCHEMA statement
ms.assetid: df74fc36-20da-4efa-b412-c4e191786695
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: fe6b5b71f4d44609671dbe8b03978bd7ae0a9336
ms.sourcegitcommit: c74bb5944994e34b102615b592fdaabe54713047
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/22/2020
ms.locfileid: "90990211"
---
# <a name="create-schema-transact-sql"></a>CREATE SCHEMA (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Cria um esquema no banco de dados atual. A transação CREATE SCHEMA também pode criar tabelas e exibições no novo esquema e definir permissões GRANT, DENY ou REVOKE nesses objetos.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql
-- Syntax for SQL Server and Azure SQL Database  
  
CREATE SCHEMA schema_name_clause [ <schema_element> [ ...n ] ]  
  
<schema_name_clause> ::=  
    {  
    schema_name  
    | AUTHORIZATION owner_name  
    | schema_name AUTHORIZATION owner_name  
    }  
  
<schema_element> ::=   
    {   
        table_definition | view_definition | grant_statement |   
        revoke_statement | deny_statement   
    }  
```  
  
```syntaxsql
-- Syntax for Azure Synapse Analytics and Parallel Data Warehouse  
  
CREATE SCHEMA schema_name [ AUTHORIZATION owner_name ] [;]  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos
 *schema_name*  
 É o nome pelo qual o esquema é identificado no banco de dados.  
  
 AUTHORIZATION *owner_name*  
 Especifica o nome da entidade de segurança no nível de banco de dados que possuirá o esquema. Essa entidade de segurança pode possuir outros esquemas e pode não usar o esquema atual como esquema padrão.  
  
 *table_definition*  
 Especifica uma instrução CREATE TABLE que cria uma tabela no esquema. A entidade de segurança que executa essa instrução deve ter a permissão CREATE TABLE no banco de dados atual.  
  
 *view_definition*  
 Especifica uma instrução CREATE VIEW que cria uma exibição no esquema. A entidade de segurança que executa essa instrução deve ter a permissão CREATE VIEW no banco de dados atual.  
  
 *grant_statement*  
 Especifica uma instrução GRANT que concede permissões em qualquer item protegível, exceto no esquema novo.  
  
 *revoke_statement*  
 Especifica uma instrução REVOKE que revoga permissões em qualquer item protegível, exceto no esquema novo.  
  
 *deny_statement*  
 Especifica uma instrução DENY que nega permissões em qualquer item protegível, exceto no esquema novo.  
  
## <a name="remarks"></a>Comentários  
  
> [!NOTE]  
>  As instruções que contêm CREATE SCHEMA AUTHORIZATION, mas não especificam um nome, são permitidas somente para compatibilidade com versões anteriores. A instrução não causa um erro, mas não cria uma esquema.  
  
 CREATE SCHEMA pode criar um esquema, as tabelas e as exibições contidas e as permissões GRANT, REVOKE ou DENY em qualquer item protegível em uma única instrução. Essa instrução deve ser executada como um lote separado. Os objetos criados pela instrução CREATE SCHEMA são criados no esquema que está sendo criado.  
  
 As transações CREATE SCHEMA são atômicas. Se algum erro ocorrer durante a execução de uma instrução CREATE SCHEMA, nenhum item protegível especificado será criado e nenhuma permissão será concedida.  
  
 Os itens protegíveis criados por CREATE SCHEMA podem ser listados em qualquer ordem, com exceção das exibições que fazem referência a outras exibições. Nesse caso, a exibição mencionada deve ser criada antes da exibição que a menciona.  
  
 Portanto, uma instrução GRANT pode conceder permissões em um objeto antes que o objeto propriamente dito seja criado ou uma instrução CREATE VIEW pode aparecer antes das instruções CREATE TABLE que criam as tabelas mencionadas pela exibição. Além disso, as instruções CREATE TABLE podem declarar chaves estrangeiras definidas posteriormente na instrução CREATE SCHEMA.  
  
> [!NOTE]  
>  As instruções CREATE SCHEMA oferecem suporte para DENY e REVOKE. As cláusulas DENY e REVOKE serão executadas na ordem em que aparecem na instrução CREATE SCHEMA.  
  
 A entidade de segurança que executa CREATE SCHEMA pode especificar outra entidade de segurança de banco de dados como o proprietário do esquema que está sendo criado. Isso requer permissões adicionais, conforme descrito na seção “Permissões”, posteriormente neste tópico.  
  
 O esquema novo é de propriedade de uma das seguintes entidades de segurança em nível de banco de dados: usuário de banco de dados, função de banco de dados ou função de aplicativo. Os objetos criados em um esquema são de propriedade do proprietário do esquema e têm **principal_id** NULL em **sys.objects**. A propriedade dos objetos contidos pelo esquema pode ser transferida para qualquer entidade de segurança no nível de banco de dados, mas o proprietário do esquema sempre retém a permissão CONTROL nos objetos do esquema.  
  
> [!CAUTION]  
>  [!INCLUDE[ssCautionUserSchema](../../includes/sscautionuserschema-md.md)]  
  
 **Esquema implícito e criação de usuário**  
  
 Em alguns casos, um usuário pode criar um banco de dados sem ter uma conta de usuário de banco de dados (uma entidade de banco de dados no banco de dados). Isso pode ocorrer nas seguintes situações:  
  
-   Um logon tem privilégios **CONTROL SERVER**.  
  
-   Um usuário do Windows não tem uma conta de usuário de banco de dados individual (uma entidade de banco de dados no banco de dados), mas acessa um banco de dados como membro de um grupo do Windows que tem uma conta de usuário de banco de dados (uma entidade de banco de dados para o grupo do Windows).  
  
 Quando um usuário sem uma conta de usuário de banco de dados cria um objeto sem especificar um esquema existente, uma entidade de banco de dados e um esquema padrão são automaticamente criados no banco de dados para esse usuário. A entidade de banco de dados e o esquema criados terão o mesmo nome que aquele usado pelo usuário ao se conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (o nome de logon de autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou o nome de usuário do Windows).  
  
 Esse comportamento é necessário para permitir que usuários com base em grupos do Windows criem e possuam objetos. No entanto, isso pode resultar na criação não intencional de esquemas e usuários. Para evitar criar usuários e esquemas implicitamente, sempre que possível crie entidades de banco de dados explicitamente e atribua um esquema padrão. Ou declare explicitamente um esquema existente ao criar objetos em um banco de dados usando nomes de objetos de duas ou três partes.  

> [!NOTE]
>  A criação implícita de um usuário do Azure Active Directory não é possível no [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]. Como a criação de um usuário do Azure AD de um provedor externo precisa verificar o status de usuários no AAD, a criação do usuário falhará com o erro 2760: **O nome do esquema especificado "\<user_name@domain>" não existe ou você não tem permissão para usá-lo.** E, em seguida, o erro 2759: **Falha em CREATE SCHEMA devido a erros anteriores.** Para resolver esses erros, crie o usuário do Azure AD por meio do provedor externo primeiro e, em seguida, execute novamente a instrução, criando o objeto.
 
  
## <a name="deprecation-notice"></a>Aviso de substituição  
 Atualmente, a compatibilidade com versões anteriores oferece suporte para instruções CREATE SCHEMA que não especificam um nome de esquema. Essas instruções não criam realmente um esquema no banco de dados, mas criam tabelas e exibições, além de concederem permissões. As entidades de segurança não precisam da permissão CREATE SCHEMA para executar essa forma anterior de CREATE SCHEMA porque nenhum esquema está sendo criado. Essa funcionalidade será removida em versões futuras do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão CREATE SCHEMA no banco de dados.  
  
 Para criar um objeto especificado na instrução CREATE SCHEMA, o usuário deve ter a permissão CREATE correspondente.  
  
 Para especificar outro usuário como o proprietário do esquema que está sendo criado, o chamador deve ter a permissão IMPERSONATE no usuário em questão. Se uma função de banco de dados for especificada como o proprietário, o chamador deve ter o seguinte: associação na função ou a permissão ALTER na função.  
  
> [!NOTE]  
>  Para a sintaxe compatível com versões anteriores, nenhuma permissão para CREATE SCHEMA é necessária porque nenhum esquema está sendo criado.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-creating-a-schema-and-granting-permissions"></a>a. Criando um esquema e concedendo permissões  
 O exemplo a seguir cria o esquema `Sprockets` possuído por `Annik` que contém a tabela `NineProngs`. A instrução concede `SELECT` a `Mandar` e nega `SELECT` a `Prasanna`. `Sprockets` e `NineProngs` são criados em uma única instrução.  
  
```sql  
USE AdventureWorks2012;  
GO  
CREATE SCHEMA Sprockets AUTHORIZATION Annik  
    CREATE TABLE NineProngs (source int, cost int, partnumber int)  
    GRANT SELECT ON SCHEMA::Sprockets TO Mandar  
    DENY SELECT ON SCHEMA::Sprockets TO Prasanna;  
GO   
```  
  
## <a name="examples-sssdwfull-and-sspdw"></a>Exemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="b-creating-a-schema-and-a-table-in-the-schema"></a>B. Criando um esquema e uma tabela no esquema  
 O exemplo a seguir cria um o esquema `Sales` e, em seguida, cria uma tabela `Sales.Region` nesse esquema.  
  
```sql  
CREATE SCHEMA Sales;  
GO
  
CREATE TABLE Sales.Region   
(Region_id INT NOT NULL,  
Region_Name CHAR(5) NOT NULL)  
WITH (DISTRIBUTION = REPLICATE);  
GO  
```  
  
### <a name="c-setting-the-owner-of-a-schema"></a>C. Definindo o proprietário de um esquema  
 O exemplo a seguir cria um esquema `Production` pertencente a `Mary`.  
  
```sql  
CREATE SCHEMA Production AUTHORIZATION [Contoso\Mary];  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [ALTER SCHEMA &#40;Transact-SQL&#41;](../../t-sql/statements/alter-schema-transact-sql.md)   
 [DROP SCHEMA &#40;Transact-SQL&#41;](../../t-sql/statements/drop-schema-transact-sql.md)   
 [GRANT &#40;Transact-SQL&#41;](../../t-sql/statements/grant-transact-sql.md)   
 [DENY &#40;Transact-SQL&#41;](../../t-sql/statements/deny-transact-sql.md)   
 [REVOKE &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-transact-sql.md)   
 [CREATE VIEW &#40;Transact-SQL&#41;](../../t-sql/statements/create-view-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [sys.schemas &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/schemas-catalog-views-sys-schemas.md)   
 [Criar um esquema de banco de dados](../../relational-databases/security/authentication-access/create-a-database-schema.md)  
  
  


