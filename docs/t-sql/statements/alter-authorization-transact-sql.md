---
description: ALTER AUTHORIZATION (Transact-SQL)
title: ALTER AUTHORIZATION (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/28/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ALTER_AUTHORIZATION_TSQL
- ALTER AUTHORIZATION
dev_langs:
- TSQL
helpviewer_keywords:
- owners [SQL Server], transferring
- modifying entity ownership
- full-text search [SQL Server], permissions
- owners [SQL Server], entities
- ALTER AUTHORIZATION statement
- entity ownership [SQL Server]
- transferring ownership
- search property lists [SQL Server], permissions
- TAKE OWNERSHIP
ms.assetid: 8c805ae2-91ed-4133-96f6-9835c908f373
author: VanMSFT
ms.author: vanto
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 1afee97fd7b7c70d30def7383e4b83453b90f19b
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97472027"
---
# <a name="alter-authorization-transact-sql"></a>ALTER AUTHORIZATION (Transact-SQL)

[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Altera a propriedade de um protegível.    
    
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)    
    
## <a name="syntax"></a>Sintaxe    
    
```syntaxsql
-- Syntax for SQL Server  
ALTER AUTHORIZATION    
   ON [ <class_type>:: ] entity_name    
   TO { principal_name | SCHEMA OWNER }    
[;]    
    
<class_type> ::=    
    {    
        OBJECT | ASSEMBLY | ASYMMETRIC KEY | AVAILABILITY GROUP | CERTIFICATE     
      | CONTRACT | TYPE | DATABASE | ENDPOINT | FULLTEXT CATALOG     
      | FULLTEXT STOPLIST | MESSAGE TYPE | REMOTE SERVICE BINDING    
      | ROLE | ROUTE | SCHEMA | SEARCH PROPERTY LIST | SERVER ROLE     
      | SERVICE | SYMMETRIC KEY | XML SCHEMA COLLECTION    
    }    
```    

```syntaxsql
-- Syntax for SQL Database  
  
ALTER AUTHORIZATION    
   ON [ <class_type>:: ] entity_name    
   TO { principal_name | SCHEMA OWNER }    
[;]    
    
<class_type> ::=    
    {    
      OBJECT | ASSEMBLY | ASYMMETRIC KEY | CERTIFICATE     
    | TYPE | DATABASE | FULLTEXT CATALOG     
    | FULLTEXT STOPLIST     
    | ROLE | SCHEMA | SEARCH PROPERTY LIST     
    | SYMMETRIC KEY | XML SCHEMA COLLECTION    
    }    
```    

    
```syntaxsql
-- Syntax for Azure Synapse Analytics  
  
ALTER AUTHORIZATION ON    
    [ <class_type> :: ] <entity_name>     
    TO { principal_name | SCHEMA OWNER }    
[;]    
    
<class_type> ::= {    
      SCHEMA     
    | OBJECT     
}    
    
<entity_name> ::=    
{    
      schema_name    
    | [ schema_name. ] object_name    
}    
```    
    
```syntaxsql
-- Syntax for Parallel Data Warehouse  
  
ALTER AUTHORIZATION ON    
    [ <class_type> :: ] <entity_name>     
    TO { principal_name | SCHEMA OWNER }    
[;]    
    
<class_type> ::= {    
      DATABASE     
    | SCHEMA     
    | OBJECT     
}    
    
<entity_name> ::=    
{    
      database_name 
    | schema_name    
    | [ schema_name. ] object_name    
}    
```    
[!INCLUDE[synapse-analytics-od-unsupported-syntax](../../includes/synapse-analytics-od-unsupported-syntax.md)]
    
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos
\<class_type> É a classe protegível da entidade para a qual o proprietário está sendo alterado. OBJECT é o padrão.    
    
|Classe|Produto|    
|-|-|    
|OBJECT|**APLICA-SE A**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e posterior, [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)], [!INCLUDE[ssSDW](../../includes/sssdwfull-md.md)] e [!INCLUDE[ssPDW](../../includes/sspdw-md.md)].|    
|ASSEMBLY|**APLICA-SE A**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e posterior, [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].|    
|ASYMMETRIC KEY|**APLICA-SE A**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e posterior, [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].|    
|AVAILABILITY GROUP |**APLICA-SE A**: SQL Server 2012 e posterior.|
|CERTIFICATE|**APLICA-SE A**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e posterior, [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].|    
|CONTRACT|**APLICA-SE A**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e posterior.|    
|DATABASE|**APLICA-SE A**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e posterior, [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]. Para obter mais informações, veja a seção de [bancos de dados ALTER AUTHORIZATION FOR](#AlterDB) abaixo.|    
|ENDPOINT|**APLICA-SE A**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e posterior.|    
|FULLTEXT CATALOG|**APLICA-SE A**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e posterior, [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].|    
|FULLTEXT STOPLIST|**APLICA-SE A**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e posterior, [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].|    
|MESSAGE TYPE|**APLICA-SE A**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e posterior.|    
|REMOTE SERVICE BINDING|**APLICA-SE A**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e posterior.|    
|ROLE|**APLICA-SE A**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e posterior, [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].|    
|ROUTE|**APLICA-SE A**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e posterior.|    
|SCHEMA|**APLICA-SE A**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e posterior, [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)], [!INCLUDE[ssSDW](../../includes/sssdwfull-md.md)] e [!INCLUDE[ssPDW](../../includes/sspdw-md.md)].|    
|SEARCH PROPERTY LIST|**APLICA-SE A**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e posterior, [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].|    
|SERVER ROLE|**APLICA-SE A**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e posterior.|    
|SERVICE|**APLICA-SE A**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e posterior.|    
|SYMMETRIC KEY|**APLICA-SE A**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e posterior, [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].|    
|TYPE|**APLICA-SE A**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e posterior, [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].|    
|XML SCHEMA COLLECTION|**APLICA-SE A**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e posterior, [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].|    
    
 *entity_name*    
 É o nome da entidade.    
    
 *principal_name* | SCHEMA OWNER    
 É o nome da entidade de segurança que possuirá a entidade. Os objetos de banco de dados devem ser de propriedade de um banco de dados principal; um usuário de banco de dados ou função. Os objetos de servidor (como bancos de dados) devem ser de propriedade de uma entidade de servidor (um logon). Especifique **SCHEMA OWNER** como o *principal_name* para indicar que o objeto deve ser de propriedade de uma entidade de segurança que tenha o esquema do objeto.    
    
