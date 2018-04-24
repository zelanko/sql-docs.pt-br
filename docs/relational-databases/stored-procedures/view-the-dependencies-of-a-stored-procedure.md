---
title: Exibir as dependências de um procedimento armazenado| Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-stored-Procs
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- stored procedures [SQL Server], dependencies
- displaying stored procedure dependencies
- viewing stored procedure dependencies
ms.assetid: 6ae0a369-1bc7-4ae4-be89-2b483697cd1f
caps.latest.revision: 26
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: On Demand
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 489595e478497d0dc326931b536f2f7068a37f13
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="view-the-dependencies-of-a-stored-procedure"></a>Exibir as dependências de um procedimento armazenado
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  Este tópico descreve como exibir dependências de procedimento armazenado no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
##  <a name="Top"></a>   
-   **Antes de começar:**  [Limitações e restrições](#Restrictions), [Segurança](#Security)  
  
-   **To view the dependencies of a procedure, using:**  [SQL Server Management Studio](#SSMSProcedure), [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Restrictions"></a> Limitações e restrições  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Função do sistema: **sys.dm_sql_referencing_entities**  
 Requer a permissão CONTROL da entidade referenciada e a permissão SELECT em sys.dm_sql_referencing_entities. Quando a entidade referenciada é uma função de partição, a permissão CONTROL é exigida no banco de dados. Por padrão, a permissão SELECT é concedida a público.  
  
 Função do sistema: **sys.dm_sql_referenced_entities**  
 Requer permissão SELECT em sys.dm_sql_referenced_entities e permissão VIEW DEFINITION na entidade de referência. Por padrão, a permissão SELECT é concedida a público. Requer permissão VIEW DEFINITION no banco de dados ou permissão ALTER DATABASE DDL TRIGGER no banco de dados quando a entidade de referência é um gatilho DDL do banco de dados. Requer permissão de VIEW ANY DEFINITION no servidor quando a entidade de referência é um gatilho DDL de servidor.  
  
 Exibição de catálogo do objeto: **sys.sql_expression_dependencies**  
 Requer permissão VIEW DEFINITION no banco de dados e permissão SELECT em sys.sql_expression_dependencies para o banco de dados. Por padrão, a permissão SELECT é concedida somente a membros da função de banco de dados fixa db_owner. Quando são concedidas permissões SELECT e VIEW DEFINITION a outro usuário, o usuário autorizado pode exibir todas as dependências no banco de dados.  
  
##  <a name="Procedures"></a> Como exibir as dependências de um procedimento armazenado  
 Você pode usar uma das seguintes opções:  
  
-   [SQL Server Management Studio](#SSMSProcedure)  
  
-   [Transact-SQL](#TsqlProcedure)  
  
###  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
 **Para exibir as dependências de um procedimento armazenado no Pesquisador de Objetos**  
  
1.  No Pesquisador de Objetos, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] e expanda-a.  
  
2.  Expanda **Bancos de Dados**, expanda o banco de dados ao qual pertence o procedimento e expanda **Programação**.  
  
3.  Expanda **Procedimentos Armazenados**, clique com o botão direito do mouse no procedimento e clique em **Exibir Dependências**.  
  
4.  Exiba a lista de objetos que dependem do procedimento.  
  
5.  Exiba a lista de objetos dos quais o procedimento depende.  
  
6.  Clique em **OK**.  
  
###  <a name="TsqlProcedure"></a> Usando o Transact-SQL  
 **Para exibir as dependências de um procedimento no Editor de Consultas**  
  
 Função do sistema: **sys.dm_sql_referencing_entities**  
 Esta função é usada para exibir os objetos que dependem de um procedimento.  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] e expanda-a.  
  
2.  Expanda **Bancos de Dados**e o banco de dados ao qual o procedimento pertence.  
  
3.  Clique em **Nova Consulta** no menu **Arquivo** .  
  
4.  Copie e cole os exemplos a seguir no editor de consultas. O primeiro exemplo cria o procedimento `uspVendorAllInfo` , que retorna os nomes de todos os fornecedores no banco de dados [!INCLUDE[ssSampleDBCoFull](../../includes/sssampledbcofull-md.md)] , os produtos que eles fornecem, suas classificações de crédito e sua disponibilidade.  
  
    ```  
    USE AdventureWorks2008R2;  
    GO  
    IF OBJECT_ID ( 'Purchasing.uspVendorAllInfo', 'P' ) IS NOT NULL   
        DROP PROCEDURE Purchasing.uspVendorAllInfo;  
    GO  
    CREATE PROCEDURE Purchasing.uspVendorAllInfo  
    WITH EXECUTE AS CALLER  
    AS  
        SET NOCOUNT ON;  
        SELECT v.Name AS Vendor, p.Name AS 'Product name',   
          v.CreditRating AS 'Rating',   
          v.ActiveFlag AS Availability  
        FROM Purchasing.Vendor v   
        INNER JOIN Purchasing.ProductVendor pv  
          ON v.BusinessEntityID = pv.BusinessEntityID   
        INNER JOIN Production.Product p  
          ON pv.ProductID = p.ProductID   
        ORDER BY v.Name ASC;  
    GO  
    ```  
  
5.  Depois que o procedimento é criado, o segundo exemplo usa a função sys.dm_sql_referencing_entities para exibir os objetos que dependem do procedimento.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    SELECT referencing_schema_name, referencing_entity_name, referencing_id, referencing_class_desc, is_caller_dependent  
    FROM sys.dm_sql_referencing_entities ('Purchasing.uspVendorAllInfo', 'OBJECT');   
    GO  
  
    ```  
  
 Função do sistema: **sys.dm_sql_referenced_entities**  
 Esta função é usada para exibir os objetos dos quais um procedimento depende.  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] e expanda-a.  
  
2.  Expanda **Bancos de Dados**e o banco de dados ao qual o procedimento pertence.  
  
3.  Clique em **Nova Consulta** no menu **Arquivo** .  
  
4.  Copie e cole os exemplos a seguir no editor de consultas. O primeiro exemplo cria o procedimento `uspVendorAllInfo` , que retorna os nomes de todos os fornecedores no banco de dados [!INCLUDE[ssSampleDBCoFull](../../includes/sssampledbcofull-md.md)] , os produtos que eles fornecem, suas classificações de crédito e sua disponibilidade.  
  
    ```  
    USE AdventureWorks2008R2;  
    GO  
    IF OBJECT_ID ( 'Purchasing.uspVendorAllInfo', 'P' ) IS NOT NULL   
        DROP PROCEDURE Purchasing.uspVendorAllInfo;  
    GO  
    CREATE PROCEDURE Purchasing.uspVendorAllInfo  
    WITH EXECUTE AS CALLER  
    AS  
        SET NOCOUNT ON;  
        SELECT v.Name AS Vendor, p.Name AS 'Product name',   
          v.CreditRating AS 'Rating',   
          v.ActiveFlag AS Availability  
        FROM Purchasing.Vendor v   
        INNER JOIN Purchasing.ProductVendor pv  
          ON v.BusinessEntityID = pv.BusinessEntityID   
        INNER JOIN Production.Product p  
          ON pv.ProductID = p.ProductID   
        ORDER BY v.Name ASC;  
    GO  
    ```  
  
5.  Depois que o procedimento é criado, o segundo exemplo usa a função sys.dm_sql_referenced_entities para exibir os objetos dos quais o procedimento depende.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    SELECT referenced_schema_name, referenced_entity_name,  
    referenced_minor_name,referenced_minor_id, referenced_class_desc,  
    is_caller_dependent, is_ambiguous  
    FROM sys.dm_sql_referencing_entities ('Purchasing.uspVendorAllInfo', 'OBJECT');  
    GO  
    ```  
  
 Exibição de catálogo do objeto: **sys.sql_expression_dependencies**  
 Esta exibição pode ser usada para exibir objetos dos quais um procedimento depende ou que dependem de um procedimento.  
  
 Exibindo os objetos que dependem de um procedimento.  
 1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] e expanda-a.  
  
2.  Expanda **Bancos de Dados**e o banco de dados ao qual o procedimento pertence.  
  
3.  Clique em **Nova Consulta** no menu **Arquivo** .  
  
4.  Copie e cole os exemplos a seguir no editor de consultas. O primeiro exemplo cria o procedimento `uspVendorAllInfo` , que retorna os nomes de todos os fornecedores no banco de dados [!INCLUDE[ssSampleDBCoFull](../../includes/sssampledbcofull-md.md)] , os produtos que eles fornecem, suas classificações de crédito e sua disponibilidade.  
  
    ```  
    USE AdventureWorks2008R2;  
    GO  
    IF OBJECT_ID ( 'Purchasing.uspVendorAllInfo', 'P' ) IS NOT NULL   
        DROP PROCEDURE Purchasing.uspVendorAllInfo;  
    GO  
    CREATE PROCEDURE Purchasing.uspVendorAllInfo  
    WITH EXECUTE AS CALLER  
    AS  
        SET NOCOUNT ON;  
        SELECT v.Name AS Vendor, p.Name AS 'Product name',   
          v.CreditRating AS 'Rating',   
          v.ActiveFlag AS Availability  
        FROM Purchasing.Vendor v   
        INNER JOIN Purchasing.ProductVendor pv  
          ON v.BusinessEntityID = pv.BusinessEntityID   
        INNER JOIN Production.Product p  
          ON pv.ProductID = p.ProductID   
        ORDER BY v.Name ASC;  
    GO  
    ```  
  
5.  Depois que o procedimento é criado, o segundo exemplo usa a exibição sys.sql_expression_dependencies para exibir os objetos que dependem do procedimento.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    SELECT OBJECT_SCHEMA_NAME ( referencing_id ) AS referencing_schema_name,  
        OBJECT_NAME(referencing_id) AS referencing_entity_name,   
        o.type_desc AS referencing_desciption,   
        COALESCE(COL_NAME(referencing_id, referencing_minor_id), '(n/a)') AS referencing_minor_id,   
        referencing_class_desc, referenced_class_desc,  
        referenced_server_name, referenced_database_name, referenced_schema_name,  
        referenced_entity_name,   
        COALESCE(COL_NAME(referenced_id, referenced_minor_id), '(n/a)') AS referenced_column_name,  
        is_caller_dependent, is_ambiguous  
    FROM sys.sql_expression_dependencies AS sed  
    INNER JOIN sys.objects AS o ON sed.referencing_id = o.object_id  
    WHERE referenced_id = OBJECT_ID(N'Purchasing.uspVendorAllInfo')  
    GO  
    ```  
  
 Exibindo os objetos dois quais um procedimento depende.  
 1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] e expanda-a.  
  
2.  Expanda **Bancos de Dados**e o banco de dados ao qual o procedimento pertence.  
  
3.  Clique em **Nova Consulta** no menu **Arquivo** .  
  
4.  Copie e cole os exemplos a seguir no editor de consultas. O primeiro exemplo cria o procedimento `uspVendorAllInfo` , que retorna os nomes de todos os fornecedores no banco de dados [!INCLUDE[ssSampleDBCoFull](../../includes/sssampledbcofull-md.md)] , os produtos que eles fornecem, suas classificações de crédito e sua disponibilidade.  
  
    ```  
    USE AdventureWorks2008R2;  
    GO  
    IF OBJECT_ID ( 'Purchasing.uspVendorAllInfo', 'P' ) IS NOT NULL   
        DROP PROCEDURE Purchasing.uspVendorAllInfo;  
    GO  
    CREATE PROCEDURE Purchasing.uspVendorAllInfo  
    WITH EXECUTE AS CALLER  
    AS  
        SET NOCOUNT ON;  
        SELECT v.Name AS Vendor, p.Name AS 'Product name',   
          v.CreditRating AS 'Rating',   
          v.ActiveFlag AS Availability  
        FROM Purchasing.Vendor v   
        INNER JOIN Purchasing.ProductVendor pv  
          ON v.BusinessEntityID = pv.BusinessEntityID   
        INNER JOIN Production.Product p  
          ON pv.ProductID = p.ProductID   
        ORDER BY v.Name ASC;  
    GO  
    ```  
  
5.  Depois que o procedimento é criado, o segundo exemplo usa a exibição sys.sql_expression_dependencies para exibir os objetos dos quais o procedimento depende.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    SELECT OBJECT_NAME(referencing_id) AS referencing_entity_name,   
        o.type_desc AS referencing_desciption,   
        COALESCE(COL_NAME(referencing_id, referencing_minor_id), '(n/a)') AS referencing_minor_id,   
        referencing_class_desc, referenced_class_desc,  
        referenced_server_name, referenced_database_name, referenced_schema_name,  
        referenced_entity_name,   
        COALESCE(COL_NAME(referenced_id, referenced_minor_id), '(n/a)') AS referenced_column_name,  
        is_caller_dependent, is_ambiguous  
    FROM sys.sql_expression_dependencies AS sed  
    INNER JOIN sys.objects AS o ON sed.referencing_id = o.object_id  
    WHERE referencing_id = OBJECT_ID(N'Purchasing.uspVendorAllInfo');  
    GO  
    ```  
  
## <a name="see-also"></a>Consulte Também  
 [Renomear um procedimento armazenado](../../relational-databases/stored-procedures/rename-a-stored-procedure.md)   
 [sys.dm_sql_referencing_entities &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-sql-referencing-entities-transact-sql.md)   
 [sys.dm_sql_referenced_entities &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-sql-referenced-entities-transact-sql.md)   
 [sys.sql_expression_dependencies &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql.md)  
  
  
