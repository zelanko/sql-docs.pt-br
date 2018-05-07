---
title: sql_referenced_entities (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/09/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dm_sql_referenced_entities_TSQL
- dm_sql_referenced_entities
- sys.dm_sql_referenced_entities
- sys.dm_sql_referenced_entities_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_sql_referenced_entities dynamic management function
ms.assetid: 077111cb-b860-4d61-916f-bac5d532912f
caps.latest.revision: 46
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 25c80c8239653415486d18d0773c45076668ca18
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
---
# <a name="sysdmsqlreferencedentities-transact-sql"></a>sys.dm_sql_referenced_entities (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Retorna uma linha para cada entidade definida pelo usuário, referenciada por nome na definição da entidade de referência especificada no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Uma dependência entre duas entidades é criada quando uma entidade definida pelo usuário, chamado de *entidade referenciada*, aparece por nome em uma expressão SQL persistente de outra entidade definida pelo usuário, chamada de *entidade de referência* . Por exemplo, se um procedimento armazenado for a entidade de referência especificada, essa função retornará todas as entidades definidas pelo usuário que são referenciadas no procedimento armazenado como tabelas, exibições, UDTs (Tipos Definidos pelo Usuário) ou outros procedimentos armazenados.  
  
 Você pode usar essa função de gerenciamento dinâmico para informar os seguintes tipos de entidades referenciadas pela entidade de referência especificada:  
  
-   Entidades associadas a esquema  
  
-   Entidades não associadas a esquema  
  
-   Entidades entre banco de dados e entre servidores  
  
-   Dependências no nível de coluna de entidades associadas e não associadas a esquema  
  
-   Tipos definidos pelo usuário (alias e UDT CLR)  
  
-   Coleções de esquemas XML  
  
-   Funções de partição  
  
**Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]), [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)].  
  
## <a name="syntax"></a>Sintaxe  
  
```  
sys.dm_sql_referenced_entities (  
    ' [ schema_name. ] referencing_entity_name ' , ' <referencing_class> ' )  
  
<referencing_class> ::=  
{  
    OBJECT  
  | DATABASE_DDL_TRIGGER  
  | SERVER_DDL_TRIGGER  
}  
```  
  
## <a name="arguments"></a>Argumentos  
 [ *schema_name*. ] *referencing_entity_name*  
 É o nome da entidade de referência. *schema_name* é necessária quando a classe de referência é OBJECT.  
  
 *schema_name.referencing_entity_name* é **nvarchar (517)**.  
  
 *< Referencing_class >* :: = {objeto | DATABASE_DDL_TRIGGER | SERVER_DDL_TRIGGER}  
 É a classe da entidade de referência especificada. Apenas uma classe pode ser especificada por instrução.  
  
 *< referencing_class >* é **nvarchar (60)**.  
  
