---
title: DATEADD (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/29/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- DATEADD
- DATEADD_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- dates [SQL Server], functions
- add interval to date or time [SQL Server]
- subtract interval from date or time [SQL Server]
- functions [SQL Server], time
- functions [SQL Server], date and time
- time [SQL Server], functions
- dates [SQL Server], intervals
- date and time [SQL Server], DATEADD
- DATEADD function [SQL Server]
ms.assetid: 89c5ae32-89c6-47e1-979e-15d97908b9f1
caps.latest.revision: 71
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: dd7dd81f8e12b0c14048fd8ab550e7edfd780cf5
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="dateadd-transact-sql"></a>DATEADD (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Retorna uma *date* especificada com um intervalo de *number* especificado (inteiro com sinal) adicionada a uma *datepart* especificada dessa *date*.
  
Para obter uma visão geral das funções e dos tipos de dados de data e hora de [!INCLUDE[tsql](../../includes/tsql-md.md)], confira [Funções e tipos de dados de data e hora &#40;Transact-SQL&#41;](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md).
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
  
```sql
DATEADD (datepart , number , date )  
```  
  
## <a name="arguments"></a>Argumentos  
*datepart*  
É a parte de *date* à qual um **integer***number* é adicionado. A tabela a seguir lista todos os argumentos válidos de *datepart*. Equivalentes de variável definidos pelo usuário não são válidos.
  
|*datepart*|Abreviações|  
|---|---|
|**year**|**yy**, **yyyy**|  
|**quarter**|**qq**, **q**|  
|**month**|**mm**, **m**|  
|**dayofyear**|**dy**, **y**|  
|**day**|**dd**, **d**|  
|**week**|**wk**, **ww**|  
|**weekday**|**dw**, **w**|  
|**hour**|**hh**|  
|**minute**|**mi**, **n**|  
|**second**|**ss**, **s**|  
|**millisecond**|**ms**|  
|**microsecond**|**mcs**|  
|**nanosecond**|**ns**|  
  
*number*  
É uma expressão que pode ser resolvida para um [int](../../t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql.md) que é adicionado a uma *datepart* de *date*. Variáveis definidas pelo usuário são válidas.  
Se você especificar um valor com uma fração decimal, a fração será truncada e não arredondada.
  
*date*  
É uma expressão que pode ser resolvida em um valor de **time**, **date**, **smalldatetime**, **datetime**, **datetime2** ou **datetimeoffset**. *date* pode ser uma expressão, uma expressão de coluna, uma variável definida pelo usuário ou um literal de cadeia de caracteres. Se a expressão for uma cadeia de caracteres literal, ela deverá ser resolvida para uma **datetime**. Para evitar ambiguidade, use anos de quatro dígitos. Para obter mais informações sobre anos de dois dígitos, consulte [Configurar a opção two digit year cutoff de configuração do servidor](../../database-engine/configure-windows/configure-the-two-digit-year-cutoff-server-configuration-option.md).
  
## <a name="return-types"></a>Tipos de retorno
O tipo de dados de retorno é o tipo de dados do argumento de *date*, com exceção de literais de cadeia de caracteres.
O tipo de dados de retorno para um literal de cadeia de caracteres é **datetime**. Um erro será gerado se a escala de segundos do literal de cadeia de caracteres tiver mais de três posições (.nnn) ou tiver a parte de deslocamento de fuso horário.
  
## <a name="return-value"></a>Valor retornado  
  
## <a name="datepart-argument"></a>Argumento datepart  
**dayofyear**, **day** e **weekday** retornam o mesmo valor.
  
Cada *datepart* e suas abreviações retornam o mesmo valor.
  
Se *datepart* for **month** e o mês *date* tiver mais dias que o mês de retorno e o dia *date* não existir no mês de retorno, o último dia do mês de retorno será retornado. Por exemplo, setembro tem 30 dias; então, as duas instruções a seguir retornam 2006-09-30 00:00:00.000:
  
```sql
SELECT DATEADD(month, 1, '20060830');
SELECT DATEADD(month, 1, '20060831');
```
  
## <a name="number-argument"></a>Argumento number  
O argumento *number* não pode exceder o intervalo de **int**. Nas instruções a seguir, o argumento *number* excede o intervalo de **int** em 1. A mensagem de erro a seguir será retornada: "`Msg 8115, Level 16, State 2, Line 1. Arithmetic overflow error converting expression to data type int."`
  
```sql
SELECT DATEADD(year,2147483648, '20060731');  
SELECT DATEADD(year,-2147483649, '20060731');  
```  
  
## <a name="date-argument"></a>Argumento date  
O argumento *date* não pode ser incrementado em um valor fora do intervalo de seu tipo de dados. Nas instruções a seguir, o valor *number* adicionado ao valor de *date* excede o intervalo do tipo de dados *date*. A mensagem de erro a seguir será retornada: "`Msg 517, Level 16, State 1, Line 1 Adding a value to a 'datetime' column caused overflow`."
  
```sql
SELECT DATEADD(year,2147483647, '20060731');  
SELECT DATEADD(year,-2147483647, '20060731');  
```  
  
## <a name="return-values-for-a-smalldatetime-date-and-a-second-or-fractional-seconds-datepart"></a>Retorna valores de uma data smalldatetime e uma parte de data de segundo ou frações de segundo  
A segunda parte de um valor [smalldatetime](../../t-sql/data-types/smalldatetime-transact-sql.md) é sempre 00. Se *date* é **smalldatetime**, o seguinte se aplica:
-   Se *datepart* é **second** e *number* está entre -30 e +29, nenhuma adição é feita.  
-   Se *datepart* é **second** e *number* é menor que -30 ou maior que +29, uma adição é feita com início em um minuto.  
-   Se *datepart* é **millisecond** e *number* está entre -30001 e +29998, nenhuma adição é feita.  
-   Se *datepart* é **millisecond** e *number* é menor que -30001 ou maior que +29998, uma adição é feita com início em um minuto.  
  
## <a name="remarks"></a>Remarks  
DATEADD pode ser usado na SELECT \<list> e nas cláusulas WHERE, HAVING, GROUP BY e ORDER BY.
  
## <a name="fractional-seconds-precision"></a>Precisão de segundos fracionários
Não é permitido adicionar um *datepart* de **microsecond** ou **nanosecond** para tipos de dados *date* de **smalldatetime**, **date**, and **datetime**.
  
Os milissegundos têm uma escala de 3 (0,123). Os microssegundos têm uma escala de 6 (0,123456). Os nanossegundos têm uma escala de 9 (0,123456789). Os tipos de dados **time**, **datetime2** e **datetimeoffset** têm uma escala máxima de 7 (.1234567). Se *datepart* é **nanosecond**, *number* deve ser 100 antes do aumento dos segundos fracionários de *date*. Um *number* entre 1 e 49 é arredondado para 0 e um número de 50 a 99 é arredondado para 100.
  
As instruções a seguir adicionam uma *datepart* de **millisecond**, **microsecond** ou **nanosecond**.
  
```sql
DECLARE @datetime2 datetime2 = '2007-01-01 13:10:10.1111111';  
SELECT '1 millisecond', DATEADD(millisecond,1,@datetime2)  
UNION ALL  
SELECT '2 milliseconds', DATEADD(millisecond,2,@datetime2)  
UNION ALL  
SELECT '1 microsecond', DATEADD(microsecond,1,@datetime2)  
UNION ALL  
SELECT '2 microseconds', DATEADD(microsecond,2,@datetime2)  
UNION ALL  
SELECT '49 nanoseconds', DATEADD(nanosecond,49,@datetime2)  
UNION ALL  
SELECT '50 nanoseconds', DATEADD(nanosecond,50,@datetime2)  
UNION ALL  
SELECT '150 nanoseconds', DATEADD(nanosecond,150,@datetime2);  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
1 millisecond     2007-01-01 13:10:10.1121111  
2 milliseconds    2007-01-01 13:10:10.1131111  
1 microsecond     2007-01-01 13:10:10.1111121  
2 microseconds    2007-01-01 13:10:10.1111131  
49 nanoseconds    2007-01-01 13:10:10.1111111  
50 nanoseconds    2007-01-01 13:10:10.1111112  
150 nanoseconds   2007-01-01 13:10:10.1111113  
```  
  
## <a name="time-zone-offset"></a>Deslocamento de fuso horário
Não é permitido acréscimo ao deslocamento de fuso horário.
  
## <a name="examples"></a>Exemplos  

### <a name="a-incrementing-datepart-by-an-interval-of-1"></a>A. Incrementando datepart em um intervalo de 1  
Cada uma das instruções a seguir incrementa *datepart* por um intervalo de 1.
  
```sql
DECLARE @datetime2 datetime2 = '2007-01-01 13:10:10.1111111';  
SELECT 'year', DATEADD(year,1,@datetime2)  
UNION ALL  
SELECT 'quarter',DATEADD(quarter,1,@datetime2)  
UNION ALL  
SELECT 'month',DATEADD(month,1,@datetime2)  
UNION ALL  
SELECT 'dayofyear',DATEADD(dayofyear,1,@datetime2)  
UNION ALL  
SELECT 'day',DATEADD(day,1,@datetime2)  
UNION ALL  
SELECT 'week',DATEADD(week,1,@datetime2)  
UNION ALL  
SELECT 'weekday',DATEADD(weekday,1,@datetime2)  
UNION ALL  
SELECT 'hour',DATEADD(hour,1,@datetime2)  
UNION ALL  
SELECT 'minute',DATEADD(minute,1,@datetime2)  
UNION ALL  
SELECT 'second',DATEADD(second,1,@datetime2)  
UNION ALL  
SELECT 'millisecond',DATEADD(millisecond,1,@datetime2)  
UNION ALL  
SELECT 'microsecond',DATEADD(microsecond,1,@datetime2)  
UNION ALL  
SELECT 'nanosecond',DATEADD(nanosecond,1,@datetime2);  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
Year         2008-01-01 13:10:10.1111111  
quarter      2007-04-01 13:10:10.1111111  
month        2007-02-01 13:10:10.1111111  
dayofyear    2007-01-02 13:10:10.1111111  
day          2007-01-02 13:10:10.1111111  
week         2007-01-08 13:10:10.1111111  
weekday      2007-01-02 13:10:10.1111111  
hour         2007-01-01 14:10:10.1111111  
minute       2007-01-01 13:11:10.1111111  
second       2007-01-01 13:10:11.1111111  
millisecond  2007-01-01 13:10:10.1121111  
microsecond  2007-01-01 13:10:10.1111121  
nanosecond   2007-01-01 13:10:10.1111111  
```  
  
### <a name="b-incrementing-more-than-one-level-of-datepart-in-one-statement"></a>B. Incrementando mais de um nível de datepart em uma instrução  
Cada uma das instruções a seguir incrementa *datepart* em um *number* grande o suficiente para também incrementar a próxima *datepart* mais alta de *date*.
  
```sql
DECLARE @datetime2 datetime2;  
SET @datetime2 = '2007-01-01 01:01:01.1111111';  
--Statement                                 Result     
-------------------------------------------------------------------   
SELECT DATEADD(quarter,4,@datetime2);     --2008-01-01 01:01:01.110  
SELECT DATEADD(month,13,@datetime2);      --2008-02-01 01:01:01.110  
SELECT DATEADD(dayofyear,365,@datetime2); --2008-01-01 01:01:01.110  
SELECT DATEADD(day,365,@datetime2);       --2008-01-01 01:01:01.110  
SELECT DATEADD(week,5,@datetime2);        --2007-02-05 01:01:01.110  
SELECT DATEADD(weekday,31,@datetime2);    --2007-02-01 01:01:01.110  
SELECT DATEADD(hour,23,@datetime2);       --2007-01-02 00:01:01.110  
SELECT DATEADD(minute,59,@datetime2);     --2007-01-01 02:00:01.110  
SELECT DATEADD(second,59,@datetime2);     --2007-01-01 01:02:00.110  
SELECT DATEADD(millisecond,1,@datetime2); --2007-01-01 01:01:01.110  
```  
  
### <a name="c-using-expressions-as-arguments-for-the-number-and-date-parameters"></a>C. Usando expressões como argumentos para os parâmetros de número e data  
Os exemplos a seguir usam diferentes tipos de expressões como argumentos para os parâmetros *number* e *date*. Os exemplos usam o banco de dados AdventureWorks.
  
#### <a name="specifying-a-column-as-date"></a>Especificando uma coluna como data  
O exemplo a seguir adiciona `2` dias a cada valor na coluna `OrderDate` para derivar uma nova coluna chamada `PromisedShipDate`.
  
```sql
SELECT SalesOrderID  
    ,OrderDate   
    ,DATEADD(day,2,OrderDate) AS PromisedShipDate  
FROM Sales.SalesOrderHeader;  
```  
  
Este é um conjunto de resultados parcial.
  
```sql
SalesOrderID OrderDate               PromisedShipDate  
------------ ----------------------- -----------------------  
43659        2005-07-01 00:00:00.000 2005-07-03 00:00:00.000  
43660        2005-07-01 00:00:00.000 2005-07-03 00:00:00.000  
43661        2005-07-01 00:00:00.000 2005-07-03 00:00:00.000  
...  
43702        2005-07-02 00:00:00.000 2005-07-04 00:00:00.000  
43703        2005-07-02 00:00:00.000 2005-07-04 00:00:00.000  
43704        2005-07-02 00:00:00.000 2005-07-04 00:00:00.000  
43705        2005-07-02 00:00:00.000 2005-07-04 00:00:00.000  
43706        2005-07-03 00:00:00.000 2005-07-05 00:00:00.000  
...  
43711        2005-07-04 00:00:00.000 2005-07-06 00:00:00.000  
43712        2005-07-04 00:00:00.000 2005-07-06 00:00:00.000  
...  
43740        2005-07-11 00:00:00.000 2005-07-13 00:00:00.000  
43741        2005-07-12 00:00:00.000 2005-07-14 00:00:00.000  
  
```  
  
#### <a name="specifying-user-defined-variables-as-number-and-date"></a>Especificando variáveis definidas pelo usuário como número e data  
O exemplo a seguir especifica variáveis definidas pelo usuário como argumentos para *number* e *date*.
  
```sql
DECLARE @days int = 365,   
        @datetime datetime = '2000-01-01 01:01:01.111'; /* 2000 was a leap year */;  
SELECT DATEADD(day, @days, @datetime);  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
-----------------------  
2000-12-31 01:01:01.110  
  
(1 row(s) affected)  
```  
  
#### <a name="specifying-scalar-system-function-as-date"></a>Especificando função de sistema escalar como data  
O exemplo a seguir especifica `SYSDATETIME` para *date*.
  
```sql
SELECT DATEADD(month, 1, SYSDATETIME());  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
---------------------------  
2013-02-06 14:29:59.6727944  
  
(1 row(s) affected)  
```  
  
#### <a name="specifying-scalar-subqueries-and-scalar-functions-as-number-and-date"></a>Especificando subconsultas e funções escalares como número e data  
O exemplo a seguir usa subconsultas escalares, `MAX(ModifiedDate)`, como argumentos para *number* e *date*. `(SELECT TOP 1 BusinessEntityID FROM Person.Person)` é um argumento artificial do parâmetro number que mostra como selecionar um argumento *number* em uma lista de valores.
  
```sql
SELECT DATEADD(month,(SELECT TOP 1 BusinessEntityID FROM Person.Person),  
    (SELECT MAX(ModifiedDate) FROM Person.Person));  
```  
  
#### <a name="specifying-numeric-expressions-and-scalar-system-functions-as-number-and-date"></a>Especificando expressões numéricas e funções de sistema escalares como número e data  
O exemplo a seguir usa uma expressão numérica (`(10/2))`, [operadores unários](../../mdx/unary-operators.md) (`-`), um [operador aritmético](../../mdx/arithmetic-operators.md) (`/`) e funções do sistema escalares (`SYSDATETIME`) como argumentos para *number* e *date*.
  
```sql
SELECT DATEADD(month,-(10/2), SYSDATETIME());  
```  
  
#### <a name="specifying-ranking-functions-as-number"></a>Especificando funções de classificação como número  
O exemplo a seguir usa uma função de classificação como argumentos para *number*.
  
```sql
SELECT p.FirstName, p.LastName  
    ,DATEADD(day,ROW_NUMBER() OVER (ORDER BY  
        a.PostalCode),SYSDATETIME()) AS 'Row Number'  
FROM Sales.SalesPerson AS s   
    INNER JOIN Person.Person AS p   
        ON s.BusinessEntityID = p.BusinessEntityID  
    INNER JOIN Person.Address AS a   
        ON a.AddressID = p.BusinessEntityID  
WHERE TerritoryID IS NOT NULL   
    AND SalesYTD <> 0;  
```  
  
#### <a name="specifying-an-aggregate-window-function-as-number"></a>Especificando uma função de janela de agregação como número  
O exemplo a seguir usa uma função de janela de agregação como um argumento para *number*.
  
```sql
SELECT SalesOrderID, ProductID, OrderQty  
    ,DATEADD(day,SUM(OrderQty)   
        OVER(PARTITION BY SalesOrderID),SYSDATETIME()) AS 'Total'  
FROM Sales.SalesOrderDetail   
WHERE SalesOrderID IN(43659,43664);  
GO  
```  
  
  
## <a name="see-also"></a>Confira também
[CAST e CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)
  
  

