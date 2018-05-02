---
title: DATEPART (Transact-SQL) | Microsoft Docs
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
- DATEPART_TSQL
- DATEPART
dev_langs:
- TSQL
helpviewer_keywords:
- dates [SQL Server], functions
- date and time [SQL Server], DATEPART
- dateparts [SQL Server]
- functions [SQL Server], time
- functions [SQL Server], date and time
- time [SQL Server], functions
- dateparts [SQL Server], datepart
- comparing dates times [SQL Server]
- DATEPART function [SQL Server]
- dates [SQL Server], dateparts
ms.assetid: 15f1a5bc-4c0c-4c48-848d-8ec03473e6c1
caps.latest.revision: 57
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: af3b28322a1d0080202cfc42c3381f8d82d0f535
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="datepart-transact-sql"></a>DATEPART (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Retorna um inteiro que representa a *datepart* especificada da *date* informada.
  
Para obter uma visão geral das funções e dos tipos de dados de data e hora de [!INCLUDE[tsql](../../includes/tsql-md.md)], confira [Funções e tipos de dados de data e hora &#40;Transact-SQL&#41;](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md).
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
  
```sql
DATEPART ( datepart , date )  
```  
  
## <a name="arguments"></a>Argumentos  
*datepart*  
É a parte de *date* (um valor de data ou hora) para a qual será retornado um **inteiro**. A tabela a seguir lista todos os argumentos válidos de *datepart*. Equivalentes de variável definidos pelo usuário não são válidos.
  
|*datepart*|Abreviações|  
|---|---|
|**year**|**yy**, **yyyy**|  
|**quarter**|**qq**, **q**|  
|**month**|**mm**, **m**|  
|**dayofyear**|**dy**, **y**|  
|**day**|**dd**, **d**|  
|**week**|**wk**, **ww**|  
|**weekday**|**dw**|  
|**hour**|**hh**|  
|**minute**|**mi, n**|  
|**second**|**ss**, **s**|  
|**millisecond**|**ms**|  
|**microsecond**|**mcs**|  
|**nanosecond**|**ns**|  
|**TZoffset**|**tz**|  
|**ISO_WEEK**|**isowk**, **isoww**|  
  
*date*  
É uma expressão que pode ser resolvida em um valor de **time**, **date**, **smalldatetime**, **datetime**, **datetime2** ou **datetimeoffset**. *date* pode ser uma expressão, uma expressão de coluna, uma variável definida pelo usuário ou uma cadeia de caracteres literal.  
Para evitar ambiguidade, use anos de quatro dígitos. Para obter mais informações sobre anos de dois dígitos, confira [Configurar a opção Corte de Ano de Dois Dígitos do servidor](../../database-engine/configure-windows/configure-the-two-digit-year-cutoff-server-configuration-option.md).
  
## <a name="return-type"></a>Tipo de retorno  
 **int**  
  
## <a name="return-value"></a>Valor retornado  
Cada *datepart* retorna o mesmo valor das abreviações dela.
  
O valor retornado depende do ambiente de idioma definido por meio da instrução [SET LANGUAGE](../../t-sql/statements/set-language-transact-sql.md) e da etapa [Configurar Idioma Padrão do servidor](../../database-engine/configure-windows/configure-the-default-language-server-configuration-option.md) do logon. Se *date* for uma cadeia de caracteres literal para alguns formatos, o valor retornado dependerá do formato especificado por meio de [SET DATEFORMAT](../../t-sql/statements/set-dateformat-transact-sql.md). SET DATEFORMAT não afeta o valor retornado quando a data é uma expressão de coluna de um tipo de dados de data de hora.
  
A tabela a seguir lista todos os argumentos de *datepart* com valores retornados correspondentes para a instrução `SELECT DATEPART(datepart,'2007-10-30 12:15:32.1234567 +05:10')`. O tipo de dados do argumento de *date* é **datetimeoffset(7)**. O valor retornado de **nanosecond***datepart* tem uma escala de 9 (0,123456700) e as últimas duas posições sempre são 00.
  
|*datepart*|Valor retornado|  
|---|---|
|**year, yyyy, yy**|2007|  
|**quarter, qq, q**|4|  
|**month, mm, m**|10|  
|**dayofyear, dy, y**|303|  
|**day, dd, d**|30|  
|**week, wk, ww**|45|  
|**weekday, dw**|1|  
|**hour, hh**|12|  
|**minute, n**|15|  
|**second, ss, s**|32|  
|**millisecond, ms**|123|  
|**microsecond, mcs**|123456|  
|**nanosecond, ns**|123456700|  
|**TZoffset, tz**|310|  
  
## <a name="week-and-weekday-datepart-arguments"></a>Argumentos week e weekday de datepart
Quando *datepart* é **week** (**wk**, **ww**) ou **weekday** (**dw**), o valor retornado depende do valor definido usando [SET DATEFIRST](../../t-sql/statements/set-datefirst-transact-sql.md).
  
O dia 1º de janeiro de qualquer ano define o número inicial de **week***datepart*, por exemplo: DATEPART (** wk**, 'Jan 1, *xxx*x') = 1, em que *xxxx* é qualquer ano.
  
A tabela a seguir lista o valor retornado por **week** e **weekday***datepart* para '2007-04-21', para cada argumento SET DATEFIRST. 1º de janeiro foi uma segunda-feira em 2007. 21 de abril foi um sábado em 2007. SET DATEFIRST 7, domingo, é o padrão para inglês norte-americano.
  
|SET DATEFIRST<br /><br /> argumento|week<br /><br /> retornado|weekday<br /><br /> retornado|  
|---|---|---|
|1|16|6|  
|2|17|5|  
|3|17|4|  
|4|17|3|  
|5|17|2|  
|6|17|1|  
|7|16|7|  
  
## <a name="year-month-and-day-datepart-arguments"></a>Argumentos year, month e day de datepart  
Os valores retornados para DATEPART (**year**, *date*), DATEPART (**month**, *date*) e DATEPART (**day**, *date*) são iguais aos retornados pelas funções [YEAR](../../t-sql/functions/year-transact-sql.md), [MONTH](../../t-sql/functions/month-transact-sql.md) e [DAY](../../t-sql/functions/day-transact-sql.md), respectivamente.
  
## <a name="isoweek-datepart"></a>Datepart ISO_WEEK  
O ISO 8601 inclui o sistema de data de semana ISO, um sistema de numeração para semanas. Cada semana está associada ao ano em que ocorre a quinta-feira. Por exemplo, a semana 1 de 2004 (2004W01) vai da segunda-feira 29 de dezembro de 2003 ao sábado 4 de janeiro de 2004. O maior número de semana em um ano é 52 ou 53. Esse estilo de numeração costuma ser usado em países/regiões da Europa, mas raramente é usado em outros lugares.
  
O sistema de numeração em países/regiões diferentes pode não estar em conformidade com o padrão ISO. Há pelo menos seis possibilidades, conforme mostrado na tabela a seguir
  
|Primeiro dia da semana|Primeira semana do ano contém|Semanas atribuídas duas vezes|Usado por/em|  
|---|---|---|---|
|Domingo|1º de janeiro,<br /><br /> Primeiro sábado,<br /><br /> 1 a 7 dias do ano|Sim|Estados Unidos|  
|Segunda-feira|1º de janeiro,<br /><br /> Primeiro domingo,<br /><br /> 1 a 7 dias do ano|Sim|A maior parte da Europa e do Reino Unido|  
|Segunda-feira|4 de janeiro,<br /><br /> Primeira quinta-feira,<br /><br /> 4 a 7 dias do ano|não|ISO 8601, Noruega e Suécia|  
|Segunda-feira|7 de janeiro,<br /><br /> Primeira segunda-feira,<br /><br /> 7 dias do ano|não||  
|Quarta-feira|1º de janeiro,<br /><br /> Primeira terça-feira,<br /><br /> 1 a 7 dias do ano|Sim||  
|Sábado|1º de janeiro,<br /><br /> Primeira sexta-feira,<br /><br /> 1 a 7 dias do ano|Sim||  
  
## <a name="tzoffset"></a>TZoffset  
A **TZoffset** (**tz**) é retornada como o número de minutos (com sinal). A instrução a seguir retorna uma diferença de fuso horário de 310 minutos.
  
```sql
SELECT DATEPART (TZoffset, '2007-05-10  00:00:01.1234567 +05:10');  
```  
O valor de TZoffset é renderizado da seguinte maneira:
- Para datetimeoffset e datetime2 e, TZoffset retorna a diferença de tempo em minutos, que é sempre 0 para esse último tipo de dados.
- Para tipos de dados que podem ser convertidos implicitamente em datetimeoffset ou datetime2, com exceção dos outros tipos de dados de data/hora, ela retorna a diferença de tempo em minutos.
- Parâmetros de todos os outros tipos resultam em erro.
  
  
## <a name="smalldatetime-date-argument"></a>Argumento smalldatetime de date  
Quando *date* é [smalldatetime](../../t-sql/data-types/smalldatetime-transact-sql.md), os segundos são retornados como 00.
  
## <a name="default-returned-for-a-datepart-that-is-not-in-a-date-argument"></a>Padrão retornado para um datepart que não está em um argumento de date  
Se o tipo de dados do argumento de *date* não tiver a *datepart* especificada, o padrão dessa *datepart* será retornado apenas quando uma cadeia de caracteres literal for informada para *date*.
  
Por exemplo, o ano-mês-dia padrão para qualquer tipo de dados de **date** é 1900-01-01. A instrução a seguir tem argumentos de parte de data para *datepart*, um argumento de hora para *date* e retorna `1900, 1, 1, 1, 2`.
  
```sql
SELECT DATEPART(year, '12:10:30.123')  
    ,DATEPART(month, '12:10:30.123')  
    ,DATEPART(day, '12:10:30.123')  
    ,DATEPART(dayofyear, '12:10:30.123')  
    ,DATEPART(weekday, '12:10:30.123');  
```  
  
Se *date* é especificada como uma variável ou coluna de tabela e o tipo de dados dessa variável ou coluna não tem uma *datepart*, é retornado o erro 9810. O exemplo de código a seguir apresenta falha porque a parte de data year não é válida para o tipo de dados de **time** declarado para a variável *@t*.
  
```sql
DECLARE @t time = '12:10:30.123';   
SELECT DATEPART(year, @t);  
```  
  
## <a name="fractional-seconds"></a>Frações de segundo
São retornadas frações de segundo, como mostrado nas seguintes instruções:
  
```sql
SELECT DATEPART(millisecond, '00:00:01.1234567'); -- Returns 123  
SELECT DATEPART(microsecond, '00:00:01.1234567'); -- Returns 123456  
SELECT DATEPART(nanosecond,  '00:00:01.1234567'); -- Returns 123456700  
```  
  
## <a name="remarks"></a>Comentários  
É possível usar DATEPART na lista de seleção e nas cláusulas WHERE, HAVING, GROUP BY e ORDER BY.
  
No [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], DATEPART converte implicitamente cadeias de caracteres literais como um tipo de **datetime2**. Isso significa que DATEPART não oferece suporte ao formato YDM quando a data é transmitida como cadeia de caracteres. É necessário converter explicitamente a cadeia de caracteres em um tipo de **datetime** ou **smalldatetime** para usar o formato YDM.
  
## <a name="examples"></a>Exemplos  
O exemplo a seguir retorna o ano base. O ano base é útil para cálculos de data. No exemplo, a data é especificada como um número. Note que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] interpreta 0 como 1º de janeiro de 1900.
  
```sql
SELECT DATEPART(year, 0), DATEPART(month, 0), DATEPART(day, 0);  
-- Returns: 1900    1    1 */  
```  
  
O exemplo a seguir retorna a parte do dia da data `12/20/1974`.
  
```sql
-- Uses AdventureWorks  
  
SELECT TOP(1) DATEPART (day,'12/20/1974') FROM dbo.DimCustomer;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
--------
20
```  
  
O exemplo a seguir retorna a parte do ano da data `12/20/1974`.
  
```sql
-- Uses AdventureWorks  
  
SELECT TOP(1) DATEPART (year,'12/20/1974') FROM dbo.DimCustomer;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
--------
1974
```  
  
## <a name="see-also"></a>Confira também
[CAST e CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)
  
  
