---
title: sys. Objects (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/30/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.objects_TSQL
- objects
- sys.objects
- objects_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.objects catalog view
- table-valued parameters, sys.objects catalog view
- user-defined table types [SQL Server]
- table types [SQL Server]
ms.assetid: f8d6163a-2474-410c-a794-997639f31b3b
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 47e332d8dfda76bbf2702335b72793c112c15d75
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68102322"
---
# <a name="sysobjects-transact-sql"></a>sys.objects (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Contém uma linha para cada objeto definido pelo usuário, no escopo do esquema que é criado dentro de um banco de dados, incluindo compilada nativamente função escalar definida pelo usuário.  
  
 Para obter mais informações, consulte [Funções escalares definidas pelo usuário para OLTP in-memory](../../relational-databases/in-memory-oltp/scalar-user-defined-functions-for-in-memory-oltp.md).  
  
> [!NOTE]  
>  sys.objects não mostra gatilhos DDL, porque eles não estão no escopo do esquema. Todos os gatilhos, DML e DDL, estão localizados em [sys. Triggers](../../relational-databases/system-catalog-views/sys-triggers-transact-sql.md). sys. Triggers dá suporte a uma mistura de regras de escopo de nome para vários tipos de gatilhos.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|name|**sysname**|Nome do objeto.|  
|object_id|**int**|Número de identificação do objeto. É exclusivo em um banco de dados.|  
|principal_id|**int**|ID do proprietário individual, se for diferente do proprietário do esquema. Por padrão, os objetos contidos no esquema pertencem ao proprietário do esquema. No entanto, um proprietário alternativo pode ser especificado usando a instrução ALTER AUTHORIZATION para alterar a propriedade.<br /><br /> Será NULL se não houver nenhum proprietário individual alternativo.<br /><br /> Será NULL se o tipo de objeto for um dos seguintes:<br /><br /> C = Restrição CHECK<br /><br /> D = DEFAULT (restrição ou autônomo)<br /><br /> F = Restrição FOREIGN KEY<br /><br /> PK = Restrição PRIMARY KEY<br /><br /> R = Regra (estilo antigo, autônomo)<br /><br /> TA = Gatilho de assembly (integração CLR)<br /><br /> TR = Gatilho SQL<br /><br /> UQ = Restrição UNIQUE<br /><br /> EC = restrição de borda |  
|schema_id|**int**|ID do esquema em que o objeto está contido.<br /><br /> Os objetos do sistema de escopo de esquema estão sempre contidos nos esquemas sys ou INFORMATION_SCHEMA.|  
|parent_object_id|**int**|ID do objeto ao qual este objeto pertence.<br /><br /> 0 = Não é um objeto filho.|  
|type|**char(2)**|Tipo de objeto:<br /><br /> AF = Função de agregação (CLR)<br /><br /> C = Restrição CHECK<br /><br /> D = DEFAULT (restrição ou autônomo)<br /><br /> F = Restrição FOREIGN KEY<br /><br /> FN = Função escalar SQL<br /><br /> FS = Função escalar de assembly (CLR)<br /><br /> FT = Função avaliada por tabela de assembly (CLR)<br /><br /> IF = Função SQL com valor de tabela embutida<br /><br /> IT = tabela interna<br /><br /> P = Procedimento armazenado SQL<br /><br /> PC = procedimento armazenado Assembly (CLR)<br /><br /> PG = Guia de plano<br /><br /> PK = Restrição PRIMARY KEY<br /><br /> R = Regra (estilo antigo, autônomo)<br /><br /> RF = Procedimento de filtro de replicação<br /><br /> S = Tabela base do sistema<br /><br /> SN = Sinônimo<br /><br /> SO = Objeto de sequência<br /><br /> U = Tabela (definida pelo usuário)<br /><br /> V = Exibição<br /><br /> EC = restrição de borda <br /><br /> <br /><br /> **Aplica-se a**: do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> <br /><br /> SQ = Fila de serviço<br /><br /> TA = Gatilho DML de assembly (CLR)<br /><br /> TF = Função com valor de tabela SQL<br /><br /> TR = Gatilho DML de SQL<br /><br /> TT = Tipo de tabela<br /><br /> UQ = Restrição UNIQUE<br /><br /> X = Procedimento armazenado estendido<br /><br /> <br /><br /> **Aplica-se ao**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] por meio [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)], [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)].<br /><br /> <br /><br /> ET = tabela externa|  
|type_desc|**nvarchar(60)**|Descrição do tipo de objeto:<br /><br /> AGGREGATE_FUNCTION<br /><br /> CHECK_CONSTRAINT<br /><br /> CLR_SCALAR_FUNCTION<br /><br /> CLR_STORED_PROCEDURE<br /><br /> CLR_TABLE_VALUED_FUNCTION<br /><br /> CLR_TRIGGER<br /><br /> DEFAULT_CONSTRAINT<br /><br /> EXTENDED_STORED_PROCEDURE<br /><br /> FOREIGN_KEY_CONSTRAINT<br /><br /> INTERNAL_TABLE<br /><br /> PLAN_GUIDE<br /><br /> PRIMARY_KEY_CONSTRAINT<br /><br /> REPLICATION_FILTER_PROCEDURE<br /><br /> RULE<br /><br /> SEQUENCE_OBJECT<br /><br /> <br /><br /> **Aplica-se a**: do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> <br /><br /> SERVICE_QUEUE<br /><br /> SQL_INLINE_TABLE_VALUED_FUNCTION<br /><br /> SQL_SCALAR_FUNCTION<br /><br /> SQL_STORED_PROCEDURE<br /><br /> SQL_TABLE_VALUED_FUNCTION<br /><br /> SQL_TRIGGER<br /><br /> SYNONYM<br /><br /> SYSTEM_TABLE<br /><br /> TABLE_TYPE<br /><br /> UNIQUE_CONSTRAINT<br /><br /> USER_TABLE<br /><br /> VIEW|  
|create_date|**datetime**|A data em que o objeto foi criado.|  
|modify_date|**datetime**|A data em que o objeto foi modificado pela última vez com uma instrução ALTER. Se o objeto for uma tabela ou uma exibição, modify_date também será alterado quando um índice clusterizado na tabela ou na exibição for criado ou alterado.|  
|is_ms_shipped|**bit**|O objeto é criado por um componente interno do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|is_published|**bit**|O objeto é publicado.|  
|is_schema_published|**bit**|Apenas o esquema do objeto é publicado.|  
  
