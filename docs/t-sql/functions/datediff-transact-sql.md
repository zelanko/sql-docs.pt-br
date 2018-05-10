---
title: DATEDIFF (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/29/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
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
caps.latest.revision: 52
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: c597985b34d078dbd640e680b5e9cf904d81567d
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="datediff-transact-sql"></a>DATEDIFF (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Retorna a contagem (inteiro com sinal) dos limites especificados de *datepart* cruzados entre os parâmetros especificados *startdate* e *enddate*.
  
Para diferenças maiores, consulte [DATEDIFF_BIG &#40;Transact-SQL&#41;](../../t-sql/functions/datediff-big-transact-sql.md). Para obter uma visão geral das funções e dos tipos de dados de data e hora de [!INCLUDE[tsql](../../includes/tsql-md.md)], confira [Funções e tipos de dados de data e hora &#40;Transact-SQL&#41;](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md).
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
  
```sql
DATEDIFF ( datepart , startdate , enddate )  
```  
  
## <a name="arguments"></a>Argumentos  
*datepart*  
É a parte da *startdate* e *enddate* que especifica o tipo de limite ultrapassado. A tabela a seguir lista todos os argumentos válidos de *datepart*. Equivalentes de variável definidos pelo usuário não são válidos.
  
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
É uma expressão que pode ser resolvida em um valor de **time**, **date**, **smalldatetime**, **datetime**, **datetime2** ou **datetimeoffset**. *date* pode ser uma expressão, uma expressão de coluna, uma variável definida pelo usuário ou um literal de cadeia de caracteres. *startdate* é subtraído de *enddate*.
  
Para evitar ambiguidade, use anos de quatro dígitos. Para obter mais informações sobre anos de dois dígitos, confira [Configurar a opção Corte de Ano de Dois Dígitos do servidor](../../database-engine/configure-windows/configure-the-two-digit-year-cutoff-server-configuration-option.md).
  
*enddate*  
Consulte *startdate*.
  
## <a name="return-type"></a>Tipo de retorno  
 **int**  
  
## <a name="return-value"></a>Valor retornado  
  
-   Cada *datepart* retorna o mesmo valor das abreviações dela.  
  
Se o valor retornado estiver fora do intervalo de **int** (-2.147.483.648 a +2.147.483.647), um erro será retornado. Para **millisecond**, a diferença máxima entre *startdate* e *enddate* é de 24 dias, 20 horas, 31 minutos e 23.647 segundos. Para **second**, a diferença máxima é de 68 anos.
  
Se *startdate* e *enddate* recebem apenas um valor temporal e a *datepart* não é uma *datepart* de hora, será retornado 0.
  
Um componente de deslocamento de fuso horário de *startdate* ou *enddate* não é usado no cálculo do valor retornado.
  
Como [smalldatetime](../../t-sql/data-types/smalldatetime-transact-sql.md) tem precisão apenas quanto ao minuto, quando um valor **smalldatetime** é usado para *startdate* ou *enddate*, os segundos e milissegundos são sempre definidos como 0 no valor retornado.
  
Se apenas um valor de hora for atribuído a uma variável de tipo de dados “data”, o valor da parte “data” faltante será definido como o valor padrão: 1900-01-01. Se apenas um valor de data for atribuído a uma variável de tipo de dados “hora” ou “data”, o valor da parte “hora” faltante será definido como o valor padrão: 00:00:00. Se *startdate* ou *enddate* tem apenas uma parte de hora e a outra apenas uma parte de data, as partes de hora e data ausentes são definidas com os valores padrão.
  
Se *startdate* e *enddate* forem de tipos de dados de data diferentes e um tiver mais partes de hora ou precisão de segundos fracionários do que o outro, as partes ausentes do outro serão definidas como 0.
  
## <a name="datepart-boundaries"></a>Limites de datepart  
As instruções a seguir têm a mesma *startdate* e *enddate*. Essas datas são adjacentes e diferem, quanto à hora, em 0,0000001 segundo. A diferença entre *startdate* e *enddate* em cada instrução cruza um calendário ou limite de hora de sua *datepart*. Cada instrução retorna 1. Se anos diferentes forem usados neste exemplo e se *startdate* e *enddate* estiverem na mesma semana de calendário, o valor retornado para **week** será 0.
  
```sql
SELECT DATEDIFF(year, '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF(quarter, '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF(month, '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF(dayofyear, '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF(day, '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF(week, '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF(hour, '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF(minute, '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF(second, '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF(millisecond, '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
```
  
## <a name="remarks"></a>Remarks  
DATEDIFF pode ser usado na lista de seleção, cláusulas WHERE, HAVING, GROUP BY e ORDER BY.
  
DATEDIFF converte implicitamente literais de cadeias de caracteres como um tipo **datetime2**. Isso significa que DATEDIFF não oferece suporte ao formato YDM quando a data é transmitida como cadeia de caracteres. É necessário converter explicitamente a cadeia de caracteres em um tipo de **datetime** ou **smalldatetime** para usar o formato YDM.
  
A especificação de SET DATEFIRST não tem nenhum efeito em DATEDIFF. DATEDIFF sempre usa Domingo como o primeiro dia da semana par assegurar que a função seja determinística.
  
## <a name="examples"></a>Exemplos  
Os exemplos a seguir usam diferentes tipos de expressões como argumentos para os parâmetros *startdate* e *enddate*.
  
### <a name="a-specifying-columns-for-startdate-and-enddate"></a>A. Especificando colunas para startdate e enddate  
O exemplo a seguir calcula o número de limites de dia que são cruzados entre as datas de duas colunas de uma tabela.
  
```sql
CREATE TABLE dbo.Duration  
    (  
    startDate datetime2  
    ,endDate datetime2  
    );  
INSERT INTO dbo.Duration(startDate,endDate)  
    VALUES('2007-05-06 12:10:09','2007-05-07 12:10:09');  
SELECT DATEDIFF(day,startDate,endDate) AS 'Duration'  
FROM dbo.Duration;  
-- Returns: 1  
```  
  
### <a name="b-specifying-user-defined-variables-for-startdate-and-enddate"></a>B. Especificando variáveis definidas pelo usuário para startdate e enddate  
O exemplo a seguir utiliza variáveis definidas pelo usuário como argumentos para *startdate* e *enddate*.
  
```sql
DECLARE @startdate datetime2 = '2007-05-05 12:10:09.3312722';  
DECLARE @enddate datetime2 = '2007-05-04 12:10:09.3312722';   
SELECT DATEDIFF(day, @startdate, @enddate);  
```  
  
### <a name="c-specifying-scalar-system-functions-for-startdate-and-enddate"></a>C. Especificando funções de sistema escalares para startdate e enddate  
O exemplo a seguir usa funções do sistema escalares como argumentos para *startdate* e *enddate*.
  
```sql
SELECT DATEDIFF(millisecond, GETDATE(), SYSDATETIME());  
```  
  
### <a name="d-specifying-scalar-subqueries-and-scalar-functions-for-startdate-and-enddate"></a>D. Especificando subconsultas e funções escalares para startdate e enddate  
O exemplo a seguir usa subconsultas e funções escalares como argumentos para *startdate* e *enddate*.
  
```sql
USE AdventureWorks2012;  
GO  
SELECT DATEDIFF(day,(SELECT MIN(OrderDate) FROM Sales.SalesOrderHeader),  
    (SELECT MAX(OrderDate) FROM Sales.SalesOrderHeader));  
```  
  
### <a name="e-specifying-constants-for-startdate-and-enddate"></a>E. Especificando constantes para startdate e enddate  
O exemplo a seguir usa constantes de caractere como argumentos para *startdate* e *enddate*.
  
```sql
SELECT DATEDIFF(day, '2007-05-07 09:53:01.0376635'  
    , '2007-05-08 09:53:01.0376635');  
```  
  
### <a name="f-specifying-numeric-expressions-and-scalar-system-functions-for-enddate"></a>F. Especificando expressões numéricas e funções de sistema escalares para enddate  
O exemplo a seguir usa uma expressão numérica, `(GETDATE ()+ 1)`, e as funções do sistema escalares, `GETDATE` e `SYSDATETIME`, como argumentos para *enddate*.
  
```sql
USE AdventureWorks2012;  
GO  
SELECT DATEDIFF(day, '2007-05-07 09:53:01.0376635', GETDATE()+ 1)   
    AS NumberOfDays  
FROM Sales.SalesOrderHeader;  
GO  
USE AdventureWorks2012;  
GO  
SELECT DATEDIFF(day, '2007-05-07 09:53:01.0376635', DATEADD(day,1,SYSDATETIME())) AS NumberOfDays  
FROM Sales.SalesOrderHeader;  
GO  
```  
  
### <a name="g-specifying-ranking-functions-for-startdate"></a>G. Especificando funções de classificação para startdate  
O exemplo a seguir usa uma função de classificação como argumento para *startdate*.
  
```sql
USE AdventureWorks2012;  
GO  
SELECT p.FirstName, p.LastName  
    ,DATEDIFF(day,ROW_NUMBER() OVER (ORDER BY   
        a.PostalCode),SYSDATETIME()) AS 'Row Number'  
FROM Sales.SalesPerson s   
    INNER JOIN Person.Person p   
        ON s.BusinessEntityID = p.BusinessEntityID  
    INNER JOIN Person.Address a   
        ON a.AddressID = p.BusinessEntityID  
WHERE TerritoryID IS NOT NULL   
    AND SalesYTD <> 0;  
```  
  
### <a name="h-specifying-an-aggregate-window-function-for-startdate"></a>H. Especificando uma função de janela de agregação para startdate  
O exemplo a seguir usa uma função de janela de agregação como argumento para *startdate*.
  
```sql
USE AdventureWorks2012;  
GO  
SELECT soh.SalesOrderID, sod.ProductID, sod.OrderQty,soh.OrderDate  
    ,DATEDIFF(day,MIN(soh.OrderDate)   
        OVER(PARTITION BY soh.SalesOrderID),SYSDATETIME() ) AS 'Total'  
FROM Sales.SalesOrderDetail sod  
    INNER JOIN Sales.SalesOrderHeader soh  
        ON sod.SalesOrderID = soh.SalesOrderID  
WHERE soh.SalesOrderID IN(43659,58918);  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Exemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
Os exemplos a seguir usam diferentes tipos de expressões como argumentos para os parâmetros *startdate* e *enddate*.
  
### <a name="i-specifying-columns-for-startdate-and-enddate"></a>I. Especificando colunas para startdate e enddate  
O exemplo a seguir calcula o número de limites de dia que são cruzados entre as datas de duas colunas de uma tabela.
  
```sql
CREATE TABLE dbo.Duration (  
    startDate datetime2  
    ,endDate datetime2  
    );  
INSERT INTO dbo.Duration(startDate,endDate)  
    VALUES('2007-05-06 12:10:09','2007-05-07 12:10:09');  
SELECT TOP(1) DATEDIFF(day,startDate,endDate) AS Duration  
FROM dbo.Duration;  
-- Returns: 1  
```  
  
### <a name="j-specifying-scalar-subqueries-and-scalar-functions-for-startdate-and-enddate"></a>J. Especificando subconsultas e funções escalares para startdate e enddate  
O exemplo a seguir usa subconsultas e funções escalares como argumentos para *startdate* e *enddate*.
  
```sql
-- Uses AdventureWorks  
  
SELECT TOP(1) DATEDIFF(day,(SELECT MIN(HireDate) FROM dbo.DimEmployee),  
    (SELECT MAX(HireDate) FROM dbo.DimEmployee))   
FROM dbo.DimEmployee;  
  
```  
  
### <a name="k-specifying-constants-for-startdate-and-enddate"></a>K. Especificando constantes para startdate e enddate  
O exemplo a seguir usa constantes de caractere como argumentos para *startdate* e *enddate*.
  
```sql
-- Uses AdventureWorks  
  
SELECT TOP(1) DATEDIFF(day, '2007-05-07 09:53:01.0376635'  
    , '2007-05-08 09:53:01.0376635') FROM DimCustomer;  
```  
  
### <a name="l-specifying-ranking-functions-for-startdate"></a>L. Especificando funções de classificação para startdate  
O exemplo a seguir usa uma função de classificação como argumento para *startdate*.
  
```sql
-- Uses AdventureWorks  
  
SELECT FirstName, LastName  
,DATEDIFF(day,ROW_NUMBER() OVER (ORDER BY   
        DepartmentName),SYSDATETIME()) AS RowNumber  
FROM dbo.DimEmployee;  
```  
  
### <a name="m-specifying-an-aggregate-window-function-for-startdate"></a>M. Especificando uma função de janela de agregação para startdate  
O exemplo a seguir usa uma função de janela de agregação como argumento para *startdate*.
  
```sql
-- Uses AdventureWorks  
  
SELECT FirstName, LastName, DepartmentName  
    ,DATEDIFF(year,MAX(HireDate)  
             OVER (PARTITION BY DepartmentName),SYSDATETIME()) AS SomeValue  
FROM dbo.DimEmployee  
```  
  
## <a name="see-also"></a>Confira também
[DATEDIFF_BIG &#40;Transact-SQL&#41;](../../t-sql/functions/datediff-big-transact-sql.md)  
[CAST e CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)
  
  


