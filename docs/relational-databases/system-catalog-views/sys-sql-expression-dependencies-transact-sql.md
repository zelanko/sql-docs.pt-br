---
title: sys.sql_expression_dependencies (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.sql_expression_dependencies
- sql_expression_dependencies_TSQL
- sql_expression_dependencies
- sys.sql_expression_dependencies_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sql_expression_dependencies catalog view
ms.assetid: 78a218e4-bf99-4a6a-acbf-ff82425a5946
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 29bf4991ce5dd52e9c66c31abade833e4fe319b2
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/09/2019
ms.locfileid: "68893540"
---
# <a name="syssql_expression_dependencies-transact-sql"></a>sys.sql_expression_dependencies (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  Contém uma linha para cada dependência por nome em uma entidade definida pelo usuário no banco de dados atual. Isso inclui dependências entre funções escalares definidas pelo usuário e compiladas nativamente, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e outros módulos. Uma dependência entre duas entidades é criada quando uma entidade, chamada de *entidade referenciada*, é exibida pelo nome em uma expressão SQL persistente de outra entidade, chamada de *entidade de referência*. Por exemplo, quando uma tabela for referenciada na definição de uma exibição, a exibição, como a entidade de referência, dependerá da tabela, a entidade referenciada. Se a tabela for descartada, a exibição será inutilizável.  
  
 Para obter mais informações, consulte [Funções escalares definidas pelo usuário para OLTP in-memory](../../relational-databases/in-memory-oltp/scalar-user-defined-functions-for-in-memory-oltp.md).  
  
 Você pode usar essa exibição do catálogo para relatar informações de dependência das seguintes entidades:  
  
-   Entidades associadas a esquema  
  
-   Entidades não associadas a esquema.  
  
-   Entidades entre banco de dados e entre servidores. São relatados os nomes de entidade; porém, os IDs da entidade não são solucionados.  
  
-   Dependências de coluna em entidades associadas a esquema. As dependências em nível de coluna para objetos não associados a esquema podem ser retornadas usando [Sys. dm _sql_referenced_entities](../../relational-databases/system-dynamic-management-views/sys-dm-sql-referenced-entities-transact-sql.md).  
  
-   A DDL no nível de servidor é disparada quando está no contexto do banco de dados mestre.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|referencing_id|**int**|ID da entidade de referência. Não permite valor nulo.|  
|referencing_minor_id|**int**|ID da coluna quando a entidade de referência for uma coluna; caso contrário, 0. Não permite valor nulo.|  
|referencing_class|**tinyint**|Classe da entidade de referência.<br /><br /> 1 = Objeto ou coluna<br /><br /> 12 = Gatilho DDL do banco de dados<br /><br /> 13 - Gatilho DDL do servidor<br /><br /> Não permite valor nulo.|  
|referencing_class_desc|**nvarchar(60)**|Descrição da classe da entidade de referência.<br /><br /> OBJECT_OR_COLUMN<br /><br /> DATABASE_DDL_TRIGGER<br /><br /> SERVER_DDL_TRIGGER<br /><br /> Não permite valor nulo.|  
|is_schema_bound_reference|**bit**|1 = A entidade referenciada é associada a esquema.<br /><br /> 0 = A entidade referenciada não é associada a esquema.<br /><br /> Não permite valor nulo.|  
|referenced_class|**tinyint**|Classe da entidade referenciada.<br /><br /> 1 = Objeto ou coluna<br /><br /> 6 = Tipo<br /><br /> 10 = Coleção de esquema XML<br /><br /> 21 = Função de partição<br /><br /> Não permite valor nulo.|  
|referenced_class_desc|**nvarchar(60)**|Descrição de classe da entidade referenciada.<br /><br /> OBJECT_OR_COLUMN<br /><br /> TYPE<br /><br /> XML_SCHEMA_COLLECTION<br /><br /> PARTITION_FUNCTION<br /><br /> Não permite valor nulo.|  
|referenced_server_name|**sysname**|Nome do servidor da entidade referenciada.<br /><br /> Essa coluna é populada para dependências entre servidores que são feitas especificando um nome de quatro partes válido. Para obter informações sobre nomes com várias partes, consulte [convenções &#40;de sintaxe Transact-&#41;SQL Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md).<br /><br /> NULL para entidades não associadas a esquema para as quais a entidade foi referenciada sem especificar um nome de quatro partes.<br /><br /> NULL para entidades associadas a esquema porque elas devem estar no mesmo banco de dados e, portanto, só podem ser definidas usando um nome de duas partes (*esquema. objeto*).|  
|referenced_database_name|**sysname**|Nome do banco de dados da entidade referenciada.<br /><br /> Essa coluna é populada para referências entre servidores ou entre bancos de dados, que são feitas especificando um nome de três ou quatro partes válido.<br /><br /> NULL para referências não associadas a esquema quando especificadas usando um nome de uma ou duas partes.<br /><br /> NULL para entidades associadas a esquema porque elas devem estar no mesmo banco de dados e, portanto, só podem ser definidas usando um nome de duas partes (*esquema. objeto*).|  
|referenced_schema_name|**sysname**|Esquema ao qual a entidade referenciada pertence.<br /><br /> NULL para referências não associadas a esquema para as quais a entidade foi referenciada sem especificar o nome do esquema.<br /><br /> Nunca NULL para referências associadas a esquema porque devem ser definidas entidades associadas a esquema e referenciadas usando um nome de duas partes.|  
|referenced_entity_name|**sysname**|Nome da entidade referenciada. Não permite valor nulo.|  
|referenced_id|**int**|ID da entidade referenciada. O valor desta coluna nunca é nulo para referências associadas a esquema. O valor desta coluna é sempre nulo para referências entre servidores e bancos de dados.<br /><br /> NULL para referências dentro do banco de dados se a ID não puder ser determinada. Para referências não associadas a esquema, a ID não pode ser resolvida nos seguintes casos:<br /><br /> A entidade referenciada não existe no banco de dados.<br /><br /> O esquema da entidade referenciada depende do esquema do chamador e é resolvido em tempo de execução. Nesse caso, is_caller_dependent está definido como 1.|  
|referenced_minor_id|**int**|ID da coluna referenciada quando a entidade de referência for uma coluna; caso contrário, 0. Não permite valor nulo.<br /><br /> Uma entidade referenciada é uma coluna quando uma coluna é identificada pelo nome na entidade de referência, ou quando a entidade pai é usada em uma instrução SELECT *.|  
|is_caller_dependent|**bit**|Indica que a associação de esquema para a entidade referenciada ocorre em tempo de execução; portanto, a resolução da ID da entidade depende do esquema do chamador. Isso ocorre quando a entidade referenciada for um procedimento armazenado, um procedimento armazenado estendido ou uma função definida pelo usuário não associada a esquema chamados em uma instrução EXECUTE.<br /><br /> 1 = A entidade referenciada é dependente do chamador e é resolvida em tempo de execução. Nesse caso, referenced_id é NULL.<br /><br /> 0 = A ID da entidade referenciada não é dependente do chamador.<br /><br /> Sempre 0 para referências associadas a esquema e referências entre bancos de dados e entre servidores que especificam explicitamente um nome de esquema. Por exemplo, uma referência para uma entidade no formato `EXEC MyDatabase.MySchema.MyProc` não é dependente do chamador. Porém, uma referência no formato `EXEC MyDatabase..MyProc` é dependente do chamador.|  
|is_ambiguous|**bit**|Indica que a referência é ambígua e pode ser resolvida em tempo de execução para uma função definida pelo usuário, um UDT (tipo definido pelo usuário) ou uma referência XQuery para uma coluna do tipo **XML**.<br /><br /> Por exemplo, suponha que a instrução `SELECT Sales.GetOrder() FROM Sales.MySales` esteja definida em um procedimento armazenado. Até que o procedimento armazenado seja executado, não se sabe se `Sales.GetOrder()` é uma função definida pelo usuário no esquema `Sales` ou é uma coluna denominada `Sales` do tipo UDT com um método denominado `GetOrder()`.<br /><br /> 1 = A referência é ambígua.<br /><br /> 0 = A referência não é ambígua ou a entidade pode ser associada com êxito quando a exibição é chamada.<br /><br /> Sempre 0 para referências associadas ao esquema.|  
  
## <a name="remarks"></a>Comentários  
 A tabela a seguir lista os tipos de entidades para os quais as informações de dependência são criadas e mantidas. As informações de dependência não são criadas nem mantidas para regras, padrões, tabelas temporárias, procedimentos armazenados temporários ou objetos do sistema.  

> [!NOTE]
> O Azure SQL data warehouse e Parallel data warehouse dão suporte a tabelas, exibições, estatísticas filtradas e tipos de entidade de procedimentos armazenados Transact-SQL desta lista.  As informações de dependência são criadas e mantidas somente para tabelas, exibições e estatísticas filtradas.  
  
|Tipo de entidade|Entidade de referência|Entidade referenciada|  
|-----------------|------------------------|-----------------------|  
|Tabela|Sim*|Sim|  
|Exibir|Sim|Sim|  
|Índice filtrado|Sim**|Não|  
|Estatísticas filtradas|Sim**|Não|  
|Procedimento armazenado [!INCLUDE[tsql](../../includes/tsql-md.md)]***|Sim|Sim|  
|procedimento armazenado CLR|Não|Sim|  
|Função [!INCLUDE[tsql](../../includes/tsql-md.md)] definida pelo usuário|Sim|Sim|  
|Função CLR definida pelo usuário|Não|Sim|  
|Gatilho CLR (DML e DDL)|Não|Não|  
|Gatilho DML [!INCLUDE[tsql](../../includes/tsql-md.md)]|Sim|Não|  
|Gatilho DDL no nível do banco de dados [!INCLUDE[tsql](../../includes/tsql-md.md)]|Sim|Não|  
|Gatilho DDL no nível do servidor [!INCLUDE[tsql](../../includes/tsql-md.md)]|Sim|Não|  
|Procedimentos armazenados estendidos|Não|Sim|  
|Fila|Não|Sim|  
|Sinônimo|Não|Sim|  
|Tipo (tipo de alias e tipo de dados CLR definido pelo usuário)|Não|Sim|  
|Coleção de esquemas XML|Não|Sim|  
|Função Partition|Não|Sim|  
  
 \*Uma tabela é rastreada como uma entidade de referência somente quando faz [!INCLUDE[tsql](../../includes/tsql-md.md)] referência a um módulo, tipo definido pelo usuário ou coleção de esquema XML na definição de uma coluna computada, restrição de verificação ou restrição padrão.  
  
 \* * Cada coluna usada no predicado de filtro é controlada como uma entidade de referência.  
  
 *** Procedimentos armazenados numerados com valor inteiro maior que 1 não são controlados, nem como entidade de referência nem como entidade referenciada.  
  
## <a name="permissions"></a>Permissões  
 Requer permissão VIEW DEFINITION no banco de dados e permissão SELECT em sys.sql_expression_dependencies para o banco de dados. Por padrão, a permissão SELECT é concedida somente a membros da função de banco de dados fixa db_owner. Quando são concedidas permissões SELECT e VIEW DEFINITION a outro usuário, o usuário autorizado pode exibir todas as dependências no banco de dados.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-returning-entities-that-are-referenced-by-another-entity"></a>A. Retornando entidades referenciadas por outra entidade  
 O exemplo a seguir retorna as tabelas e colunas referenciadas na exibição `Production.vProductAndDescription`. A exibição depende das entidades (tabelas e colunas) retornadas nas colunas `referenced_entity_name` e `referenced_column_name`.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT OBJECT_NAME(referencing_id) AS referencing_entity_name,   
    o.type_desc AS referencing_desciption,   
    COALESCE(COL_NAME(referencing_id, referencing_minor_id), '(n/a)') AS referencing_minor_id,   
    referencing_class_desc,  
    referenced_server_name, referenced_database_name, referenced_schema_name,  
    referenced_entity_name,   
    COALESCE(COL_NAME(referenced_id, referenced_minor_id), '(n/a)') AS referenced_column_name,  
    is_caller_dependent, is_ambiguous  
FROM sys.sql_expression_dependencies AS sed  
INNER JOIN sys.objects AS o ON sed.referencing_id = o.object_id  
WHERE referencing_id = OBJECT_ID(N'Production.vProductAndDescription');  
GO  
  
```  
  
### <a name="b-returning-entities-that-reference-another-entity"></a>B. Retornando entidades que referenciam outra entidade  
 O exemplo a seguir retorna as entidades que referenciam a tabela `Production.Product`. As entidades retornadas na coluna `referencing_entity_name` dependem da tabela `Product`.  
  
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
WHERE referenced_id = OBJECT_ID(N'Production.Product');  
GO  
  
```  
  
### <a name="c-returning-cross-database-dependencies"></a>C. Retornando dependências entre bancos de dados  
 O exemplo a seguir retorna todas as dependências entre banco de dados. O exemplo cria primeiramente um banco de dados `db1` e dois procedimentos armazenados que referenciam tabelas dos bancos de dados `db2` e `db3`. A tabela `sys.sql_expression_dependencies` é consultada em seguida, para relatar as dependências entre bancos de dados existentes entre procedimentos e tabelas. Observe que NULL é retornado na coluna `referenced_schema_name` para a entidade referenciada `t3` porque o nome de esquema daquela entidade não foi especificado na definição do procedimento.  
  
```  
CREATE DATABASE db1;  
GO  
USE db1;  
GO  
CREATE PROCEDURE p1 AS SELECT * FROM db2.s1.t1;  
GO  
CREATE PROCEDURE p2 AS  
    UPDATE db3..t3  
    SET c1 = c1 + 1;  
GO  
SELECT OBJECT_NAME (referencing_id),referenced_database_name,   
    referenced_schema_name, referenced_entity_name  
FROM sys.sql_expression_dependencies  
WHERE referenced_database_name IS NOT NULL;  
GO  
USE master;  
GO  
DROP DATABASE db1;  
GO  
  
```  
  
## <a name="see-also"></a>Consulte também  
 [sys.dm_sql_referenced_entities &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-sql-referenced-entities-transact-sql.md)   
 [sys.dm_sql_referencing_entities &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-sql-referencing-entities-transact-sql.md)  
  
  