## <a name="table-returned"></a>Tabela retornada  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|referencing_minor_id|**Int**|ID da coluna quando a entidade de referência for uma coluna; caso contrário, 0. Não permite valor nulo.|  
|referenced_server_name|**sysname**|Nome do servidor da entidade referenciada.<br /><br /> Essa coluna é populada para dependências entre servidores que são feitas especificando um nome de quatro partes válido. Para obter informações sobre nomes de várias partes, consulte [convenções de sintaxe Transact-SQL &#40;Transact-SQL&#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md).<br /><br /> NULL para dependências não associadas a esquema para as quais a entidade foi referenciada sem especificar um nome de quatro partes.<br /><br /> NULL para entidades associadas a esquema porque elas devem estar no mesmo banco de dados e portanto, só podem ser definidas usando uma de duas partes (*Object*) nome.|  
|referenced_database_name|**sysname**|Nome do banco de dados da entidade referenciada.<br /><br /> Essa coluna é populada para referências entre servidores ou entre bancos de dados, que são feitas especificando um nome de três ou quatro partes válido.<br /><br /> NULL para referências não associadas a esquema quando especificadas usando um nome de uma ou duas partes.<br /><br /> NULL para entidades associadas a esquema porque elas devem estar no mesmo banco de dados e portanto, só podem ser definidas usando uma de duas partes (*Object*) nome.|  
|referenced_schema_name|**sysname**|Esquema ao qual a entidade referenciada pertence.<br /><br /> NULL para referências não associadas a esquema para as quais a entidade foi referenciada sem especificar o nome do esquema.<br /><br /> Jamais NULL para referências associadas a esquema.|  
|referenced_entity_name|**sysname**|Nome da entidade referenciada. Não permite valor nulo.|  
|referenced_minor_name|**sysname**|Nome da coluna quando a entidade referenciada é uma coluna; caso contrário, NULL. Por exemplo, referenced_minor_name é NULL na linha que lista a própria entidade referenciada.<br /><br /> Uma entidade referenciada é uma coluna quando uma coluna é identificada pelo nome na entidade de referência, ou quando a entidade pai é usada em uma instrução SELECT *.|  
|referenced_id|**Int**|ID da entidade referenciada. Quando referenced_minor_id não é 0, referenced_id é a entidade na qual a coluna é definida.<br /><br /> Sempre NULL para referências entre servidores.<br /><br /> NULL para referências entre bancos de dados quando a ID não pode ser determinada, porque o banco de dados está offline ou a entidade não pode ser associada.<br /><br /> NULL para referências dentro do banco de dados se a ID não puder ser determinada. Para referências não associadas a esquema, a ID não pode ser resolvida quando a entidade referenciada não existe no banco de dados ou quando a resolução de nomes é dependente do chamador.  No último caso, is_caller_dependent está definido como 1.<br /><br /> Jamais NULL para referências associadas a esquema.|  
|referenced_minor_id|**Int**|ID da coluna quando a entidade referenciada é uma coluna; caso contrário, 0. Por exemplo, referenced_minor_is é 0 na linha que lista a própria entidade referenciada.<br /><br /> Para referências não associadas a esquema, as dependências de coluna são informadas somente quando todas as entidades referenciadas podem ser associadas. Se não for possível associar alguma entidade referenciada, nenhuma dependência no nível de coluna será informada e referenced_minor_id será 0. Consulte o exemplo D.|  
|referenced_class|**tinyint**|Classe da entidade referenciada.<br /><br /> 1 = Objeto ou coluna<br /><br /> 6 = Tipo<br /><br /> 10 = Coleção de esquema XML<br /><br /> 21 = Função de partição|  
|referenced_class_desc|**nvarchar(60)**|Descrição de classe da entidade referenciada.<br /><br /> OBJECT_OR_COLUMN<br /><br /> TYPE<br /><br /> XML_SCHEMA_COLLECTION<br /><br /> PARTITION_FUNCTION|  
|is_caller_dependent|**bit**|Indica que a associação de esquema para a entidade referenciada ocorre em tempo de execução; portanto, a resolução da ID da entidade depende do esquema do chamador. Isso ocorre quando a entidade referenciada é um procedimento armazenado, um procedimento armazenado estendido ou uma função definida pelo usuário chamada em uma instrução EXECUTE.<br /><br /> 1 = A entidade referenciada depende do chamador e é resolvida em tempo de execução. Nesse caso, referenced_id é NULL.<br /><br /> 0 = A ID da entidade referenciada não é dependente do chamador. Sempre 0 para referências associadas a esquema e referências entre bancos de dados e entre servidores que especificam explicitamente um nome de esquema. Por exemplo, uma referência para uma entidade no formato `EXEC MyDatabase.MySchema.MyProc` não é dependente do chamador. Porém, uma referência no formato `EXEC MyDatabase..MyProc` é dependente do chamador.|  
|is_ambiguous|**bit**|Indica a referência é ambígua e pode ser resolvida em tempo de execução para uma função definida pelo usuário, um tipo definido pelo usuário (UDT) ou uma referência xquery para uma coluna do tipo **xml**. Por exemplo, suponha que a instrução `SELECT Sales.GetOrder() FROM Sales.MySales` está definido em um procedimento armazenado. Até que o procedimento armazenado seja executado, não se sabe se `Sales.GetOrder()` é uma função definida pelo usuário no esquema `Sales` ou é uma coluna denominada `Sales` do tipo UDT com um método denominado `GetOrder()`.<br /><br /> 1 = A referência a uma função definida pelo usuário ou a um método UDT (Tipo Definido pelo Usuário) de coluna é ambígua.<br /><br /> 0 = A referência não é ambígua ou a entidade pode ser associada com êxito quando a função é chamada.<br /><br /> Sempre 0 para referências associadas a esquema.|  
|is_selected|**bit**|**Aplica-se a**: do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> 1 = O objeto ou coluna é selecionada.|  
|is_updated|**bit**|**Aplica-se a**: do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> 1 = O objeto ou coluna é modificada.|  
|is_select_all|**bit**|**Aplica-se a**: do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> 1 = O objeto é usado em uma cláusula SELECT * (somente no nível do objeto).|  
|is_all_columns_found|**bit**|**Aplica-se a**: do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> 1 = Todas as dependências de colunas do objeto poderiam ser encontradas.<br /><br /> 0 = As dependências de colunas do objeto não poderiam ser encontradas.|
|is_insert_all|**bit**|**Aplica-se a**: do [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> 1 = o objeto é usado em uma instrução INSERT sem uma lista de colunas (nível de objeto somente).|  
|is_incomplete|**bit**|**Aplica-se a:** [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP2 até [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> 1 = o objeto ou coluna tem um erro de associação e está incompleta.|
  
## <a name="exceptions"></a>Exceções  
 Retorna um conjunto de resultados vazio em qualquer uma das seguintes condições:  
  
-   Um objeto de sistema é especificado.  
  
-   A entidade especificada não existe no banco de dados atual.  
  
-   A entidade especificada não faz referência a nenhuma entidade.  
  
-   Um parâmetro inválido é passado.  
  
 Retorna um erro quando a entidade de referência especificada é um procedimento armazenado numerado.  
  
 Retorna o erro 2020 quando as dependências de coluna não podem ser resolvidas. Esse erro não impede que a consulta retorne dependências no nível do objeto.  
  
## <a name="remarks"></a>Remarks  
 Essa função pode ser executada no contexto de qualquer banco de dados para retornar as entidades que fazem referência a um gatilho DDL no nível do servidor.  
  
 A tabela a seguir lista os tipos de entidades para os quais as informações de dependência são criadas e mantidas. As informações de dependência não são criadas nem mantidas para regras, padrões, tabelas temporárias, procedimentos armazenados temporários ou objetos do sistema.  
  
|Tipo de entidade|Entidade de referência|Entidade referenciada|  
|-----------------|------------------------|-----------------------|  
|Table|Sim*|Sim|  
|Exibição|Sim|Sim|  
|Procedimento armazenado [!INCLUDE[tsql](../../includes/tsql-md.md)]**|Sim|Sim|  
|procedimento armazenado CLR|não|Sim|  
|Função [!INCLUDE[tsql](../../includes/tsql-md.md)] definida pelo usuário|Sim|Sim|  
|Função CLR definida pelo usuário|não|Sim|  
|Gatilho CLR (DML e DDL)|não|não|  
|Gatilho DML [!INCLUDE[tsql](../../includes/tsql-md.md)] |Sim|não|  
|Gatilho DDL no nível do banco de dados [!INCLUDE[tsql](../../includes/tsql-md.md)]|Sim|não|  
|Gatilho DDL no nível do servidor [!INCLUDE[tsql](../../includes/tsql-md.md)]|Sim|não|  
|Procedimentos armazenados estendidos|não|Sim|  
|Fila|não|Sim|  
|Sinônimo|não|Sim|  
|Tipo (tipo de alias e tipo de dados CLR definido pelo usuário)|não|Sim|  
|Coleção de esquemas XML|não|Sim|  
|Função de partição|não|Sim|  
  
 \* Uma tabela é controlada como uma entidade de referência apenas quando ela faz referência a um [!INCLUDE[tsql](../../includes/tsql-md.md)] módulo, tipo definido pelo usuário ou coleção de esquemas XML na definição de coluna computada, restrição CHECK ou restrição padrão.  
  
 ** Os procedimentos armazenados numerados com um valor inteiro maior que 1 não são controlados como entidade que faz referência nem como entidade referenciada.  
  
## <a name="permissions"></a>Permissões  
 Requer permissão SELECT em sys.dm_sql_referenced_entities e permissão VIEW DEFINITION na entidade de referência. Por padrão, a permissão SELECT é concedida a público. Requer permissão VIEW DEFINITION no banco de dados ou permissão ALTER DATABASE DDL TRIGGER no banco de dados quando a entidade de referência é um gatilho DDL do banco de dados. Requer permissão de VIEW ANY DEFINITION no servidor quando a entidade de referência é um gatilho DDL de servidor.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-returning-entities-that-are-referenced-by-a-database-level-ddl-trigger"></a>A. Retornando entidades referenciadas por um gatilho DDL em nível de banco de dados  
 O exemplo a seguir retorna as entidades (tabelas e colunas) referenciadas pelo gatilho DDL `ddlDatabaseTriggerLog` de banco de dados.  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT referenced_schema_name, referenced_entity_name, referenced_minor_name,   
    referenced_minor_id, referenced_class_desc  
FROM sys.dm_sql_referenced_entities ('ddlDatabaseTriggerLog', 'DATABASE_DDL_TRIGGER');  
GO  
```  
  
### <a name="b-returning-entities-that-are-referenced-by-an-object"></a>B. Retornando entidades referenciadas por um objeto  
 O exemplo seguinte retorna as entidades referenciadas pela função `dbo.ufnGetContactInformation` definida pelo usuário.  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT referenced_schema_name, referenced_entity_name, referenced_minor_name,   
    referenced_minor_id, referenced_class_desc, is_caller_dependent, is_ambiguous  
FROM sys.dm_sql_referenced_entities ('dbo.ufnGetContactInformation', 'OBJECT');  
GO  
```  
  
### <a name="c-returning-column-dependencies"></a>C. Retornando dependências de coluna  
 O exemplo seguinte cria a tabela `Table1` com a coluna computada `c` definida como a soma de colunas `a` e `b`. A exibição `sys.dm_sql_referenced_entities` então é chamada. A exibição retorna duas linhas, um para cada coluna definida na coluna computada.  
  
```sql  
USE AdventureWorks2012;  
GO  
CREATE TABLE dbo.Table1 (a int, b int, c AS a + b);  
GO  
SELECT referenced_schema_name AS schema_name,  
    referenced_entity_name AS table_name,  
    referenced_minor_name AS referenced_column,  
    COALESCE(COL_NAME(OBJECT_ID(N'dbo.Table1'),referencing_minor_id), 'N/A') AS referencing_column_name  
FROM sys.dm_sql_referenced_entities ('dbo.Table1', 'OBJECT');  
GO

-- Remove the table.  
DROP TABLE dbo.Table1;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
 schema_name table_name referenced_column referencing_column  
 ----------- ---------- ----------------- ------------------  
 dbo         Table1     a                 c  
 dbo         Table1     b                 c  
```

### <a name="d-returning-non-schema-bound-column-dependencies"></a>D. Retornando dependências de colunas não associadas a esquema  
 O exemplo a seguir descarta a `Table1` e cria a `Table2` e o procedimento armazenado `Proc1`. O procedimento referencia a `Table2` e a tabela inexistente `Table1`. A exibição `sys.dm_sql_referenced_entities` é executada com o procedimento armazenado especificado como entidade de referência. O conjunto de resultados mostra uma linha da `Table1` e 3 da `Table2`. Como a `Table1` não existe, as dependências de coluna não podem ser resolvidas e o erro 2020 é retornado. A coluna `is_all_columns_found` retorna 0 para `Table1` que indica que havia colunas que não puderam ser descobertas.  
  
```sql  
USE AdventureWorks2012;  
GO  
IF OBJECT_ID ( 'dbo.Table1', 'U' ) IS NOT NULL   
    DROP TABLE dbo.Table1;  
GO  
CREATE TABLE dbo.Table2 (c1 int, c2 int);  
GO  
CREATE PROCEDURE dbo.Proc1 AS  
    SELECT a, b, c FROM Table1;  
    SELECT c1, c2 FROM Table2;  
GO  
SELECT referenced_id, referenced_entity_name AS table_name, referenced_minor_name AS referenced_column_name, is_all_columns_found  
FROM sys.dm_sql_referenced_entities ('dbo.Proc1', 'OBJECT');  
GO  
  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
 referenced_id table_name   referenced_column_name  is_all_columns_found  
 ------------- ------------ ----------------------- --------------------  
 935674381     Table2       NULL                    1  
 935674381     Table2       C1                      1  
 935674381     Table2       C2                      1  
 NULL          Table1       NULL                    0  

 Msg 2020, Level 16, State 1, Line 1The dependencies reported for entity "dbo.Proc1" might not include references to all columns. This is either because the entity references an object that does not exist or because of an error in one or more statements in the entity.  Before rerunning the query, ensure that there are no errors in the entity and that all objects referenced by the entity exist.
 ```
  
### <a name="e-demonstrating-dynamic-dependency-maintenance"></a>E. Demonstrando manutenção de dependência dinâmica  
 O exemplo a seguir estende o Exemplo D para mostrar que dependências são mantidas dinamicamente. O exemplo recria primeiro a `Table1`que foi cancelada no exemplo D. Depois `sys.dm_sql_referenced_entities` é executado novamente com o procedimento armazenado especificado como a entidade de referência. O conjunto de resultados mostra que as tabelas e suas colunas respectivas definidas no procedimento armazenado são retornadas. Além disso, a coluna `is_all_columns_found` retorna um 1 para todos os objetos e colunas.  
  
```sql  
USE AdventureWorks2012;  
GO  
CREATE TABLE Table1 (a int, b int, c AS a + b);  
GO   
SELECT referenced_id, referenced_entity_name AS table_name, referenced_minor_name as column_name, is_all_columns_found  
FROM sys.dm_sql_referenced_entities ('dbo.Proc1', 'OBJECT');  
GO  
DROP TABLE Table1, Table2;  
DROP PROC Proc1;  
GO  
  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
 referenced_id table_name   referenced_column_name  is_all_columns_found  
 ------------- ------------ ----------------------- --------------------  
 935674381     Table2       NULL                    1 
 935674381     Table2       c1                      1 
 935674381     Table2       c2                      1 
 967674495     Table1       NULL                    1 
 967674495     Table1       a                       1  
 967674495     Table1       b                       1  
 967674495     Table1       c                       1  
 ```
 
### <a name="f-returning-object-or-column-usage"></a>F. Retornando o uso de objeto ou de coluna  
 O exemplo a seguir retorna os objetos e as dependências de coluna do procedimento armazenado `HumanResources.uspUpdateEmployeePersonalInfo`. Esse procedimento atualiza as colunas `NationalIDNumber`, `BirthDate,``MaritalStatus`, e `Gender` do `Employee` tabela baseada em determinado `BusinessEntityID` valor. Outro procedimento armazenado, `upsLogError` é definido em um bloco TRY.CATCH para capturar qualquer erro de execução. As colunas `is_selected`, `is_updated`e `is_select_all` retornam informações sobre como são usados esses objetos e colunas dentro do objeto de referência. A tabela e colunas que são modificadas são indicadas por um 1 na coluna is_updated. A coluna `BusinessEntityID` só é selecionada e o procedimento armazenado `uspLogError` não é selecionado, nem modificado.  
  
**Aplica-se a**: do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
```sql  
SELECT referenced_entity_name AS table_name, referenced_minor_name as column_name, is_selected, is_updated, is_select_all  
FROM sys.dm_sql_referenced_entities ('HumanResources.uspUpdateEmployeePersonalInfo', 'OBJECT');  
  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
 table_name    column_name         is_selected is_updated is_select_all  
 ------------- ------------------- ----------- ---------- -------------  
 uspLogError   NULL                0           0          0  
 Employee      NULL                0           1          0  
 Employee      BusinessEntityID    1           0          0  
 Employee      NationalIDNumber    0           1          0  
 Employee      BirthDate           0           1          0  
 Employee      MaritalStatus       0           1          0  
 Employee      Gender              0           1          0
 ```
  
## <a name="see-also"></a>Consulte também  
 [sys.dm_sql_referencing_entities &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-sql-referencing-entities-transact-sql.md)   
 [sys.sql_expression_dependencies &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql.md)  
  
  
