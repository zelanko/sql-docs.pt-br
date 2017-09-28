---
title: LEN (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 09/03/2015
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: 47
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 532b996c23a8f9746a52434d78783da2a24d1add
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="len-transact-sql"></a>LEN (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Retorna o número de caracteres da expressão da cadeia de caracteres especificada, excluindo espaços em branco à direita.  
  
> [!NOTE]  
>  Para retornar o número de bytes usados para representar uma expressão, use o [DATALENGTH](../../t-sql/functions/datalength-transact-sql.md) função.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
LEN ( string_expression )  
```  
  
## <a name="arguments"></a>Argumentos  
 *string_expression*  
 É a cadeia de caracteres [expressão](../../t-sql/language-elements/expressions-transact-sql.md) a ser avaliada. *string_expression* pode ser uma constante, variável ou coluna de caracteres ou dados binários.  
  
## <a name="return-types"></a>Tipos de retorno  
 **bigint** se *expressão* é o **varchar (max)**, **nvarchar (max)** ou **varbinary (max)** tipos de dados. Caso contrário, **int**.  
  
 Se você estiver usando agrupamentos de caracteres suplementares, o valor inteiro retornado contará os pares alternativos UTF-16 como um único caractere. Para obter mais informações, consulte [Suporte a agrupamentos e Unicode](../../relational-databases/collations/collation-and-unicode-support.md).  
  
## <a name="remarks"></a>Comentários  
 LEN exclui os espaços em branco. Se esse for um problema, considere o uso de [DATALENGTH &#40; Transact-SQL &#41; ](../../t-sql/functions/datalength-transact-sql.md) função trim não a cadeia de caracteres. Se o processamento de uma cadeia de caracteres unicode, DATALENGTH retornará duas vezes o número de caracteres. O exemplo a seguir demonstra LEN e DATALENGTH com um espaço à direita.  
  
```  
DECLARE @v1 varchar(40),  
    @v2 nvarchar(40);  
SELECT   
@v1 = 'Test of 22 characters ',   
@v2 = 'Test of 22 characters ';  
SELECT LEN(@v1) AS [varchar LEN] , DATALENGTH(@v1) AS [varchar DATALENGTH];  
SELECT LEN(@v2) AS [nvarchar LEN], DATALENGTH(@v2) AS [nvarchar DATALENGTH];  
  
```  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir seleciona o número de caracteres e os dados de `FirstName` para pessoas localizadas na `Australia`. Este exemplo usa o banco de dados [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)].  
  
```  
SELECT LEN(FirstName) AS Length, FirstName, LastName   
FROM Sales.vIndividualCustomer  
WHERE CountryRegionName = 'Australia';  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Exemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 O exemplo a seguir retorna o número de caracteres na coluna `FirstName` e os nomes e sobrenomes de funcionários localizados em `Australia`.  
  
```  
-- Uses AdventureWorks  
  
SELECT DISTINCT LEN(FirstName) AS FNameLength, FirstName, LastName   
FROM dbo.DimEmployee AS e  
INNER JOIN dbo.DimGeography AS g   
    ON e.SalesTerritoryKey = g.SalesTerritoryKey   
WHERE EnglishCountryRegionName = 'Australia';  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `FNameLength  FirstName  LastName`  
  
 `-----------  ---------  ---------------`  
  
 `4            Lynn       Tsoflias`  
  
## <a name="see-also"></a>Consulte também  
 [Tipos de dados &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [Funções de cadeia de caracteres &#40; Transact-SQL &#41;](../../t-sql/functions/string-functions-transact-sql.md)   
 [DATALENGTH &#40; Transact-SQL &#41;](../../t-sql/functions/datalength-transact-sql.md)   
 [ESQUERDA &#40; Transact-SQL &#41;](../../t-sql/functions/left-transact-sql.md)   
 [DIREITA &#40; Transact-SQL &#41;](../../t-sql/functions/right-transact-sql.md)  
  
  



