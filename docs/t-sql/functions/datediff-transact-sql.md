---
title: DATEDIFF (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 12/13/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DATEDIFF_TSQL
- DATEDIFF
dev_langs:
- TSQL
helpviewer_keywords:
- dates [SQL Server], functions
- DATEDIFF function [SQL Server]
- time [SQL Server], crossed boundaries
- differences in date and time [SQL Server]
- counting crossed date time boundaries [SQL Server]
- date and time [SQL Server], DATEDIFF
- dates [SQL Server], crossed boundaries
- boundary differences date and time [SQL Server]
- functions [SQL Server], time
- functions [SQL Server], date and time
- interval dates [SQL Server]
- time [SQL Server], functions
- crossing date time boundaries [SQL Server]
- calculating dates times [SQL Server]
ms.assetid: eba979f2-1a8d-4cce-9d75-b74f9b519b37
author: MashaMSFT
ms.author: mathoma
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 7381dbf667c969765a189df469cc94a9e4b0c5a9
ms.sourcegitcommit: 622bcdaa0b21258248b259f003f38e9d6f73e05a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/17/2019
ms.locfileid: "65836193"
---
# <a name="datediff-transact-sql"></a>DATEDIFF (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Essa função retorna a contagem (como um valor inteiro com sinal) dos limites de datepart especificados cruzados entre os parâmetros especificados *startdate* e *enddate*.
  
Consulte [DATEDIFF_BIG &#40;Transact-SQL&#41;](../../t-sql/functions/datediff-big-transact-sql.md) para obter uma função que manipula diferenças maiores entre os valores *startdate* e *enddate*. Consulte [Tipos de dados e funções de data e hora &#40;Transact-SQL&#41;](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md) para obter uma visão geral de todos os tipos de dados e funções de data e hora do [!INCLUDE[tsql](../../includes/tsql-md.md)].
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
  
```sql
DATEDIFF ( datepart , startdate , enddate )  
```  
  
## <a name="arguments"></a>Argumentos  
*datepart*  
A parte de *startdate* e de *enddate* que especifica o tipo de limite ultrapassado. `DATEDIFF` não aceitarão equivalentes de variável definidos pelo usuário. Esta tabela lista todos os argumentos *datepart* válidos.
  
|*datepart*|Abreviações|  
|---|---|
|**year**|**yy, yyyy**|  
|**quarter**|**qq, q**|  
|**month**|**mm, m**|  
|**dayofyear**|**dy, y**|  
|**day**|**dd, d**|  
|**week**|**wk, ww**|  
|**hour**|**hh**|  
|**minute**|**mi, n**|  
|**second**|**ss, s**|  
|**millisecond**|**ms**|  
|**microsecond**|**mcs**|  
|**nanosecond**|**ns**|  
  
*startdate*  
Uma expressão que pode resolver um dos seguintes valores:

+ **date**
+ **datetime**
+ **datetimeoffset**
+ **datetime2** 
+ **smalldatetime**
+ **time**
  
Use anos de quatro dígitos para evitar ambiguidade. Consulte [Configurar a opção two digit year cutoff de configuração de servidor](../../database-engine/configure-windows/configure-the-two-digit-year-cutoff-server-configuration-option.md) para obter informações sobre valores de anos de dois dígitos.
  
*enddate*  
Consulte *startdate*.
  
## <a name="return-type"></a>Tipo de retorno  
 **int**  
  
## <a name="return-value"></a>Valor retornado  
  
Cada *datepart* específico e as abreviações desse *datepart* retornarão o mesmo valor.  
  
Para um valor retornado fora do intervalo para **int** (-2.147.483.648 a +2.147.483.647), `DATEDIFF` retorna um erro.  Para **millisecond**, a diferença máxima entre *startdate* e *enddate* é de 24 dias, 20 horas, 31 minutos e 23.647 segundos. Para **segundo**, a diferença máxima é de 68 anos, 19 dias, 3 horas, 14 minutos e 7 segundos.
  
Se *startdate* e *enddate* receberem apenas um valor temporal e *datepart* não for um *datepart* de hora, `DATEDIFF` retornará 0.
  
`DATEDIFF` não usa um componente de deslocamento de fuso horário de *startdate* ou *enddate* para calcular o valor retornado.
  
Como [smalldatetime](../../t-sql/data-types/smalldatetime-transact-sql.md) tem precisão apenas quanto ao minuto, segundos e milissegundos são sempre definidos como 0 no valor retornado quando um valor *smalldatetime* é usado para *startdate* ou **enddate**.
  
Se apenas um valor temporal for atribuído a uma variável de tipo de dados de data, `DATEDIFF` definirá o valor da parte de data ausente como o valor padrão: `1900-01-01`. Se apenas um valor de data for atribuído a uma variável de um tipo de dados de data ou hora, `DATEDIFF` definirá o valor da parte de hora ausente como o valor padrão: `00:00:00`. Se *startdate* ou *enddate* tiver apenas uma parte de hora e a outra apenas uma parte de data, `DATEDIFF` definirá as partes de hora e data ausentes como os valores padrão.
  
Se *startdate* e *enddate* tiverem diferentes tipos de dados de data e um tiver mais partes de hora ou precisão de segundos fracionários do que o outro, `DATEDIFF` definirá as partes ausentes do outro como 0.
  
## <a name="datepart-boundaries"></a>Limites de datepart  
As instruções a seguir têm os mesmos valores de *startdate* e de *enddate*. Essas datas são adjacentes e diferem no tempo em 100 nanossegundos (0,0000001 segundo). A diferença entre *startdate* e *enddate* em cada instrução cruza um calendário ou limite de hora de sua *datepart*. Cada instrução retorna 1. Se *startdate* e *enddate* tiverem diferentes valores de ano, mas os mesmos valores semanais de calendário, `DATEDIFF` retornará 0 para *datepart* **week**.
  
```sql
SELECT DATEDIFF(year,        '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF(quarter,     '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF(month,       '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF(dayofyear,   '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF(day,         '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF(week,        '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF(hour,        '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF(minute,      '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF(second,      '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF(millisecond, '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF(microsecond, '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
```
  
## <a name="remarks"></a>Remarks  
Use `DATEDIFF` nas cláusulas `SELECT <list>`, `WHERE`, `HAVING`, `GROUP BY` e `ORDER BY`.
  
`DATEDIFF` converte implicitamente literais de cadeias de caracteres como um tipo **datetime2**. Isso significa que `DATEDIFF` não é compatível com o formato YDM quando a data é transmitida como cadeia de caracteres. É necessário converter explicitamente a cadeia de caracteres em um tipo de **datetime** ou **smalldatetime** para usar o formato YDM.
  
Especificar `SET DATEFIRST` não tem efeito sobre `DATEDIFF`. `DATEDIFF` sempre usa domingo como o primeiro dia da semana para garantir que a função opere de maneira determinística.

`DATEDIFF` poderá estourar com uma precisão de **minuto** ou mais se a diferença entre *enddate* e *startdate* retornar um valor fora do intervalo para **int**.
  
## <a name="examples"></a>Exemplos  
Esses exemplos usam diferentes tipos de expressões como argumentos para os parâmetros *startdate* e *enddate*.
  
### <a name="a-specifying-columns-for-startdate-and-enddate"></a>A. Especificando colunas para startdate e enddate  
Este exemplo calcula o número de limites de dia cruzados entre datas em duas colunas de uma tabela.
  
```sql
CREATE TABLE dbo.Duration  
    (startDate datetime2, endDate datetime2);  
    
INSERT INTO dbo.Duration(startDate, endDate)  
    VALUES ('2007-05-06 12:10:09', '2007-05-07 12:10:09');  
    
SELECT DATEDIFF(day, startDate, endDate) AS 'Duration'  
    FROM dbo.Duration;  
-- Returns: 1  
```  
  
### <a name="b-specifying-user-defined-variables-for-startdate-and-enddate"></a>B. Especificando variáveis definidas pelo usuário para startdate e enddate  
Nesse exemplo, variáveis definidas pelo usuário funcionam como argumentos para *startdate* e *enddate*.
  
```sql
DECLARE @startdate datetime2 = '2007-05-05 12:10:09.3312722';  
DECLARE @enddate   datetime2 = '2007-05-04 12:10:09.3312722';   
SELECT DATEDIFF(day, @startdate, @enddate);  
```  
  
### <a name="c-specifying-scalar-system-functions-for-startdate-and-enddate"></a>C. Especificando funções de sistema escalares para startdate e enddate  
Esse exemplo usa funções do sistema escalares como argumentos para *startdate* e *enddate*.
  
```sql
SELECT DATEDIFF(millisecond, GETDATE(), SYSDATETIME());  
```  
  
### <a name="d-specifying-scalar-subqueries-and-scalar-functions-for-startdate-and-enddate"></a>D. Especificando subconsultas e funções escalares para startdate e enddate  
Este exemplo usa subconsultas e funções escalares como argumentos para *startdate* e *enddate*.
  
```sql
USE AdventureWorks2012;  
GO  
SELECT DATEDIFF(day,
    (SELECT MIN(OrderDate) FROM Sales.SalesOrderHeader),  
    (SELECT MAX(OrderDate) FROM Sales.SalesOrderHeader));  
```  
  
### <a name="e-specifying-constants-for-startdate-and-enddate"></a>E. Especificando constantes para startdate e enddate  
Este exemplo usa constantes de caractere como argumentos para *startdate* e *enddate*.
  
```sql
SELECT DATEDIFF(day,
   '2007-05-07 09:53:01.0376635',
   '2007-05-08 09:53:01.0376635');  
```  
  
### <a name="f-specifying-numeric-expressions-and-scalar-system-functions-for-enddate"></a>F. Especificando expressões numéricas e funções de sistema escalares para enddate  
Esse exemplo usa uma expressão numérica, `(GETDATE() + 1)`, e as funções do sistema escalares, `GETDATE` e `SYSDATETIME`, como argumentos para *enddate*.
  
```sql
USE AdventureWorks2012;  
GO  
SELECT DATEDIFF(day, '2007-05-07 09:53:01.0376635', GETDATE() + 1)   
    AS NumberOfDays  
    FROM Sales.SalesOrderHeader;  
GO  
USE AdventureWorks2012;  
GO  
SELECT DATEDIFF(day, '2007-05-07 09:53:01.0376635', DATEADD(day, 1, SYSDATETIME())) AS NumberOfDays  
    FROM Sales.SalesOrderHeader;  
GO  
```  
  
### <a name="g-specifying-ranking-functions-for-startdate"></a>G. Especificando funções de classificação para startdate  
Este exemplo usa uma função de classificação como um argumento para *startdate*.
  
```sql
USE AdventureWorks2012;  
GO  
SELECT p.FirstName, p.LastName  
    ,DATEDIFF(day, ROW_NUMBER() OVER (ORDER BY   
        a.PostalCode), SYSDATETIME()) AS 'Row Number'  
FROM Sales.SalesPerson s   
    INNER JOIN Person.Person p   
        ON s.BusinessEntityID = p.BusinessEntityID  
    INNER JOIN Person.Address a   
        ON a.AddressID = p.BusinessEntityID  
WHERE TerritoryID IS NOT NULL   
    AND SalesYTD <> 0;  
```  
  
### <a name="h-specifying-an-aggregate-window-function-for-startdate"></a>H. Especificando uma função de janela de agregação para startdate  
Este exemplo usa uma função de janela de agregação como um argumento para *startdate*.
  
```sql
USE AdventureWorks2012;  
GO  
SELECT soh.SalesOrderID, sod.ProductID, sod.OrderQty, soh.OrderDate,
    DATEDIFF(day, MIN(soh.OrderDate)   
        OVER(PARTITION BY soh.SalesOrderID), SYSDATETIME()) AS 'Total'  
FROM Sales.SalesOrderDetail sod  
    INNER JOIN Sales.SalesOrderHeader soh  
        ON sod.SalesOrderID = soh.SalesOrderID  
WHERE soh.SalesOrderID IN(43659, 58918);  
GO  
```  

### <a name="i-finding-difference-between-startdate-and-enddate-as-date-parts-strings"></a>I. Localizando a diferença entre startdate e enddate como cadeias de caracteres de partes de data

```sql
DECLARE @date1 DATETIME, @date2 DATETIME, @result VARCHAR(100)
DECLARE @years INT, @months INT, @days INT, @hours INT, @minutes INT, @seconds INT, @milliseconds INT

SET @date1 = '1900-01-01 00:00:00.000'
SET @date2 = '2018-12-12 07:08:01.123'

SELECT @years = DATEDIFF(yy, @date1, @date2)
IF DATEADD(yy, -@years, @date2) < @date1 
SELECT @years = @years-1
SET @date2 = DATEADD(yy, -@years, @date2)

SELECT @months = DATEDIFF(mm, @date1, @date2)
IF DATEADD(mm, -@months, @date2) < @date1 
SELECT @months=@months-1
SET @date2= DATEADD(mm, -@months, @date2)

SELECT @days=DATEDIFF(dd, @date1, @date2)
IF DATEADD(dd, -@days, @date2) < @date1 
SELECT @days=@days-1
SET @date2= DATEADD(dd, -@days, @date2)

SELECT @hours=DATEDIFF(hh, @date1, @date2)
IF DATEADD(hh, -@hours, @date2) < @date1 
SELECT @hours=@hours-1
SET @date2= DATEADD(hh, -@hours, @date2)

SELECT @minutes=DATEDIFF(mi, @date1, @date2)
IF DATEADD(mi, -@minutes, @date2) < @date1 
SELECT @minutes=@minutes-1
SET @date2= DATEADD(mi, -@minutes, @date2)

SELECT @seconds=DATEDIFF(s, @date1, @date2)
IF DATEADD(s, -@seconds, @date2) < @date1 
SELECT @seconds=@seconds-1
SET @date2= DATEADD(s, -@seconds, @date2)

SELECT @milliseconds=DATEDIFF(ms, @date1, @date2)

SELECT @result= ISNULL(CAST(NULLIF(@years,0) AS VARCHAR(10)) + ' years,','')
     + ISNULL(' ' + CAST(NULLIF(@months,0) AS VARCHAR(10)) + ' months,','')    
     + ISNULL(' ' + CAST(NULLIF(@days,0) AS VARCHAR(10)) + ' days,','')
     + ISNULL(' ' + CAST(NULLIF(@hours,0) AS VARCHAR(10)) + ' hours,','')
     + ISNULL(' ' + CAST(@minutes AS VARCHAR(10)) + ' minutes and','')
     + ISNULL(' ' + CAST(@seconds AS VARCHAR(10)) 
          + CASE WHEN @milliseconds > 0 THEN '.' + CAST(@milliseconds AS VARCHAR(10)) 
               ELSE '' END 
          + ' seconds','')

SELECT @result
```

[!INCLUDE[ssResult](../../includes/ssresult-md.md)] 

```
118 years, 11 months, 11 days, 7 hours, 8 minutes and 1.123 seconds
```
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Exemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
Esses exemplos usam diferentes tipos de expressões como argumentos para os parâmetros *startdate* e *enddate*.
  
### <a name="j-specifying-columns-for-startdate-and-enddate"></a>J. Especificando colunas para startdate e enddate  
Este exemplo calcula o número de limites de dia cruzados entre datas em duas colunas de uma tabela.
  
```sql
CREATE TABLE dbo.Duration 
    (startDate datetime2, endDate datetime2);
    
INSERT INTO dbo.Duration (startDate, endDate)  
    VALUES ('2007-05-06 12:10:09', '2007-05-07 12:10:09');  
    
SELECT TOP(1) DATEDIFF(day, startDate, endDate) AS Duration  
    FROM dbo.Duration;  
-- Returns: 1  
```  
  
### <a name="k-specifying-scalar-subqueries-and-scalar-functions-for-startdate-and-enddate"></a>K. Especificando subconsultas e funções escalares para startdate e enddate  
Este exemplo usa subconsultas e funções escalares como argumentos para *startdate* e *enddate*.
  
```sql
-- Uses AdventureWorks  
  
SELECT TOP(1) DATEDIFF(day, (SELECT MIN(HireDate) FROM dbo.DimEmployee),  
    (SELECT MAX(HireDate) FROM dbo.DimEmployee))   
FROM dbo.DimEmployee;  
  
```  
  
### <a name="l-specifying-constants-for-startdate-and-enddate"></a>L. Especificando constantes para startdate e enddate  
Este exemplo usa constantes de caractere como argumentos para *startdate* e *enddate*.
  
```sql
-- Uses AdventureWorks  
  
SELECT TOP(1) DATEDIFF(day,
    '2007-05-07 09:53:01.0376635',
    '2007-05-08 09:53:01.0376635') FROM DimCustomer;  
```  
  
### <a name="m-specifying-ranking-functions-for-startdate"></a>M. Especificando funções de classificação para startdate  
Este exemplo usa uma função de classificação como um argumento para *startdate*.
  
```sql
-- Uses AdventureWorks  
  
SELECT FirstName, LastName,
    DATEDIFF(day, ROW_NUMBER() OVER (ORDER BY   
        DepartmentName), SYSDATETIME()) AS RowNumber  
FROM dbo.DimEmployee;  
```  
  
### <a name="n-specifying-an-aggregate-window-function-for-startdate"></a>N. Especificando uma função de janela de agregação para startdate  
Este exemplo usa uma função de janela de agregação como um argumento para *startdate*.
  
```sql
-- Uses AdventureWorks  
  
SELECT FirstName, LastName, DepartmentName,
    DATEDIFF(year, MAX(HireDate)  
        OVER (PARTITION BY DepartmentName), SYSDATETIME()) AS SomeValue  
FROM dbo.DimEmployee  
```  
  
## <a name="see-also"></a>Confira também
[DATEDIFF_BIG &#40;Transact-SQL&#41;](../../t-sql/functions/datediff-big-transact-sql.md)  
[CAST e CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)
  
