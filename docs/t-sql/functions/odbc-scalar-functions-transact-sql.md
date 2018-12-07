---
title: Funções escalares do ODBC (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- CURDATE ODBC function
- DAYOFMONTH ODBC function
- WEEK ODBC function
- functions, ODBC CONCAT
- SECOND ODBC function
- functions, ODBC CURRENT_TIME
- functions, ODBC HOUR
- functions, ODBC QUARTER
- TRUNCATE ODBC function
- functions, ODBC SECOND
- DAYOFWEEK ODBC function
- CURRENT_DATE ODBC function
- DAYNAME ODBC function
- CURTIME ODBC function
- functions, ODBC CURRENT_DATE
- MINUTE ODBC function
- functions, ODBC BIT_LENGTH
- functions, ODBC OCTET_LENGTH
- CONCAT ODBC function
- MONTHNAME ODBC function
- functions, ODBC DAYOFYEAR
- OCTET_LENGTH ODBC function
- functions [SQL Server], ODBC scalar functions
- BIT_LENGTH ODBC function
- functions, ODBC DAYOFMONTH
- CURRENT_TIME ODBC function
- functions, ODBC CURDATE
- functions, ODBC CURTIME
- functions, ODBC TRUNCATE
- functions, ODBC MONTHNAME
- functions, ODBC DAYNAME
- ODBC scalar functions
- functions, ODBC MINUTE
- functions, ODBC DAYOFWEEK
- QUARTER ODBC function
- DAYOFYEAR ODBC function
- functions, ODBC WEEK
- HOUR ODBC function
ms.assetid: a0df1ac2-6699-4ac0-8f79-f362f23496f1
author: MashaMSFT
ms.author: mathoma
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 6456a8ad03e4f0cb86c5299f1d817775688c1330
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52535590"
---
# <a name="odbc-scalar-functions-transact-sql"></a>Funções escalares ODBC (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  É possível usar [Funções escalares do ODBC](https://go.microsoft.com/fwlink/?LinkID=88579) em instruções [!INCLUDE[tsql](../../includes/tsql-md.md)]. Essas instruções são interpretadas pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Elas podem ser usadas em procedimentos armazenados e em funções definidas pelo usuário. Elas incluem funções de cadeia de caracteres, numéricas, de tempo, de data, de intervalo e de sistema.  
  
## <a name="usage"></a>Uso  
 `SELECT {fn <function_name> [ (<argument>,....n) ] }`  
  
## <a name="functions"></a>Funções  
 As tabelas a seguir listam funções escalares ODBC que não são duplicadas no [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
### <a name="string-functions"></a>Funções de cadeia de caracteres  
  
|Função|Descrição|  
|--------------|-----------------|  
|BIT_LENGTH( string_exp ) (ODBC 3.0)|Retorna o comprimento em bits da expressão de cadeia de caracteres.<br /><br /> Não funciona apenas em tipos de dados de cadeia de caracteres. Portanto, não converterá implicitamente string_exp em cadeia de caracteres. Em vez disso, retornará o tamanho (interno) de qualquer tipo de dados especificado.|  
|CONCAT( string_exp1,string_exp2) (ODBC 1.0)|Retorna uma cadeia de caracteres que é o resultado da concatenação de string_exp2 com string_exp1. A cadeia de caracteres resultante é dependente de DBMS. Por exemplo, se a coluna representada por string_exp1 tivesse um valor NULL, DB2 retornaria NULL, mas o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] retornaria a cadeia de caracteres non-NULL.|  
|OCTET_LENGTH( string_exp ) (ODBC 3.0)|Retorna o comprimento em bytes da expressão de cadeia de caracteres. O resultado é o menor número inteiro, não menos que o número de bits dividido por 8.<br /><br /> Não funciona apenas em tipos de dados de cadeia de caracteres. Portanto, não converterá implicitamente string_exp em cadeia de caracteres. Em vez disso, retornará o tamanho (interno) de qualquer tipo de dados especificado.|  
  
### <a name="numeric-function"></a>Função numérica  
  
|Função|Descrição|  
|--------------|-----------------|  
|TRUNCATE( numeric_exp, integer_exp) (ODBC 2.0)|Retorna numeric_exp truncado com posições integer_exp à direita da casa decimal. Se integer_exp for negativo, numeric_exp será truncado com as posições &#124;integer_exp&#124; à esquerda da vírgula decimal.|  
  
### <a name="time-date-and-interval-functions"></a>Funções de hora, data e intervalo  
  
|Função|Descrição|  
|--------------|-----------------|  
|CURRENT_DATE( ) (ODBC 3.0)|Retorna a data atual.|  
|CURDATE( ) (ODBC 3.0)|Retorna a data atual.|  
|CURRENT_TIME`[( time-precision )]` (ODBC 3.0)|Retorna a hora local atual. O argumento time-precision determina a precisão em segundos do valor retornado|  
|CURTIME() (ODBC 3.0)|Retorna a hora local atual.|  
|DAYNAME( date_exp ) (ODBC 2.0)|Retorna uma cadeia de caracteres que contém o nome específico da fonte de dados do dia (por exemplo, domingo a sábado ou dom. a Sat. para uma fonte de dados que usa o inglês, ou Sonntag a Samstag para uma fonte de dados que usa alemão) para a parte do dia de date_exp.|  
|DAYOFMONTH( date_exp ) (ODBC 1.0)|Retorna o dia do mês com base no campo de mês em date_exp como um valor inteiro no intervalo de 1 a 31.|  
|DAYOFWEEK( date_exp ) (ODBC 1.0)|Retorna o dia da semana com base no campo de semana em date_exp como um valor inteiro no intervalo de 1 a 7, em que 1 representa domingo.|  
|HOUR( time_exp ) (ODBC 1.0)|Retorna a hora com base no campo de hora em time_exp como um valor inteiro no intervalo de 0 a 23.|  
|MINUTE( time_exp ) (ODBC 1.0)|Retorna o minuto com base no campo de minuto em time_exp como um valor inteiro no intervalo de 0 a 59.|  
|SECOND( time_exp ) (ODBC 1.0)|Retorna o segundo com base no campo de segundo em time_exp como um valor inteiro no intervalo de 0 a 59.|  
|MONTHNAME( date_exp ) (ODBC 2.0)|Retorna uma cadeia de caracteres que contém um nome específico de fonte de dados do mês (por exemplo, January a December ou Jan a Dec para a fonte de dados que utiliza o inglês ou Januar a Dezember para uma fonte de dados que usa o alemão) para a parte de mês em date_exp.|  
|QUARTER( date_exp ) (ODBC 1.0)|Retorna o trimestre em date_exp como um valor inteiro no intervalo de 1 a 4, em que 1 representa 1 de janeiro a 31 de março.|  
|WEEK( date_exp ) (ODBC 1.0)|Retorna a semana do ano, com base no campo de semana em date_exp como um valor inteiro no intervalo de 1 a 53.|  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-using-an-odbc-function-in-a-stored-procedure"></a>A. Usando uma função ODBC em um procedimento armazenado  
 O seguinte exemplo usa uma função ODBC em um procedimento armazenado:  
  
```  
CREATE PROCEDURE dbo.ODBCprocedure  
    (  
    @string_exp nvarchar(4000)  
    )  
AS  
SELECT {fn OCTET_LENGTH( @string_exp )};  
```  
  
### <a name="b-using-an-odbc-function-in-a-user-defined-function"></a>B. Usando uma função ODBC em uma função definida pelo usuário  
 O seguinte exemplo usa uma função ODBC em uma função definida pelo usuário:  
  
```  
CREATE FUNCTION dbo.ODBCudf  
    (  
    @string_exp nvarchar(4000)  
    )  
RETURNS int  
AS  
BEGIN  
DECLARE @len int  
SET @len = (SELECT {fn OCTET_LENGTH( @string_exp )})  
RETURN(@len)  
END ;  
  
SELECT dbo.ODBCudf('Returns the length.');  
--Returns 38  
  
```  
  
### <a name="c-using-an-odbc-functions-in-select-statements"></a>C. Usando funções ODBC em instruções SELECT  
 As seguintes instruções SELECT usam funções ODBC:  
  
```  
DECLARE @string_exp nvarchar(4000) = 'Returns the length.';  
SELECT {fn BIT_LENGTH( @string_exp )};  
-- Returns 304  
SELECT {fn OCTET_LENGTH( @string_exp )};  
-- Returns 38  
  
SELECT {fn CONCAT( 'CONCAT ','returns a character string')};  
-- Returns CONCAT returns a character string  
SELECT {fn TRUNCATE( 100.123456, 4)};  
-- Returns 100.123400  
SELECT {fn CURRENT_DATE( )};  
-- Returns 2007-04-20  
SELECT {fn CURRENT_TIME(6)};  
-- Returns 10:27:11.973000  
  
DECLARE @date_exp nvarchar(30) = '2007-04-21 01:01:01.1234567';  
SELECT {fn DAYNAME( @date_exp )};  
-- Returns Saturday  
SELECT {fn DAYOFMONTH( @date_exp )};  
-- Returns 21  
SELECT {fn DAYOFWEEK( @date_exp )};  
-- Returns 7  
SELECT {fn HOUR( @date_exp)};  
-- Returns 1   
SELECT {fn MINUTE( @date_exp )};  
-- Returns 1  
SELECT {fn SECOND( @date_exp )};  
-- Returns 1  
SELECT {fn MONTHNAME( @date_exp )};  
-- Returns April  
SELECT {fn QUARTER( @date_exp )};  
-- Returns 2  
SELECT {fn WEEK( @date_exp )};  
-- Returns 16  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Exemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="d-using-an-odbc-function-in-a-stored-procedure"></a>D. Usando uma função ODBC em um procedimento armazenado  
 O seguinte exemplo usa uma função ODBC em um procedimento armazenado:  
  
```  
CREATE PROCEDURE dbo.ODBCprocedure  
    (  
    @string_exp nvarchar(4000)  
    )  
AS  
SELECT {fn BIT_LENGTH( @string_exp )};  
```  
  
### <a name="e-using-an-odbc-function-in-a-user-defined-function"></a>E. Usando uma função ODBC em uma função definida pelo usuário  
 O seguinte exemplo usa uma função ODBC em uma função definida pelo usuário:  
  
```  
CREATE FUNCTION dbo.ODBCudf  
    (  
    @string_exp nvarchar(4000)  
    )  
RETURNS int  
AS  
BEGIN  
DECLARE @len int  
SET @len = (SELECT {fn BIT_LENGTH( @string_exp )})  
RETURN(@len)  
END ;  
  
SELECT dbo.ODBCudf('Returns the length in bits.');  
--Returns 432  
  
```  
  
### <a name="f-using-an-odbc-functions-in-select-statements"></a>F. Usando funções ODBC em instruções SELECT  
 As seguintes instruções SELECT usam funções ODBC:  
  
```  
DECLARE @string_exp nvarchar(4000) = 'Returns the length.';  
SELECT {fn BIT_LENGTH( @string_exp )};  
-- Returns 304  
  
SELECT {fn CONCAT( 'CONCAT ','returns a character string')};  
-- Returns CONCAT returns a character string  
SELECT {fn CURRENT_DATE( )};  
-- Returns todays date  
SELECT {fn CURRENT_TIME(6)};  
-- Returns the time  
  
DECLARE @date_exp nvarchar(30) = '2007-04-21 01:01:01.1234567';  
SELECT {fn DAYNAME( @date_exp )};  
-- Returns Saturday  
SELECT {fn DAYOFMONTH( @date_exp )};  
-- Returns 21  
SELECT {fn DAYOFWEEK( @date_exp )};  
-- Returns 7  
SELECT {fn HOUR( @date_exp)};  
-- Returns 1   
SELECT {fn MINUTE( @date_exp )};  
-- Returns 1  
SELECT {fn SECOND( @date_exp )};  
-- Returns 1  
SELECT {fn MONTHNAME( @date_exp )};  
-- Returns April  
SELECT {fn QUARTER( @date_exp )};  
-- Returns 2  
SELECT {fn WEEK( @date_exp )};  
-- Returns 16  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Funções internas &#40;Transact-SQL&#41;](~/t-sql/functions/functions.md)  
  
  



