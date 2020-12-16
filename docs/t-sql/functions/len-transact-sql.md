---
description: LEN (Transact-SQL)
title: LEN (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/03/2015
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- LEN
- LEN_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- LEN function
- characters [SQL Server], number of
- number of characters
ms.assetid: fa20fee4-884d-4301-891a-c03e901345ae
author: pmasl
ms.author: pelopes
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: e73132566ae66f05da30e250e50f7e8367b9bac1
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97472077"
---
# <a name="len-transact-sql"></a>LEN (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

Retorna o número de caracteres da expressão de cadeia de caracteres especificada, excluindo espaços à direita.  
  
> [!NOTE]  
> Para retornar o número de bytes usado para representar uma expressão, use a função [DATALENGTH](../../t-sql/functions/datalength-transact-sql.md).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql
LEN ( string_expression )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos
 *string_expression*  
 É a [expression](../../t-sql/language-elements/expressions-transact-sql.md) da cadeia de caracteres a ser avaliada. *character_expression* pode ser uma constante, uma variável ou uma coluna de dados de caracteres e binários.  
  
## <a name="return-types"></a>Tipos de retorno  
 **bigint** if *expression* é dos tipos de dados **varchar(max)**, **nvarchar(max)** ou **varbinary(max)**; caso contrário, **int**.  
  
 Se você estiver usando ordenações de caracteres suplementares, o valor inteiro retornado contará os pares alternativos UTF-16 como um único caractere. Para obter mais informações, consulte [Suporte a ordenações e a Unicode](../../relational-databases/collations/collation-and-unicode-support.md).  
  
## <a name="remarks"></a>Comentários  
LEN exclui os espaços à direita. Se isso for um problema, considere usar a função [DATALENGTH &#40;Transact-SQL&#41;](../../t-sql/functions/datalength-transact-sql.md), que não corta a cadeia de caracteres. Se estiver processando uma cadeia de caracteres unicode, DATALENGTH retornará um número que pode não ser igual ao número de caracteres. O exemplo a seguir demonstra LEN e DATALENGTH com um espaço à direita.  
  
```sql  
  DECLARE @v1 VARCHAR(40),  
    @v2 NVARCHAR(40);  
SELECT   
@v1 = 'Test of 22 characters ',   
@v2 = 'Test of 22 characters ';  
SELECT LEN(@v1) AS [VARCHAR LEN] , DATALENGTH(@v1) AS [VARCHAR DATALENGTH];  
SELECT LEN(@v2) AS [NVARCHAR LEN], DATALENGTH(@v2) AS [NVARCHAR DATALENGTH];  
```  

> [!NOTE]
> Use [LEN](../../t-sql/functions/len-transact-sql.md) para retornar o número de caracteres codificados em determinada expressão de cadeia de caracteres e [DATALENGTH](../../t-sql/functions/datalength-transact-sql.md) para retornar o tamanho em bytes de determinada expressão de cadeia de caracteres. Essas saídas podem ser diferentes dependendo do tipo de dados e do tipo de codificação usado na coluna. Para obter mais informações sobre as diferenças de armazenamento entre diferentes tipos de codificação, confira [Suporte a agrupamentos e Unicode](../../relational-databases/collations/collation-and-unicode-support.md).

## <a name="examples"></a>Exemplos  
 O exemplo a seguir seleciona o número de caracteres e os dados de `FirstName` para pessoas localizadas na `Australia`. Este exemplo usa o banco de dados AdventureWorks.  
  
```sql  
SELECT LEN(FirstName) AS Length, FirstName, LastName   
FROM Sales.vIndividualCustomer  
WHERE CountryRegionName = 'Australia';  
GO  
```  
  
## <a name="examples-sssdwfull-and-sspdw"></a>Exemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 O exemplo a seguir retorna o número de caracteres na coluna `FirstName` e os nomes e sobrenomes de funcionários localizados em `Australia`.  
  
```sql  
USE AdventureWorks2016  
GO  
SELECT DISTINCT LEN(FirstName) AS FNameLength, FirstName, LastName   
FROM dbo.DimEmployee AS e  
INNER JOIN dbo.DimGeography AS g   
    ON e.SalesTerritoryKey = g.SalesTerritoryKey   
WHERE EnglishCountryRegionName = 'Australia';  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```
FNameLength  FirstName  LastName  
-----------  ---------  ---------------  
4            Lynn       Tsoflias
```  
  
## <a name="see-also"></a>Consulte Também  
 [DATALENGTH &#40;Transact-SQL&#41;](../../t-sql/functions/datalength-transact-sql.md)   
 [CHARINDEX &#40;Transact-SQL&#41;](../../t-sql/functions/charindex-transact-sql.md)  
 [PATINDEX &#40;Transact-SQL&#41;](../../t-sql/functions/patindex-transact-sql.md)  
 [LEFT &#40;Transact-SQL&#41;](../../t-sql/functions/left-transact-sql.md)   
 [RIGHT &#40;Transact-SQL&#41;](../../t-sql/functions/right-transact-sql.md)  
 [Tipos de dados &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [Funções de cadeia de caracteres &#40;Transact-SQL&#41;](../../t-sql/functions/string-functions-transact-sql.md)   
  
  
