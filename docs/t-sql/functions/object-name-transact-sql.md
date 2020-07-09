---
title: OBJECT_NAME (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- OBJECT_NAME
- OBJECT_NAME_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- OBJECT_NAME function
- viewing database object names
- objects [SQL Server], names
- database objects [SQL Server], names
- displaying database object names
- database objects [SQL Server]
- names [SQL Server], database objects
ms.assetid: 7d5b923f-0c3e-4af9-b39b-132807a6d5b3
author: VanMSFT
ms.author: vanto
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 8dafb369a94eda03a959c26b4dfe12df03c7e860
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86005089"
---
# <a name="object_name-transact-sql"></a>OBJECT_NAME (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Retorna o nome de objeto de banco de dados para objetos no escopo do esquema. Para obter uma lista de objetos no escopo do esquema, consulte [sys.objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql
OBJECT_NAME ( object_id [, database_id ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 *object_id*  
 É a ID do objeto a ser usado. *object_id* é **int** e é considerado um objeto no escopo do esquema no banco de dados especificado ou no contexto de banco de dados atual.  
  
 *database_id*  
 É a ID do banco de dados onde o objeto deve ser pesquisado. *database_id* é **int**.  
  
## <a name="return-types"></a>Tipos de retorno  
 **sysname**  
  
## <a name="exceptions"></a>Exceções  
 Retornará NULL em caso de erro ou se um chamador não tiver permissão para exibir o objeto. Se o banco de dados de destino tiver a opção AUTO_CLOSE definida como ON, a função abrirá o banco de dados.  
  
 Um usuário só pode exibir metadados de protegíveis de sua propriedade ou para os quais recebeu permissão. Isso significa que as funções internas que emitem metadados, como OBJECT_NAME, poderão retornar NULL se o usuário não tiver nenhuma permissão no objeto. Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="permissions"></a>Permissões  
 Requer permissão ANY para o objeto. Para especificar uma identificação de banco de dados, é exigida também a permissão CONNECT para o banco de dados ou a conta de convidado deve ser habilitada.  
  
## <a name="remarks"></a>Comentários  
 As funções de sistema podem ser usadas na lista de seleção, na cláusula WHERE e em qualquer local onde uma expressão for permitida. Para obter mais informações, consulte [Expressões](../../t-sql/language-elements/expressions-transact-sql.md) e [WHERE](../../t-sql/queries/where-transact-sql.md).  
  
 O valor retornado por esta função de sistema usa a ordenação do banco de dados atual.  
  
 Por padrão, o [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] considera que *object_id* está no contexto do banco de dados atual. Uma consulta que faz referência a um *object_id* em outro banco de dados retorna NULL ou resultados incorretos. Por exemplo, na consulta a seguir o contexto do banco de dados atual é [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]. O [!INCLUDE[ssDE](../../includes/ssde-md.md)] tenta retornar um nome de objeto para a identificação do objeto especificado naquele banco de dados em vez do banco de dados especificado na cláusula FROM da consulta. Portanto, informações incorretas são retornadas.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT DISTINCT OBJECT_NAME(object_id)  
FROM master.sys.objects;  
GO  
```  
  
 Você pode resolver nomes de objeto no contexto de outro banco de dados especificando uma identificação de banco de dados. O exemplo a seguir especifica a identificação de banco de dados para o banco de dados `master` na função `OBJECT_SCHEMA_NAME` e retorna os resultados corretos.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT DISTINCT OBJECT_SCHEMA_NAME(object_id, 1) AS schema_name  
FROM master.sys.objects;  
GO  
```  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-using-object_name-in-a-where-clause"></a>a. Usando OBJECT_NAME em uma cláusula WHERE  
 O exemplo a seguir retorna colunas da exibição de catálogo `sys.objects` para o objeto especificado por `OBJECT_NAME` na cláusula `WHERE` da instrução `SELECT`.  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @MyID INT;  
SET @MyID = (SELECT OBJECT_ID('AdventureWorks2012.Production.Product',  
    'U'));  
SELECT name, object_id, type_desc  
FROM sys.objects  
WHERE name = OBJECT_NAME(@MyID);  
GO  
```  
  
### <a name="b-returning-the-object-schema-name-and-object-name"></a>B. Retornando o nome do esquema do objeto e o nome do objeto  
 O exemplo a seguir retorna o nome de esquema do objeto, nome de objeto e texto de SQL para todos os planos de consulta em cache que não sejam instruções ad hoc ou preparadas.  
  
```  
SELECT DB_NAME(st.dbid) AS database_name,   
    OBJECT_SCHEMA_NAME(st.objectid, st.dbid) AS schema_name,  
    OBJECT_NAME(st.objectid, st.dbid) AS object_name,   
    st.text AS query_text  
FROM sys.dm_exec_query_stats AS qs  
CROSS APPLY sys.dm_exec_sql_text(qs.sql_handle) AS st  
WHERE st.objectid IS NOT NULL;  
GO  
```  
  
### <a name="c-returning-three-part-object-names"></a>C. Retornando nomes de objetos de três partes  
 O exemplo a seguir retorna o banco de dados, esquema e nome de objeto juntamente com todas as outras colunas na exibição de gerenciamento dinâmico `sys.dm_db_index_operational_stats` de todos os objetos em todos os bancos de dados.  
  
```  
SELECT QUOTENAME(DB_NAME(database_id))   
    + N'.'   
    + QUOTENAME(OBJECT_SCHEMA_NAME(object_id, database_id))   
    + N'.'   
    + QUOTENAME(OBJECT_NAME(object_id, database_id))  
    , *   
FROM sys.dm_db_index_operational_stats(NULL, NULL, NULL, NULL);  
GO  
```  
  
## <a name="examples-sssdwfull-and-sspdw"></a>Exemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="d-using-object_name-in-a-where-clause"></a>D. Usando OBJECT_NAME em uma cláusula WHERE  
 O exemplo a seguir retorna colunas da exibição de catálogo `sys.objects` para o objeto especificado por `OBJECT_NAME` na cláusula `WHERE` da instrução `SELECT`. O número do seu objeto (274100017, no exemplo a seguir) será diferente.  Para testar este exemplo, pesquise um número válido de objeto executando `SELECT name, object_id FROM sys.objects;` no banco de dados.)  
  
```  
SELECT name, object_id, type_desc  
FROM sys.objects  
WHERE name = OBJECT_NAME(274100017);  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Funções de metadados &#40;Transact-SQL&#41;](../../t-sql/functions/metadata-functions-transact-sql.md)   
 [OBJECT_DEFINITION &#40;Transact-SQL&#41;](../../t-sql/functions/object-definition-transact-sql.md)   
 [OBJECT_ID &#40;Transact-SQL&#41;](../../t-sql/functions/object-id-transact-sql.md)  
  
  

