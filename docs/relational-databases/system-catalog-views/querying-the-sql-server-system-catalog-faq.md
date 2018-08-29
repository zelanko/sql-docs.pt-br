---
title: Consultando o catálogo de sistema do SQL Server perguntas Frequentes | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- catalog views [SQL Server], examples
- metadata [SQL Server], frequently asked questions
- metadata [SQL Server], example queries
- system catalogs [SQL Server], example queries
- catalog views [SQL Server], frequently asked questions
ms.assetid: ca202580-c37e-4ccd-9275-77ce79481f64
caps.latest.revision: 51
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: bf88696005c7ac3f743f23f1ee75fd362a3e5243
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43030504"
---
# <a name="querying-the-sql-server-system-catalog-faq"></a>Consultando as perguntas frequentes do catálogo do sistema do SQL Server
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Este tópico contém uma lista de perguntas frequentes. As respostas a essas perguntas são consultas baseadas em exibições do catálogo.  
  
##  <a name="_TOP"></a> Perguntas frequentes  
 As seções a seguir listam as perguntas frequentes por categoria.  
  
### <a name="data-types"></a>Tipos de dados  
  
-   [Como localizar os tipos de dados das colunas de uma tabela especificada?](#_FAQ7)  
  
-   [Como localizar os tipos de dados LOB de uma tabela especificada?](#_FAQ14)  
  
-   [Como localizar as colunas que dependem de um tipo de dados especificado?](#_FAQ22)  
  
-   [Como localizar as colunas computadas que dependem de um tipo especificado do CLR definidas pelo usuário ou tipo de dados de alias?](#_FAQ23)  
  
-   [Como localizar os parâmetros que dependem de um tipo especificado do CLR definidas pelo usuário ou tipo de alias?](#_FAQ24)  
  
-   [Como posso encontrar as restrições CHECK que dependem de um tipo definido pelo usuário CLR especificado?](#_FAQ25)  
  
-   [Como localizar as exibições, funções Transact-SQL e procedimentos armazenados Transact-SQL que dependem de um tipo especificado do CLR definidas pelo usuário ou tipo de alias?](#_FAQ26)  
  
### <a name="tables-indexes-views-and-constraints"></a>Tabelas, índices, exibições e restrições  
  
-   [Como localizar todas as tabelas definidas pelo usuário em um banco de dados especificado?](#_FAQ31)  
  
-   [Como localizar todas as tabelas que não têm um índice clusterizado em um banco de dados especificado?](#_FAQ1)  
  
-   [Como localizar todas as tabelas que não têm um índice?](#_FAQ4)  
  
-   [Como localizar todas as tabelas que não têm uma chave primária?](#_FAQ3)  
  
-   [Como localizar todas as tabelas que têm uma coluna de identidade?](#_FAQ5)  
  
-   [Como localizar todas as tabelas e índices particionados?](#_FAQ32)  
  
-   [Como localizar todas as exibições em um banco de dados?](#_FAQ13)  
  
-   [Como localizar a definição de um modo de exibição?](#_FAQ35)  
  
-   [Como localizar todas as entidades que foram modificadas nos últimos N dias?](#_FAQ6)  
  
-   [Como localizar as colunas de uma chave primária para uma tabela especificada?](#_FAQ16)  
  
-   [Como localizar as colunas de uma chave estrangeira para uma tabela especificada?](#_FAQ17)  
  
-   [Como determinar se uma coluna é usada em uma expressão de coluna computada?](#_FAQ20)  
  
-   [Como localizar todas as colunas que são usadas em uma expressão de coluna computada?](#_FAQ21)  
  
-   [Como localizar todas as restrições para uma tabela especificada?](#_FAQ27)  
  
-   [Como localizar todos os índices para uma tabela especificada?](#_FAQ28)  
  
-   [Como localizar todas as tabelas que têm um nome de coluna especificado?](#_FAQ30)  
  
-   [Como localizar todas as estatísticas em um objeto especificado?](#_FAQ33)  
  
-   [Como localizar todas as estatísticas e as colunas em um objeto especificado?](#_FAQ34)  
  
### <a name="modules-stored-procedures-user-defined-functions-and-triggers"></a>Módulos (procedimentos armazenados, funções definidas pelo usuário e gatilhos)  
  
-   [Como localizar todos os procedimentos armazenados em um banco de dados?](#_FAQ9)  
  
-   [Como localizar todas as funções definidas pelo usuário em um banco de dados?](#_FAQ12)  
  
-   [Como localizar os parâmetros para uma função ou procedimento armazenado especificado?](#_FAQ10)  
  
-   [Como localizar as dependências em uma função especificada?](#_FAQ8)  
  
-   [Como posso exibir a definição de um módulo?](#_FAQ15)  
  
-   [Como posso exibir a definição de um gatilho de nível de servidor?](#_FAQ19)  
  
### <a name="schemas-users-roles-and-permissions"></a>Esquemas, usuários, funções e permissões  
  
-   [Como localizar todos os proprietários de entidades contidos em um esquema especificado?](#_FAQ2)  
  
-   [Como localizar as permissões concedidas ou negadas a uma entidade especificada?](#_FAQ18)  
  
## <a name="answers"></a>Respostas  
  
###  <a name="_FAQ1"></a> Como localizar todas as tabelas que não têm um índice clusterizado em um banco de dados especificado?  
 Antes de executar as consultas a seguir, substitua `<database_name>` pelo nome de um banco de dados válido.  
  
```  
SELECT SCHEMA_NAME(t.schema_id) AS schema_name, t.name AS table_name  
FROM sys.tables AS t  
WHERE NOT EXISTS   
   (  
     SELECT * FROM sys.indexes AS i  
     WHERE i.object_id = t.object_id  
     AND i.type = 1  -- or type_desc = 'CLUSTERED'  
   )  
ORDER BY schema_name, table_name;  
GO  
  
```  
  
 Ou então, use a função `OBJECTPROPERTY`, conforme mostrado no exemplo a seguir.  
  
```  
USE <database_name>;  
GO  
SELECT SCHEMA_NAME(schema_id) AS schema_name, name AS table_name  
FROM sys.tables   
WHERE OBJECTPROPERTY(object_id,'TableHasClustIndex') = 0  
ORDER BY schema_id, name;  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="_FAQ2"></a> Como localizar todos os proprietários de entidades contidos em um esquema especificado?  
 Antes de executar a consulta a seguir, substitua `<database_name>` e `<schema_name>` por nomes válidos.  
  
```  
USE <database_name>;  
GO  
SELECT 'OBJECT' AS entity_type  
    ,USER_NAME(OBJECTPROPERTY(object_id, 'OwnerId')) AS owner_name  
    ,name   
FROM sys.objects WHERE SCHEMA_NAME(schema_id) = '<schema_name>'  
UNION   
SELECT 'TYPE' AS entity_type  
    ,USER_NAME(TYPEPROPERTY(SCHEMA_NAME(schema_id) + '.' + name, 'OwnerId')) AS owner_name  
    ,name   
FROM sys.types WHERE SCHEMA_NAME(schema_id) = '<schema_name>'   
UNION  
SELECT 'XML SCHEMA COLLECTION' AS entity_type   
    ,COALESCE(USER_NAME(xsc.principal_id),USER_NAME(s.principal_id)) AS owner_name  
    ,xsc.name   
FROM sys.xml_schema_collections AS xsc JOIN sys.schemas AS s  
    ON s.schema_id = xsc.schema_id  
WHERE s.name = '<schema_name>';  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="_FAQ3"></a> Como localizar todas as tabelas que não têm uma chave primária?  
 Antes de executar as consultas a seguir, substitua `<database_name>` pelo nome de um banco de dados válido.  
  
```  
USE <database_name>;  
GO  
SELECT SCHEMA_NAME(t.schema_id) AS schema_name  
    ,t.name AS table_name  
FROM sys.tables t   
WHERE object_id NOT IN   
   (  
    SELECT parent_object_id   
    FROM sys.key_constraints   
    WHERE type_desc = 'PRIMARY_KEY_CONSTRAINT' -- or type = 'PK'  
    );  
GO  
  
```  
  
 Ou então, execute a consulta a seguir.  
  
```  
USE <database_name>;  
GO  
SELECT SCHEMA_NAME(schema_id) AS schema_name  
    ,name AS table_name   
FROM sys.tables   
WHERE OBJECTPROPERTY(object_id,'TableHasPrimaryKey') = 0  
ORDER BY schema_name, table_name;  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="_FAQ4"></a> Como localizar todas as tabelas que não têm um índice?  
 Antes de executar a consulta a seguir, substitua `<database_name>` pelo nome de um banco de dados válido.  
  
```  
USE <database_name>;  
GO  
SELECT SCHEMA_NAME(schema_id) AS schema_name  
    ,name AS table_name  
FROM sys.tables   
WHERE OBJECTPROPERTY(object_id,'IsIndexed') = 0  
ORDER BY schema_name, table_name;  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="_FAQ5"></a> Como localizar todas as tabelas que têm uma coluna de identidade?  
 Antes de executar a consulta a seguir, substitua `<database_name>` pelo nome de um banco de dados válido.  
  
```  
USE <database_name>;  
GO  
SELECT SCHEMA_NAME(schema_id) AS schema_name  
    , t.name AS table_name  
    , c.name AS column_name  
FROM sys.tables AS t  
JOIN sys.identity_columns c ON t.object_id = c.object_id  
ORDER BY schema_name, table_name;  
GO  
  
```  
  
 Ou então, execute a consulta a seguir.  
  
> [!NOTE]  
>  Essa consulta não retorna o nome das colunas.  
  
```  
USE <database_name>;  
GO  
SELECT SCHEMA_NAME(schema_id) AS schema_name  
    ,name AS table_name   
FROM sys.tables   
WHERE OBJECTPROPERTY(object_id,'TableHasIdentity') = 1  
ORDER BY schema_name, table_name;  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="_FAQ7"></a> Como localizar os tipos de dados das colunas de uma tabela especificada?  
 Antes de executar a consulta a seguir, substitua `<database_name>` e `<schema_name.table_name>` por nomes válidos.  
  
```  
USE <database_name>;  
GO  
SELECT c.name AS column_name  
    ,c.column_id  
    ,SCHEMA_NAME(t.schema_id) AS type_schema  
    ,t.name AS type_name  
    ,t.is_user_defined  
    ,t.is_assembly_type  
    ,c.max_length  
    ,c.precision  
    ,c.scale  
FROM sys.columns AS c   
JOIN sys.types AS t ON c.user_type_id=t.user_type_id  
WHERE c.object_id = OBJECT_ID('<schema_name.table_name>')  
ORDER BY c.column_id;  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="_FAQ8"></a> Como localizar as dependências em uma função especificada?  
 Antes de executar a consulta a seguir, substitua `<database_name>` e `<schema_name.function_name>` por nomes válidos.  
  
```  
USE <database_name>;  
GO  
SELECT OBJECT_NAME(object_id) AS referencing_object_name  
    ,COALESCE(COL_NAME(object_id, column_id), '(n/a)') AS referencing_column_name  
    ,*  
FROM sys.sql_dependencies  
WHERE referenced_major_id = OBJECT_ID('<schema_name.function_name>')  
ORDER BY OBJECT_NAME(object_id), COL_NAME(object_id, column_id);  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="_FAQ9"></a> Como localizar todos os procedimentos armazenados em um banco de dados?  
 Antes de executar a consulta a seguir, substitua `<database_name>` por um nome válido.  
  
```  
  
USE <database_name>;  
GO  
SELECT name AS procedure_name   
    ,SCHEMA_NAME(schema_id) AS schema_name  
    ,type_desc  
    ,create_date  
    ,modify_date  
FROM sys.procedures;  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="_FAQ10"></a> Como localizar os parâmetros para uma função ou procedimento armazenado especificado?  
 Antes de executar a consulta a seguir, substitua `<database_name>` e `<schema_name.object_name>` por nomes válidos.  
  
```  
USE <database_name>;  
GO  
SELECT SCHEMA_NAME(schema_id) AS schema_name  
    ,o.name AS object_name  
    ,o.type_desc  
    ,p.parameter_id  
    ,p.name AS parameter_name  
    ,TYPE_NAME(p.user_type_id) AS parameter_type  
    ,p.max_length  
    ,p.precision  
    ,p.scale  
    ,p.is_output  
FROM sys.objects AS o  
INNER JOIN sys.parameters AS p ON o.object_id = p.object_id  
WHERE o.object_id = OBJECT_ID('<schema_name.object_name>')  
ORDER BY schema_name, object_name, p.parameter_id;  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="_FAQ12"></a> Como localizar todas as funções definidas pelo usuário em um banco de dados?  
 Antes de executar a consulta a seguir, substitua `<database_name>` pelo nome de um banco de dados válido.  
  
```  
USE <database_name>;  
GO  
SELECT name AS function_name   
  ,SCHEMA_NAME(schema_id) AS schema_name  
  ,type_desc  
  ,create_date  
  ,modify_date  
FROM sys.objects  
WHERE type_desc LIKE '%FUNCTION%';  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="_FAQ13"></a> Como localizar todas as exibições em um banco de dados?  
 Antes de executar a consulta a seguir, substitua `<database_name>` pelo nome de um banco de dados válido.  
  
```  
USE <database_name>;  
GO  
SELECT name AS view_name   
  ,SCHEMA_NAME(schema_id) AS schema_name  
  ,OBJECTPROPERTYEX(object_id,'IsIndexed') AS IsIndexed  
  ,OBJECTPROPERTYEX(object_id,'IsIndexable') AS IsIndexable  
  ,create_date  
  ,modify_date  
FROM sys.views;  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="_FAQ6"></a> Como localizar todas as entidades que foram modificadas nos últimos N dias?  
 Antes de executar a consulta a seguir, substitua `<database_name>` e `<n_days>` por valores válidos.  
  
```  
USE <database_name>;  
GO  
SELECT name AS object_name   
  ,SCHEMA_NAME(schema_id) AS schema_name  
  ,type_desc  
  ,create_date  
  ,modify_date  
FROM sys.objects  
WHERE modify_date > GETDATE() - <n_days>  
ORDER BY modify_date;  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="_FAQ14"></a> Como localizar os tipos de dados LOB de uma tabela especificada?  
 Antes de executar a consulta a seguir, substitua `<database_name>` e `<schema_name.table_name>` por nomes válidos.  
  
```  
  
USE <database_name>;  
GO  
SELECT name AS column_name   
    ,column_id   
    ,TYPE_NAME(user_type_id) AS type_name  
    ,max_length  
    ,CASE   
       WHEN max_length = -1 AND TYPE_NAME(user_type_id) <> 'xml'  
            THEN 1  
            ELSE 0  
     END AS [(max)]  
FROM sys.columns  
WHERE object_id=OBJECT_ID('<schema_name.table_name>')   
    AND ( TYPE_NAME(user_type_id) IN ('xml','text', 'ntext','image')  
         OR (TYPE_NAME(user_type_id) IN ('varchar','nvarchar','varbinary')  
         AND max_length = -1)  
        );  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="_FAQ15"></a> Como posso exibir a definição de um módulo?  
 Antes de executar a consulta a seguir, substitua `<database_name>` e `<schema_name.object_name>` por nomes válidos.  
  
```  
USE <database_name>;  
GO  
SELECT definition  
FROM sys.sql_modules  
WHERE object_id = OBJECT_ID('<schema_name.object_name>');  
GO  
  
```  
  
 Ou então, use a função `OBJECT_DEFINITION`, conforme mostrado no exemplo a seguir.  
  
```  
USE <database_name>;  
GO  
SELECT OBJECT_DEFINITION (OBJECT_ID('<schema_name.object_name>')) AS ObjectDefinition;  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="_FAQ19"></a> Como posso exibir a definição de um gatilho de nível de servidor?  
  
```  
SELECT definition  
FROM sys.server_sql_modules;  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="_FAQ16"></a> Como localizar as colunas de uma chave primária para uma tabela especificada?  
 Antes de executar a consulta a seguir, substitua `<database_name>` e `<schema_name.table_name>` por nomes válidos.  
  
```  
USE <database_name>;  
GO  
SELECT i.name AS index_name  
    ,ic.index_column_id  
    ,key_ordinal  
    ,c.name AS column_name  
    ,TYPE_NAME(c.user_type_id)AS column_type   
    ,is_identity  
FROM sys.indexes AS i  
INNER JOIN sys.index_columns AS ic   
    ON i.object_id = ic.object_id AND i.index_id = ic.index_id  
INNER JOIN sys.columns AS c   
    ON ic.object_id = c.object_id AND c.column_id = ic.column_id  
WHERE i.is_primary_key = 1   
    AND i.object_id = OBJECT_ID('<schema_name.table_name>');  
GO  
  
```  
  
 Ou então, use a função `COL_NAME`, conforme mostrado no exemplo a seguir.  
  
```  
USE <database_name>;  
GO  
SELECT i.name AS index_name  
    ,COL_NAME(ic.object_id,ic.column_id) AS column_name  
    ,ic.index_column_id  
    ,key_ordinal  
FROM sys.indexes AS i  
INNER JOIN sys.index_columns AS ic   
    ON i.object_id = ic.object_id AND i.index_id = ic.index_id  
WHERE i.is_primary_key = 1   
    AND i.object_id = OBJECT_ID('<schema_name.table_name>');  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="_FAQ17"></a> Como localizar as colunas de uma chave estrangeira para uma tabela especificada?  
 Antes de executar a consulta a seguir, substitua `<database_name>` e `<schema_name.table_name>` por nomes válidos.  
  
```  
USE <database_name>;  
GO  
SELECT   
    f.name AS foreign_key_name  
   ,OBJECT_NAME(f.parent_object_id) AS table_name  
   ,COL_NAME(fc.parent_object_id, fc.parent_column_id) AS constraint_column_name  
   ,OBJECT_NAME (f.referenced_object_id) AS referenced_object  
   ,COL_NAME(fc.referenced_object_id, fc.referenced_column_id) AS referenced_column_name  
   ,is_disabled  
   ,delete_referential_action_desc  
   ,update_referential_action_desc  
FROM sys.foreign_keys AS f  
INNER JOIN sys.foreign_key_columns AS fc   
   ON f.object_id = fc.constraint_object_id   
WHERE f.parent_object_id = OBJECT_ID('<schema_name.table_name>');  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="_FAQ18"></a> Como localizar as permissões concedidas ou negadas a uma entidade especificada?  
 O exemplo a seguir cria uma função para retornar o nome da entidade na qual as permissões são verificadas. A função é chamada nas consultas a seguir. A função deve ser criada em cada banco de dados no qual você quer verificar permissões.  
  
```  
-- Create a function to return the name of the entity on which the permissions are checked.  
IF OBJECT_ID (N'dbo.entity_instance_name', N'FN') IS NOT NULL  
    DROP FUNCTION dbo.entity_instance_name;  
GO  
CREATE FUNCTION dbo.entity_instance_name(@class_desc nvarchar(60), @major_id int)   
RETURNS sysname AS  
BEGIN  
    DECLARE @the_entity_name sysname  
    SELECT @the_entity_name = CASE  
        WHEN @class_desc = 'DATABASE' THEN DB_NAME()  
        WHEN @class_desc = 'SCHEMA' THEN SCHEMA_NAME(@major_id)  
        WHEN @class_desc = 'OBJECT_OR_COLUMN' THEN OBJECT_NAME(@major_id)  
        WHEN @class_desc = 'DATABASE_PRINCIPAL' THEN USER_NAME(@major_id)  
        WHEN @class_desc = 'ASSEMBLY' THEN   
            (SELECT name FROM sys.assemblies WHERE assembly_id=@major_id)  
        WHEN @class_desc = 'TYPE' THEN TYPE_NAME(@major_id)  
        WHEN @class_desc = 'XML_SCHEMA_COLLECTION' THEN   
            (SELECT name FROM sys.xml_schema_collections  
              WHERE xml_collection_id=@major_id)  
        WHEN @class_desc = 'MESSAGE_TYPE' THEN   
            (SELECT name FROM sys.service_message_types WHERE message_type_id=@major_id)  
        WHEN @class_desc = 'SERVICE_CONTRACT' THEN   
           (SELECT name FROM sys.service_contracts  
              WHERE service_contract_id=@major_id)  
        WHEN @class_desc = 'SERVICE' THEN  
          (SELECT name FROM sys.services WHERE service_id=@major_id)  
        WHEN @class_desc = 'REMOTE_SERVICE_BINDING' THEN  
          (SELECT name FROM sys.remote_service_bindings  
             WHERE remote_service_binding_id=@major_id)  
        WHEN @class_desc = 'ROUTE' THEN  
          (SELECT name FROM sys.routes WHERE route_id=@major_id)  
        WHEN @class_desc = 'FULLTEXT_CATALOG' THEN  
          (SELECT name FROM sys.fulltext_catalogs WHERE fulltext_catalog_id=@major_id)  
        WHEN @class_desc = 'SYMMETRIC_KEY' THEN  
          (SELECT name FROM sys.symmetric_keys WHERE symmetric_key_id=@major_id)  
        WHEN @class_desc = 'CERTIFICATE' THEN  
          (SELECT name FROM sys.certificates WHERE certificate_id=@major_id)  
        WHEN @class_desc = 'ASYMMETRIC_KEY' THEN  
          (SELECT name FROM sys.asymmetric_keys WHERE asymmetric_key_id=@major_id)  
        WHEN @class_desc = 'SERVER' THEN   
             (SELECT name FROM sys.servers WHERE server_id=@major_id)  
        WHEN @class_desc = 'SERVER_PRINCIPAL' THEN SUSER_NAME(@major_id)  
        WHEN @class_desc = 'ENDPOINT' THEN   
             (SELECT name FROM sys.endpoints WHERE endpoint_id=@major_id)        
        ELSE '?'  
    END  
    RETURN @the_entity_name  
END;  
GO  
-- Return server-level permissions for the user.  
SELECT class  
    ,class_desc  
    ,dbo.entity_instance_name(class_desc, major_id) AS entity_name   
    ,minor_id  
    ,SUSER_NAME(grantee_principal_id) AS grantee  
    ,SUSER_NAME(grantor_principal_id) AS grantor  
    ,type  
    ,permission_name  
    ,state_desc   
FROM sys.server_permissions   
WHERE grantee_principal_id = SUSER_ID('public');  
GO  
-- Return database-level permissions for the user.  
SELECT class  
    ,class_desc  
    ,dbo.entity_instance_name(class_desc , major_id) AS entity_name   
    ,minor_id  
    ,USER_NAME(grantee_principal_id) AS grantee  
    ,USER_NAME(grantor_principal_id) AS grantor  
    ,type  
    ,permission_name  
    ,state_desc     
FROM  sys.database_permissions   
WHERE grantee_principal_id = DATABASE_PRINCIPAL_ID('public');  
GO  
```  
  
 [TOP](#_TOP)  
  
###  <a name="_FAQ20"></a> Como determinar se uma coluna é usada em uma expressão de coluna computada?  
 Antes de executar a consulta a seguir, substitua `<database_name>`, `<schema_name.table_name>` e `<column_name`> por nomes válidos.  
  
```  
USE <database_name>;  
GO  
SELECT OBJECT_NAME(object_id) AS object_name  
    ,COL_NAME(object_id, column_id) AS computed_column   
    ,class_desc  
    ,is_selected  
    ,is_updated  
    ,is_select_all  
FROM sys.sql_dependencies  
WHERE referenced_major_id = OBJECT_ID('<schema_name.table_name>')  
    AND referenced_minor_id = COLUMNPROPERTY(referenced_major_id, '<column_name>', 'ColumnId')  
    AND class = 1;  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="_FAQ21"></a> Como localizar todas as colunas que são usadas em uma expressão de coluna computada?  
 Antes de executar a consulta a seguir, substitua `<database_name>` por um nome válido.  
  
```  
USE <database_name>;  
GO  
SELECT OBJECT_NAME(d.referenced_major_id) AS object_name  
    ,COL_NAME(d.referenced_major_id, d.referenced_minor_id) AS column_name  
    ,OBJECT_NAME(referenced_major_id) AS dependent_object_name   
    ,COL_NAME(d.object_id, d.column_id) AS dependent_computed_column  
    ,cc.definition AS computed_column_definition  
FROM sys.sql_dependencies AS d  
JOIN sys.computed_columns AS cc   
    ON cc.object_id = d.object_id AND cc.column_id = d.column_id AND d.object_id=d.referenced_major_id       
WHERE d.class = 1  
ORDER BY object_name, column_name;  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="_FAQ22"></a> Como localizar as colunas que dependem de um tipo especificado do CLR definidas pelo usuário ou tipo de alias?  
 Antes de executar a consulta a seguir, substitua `<database_name>` com um nome válido e `<schema_name.data_type_name>` com válido e qualificado por esquema CLR-tipo definido pelo usuário ou nome de tipo qualificado por esquema ou alias. A consulta a seguir requer a participação na **db_owner** função ou permissões para ver todas as colunas dependentes e a coluna computada metadados no banco de dados.  
  
```  
USE <database_name>;  
GO  
SELECT OBJECT_NAME(object_id) AS object_name   
    ,c.name AS column_name   
    ,SCHEMA_NAME(t.schema_id) AS schema_name  
    ,TYPE_NAME(c.user_type_id) AS user_type_name  
    ,c.max_length  
    ,c.precision  
    ,c.scale  
    ,c.is_nullable  
    ,c.is_computed  
FROM sys.columns AS c  
INNER JOIN sys.types AS t ON c.user_type_id = t.user_type_id  
WHERE c.user_type_id = TYPE_ID('<schema_name.data_type_name>');   
GO  
  
```  
  
 A consulta a seguir retorna uma exibição restrita e estrita de colunas dependentes de um tipo CLR definido pelo usuário ou alias, mas o conjunto de resultados é visível para o **pública** função. Você poderá usar essa consulta se tiver concedido permissões REFERENCE em seu tipo definido pelo usuário para outros e se você não tiver permissão para exibir os metadados dos objetos que outros criaram e que usam o tipo.  
  
```  
USE <database_name>;  
GO  
SELECT OBJECT_NAME(object_id) AS object_name   
    ,COL_NAME(object_id, column_id) AS column_name  
    ,TYPE_NAME(user_type_id) AS user_type  
FROM sys.column_type_usages  
WHERE user_type_id = TYPE_ID('<schema_name.data_type_name>');  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="_FAQ23"></a> Como localizar as colunas computadas que dependem de um tipo especificado do CLR definidas pelo usuário ou tipo de alias?  
 Antes de você executar a consulta a seguir, substitua `<database_name>` por um nome válido e `<schema_name.data_type_name>` por um tipo de dados CLR definido pelo usuário válido e qualificado por esquema ou nome de tipo de alias.  
  
```  
USE <database_name>;  
GO  
SELECT OBJECT_NAME(object_id) AS object_name  
    ,COL_NAME(object_id, column_id) AS column_name  
FROM sys.sql_dependencies  
WHERE referenced_major_id = TYPE_ID('<schema_name.data_type_name>')  
    AND class = 2 -- schema-bound references to type  
    AND OBJECTPROPERTY(object_id, 'IsTable') = 1;   -- exclude non-table dependencies  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="_FAQ24"></a> Como localizar os parâmetros que dependem de um tipo especificado do CLR definidas pelo usuário ou tipo de alias?  
 Antes de você executar a consulta a seguir, substitua `<database_name>` por um nome válido e `<schema_name.data_type_name>` por um tipo de dados CLR definido pelo usuário válido e qualificado por esquema ou nome de tipo de alias. A consulta a seguir requer a participação na **db_owner** função ou permissões para ver todas as colunas dependentes e a coluna computada metadados no banco de dados.  
  
```  
USE <database_name>;  
GO  
SELECT OBJECT_NAME(object_id) AS object_name  
    ,NULL AS procedure_number  
    ,name AS param_name  
    ,parameter_id AS param_num  
    ,TYPE_NAME(p.user_TYPE_ID) AS type_name  
FROM sys.parameters AS p  
WHERE p.user_TYPE_ID = TYPE_ID('<schema_name.data_type_name>')  
UNION   
SELECT OBJECT_NAME(object_id) AS object_name  
    ,procedure_number  
    ,name AS param_name  
    ,parameter_id AS param_num  
    ,TYPE_NAME(p.user_TYPE_ID) AS type_name  
FROM sys.numbered_procedure_parameters AS p  
WHERE p.user_TYPE_ID = TYPE_ID('<schema_name.data_type_name>')  
ORDER BY object_name, procedure_number, param_num;  
GO  
  
```  
  
 A consulta a seguir retorna uma exibição restrita e estrita de parâmetros que dependem de um tipo CLR definido pelo usuário ou alias, mas o conjunto de resultados é visível para o **pública** função. Você poderá usar essa consulta se tiver concedido permissões REFERENCE em seu tipo definido pelo usuário para outros e se você não tiver permissão para exibir os metadados dos objetos que outros criaram e que usam o tipo.  
  
```  
USE <database_name>;  
GO  
SELECT OBJECT_NAME(object_id) AS object_name  
    ,parameter_id  
    ,TYPE_NAME(user_type_id) AS type_name  
FROM sys.parameter_type_usages   
WHERE user_type_id = TYPE_ID('<schema_name.data_type_name>');  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="_FAQ25"></a> Como posso encontrar as restrições CHECK que dependem de um tipo definido pelo usuário CLR especificado?  
 Antes de executar a consulta a seguir, substitua `<database_name>` com um nome válido e `<schema_name.data_type_name>` com um nome válido e qualificado por esquema de tipo definido pelo usuário CLR.  
  
```  
USE <database_name>;  
GO  
SELECT SCHEMA_NAME(o.schema_id) AS schema_name  
    ,OBJECT_NAME(o.parent_object_id) AS table_name  
    ,OBJECT_NAME(o.object_id) AS constraint_name  
FROM sys.sql_dependencies AS d  
JOIN sys.objects AS o ON o.object_id = d.object_id  
WHERE referenced_major_id = TYPE_ID('<schema_name.data_type_name>')  
    AND class = 2 -- schema-bound references to type  
    AND OBJECTPROPERTY(o.object_id, 'IsCheckCnst') = 1; -- exclude non-CHECK dependencies  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="_FAQ26"></a> Como localizar as exibições, funções Transact-SQL e procedimentos armazenados Transact-SQL que dependem de um tipo especificado do CLR definidas pelo usuário ou tipo de alias?  
 Antes de você executar a consulta a seguir, substitua `<database_name>` por um nome válido e `<schema_name.data_type_name>` por um tipo de dados CLR definido pelo usuário válido e qualificado por esquema ou nome de tipo de alias.  
  
 Os parâmetros definidos em uma função ou procedimento são implicitamente associados ao esquema. Portanto, os parâmetros que dependem de um tipo CLR definido pelo usuário ou tipo de alias podem ser exibidos usando o [sys. sql_dependencies](../../relational-databases/system-catalog-views/sys-sql-dependencies-transact-sql.md) exibição do catálogo. Os procedimentos e os gatilhos não são associados ao esquema. Isso significa que as dependências entre qualquer expressão definida no corpo do procedimento ou gatilho e um tipo de dados CLR definido pelo usuário ou tipo de alias não é mantido. Exibições associadas ao esquema e funções definidas pelo usuário que têm expressões que dependem de um tipo CLR definidos pelo usuário associadas a esquema ou tipo de alias são mantidas na **sys. sql_dependencies** exibição do catálogo. Não são mantidas dependências entre tipos, funções CLR e procedimentos CLR.  
  
 A consulta a seguir retorna todas as dependências associadas por esquema em exibições, funções do [!INCLUDE[tsql](../../includes/tsql-md.md)] e procedimentos armazenados [!INCLUDE[tsql](../../includes/tsql-md.md)] para um tipo de dados CLR definido pelo usuário ou de alias especificado.  
  
```  
USE <database_name>;  
GO  
SELECT SCHEMA_NAME(o.schema_id) AS dependent_object_schema  
  ,OBJECT_NAME(o.object_id) AS dependent_object_name  
  ,o.type_desc AS dependent_object_type  
  ,d.class_desc AS kind_of_dependency  
  ,TYPE_NAME (d.referenced_major_id) AS type_name  
FROM sys.sql_dependencies AS d   
JOIN sys.objects AS o  
  ON d.object_id = o.object_id  
  AND o.type IN ('FN','IF','TF', 'V', 'P')  
WHERE d.class = 2 -- dependencies on types  
  AND d.referenced_major_id = TYPE_ID('<schema_name.data_type_name>')  
ORDER BY dependent_object_schema, dependent_object_name;  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="_FAQ27"></a> Como localizar todas as restrições para uma tabela especificada?  
 Antes de executar a consulta a seguir, substitua `<database_name>` e `<schema_name.table_name>` por nomes válidos.  
  
```  
USE <database_name>;  
GO  
SELECT OBJECT_NAME(object_id) as constraint_name  
    ,SCHEMA_NAME(schema_id) AS schema_name  
    ,OBJECT_NAME(parent_object_id) AS table_name  
    ,type_desc  
    ,create_date  
    ,modify_date  
    ,is_ms_shipped  
    ,is_published  
    ,is_schema_published  
FROM sys.objects  
WHERE type_desc LIKE '%CONSTRAINT'   
    AND parent_object_id = OBJECT_ID('<schema_name.table_name>');  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="_FAQ28"></a> Como localizar todos os índices para uma tabela especificada?  
 Antes de executar a consulta a seguir, substitua `<database_name>` e `<schema_name.table_name>` por nomes válidos.  
  
```  
USE <database_name>;  
GO  
SELECT i.name AS index_name  
    ,i.type_desc  
    ,is_unique  
    ,ds.type_desc AS filegroup_or_partition_scheme  
    ,ds.name AS filegroup_or_partition_scheme_name  
    ,ignore_dup_key  
    ,is_primary_key  
    ,is_unique_constraint  
    ,fill_factor  
    ,is_padded  
    ,is_disabled  
    ,allow_row_locks  
    ,allow_page_locks  
FROM sys.indexes AS i  
INNER JOIN sys.data_spaces AS ds ON i.data_space_id = ds.data_space_id  
WHERE is_hypothetical = 0 AND i.index_id <> 0   
AND i.object_id = OBJECT_ID('<schema_name.table_name>');  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="_FAQ30"></a> Como localizar todos os objetos que têm um nome de coluna especificado?  
 Antes de executar a consulta a seguir, substitua `<database_name>` e `<column_name>` por nomes válidos.  
  
```  
USE <database_name>;  
GO  
SELECT OBJECT_NAME(object_id)  
FROM sys.columns  
WHERE name = '<column_name>';  
GO  
  
```  
  
 Ou  
  
```  
USE <database_name>;  
GO  
SELECT SCHEMA_NAME(o.schema_id) AS schema_name   
    ,o.name AS object_name  
    ,type_desc  
FROM sys.objects AS o  
INNER JOIN sys.columns AS c ON o.object_id = c.object_id  
WHERE c.name = '<column_name>';  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="_FAQ31"></a> Como localizar todas as tabelas definidas pelo usuário em um banco de dados especificado?  
 Antes de executar a consulta a seguir, substitua `<database_name>` por um nome válido.  
  
```  
USE <database_name>;  
GO  
SELECT *   
FROM sys.tables;  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="_FAQ32"></a> Como localizar todas as tabelas e índices particionados?  
 Antes de executar a consulta a seguir, substitua `<database_name>` por um nome válido.  
  
```  
USE <database_name>;  
GO  
SELECT SCHEMA_NAME(o.schema_id) AS schema_name  
    ,OBJECT_NAME(p.object_id) AS table_name  
    ,i.name AS index_name  
    ,p.partition_number  
    ,rows   
FROM sys.partitions AS p  
INNER JOIN sys.indexes AS i ON p.object_id = i.object_id AND p.index_id = i.index_id  
INNER JOIN sys.partition_schemes ps ON i.data_space_id=ps.data_space_id  
INNER JOIN sys.objects AS o ON o.object_id = i.object_id  
ORDER BY index_name, partition_number;  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="_FAQ33"></a> Como localizar todas as estatísticas em um objeto especificado?  
 Antes de executar a consulta a seguir, substitua `<database_name>` por um nome válido e `<schema_name.object_name>` por uma tabela válida, exibição indexada ou nome de função com valor de tabela.  
  
```  
USE <database_name>;  
GO  
SELECT name AS statistics_name  
    ,stats_id  
    ,auto_created  
    ,user_created  
    ,no_recompute  
FROM sys.stats  
WHERE object_id = OBJECT_ID('<schema_name.object_name>');  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="_FAQ34"></a> Como localizar todas as estatísticas e as colunas em um objeto especificado?  
 Antes de executar a consulta a seguir, substitua `<database_name>` por um nome válido e `<schema_name.object_name>` por uma tabela válida, exibição indexada ou nome de função com valor de tabela.  
  
```  
USE <database_name>;  
GO  
SELECT s.name AS statistics_name  
    ,c.name AS column_name  
    ,sc.stats_column_id  
FROM sys.stats AS s  
INNER JOIN sys.stats_columns AS sc   
    ON s.object_id = sc.object_id AND s.stats_id = sc.stats_id  
INNER JOIN sys.columns AS c   
    ON sc.object_id = c.object_id AND c.column_id = sc.column_id  
WHERE s.object_id = OBJECT_ID('<schema_name.object_name>');  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="_FAQ35"></a> Como localizar a definição de um modo de exibição?  
 Antes de executar a consulta a seguir, substitua `<database_name>` e `<schema_name.object_name>` por nomes válidos.  
  
```  
USE <database_name>;  
GO  
SELECT definition  
FROM sys.sql_modules  
WHERE object_id = OBJECT_ID('<schema_name.object_name>');  
GO  
  
```  
  
 Ou então, use a função `OBJECT_DEFINITION`, conforme mostrado no exemplo a seguir.  
  
```  
USE <database_name>;  
GO  
SELECT OBJECT_DEFINITION (OBJECT_ID('<schema_name.object_name>')) AS ObjectDefinition;  
GO  
  
```  
  
 [TOP](#_TOP)  
  
## <a name="see-also"></a>Consulte também  
 [Mapeando tabelas do sistema para exibições do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)  
  
  