## <a name="remarks"></a>Comentários  
 Você pode aplicar a [OBJECT_ID](../../t-sql/functions/object-id-transact-sql.md), [OBJECT_NAME](../../t-sql/functions/object-name-transact-sql.md), e [OBJECTPROPERTY](../../t-sql/functions/objectproperty-transact-sql.md)() funções internas para os objetos mostrados em sys. Objects.  
  
 Há uma versão desta exibição com o mesmo esquema, chamado [sys. system_objects](../../relational-databases/system-catalog-views/sys-system-objects-transact-sql.md), que mostra os objetos do sistema. Não há outra exibição denominada [all_objects](../../relational-databases/system-catalog-views/sys-all-objects-transact-sql.md) que mostra os objetos de sistema e do usuário. Todas as três exibições do catálogo têm a mesma estrutura.  
  
 Nesta versão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], um índice estendido, como um índice XML ou índice espacial, é considerado uma tabela interna em sys.objects (type = IT and type_desc = INTERNAL_TABLE). Para um índice estendido:  
  
-   name é o nome interno da tabela de índice.  
  
-   parent_object_id é o object_id da tabela base.  
  
-   As colunas is_ms_shipped, is_published e is_schema_published são definidas como 0.  

**Exibições do sistema úteis relacionados**  
Subconjuntos de objetos podem ser exibidos usando exibições do sistema para um tipo específico de objeto, como:  
- [sys.tables](sys-tables-transact-sql.md)  
- [sys.views](sys-views-transact-sql.md)  
- [sys.procedures](sys-procedures-transact-sql.md)  
  
## <a name="permissions"></a>Permissões  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-returning-all-the-objects-that-have-been-modified-in-the-last-n-days"></a>A. Retornando todos os objetos que foram modificados nos últimos N dias  
 Antes de executar a consulta a seguir, substitua `<database_name>` e `<n_days>` por valores válidos.  
  
```sql  
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
  
### <a name="b-returning-the-parameters-for-a-specified-stored-procedure-or-function"></a>B. Retornando os parâmetros para uma função ou procedimento armazenado especificado  
 Antes de executar a consulta a seguir, substitua `<database_name>` e `<schema_name.object_name>` por nomes válidos.  
  
```sql  
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
  
### <a name="c-returning-all-the-user-defined-functions-in-a-database"></a>C. Retornando todas as funções definidas pelo usuário em um banco de dados  
 Antes de executar a consulta a seguir, substitua `<database_name>` pelo nome de um banco de dados válido.  
  
```sql  
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
  
### <a name="d-returning-the-owner-of-each-object-in-a-schema"></a>D. Retornando o proprietário de cada objeto em um esquema.  
 Antes de executar a consulta a seguir, substitua todas as ocorrências de `<database_name>` e `<schema_name>` por nomes válidos.  
  
```sql  
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
  
## <a name="see-also"></a>Consulte também  
 [Exibições de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [sys.all_objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-all-objects-transact-sql.md)   
 [sys.system_objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-system-objects-transact-sql.md)   
 [sys.triggers &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-triggers-transact-sql.md)   
 [Exibições de catálogo de objeto&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [Consultando o catálogo de sistema do SQL Server perguntas Frequentes](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)   
 [sys.internal_tables &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-internal-tables-transact-sql.md)  
  
  
