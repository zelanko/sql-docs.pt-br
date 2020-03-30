---
title: OBJECT_ID (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- OBJECT_ID
- OBJECT_ID_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- objects [SQL Server], IDs
- identification numbers [SQL Server], database objects
- checking object exists
- IDs [SQL Server], database objects
- OBJECT_ID function
- database objects [SQL Server], IDs
- displaying object IDs
- viewing object IDs
- verifying object exists
ms.assetid: f89286db-440f-4218-a828-30881ce3077a
author: VanMSFT
ms.author: vanto
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 2191fbd39cea24142b866f0acc9a27717896dab9
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "67914860"
---
# <a name="object_id-transact-sql"></a>OBJECT_ID (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Retorna o número de identificação do banco de dados do objeto de escopo de esquema.  
  
> [!IMPORTANT]  
>  Os objetos que não são de escopo de esquema, como gatilhos DDL, não podem ser consultados com o uso de OBJECT_ID. Para objetos não encontrados na exibição do catálogo [sys.objects](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md), obtenha os números de identificação de objeto consultando a exibição do catálogo apropriada. Por exemplo, para retornar o número de identificação de objeto de um gatilho DDL, use `SELECT OBJECT_ID FROM sys.triggers WHERE name = 'DatabaseTriggerLog``'`.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
OBJECT_ID ( '[ database_name . [ schema_name ] . | schema_name . ]   
  object_name' [ ,'object_type' ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 **'** *object_name* **'**  
 É o objeto a ser usado. *object_name* é **varchar** ou **nvarchar**. Se *object_name* for **varchar**, ele será convertido implicitamente em **nvarchar**. A especificação dos nomes de banco de dados e esquema é opcional.  
  
 **'** *object_type* **'**  
 É o tipo do objeto no escopo do esquema. *object_type* é **varchar** ou **nvarchar**. Se *object_type* for **varchar**, ele será convertido implicitamente em **nvarchar**. Para obter uma lista de tipos de objeto, consulte a coluna **type** em [sys.objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md).  
  
## <a name="return-types"></a>Tipos de retorno  
 **int**  
  
## <a name="exceptions"></a>Exceções  
 Para um índice de espaço, OBJECT_ID retorna NULL.  
  
 Retorna NULL em caso de erro.  
  
 Um usuário só pode exibir metadados de protegíveis de sua propriedade ou para os quais recebeu permissão. Isso significa que funções internas que emitem metadados, como OBJECT_ID, poderão retornar o NULL se o usuário não tiver nenhuma permissão para o objeto. Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="remarks"></a>Comentários  
 Quando o parâmetro para uma função de sistema for opcional, o banco de dados atual, o computador host, o usuário do servidor ou o usuário do banco de dados será presumido. As funções internas sempre devem ser seguidas por parênteses.  
  
 Quando uma tabela temporária é especificada, o nome do banco de dados deve vir antes do nome da tabela temporária, a menos que o banco de dados seja **tempdb**. Por exemplo: `SELECT OBJECT_ID('tempdb..#mytemptable')`.  
  
 As funções de sistema podem ser usadas na lista de seleção, na cláusula WHERE e em qualquer local onde uma expressão for permitida. Para obter mais informações, consulte [Expressões &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md) e [WHERE &#40;Transact-SQL&#41;](../../t-sql/queries/where-transact-sql.md).  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-returning-the-object-id-for-a-specified-object"></a>a. Retornando a ID de um objeto especificado  
 O exemplo seguinte retorna a ID de objeto para a tabela `Production.WorkOrder` do banco de dados [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)].  
  
```  
USE master;  
GO  
SELECT OBJECT_ID(N'AdventureWorks2012.Production.WorkOrder') AS 'Object ID';  
GO  
```  
  
### <a name="b-verifying-that-an-object-exists"></a>B. Verificando se um objeto existe  
 O exemplo a seguir confirma a existência de uma tabela especificada ao verificar se ela tem uma ID de objeto. Se a tabela existir, ela será excluída. Se a tabela não existir, a instrução `DROP TABLE` não será executada.  
  
```  
USE AdventureWorks2012;  
GO  
IF OBJECT_ID (N'dbo.AWBuildVersion', N'U') IS NOT NULL  
DROP TABLE dbo.AWBuildVersion;  
GO  
```  
  
### <a name="c-using-object_id-to-specify-the-value-of-a-system-function-parameter"></a>C. Usando OBJECT_ID para especificar o valor de um parâmetro de função do sistema  
 O exemplo a seguir retorna informações de todos os índices e partições da tabela `Person.Address` do banco de dados [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] usando a função [sys.dm_db_index_operational_stats](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-operational-stats-transact-sql.md).  
  
> [!IMPORTANT]  
>  Quando você está usando as funções DB_ID e OBJECT_ID do [!INCLUDE[tsql](../../includes/tsql-md.md)] para retornar um valor de parâmetro, sempre confirme se é retornada uma ID válida. Se o banco de dados ou nome de objeto não puder ser encontrado, por não existir ou por estar escrito incorretamente, ambas as funções retornarão NULL. A função **sys.dm_db_index_operational_stats** interpreta NULL como um valor de curinga que especifica todos os bancos de dados ou todos os objetos. Como pode se tratar de uma operação não intencional, os exemplos nesta seção demonstram a maneira segura de determinar a identificação do banco de dados e do objeto.  
  
```  
DECLARE @db_id int;  
DECLARE @object_id int;  
SET @db_id = DB_ID(N'AdventureWorks2012');  
SET @object_id = OBJECT_ID(N'AdventureWorks2012.Person.Address');  
IF @db_id IS NULL   
  BEGIN;  
    PRINT N'Invalid database';  
  END;  
ELSE IF @object_id IS NULL  
  BEGIN;  
    PRINT N'Invalid object';  
  END;  
ELSE  
  BEGIN;  
    SELECT * FROM sys.dm_db_index_operational_stats(@db_id, @object_id, NULL, NULL);  
  END;  
GO  
```  
  
## <a name="examples-sssdwfull-and-sspdw"></a>Exemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="d-returning-the-object-id-for-a-specified-object"></a>D: retornando a ID de um objeto especificado  
 O exemplo seguinte retorna a ID de objeto para a tabela `FactFinance` do banco de dados [!INCLUDE[ssawPDW](../../includes/ssawpdw-md.md)].  
  
```  
SELECT OBJECT_ID('AdventureWorksPDW2012.dbo.FactFinance') AS 'Object ID';  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Funções de metadados &#40;Transact-SQL&#41;](../../t-sql/functions/metadata-functions-transact-sql.md)   
 [sys.objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [sys.dm_db_index_operational_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-operational-stats-transact-sql.md)   
 [OBJECT_DEFINITION &#40;Transact-SQL&#41;](../../t-sql/functions/object-definition-transact-sql.md)   
 [OBJECT_NAME &#40;Transact-SQL&#41;](../../t-sql/functions/object-name-transact-sql.md)  
  
  