## <a name="remarks"></a>Comentários    
 ALTER AUTHORIZATION pode ser usado para alterar a propriedade de qualquer entidade que tenha um proprietário. A propriedade de entidades contidas no banco de dados pode ser transferida a qualquer entidade em nível de banco de dados. A propriedade de entidades em nível de servidor pode ser transferida apenas a entidades em nível de servidor.    
    
> [!IMPORTANT]    
>  A partir do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], um usuário pode possuir um OBJECT ou TYPE que esteja contido por um esquema de propriedade de outro usuário do banco de dados. Essa é uma alteração de comportamento de versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter mais informações, veja [OBJECTPROPERTY &#40;Transact-SQL&#41; ](../../t-sql/functions/objectproperty-transact-sql.md) e [TYPEPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/typeproperty-transact-sql.md).    
    
 A propriedade das seguintes entidades contidas por esquema de tipo "objeto" pode ser transferida: tabelas, exibições, funções, procedimentos, filas e sinônimos.    
    
 A propriedade das seguintes entidades não pode ser transferida: servidores vinculados, estatísticas, restrições, regras, padrões, gatilhos, filas do [!INCLUDE[ssSB](../../includes/sssb-md.md)], credenciais, funções de partição, esquemas de partição, chaves mestras de banco de dados, chave mestra de serviço e notificações de eventos.    
    
 A propriedade de membros das seguintes classes protegíveis não pode ser transferida: servidor, logon, usuário, função de aplicativo e coluna.    
    
 A opção SCHEMA OWNER é válida apenas quando você está transferindo propriedade de uma entidade contida por esquema. SCHEMA OWNER transferirá a propriedade da entidade ao proprietário do esquema no qual ela reside. Apenas entidades de classe OBJECT, TYPE ou XML SCHEMA COLLECTION são contidas por esquema.    
    
 Se a entidade de destino não for um banco de dados e estiver sendo transferida a um novo proprietário, todas as permissões no destino serão descartadas.    
    
> [!CAUTION]    
>  No [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], o comportamento de esquemas mudou em relação ao comportamento em versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. O código que pressupõe que esquemas são equivalentes a usuários de banco de dados pode não retornar resultados corretos. Exibições antigas do catálogo, incluindo sysobjects, não devem ser usadas em um banco de dados no qual uma das instruções DDL a seguir já tenha sido utilizada: CREATE SCHEMA, ALTER SCHEMA, DROP SCHEMA, CREATE USER, ALTER USER, DROP USER, CREATE ROLE, ALTER ROLE, DROP ROLE, CREATE APPROLE, ALTER APPROLE, DROP APPROLE, ALTER AUTHORIZATION. Em um banco de dados no qual qualquer uma dessas instruções tenha sido usada alguma vez, você deve usar as novas exibições do catálogo. As novas exibições do catálogo levam em conta a separação de entidades e esquemas introduzida no [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]. Para mais informações sobre exibições do catálogo, consulte [Exibições do catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md).    
    
 Além disso, observe o seguinte:    
    
> [!IMPORTANT]    
>  O único modo confiável de localizar o proprietário de um objeto é consultar a exibição do catálogo **sys.objects**. O único modo seguro para localizar o proprietário de um tipo é usar a função TYPEPROPERTY.    
    
## <a name="special-cases-and-conditions"></a>Casos e condições especiais    
 A tabela a seguir lista casos, exceções e condições especiais que se aplicam a autorização de alteração.    
    
|Classe|Condição|    
|-----------|---------------|    
|OBJECT|Não pode alterar propriedade de gatilhos, restrições, regras, padrões, estatísticas, objetos de sistema, filas, exibições indexadas ou tabelas com exibições indexadas.|    
|SCHEMA|Quando a propriedade é transferida, permissões em objetos contidos por esquema que não têm proprietários explícitos serão descartadas. Não é possível alterar o proprietário de sys, dbo ou information_schema.|    
|TYPE|Não é possível alterar a propriedade de um TYPE que pertença a sys ou information_schema.|    
|CONTRACT, MESSAGE TYPE ou SERVICE|Não podem alterar a propriedade de entidades do sistema.|    
|SYMMETRIC KEY|Não pode alterar a propriedade de chaves temporárias globais.|    
|CERTIFICATE ou ASYMMETRIC KEY|Não pode transferir a propriedade dessas entidades a uma função ou grupo.|    
|ENDPOINT|A entidade deve ser um logon.|    
  
## <a name="alter-authorization-for-databases"></a><a name="AlterDB"></a> ALTER AUTHORIZATION para bancos de dados  
**APLICA-SE A**: [!INCLUDE[ssSQL15](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
### <a name="for-sql-server"></a>Para SQL Server:  
**Requisitos para o novo proprietário:**    
A nova entidade de segurança do proprietário deve ser uma das seguintes:  

-   Um logon de autenticação do SQL Server.  
-   Um logon de autenticação do Windows que representa um usuário do Windows (não um grupo).  
-   Um usuário do Windows que se autentica por meio de um logon de autenticação do Windows que representa um grupo do Windows.  
  
**Requisitos para a pessoa que está executando a instrução ALTER AUTHORIZATION:**  
Se você não for um membro da função de servidor fixa **sysadmin**, deverá ter pelo menos a permissão TAKE OWNERSHIP no banco de dados e a permissão IMPERSONATE no novo logon do proprietário.   

### <a name="for-azure-sql-database"></a>Para o Banco de Dados SQL do Azure:  
**Requisitos para o novo proprietário:**    
A nova entidade de segurança do proprietário deve ser uma das seguintes:  

-   Um logon de autenticação do SQL Server.  
-   Um usuário federado (não um grupo) presente no Azure AD.  
-   Um usuário gerenciado (não um grupo) ou um aplicativo presente no Azure AD.    

> Se o novo proprietário for um usuário do Azure Active Directory, ele não poderá existir como um usuário no banco de dados em que o novo proprietário vá se tornar o novo DBO. Esse usuário do Azure AD deve primeiro ser removido do banco de dados antes de executar a instrução ALTER AUTHORIZATION alterando a propriedade de banco de dados para o novo usuário. Para obter mais informações de como configurar usuários do Azure Active Directory com o Banco de Dados SQL, confira [Como se conectar ao Banco de Dados SQL ou ao [!INCLUDE[ssSDW](../../includes/sssdwfull-md.md)] usando a Autenticação do Azure Active Directory](https://azure.microsoft.com/documentation/articles/sql-database-aad-authentication/).   
  
**Requisitos para a pessoa que está executando a instrução ALTER AUTHORIZATION:**  
Você deve se conectar ao banco de dados de destino para alterar o proprietário daquele banco de dados.  

Os seguintes tipos de contas podem alterar o proprietário de um banco de dados. 

* O logon da entidade de segurança em nível de serviço. (O administrador do SQL Azure provisionado quando o servidor de Banco de Dados SQL foi criado.)  
* O administrador do Azure Active Directory para o SQL Server do Azure.   
* O proprietário atual do banco de dados.   
 
  
A tabela a seguir resume os requisitos:  
  
Executor  |Destino  |Result    
---------|---------|---------  
Logon de Autenticação do SQL Server     |Logon de Autenticação do SQL Server         |Sucesso  
Logon de Autenticação do SQL Server     |Usuário do Azure AD         |Falha           
Usuário do Azure AD     |Logon de Autenticação do SQL Server         |Sucesso           
Usuário do Azure AD     |Usuário do Azure AD         |Sucesso           
  
Para verificar um proprietário do banco de dados do Azure AD, execute o seguinte comando do Transact-SQL em um banco de dados de usuário (neste exemplo `testdb`).  
    
```sql    
SELECT CAST(owner_sid as uniqueidentifier) AS Owner_SID   
FROM sys.databases   
WHERE name = 'testdb';  
```    
    
A saída será um identificador (como 6D8B81F6-7C79-444C-8858-4AF896C03C67) que corresponde à ObjectID do Azure AD atribuída ao `richel@cqclinic.onmicrosoft.com`  
Quando um usuário de logon de autenticação do SQL Server for o proprietário do banco de dados, execute a seguinte instrução no banco de dados mestre para verificar o proprietário do banco de dados:  
    
```sql    
SELECT d.name, d.owner_sid, sl.name   
FROM sys.databases AS d  
JOIN sys.sql_logins AS sl  
ON d.owner_sid = sl.sid;  
    
```    
  
### <a name="best-practice"></a>Melhor prática  
  
Em vez de usar os usuários do Azure AD como proprietários individuais do banco de dados, use um grupo do Azure AD como um membro da função fixa de banco de dados **db_owner**. As etapas a seguir mostram como configurar um logon desabilitado como o proprietário do banco de dados e tornar um grupo do Azure Active Directory (`mydbogroup`) um membro da função **db_owner**. 

1.  Faça logon no SQL Server como administrador do Azure AD e altere o proprietário do banco de dados para um logon de autenticação do SQL Server desabilitado. Por exemplo, do banco de dados de usuário, execute:  
  ```sql    
  ALTER AUTHORIZATION ON database::testdb TO DisabledLogin;  
  ```  
  
2.  Crie um grupo do Azure AD que deve ser o proprietário do banco de dados e adicioná-lo como um usuário ao banco de dados do usuário. Por exemplo:  
  ```sql    
  CREATE USER [mydbogroup] FROM EXTERNAL PROVIDER;  
  ```   
  
3.  No banco de dados de usuário, adicione o usuário que representa o grupo do Azure AD, como a função fixa de banco de dados **db_owner**. Por exemplo:  
  ```sql    
  ALTER ROLE db_owner ADD MEMBER mydbogroup;  
  ```    
  
Agora, os membros do `mydbogroup` podem gerenciar centralmente o banco de dados como membros da função **db_owner**.  
- Quando os membros desse grupo são removidos do grupo do Azure AD, eles perdem automaticamente as permissões de dbo do banco de dados.  
- Da mesma forma, se novos membros são adicionados ao `mydbogroup` grupo do Azure AD, eles obtêm automaticamente acesso de dbo para esse banco de dados.  
  
Para verificar se um usuário específico tem a permissão de dbo efetiva, peça para o usuário executar a seguinte instrução:  
    
```sql    
SELECT IS_MEMBER ('db_owner');  
```    
  
Um valor retornado de 1 indica que o usuário é um membro da função.  
   
    
## <a name="permissions"></a>Permissões    
 Requer permissão TAKE OWNERSHIP na entidade. Se o novo proprietário não for o usuário que está executando esta instrução, também requererá: 1) permissão IMPERSONATE no novo proprietário se ele for um usuário ou logon; ou 2) se o novo proprietário for uma função, associação na função ou permissão ALTER na função; ou 3) se o novo proprietário for uma função de aplicativo, permissão ALTER na função do aplicativo.    
    
## <a name="examples"></a>Exemplos    
    
### <a name="a-transfer-ownership-of-a-table"></a>a. Transferir a propriedade de uma tabela    
 O exemplo a seguir transfere a propriedade da tabela `Sprockets` ao usuário `MichikoOsada`. A tabela está localizada dentro do esquema `Parts`.    
    
```sql    
ALTER AUTHORIZATION ON OBJECT::Parts.Sprockets TO MichikoOsada;    
GO    
```    
    
A consulta também pode ser semelhante à seguinte:    
    
```sql    
ALTER AUTHORIZATION ON Parts.Sprockets TO MichikoOsada;    
GO    
```    
    
Se o esquema de objetos não for incluído como parte da instrução, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] procurará o objeto no esquema padrão de usuários. Por exemplo:    
    
