---
title: DATEADD (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/29/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 6a90b51a1ef2156a2a05b8d3dd4e15111872edf6
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="dateadd-transact-sql"></a>DATEADD (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Retorna um especificado *data* com especificado *número* intervalo (inteiro assinado) adicionado à especificada *datepart* que *data*.
  
Para obter uma visão geral de todos os [!INCLUDE[tsql](../../includes/tsql-md.md)] tipos de dados de data e hora e funções, consulte [data e hora tipos de dados e funções &#40; Transact-SQL &#41; ](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md).
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
  
```sql
DATEADD (datepart , number , date )  
```  
  
## <a name="arguments"></a>Argumentos  
*datepart*  
É a parte do *data* para o qual um **inteiro***número* é adicionado. A seguinte tabela lista válida *datepart* argumentos. Equivalentes de variável definidos pelo usuário não são válidos.
  
|*datepart*|Abreviações|  
|---|---|
|**ano**|**AA**, **aaaa**|  
|**trimestre**|**tq**, **p**|  
|**mês**|**mm**, **m**|  
|**DAYOFYEAR**|**dy**, **y**|  
|**dia**|**dd**, **d**|  
|**semana**|**wk**, **ww**|  
|**dia da semana**|**DW**, **w**|  
|**hora**|**hh**|  
|**minuto**|**mi**,**n**|  
|**segundo**|**SS**, **s**|  
|**milissegundos**|**MS**|  
|**microssegundos**|**MCS**|  
|**nanossegundos**|**NS**|  
  
*number*  
É uma expressão que pode ser resolvida para um [int](../../t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql.md) que é adicionado a um *datepart* de *data*. Variáveis definidas pelo usuário são válidas.  
Se você especificar um valor com uma fração decimal, a fração será truncada e não arredondada.
  
*date*  
É uma expressão que pode ser resolvida para um **tempo**, **data**, **smalldatetime**, **datetime**, **datetime2**, ou **datetimeoffset** valor. *data* pode ser uma expressão, a expressão de coluna, a variável definida pelo usuário ou a cadeia de caracteres literal. Se a expressão for uma cadeia de caracteres literal, ele deve ser resolvido para um **datetime**. Para evitar ambiguidade, use anos de quatro dígitos. Para obter informações sobre anos de dois dígitos, consulte [configurar o ano de dois dígitos corte opção de configuração de servidor](../../database-engine/configure-windows/configure-the-two-digit-year-cutoff-server-configuration-option.md).
  
## <a name="return-types"></a>Tipos de retorno
O tipo de dados de retorno é o tipo de dados de *data* argumento, exceto para literais de cadeia de caracteres.
Os dados de retorno de tipo para um literal de cadeia de caracteres é **datetime**. Um erro será gerado se a escala de segundos do literal de cadeia de caracteres tiver mais de três posições (.nnn) ou tiver a parte de deslocamento de fuso horário.
  
## <a name="return-value"></a>Valor de retorno  
  
## <a name="datepart-argument"></a>Argumento datepart  
**DAYOFYEAR**, **dia**, e **dia da semana** retornam o mesmo valor.
  
Cada *datepart* e suas abreviações retornam o mesmo valor.
  
Se *datepart* é **mês** e *data* mês tem mais dias do mês de retorno de e *data* dia não existe no mês de retorno o último dia do mês de retorno será retornado. Por exemplo, setembro tem 30 dias; então, as duas instruções a seguir retornam 2006-09-30 00:00:00.000:
  
```sql
SELECT DATEADD(month, 1, '2006-08-30');
SELECT DATEADD(month, 1, '2006-08-31');
```
  
## <a name="number-argument"></a>Argumento number  
O *número* argumento não pode exceder o intervalo de **int**. Nas instruções a seguir, o argumento para *número* excede o intervalo de **int** em 1. A mensagem de erro a seguir será retornada: "`Msg 8115, Level 16, State 2, Line 1. Arithmetic overflow error converting expression to data type int."`
  
```sql
SELECT DATEADD(year,2147483648, '2006-07-31');  
SELECT DATEADD(year,-2147483649, '2006-07-31');  
```  
  
## <a name="date-argument"></a>Argumento date  
O *data* argumento não pode ser incrementado em um valor fora do intervalo de seu tipo de dados. Nas instruções a seguir, o *número* valor que é adicionado para o *data* valor excede o intervalo da *data* tipo de dados. A mensagem de erro a seguir será retornada: "`Msg 517, Level 16, State 1, Line 1 Adding a value to a 'datetime' column caused overflow`."
  
```sql
SELECT DATEADD(year,2147483647, '2006-07-31');  
SELECT DATEADD(year,-2147483647, '2006-07-31');  
```  
  
## <a name="return-values-for-a-smalldatetime-date-and-a-second-or-fractional-seconds-datepart"></a>Retorna valores de uma data smalldatetime e uma parte de data de segundo ou frações de segundo  
A segunda parte de um [smalldatetime](../../t-sql/data-types/smalldatetime-transact-sql.md) valor é sempre 00. Se *data* é **smalldatetime**, a seguir se aplicarem:
-   Se *datepart* é **segundo** e *número* está entre-30 e +29, nenhum acréscimo será executado.  
-   Se *datepart* é **segundo** e *número* é menor que-30 ou mais de +29, acréscimo será executado iniciando em um minuto.  
-   Se *datepart* é **milissegundo** e *número* está entre-30001 e + 29998, nenhum acréscimo será executado.  
-   Se *datepart* é **milissegundo** e *número* for inferior a -30001 ou mais 29998, acréscimo será executado iniciando em um minuto.  
  
## <a name="remarks"></a>Comentários  
DATEADD pode ser usada em SELECT \<lista >, WHERE, HAVING, cláusulas GROUP BY e ORDER BY.
  
## <a name="fractional-seconds-precision"></a>Precisão de segundos fracionários
Adição de um *datepart* de **microssegundos** ou **nanossegundos** para *data* tipos de dados **smalldatetime**, **data**, e **datetime** não é permitido.
  
Os milissegundos têm uma escala de 3 (0,123). Os microssegundos têm uma escala de 6 (0,123456). Os nanossegundos têm uma escala de 9 (0,123456789). O **tempo**, **datetime2**, e **datetimeoffset** tipos de dados têm uma escala máxima de 7 (. 1234567). Se *datepart* é **nanossegundos**, *número* deve ser 100 antes das frações de segundo de *data* aumentar. Um *número* entre 1 e 49 será arredondado para 0 e um número de 50 a 99 será arredondado para 100.
  
As instruções a seguir adicionam um *datepart* de **milissegundo**, **microssegundos**, ou **nanossegundos**.
  
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
Cada uma das instruções a seguir incrementa *datepart* por um *número* grande o suficiente para também incrementar a próxima maior *datepart* de *data*.
  
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
Os exemplos a seguir usam diferentes tipos de expressões como argumentos para o *número* e *data* parâmetros. Os exemplos usam o banco de dados AdventureWorks.
  
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
O exemplo a seguir especifica as variáveis definidas pelo usuário como argumentos para *número* e *data*.
  
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
O exemplo a seguir especifica `SYSDATETIME` para *data*.
  
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
O exemplo a seguir usa subconsultas escalares, `MAX(ModifiedDate)`, como argumentos para *número* e *data*. `(SELECT TOP 1 BusinessEntityID FROM Person.Person)`é um argumento artificial para o parâmetro de número mostrar como selecionar um *número* argumento de uma lista de valores.
  
```sql
SELECT DATEADD(month,(SELECT TOP 1 BusinessEntityID FROM Person.Person),  
    (SELECT MAX(ModifiedDate) FROM Person.Person));  
```  
  
#### <a name="specifying-numeric-expressions-and-scalar-system-functions-as-number-and-date"></a>Especificando expressões numéricas e funções de sistema escalares como número e data  
O exemplo a seguir usa uma expressão numérica (-`(10/2))`, [operadores unários](../../mdx/unary-operators.md) (`-`), uma [operador aritmético](../../mdx/arithmetic-operators.md) (`/`) e funções de sistema escalares (`SYSDATETIME`) como argumentos para *número* e *data*.
  
```sql
SELECT DATEADD(month,-(10/2), SYSDATETIME());  
```  
  
#### <a name="specifying-ranking-functions-as-number"></a>Especificando funções de classificação como número  
O exemplo a seguir usa uma função de classificação como argumentos para *número*.
  
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
O exemplo a seguir usa uma função de janela de agregação como um argumento para *número*.
  
```sql
SELECT SalesOrderID, ProductID, OrderQty  
    ,DATEADD(day,SUM(OrderQty)   
        OVER(PARTITION BY SalesOrderID),SYSDATETIME()) AS 'Total'  
FROM Sales.SalesOrderDetail   
WHERE SalesOrderID IN(43659,43664);  
GO  
```  
  
  
## <a name="see-also"></a>Consulte também
[CAST e CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)
  
  


