---
title: GROUPING (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 12/03/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- GROUPING
- GROUPING_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- null values [SQL Server], GROUPING function
- grouping columns
- ROLLUP operator
- GROUP BY clause, GROUPING function
- GROUPING function
- CUBE operator
ms.assetid: 4efa3868-1fc4-4626-8fb1-e863cc03e422
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 23b05c6355151aa556ad7531de60e3ccf65ea0ea
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85631559"
---
# <a name="grouping-transact-sql"></a>GROUPING (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-asdw-xxx-md.md)]

  Indica se uma expressão de coluna especificada em uma lista GROUP BY é agregada ou não. GROUPING retorna 1 para agregada ou 0 para não agregada no conjunto de resultados. GROUPING pode ser usado apenas na lista SELECT \<select>, nas cláusulas HAVING e ORDER BY, quando GROUP BY é especificado.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
GROUPING ( <column_expression> )  
```  
  
## <a name="arguments"></a>Argumentos  
 \<column_expression>  
 É uma coluna ou uma expressão que contém uma coluna em uma cláusula [GROUP BY](../../t-sql/queries/select-group-by-transact-sql.md).  
  
## <a name="return-types"></a>Tipos de retorno  
 **tinyint**  
  
## <a name="remarks"></a>Comentários  
 GROUPING é usado para distinguir os valores nulos retornados por ROLLUP, CUBE ou GROUPING SETS dos valores nulos padrão. O NULL retornado como resultado de uma operação ROLLUP, CUBE ou GROUPING SETS é um uso especial de NULL. Isto atua como um espaço reservado de coluna no conjunto de resultados e significa tudo.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir agrupa `SalesQuota` e agrega quantias de `SaleYTD` no banco de dados [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]. A função `GROUPING` é aplicada à coluna `SalesQuota`.  
  
```  
SELECT SalesQuota, SUM(SalesYTD) 'TotalSalesYTD', GROUPING(SalesQuota) AS 'Grouping'  
FROM Sales.SalesPerson  
GROUP BY SalesQuota WITH ROLLUP;  
GO  
```  
  
 O conjunto de resultados mostra dois valores nulos em `SalesQuota`. O primeiro `NULL` representa o grupo de valores nulos desta coluna na tabela. O segundo `NULL` está na linha de resumo somada pela operação ROLLUP. A linha de resumo mostra as quantidades de `TotalSalesYTD` para todos os grupos `SalesQuota` e é indicada por `1` na coluna `Grouping`.  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
 SalesQuota     TotalSalesYTD       Grouping  
------------   -----------------   --------  
NULL           1533087.5999          0  
250000.00      33461260.59           0  
300000.00      9299677.9445          0  
NULL           44294026.1344         1  

(4 row(s) affected)
```  
  
## <a name="see-also"></a>Consulte Também  
 [GROUPING_ID &#40;Transact-SQL&#41;](../../t-sql/functions/grouping-id-transact-sql.md)   
 [GROUP BY &#40;Transact-SQL&#41;](../../t-sql/queries/select-group-by-transact-sql.md)  
  
  