```sql    
ALTER AUTHORIZATION ON Sprockets TO MichikoOsada;    
ALTER AUTHORIZATION ON OBJECT::Sprockets TO MichikoOsada;    
```    
    
### <a name="b-transfer-ownership-of-a-view-to-the-schema-owner"></a>B. Transferir a propriedade de uma exibição ao proprietário do esquema    
 O exemplo a seguir transfere a propriedade da exibição `ProductionView06` ao proprietário do esquema que a contém. A exibição está localizada dentro do esquema `Production`.    
    
```sql    
ALTER AUTHORIZATION ON OBJECT::Production.ProductionView06 TO SCHEMA OWNER;    
GO    
```    
    
### <a name="c-transfer-ownership-of-a-schema-to-a-user"></a>C. Transferir a propriedade de um esquema a um usuário    
 O exemplo a seguir transfere a propriedade do esquema `SeattleProduction11` ao usuário `SandraAlayo`.    
    
```sql    
ALTER AUTHORIZATION ON SCHEMA::SeattleProduction11 TO SandraAlayo;    
GO    
```    
    
### <a name="d-transfer-ownership-of-an-endpoint-to-a-sql-server-login"></a>D. Transferir a propriedade de um ponto de extremidade a um logon do SQL Server    
 O exemplo a seguir transfere a propriedade do ponto de extremidade `CantabSalesServer1` a `JaePak`. Como o ponto de extremidade é um protegível em nível de servidor, o ponto de extremidade só pode ser transferido a uma entidade principal no nível de servidor.    
    
**Aplica-se a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e posterior.    
    
```sql    
ALTER AUTHORIZATION ON ENDPOINT::CantabSalesServer1 TO JaePak;    
GO    
```    
    
### <a name="e-changing-the-owner-of-a-table"></a>E. Alterando o proprietário de uma tabela    
 Cada um dos exemplos a seguir altera o proprietário da tabela `Sprockets` no banco de dados `Parts` para o usuário do banco de dados `MichikoOsada`.    
 
```sql    
ALTER AUTHORIZATION ON Sprockets TO MichikoOsada;    
ALTER AUTHORIZATION ON dbo.Sprockets TO MichikoOsada;    
ALTER AUTHORIZATION ON OBJECT::Sprockets TO MichikoOsada;    
ALTER AUTHORIZATION ON OBJECT::dbo.Sprockets TO MichikoOsada;    
```    
    
### <a name="f-changing-the-owner-of-a-database"></a>F. Alterar o proprietário de um banco de dados    
 **APLICA-SE A**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e posterior, [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] e [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)].    
    
 O exemplo a seguir alterar o proprietário do banco de dados `Parts` para o logon `MichikoOsada`.    
    
```sql    
ALTER AUTHORIZATION ON DATABASE::Parts TO MichikoOsada;    
```    
  
### <a name="g-changing-the-owner-of-a-sql-database-to-an-azure-ad-user"></a>G. Alterando o proprietário do Banco de Dados SQL para um usuário do Azure AD  
No exemplo a seguir, um administrador do Azure Active Directory para o SQL Server em uma organização com um Active Directory denominado `cqclinic.onmicrosoft.com` poderá alterar a propriedade atual de um banco de dados `targetDB` e tornar um usuário do AAD `richel@cqclinic.onmicorsoft.com` o novo proprietário do banco de dados do usando o seguinte comando:  
    
```sql    
ALTER AUTHORIZATION ON database::targetDB TO [rachel@cqclinic.onmicrosoft.com];   
```    
    
 Observe que, para os usuários do Azure AD, os colchetes em torno do nome de usuário devem ser usados.  
  
    
## <a name="see-also"></a>Consulte Também    
 [OBJECTPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/objectproperty-transact-sql.md)     
 [TYPEPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/typeproperty-transact-sql.md)     
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)    
 
