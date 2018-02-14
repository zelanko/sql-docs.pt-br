---
title: DATEPART (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/29/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 05547f2dd50d7f130438d6a07b6952b8c29ec816
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="datepart-transact-sql"></a>DATEPART (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Retorna um inteiro que representa a *datepart* especificada *data*.
  
Para obter uma visão geral de todos os [!INCLUDE[tsql](../../includes/tsql-md.md)] tipos de dados de data e hora e funções, consulte [data e hora tipos de dados e funções &#40; Transact-SQL &#41; ](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md).
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
  
```sql
DATEPART ( datepart , date )  
```  
  
## <a name="arguments"></a>Argumentos  
*datepart*  
É a parte do *data* (um valor de data ou hora) para o qual um **inteiro** será retornado. A seguinte tabela lista válida *datepart* argumentos. Equivalentes de variável definidos pelo usuário não são válidos.
  
|*datepart*|Abreviações|  
|---|---|
|**ano**|**AA**, **aaaa**|  
|**trimestre**|**tq**, **p**|  
|**mês**|**mm**, **m**|  
|**DAYOFYEAR**|**dy**, **y**|  
|**dia**|**dd**, **d**|  
|**semana**|**wk**, **ww**|  
|**dia da semana**|**dw**|  
|**hora**|**hh**|  
|**minuto**|**min, n**|  
|**segundo**|**SS**, **s**|  
|**milissegundos**|**MS**|  
|**microssegundos**|**MCS**|  
|**nanossegundos**|**NS**|  
|**TZoffset**|**TZ**|  
|**ISO_WEEK**|**isowk**, **isoww**|  
  
*date*  
É uma expressão que pode ser resolvida para um **tempo**, **data**, **smalldatetime**, **datetime**, **datetime2**, ou **datetimeoffset** valor. *data* pode ser uma expressão, a expressão de coluna, a variável definida pelo usuário ou a cadeia de caracteres literal.  
Para evitar ambiguidade, use anos de quatro dígitos. Para obter informações sobre anos de dois dígitos, consulte [configurar o ano de dois dígitos corte opção de configuração de servidor](../../database-engine/configure-windows/configure-the-two-digit-year-cutoff-server-configuration-option.md).
  
## <a name="return-type"></a>Tipo de retorno  
 **int**  
  
## <a name="return-value"></a>Valor de retorno  
Cada *datepart* e suas abreviações retornam o mesmo valor.
  
O valor de retorno depende do ambiente de idioma definido por meio de [SET LANGUAGE](../../t-sql/statements/set-language-transact-sql.md) e o [configurar o idioma padrão da opção de configuração de servidor](../../database-engine/configure-windows/configure-the-default-language-server-configuration-option.md) do logon. Se *data* é uma cadeia de caracteres literal para alguns formatos, o valor de retorno depende do formato especificado usando [SET DATEFORMAT](../../t-sql/statements/set-dateformat-transact-sql.md). SET DATEFORMAT não afeta o valor de retorno quando a data é uma expressão de coluna de um tipo de dados de data de hora.
  
A tabela a seguir lista todos os *datepart* argumentos com correspondente retornam valores para a instrução `SELECT DATEPART(datepart,'2007-10-30 12:15:32.1234567 +05:10')`. O tipo de dados de *data* argumento é **datetimeoffset(7)**. O **nanossegundos***datepart* retornar valor tem uma escala de 9 (. 123456700) e as últimas duas posições sempre são 00.
  
|*datepart*|Valor de retorno|  
|---|---|
|**ano, dd, AA**|2007|  
|**trimestre, tq, t**|4|  
|**mês, mm, m**|10|  
|**DAYOFYEAR, dy, y**|303|  
|**dia, dd, d**|30|  
|**semana, wk, ww**|45|  
|**dia da semana, dw**|1|  
|**hora, hh**|12|  
|**minuto, n**|15|  
|**segundo, ss, s**|32|  
|**milissegundo, ms**|123|  
|**microssegundos, mcs**|123456|  
|**nanossegundos, ns**|123456700|  
|**TZoffset, tz**|310|  
  
## <a name="week-and-weekday-datepart-arguments"></a>Argumentos datepart de Week e weekday
Quando *datepart* é **semana** (**wk**, **ww**) ou **dia da semana** (**dw**), o valor de retorno depende do valor que é definido usando [SET DATEFIRST](../../t-sql/statements/set-datefirst-transact-sql.md).
  
1º de janeiro de qualquer ano define o número inicial de **semana***datepart*, por exemplo: DATEPART (**wk**, ' 1 de janeiro, *xxx*x') = 1, onde *xxxx* é qualquer ano.
  
A tabela a seguir lista o valor de retorno de **semana** e **dia da semana***datepart* para ' 2007-04-21' para cada argumento SET DATEFIRST. O dia 1º de Janeiro é uma segunda-feira no ano de 2007. O dia 21 de abril é um sábado do ano de 2007. SET DATEFIRST 7, domingo, é o padrão para inglês norte-americano.
  
|SET DATEFIRST<br /><br /> argumento|week<br /><br /> retornado|dia útil<br /><br /> retornado|  
|---|---|---|
|1|16|6|  
|2|17|5|  
|3|17|4|  
|4|17|3|  
|5|17|2|  
|6|17|1|  
|7|16|7|  
  
## <a name="year-month-and-day-datepart-arguments"></a>Argumentos datepart de year, month e day  
Os valores que são retornados para DATEPART (**ano**, *data*), DATEPART (**mês**, *data*) e DATEPART (**dia** , *data*) são iguais aos retornados pelas funções [ano](../../t-sql/functions/year-transact-sql.md), [mês](../../t-sql/functions/month-transact-sql.md), e [dia](../../t-sql/functions/day-transact-sql.md), f respectivamente.
  
## <a name="isoweek-datepart"></a>ISO_WEEK datepart  
O ISO 8601 inclui o sistema de data de semana ISO, um sistema de numeração para semanas. Cada semana está associada ao ano em que ocorre a quinta-feira. Por exemplo, a semana 1 de 2004 (2004W01) vai de segunda-feira, 29 de dezembro de 2003 a sábado, 4 de janeiro de 2004. O número de semana mais alto em um ano pode ser 52 ou 53. Esse estilo de numeração é geralmente usado em países/regiões europeus, mas raramente em outro lugar.
  
O sistema de numeração em países/regiões diferentes pode não estar em conformidade com o padrão ISO. Há pelo menos seis possibilidades, conforme mostrado na tabela a seguir
  
|Primeiro dia da semana|Primeira semana do ano contém|Semanas atribuídas duas vezes|Usado por/em|  
|---|---|---|---|
|Domingo|1º de janeiro,<br /><br /> Primeiro sábado,<br /><br /> 1 a 7 dias do ano|Sim|United States|  
|Segunda-feira|1º de janeiro,<br /><br /> Primeiro domingo,<br /><br /> 1 a 7 dias do ano|Sim|A maior parte da Europa e do Reino Unido|  
|Segunda-feira|4 de janeiro,<br /><br /> Primeira quinta-feira,<br /><br /> 4 a 7 dias do ano|Não|ISO 8601, Noruega e Suécia|  
|Segunda-feira|7 de janeiro,<br /><br /> Primeira segunda-feira,<br /><br /> 7 dias do ano|Não||  
|Quarta-feira|1º de janeiro,<br /><br /> Primeira terça-feira,<br /><br /> 1 a 7 dias do ano|Sim||  
|Sábado|1º de janeiro,<br /><br /> Primeira sexta-feira,<br /><br /> 1 a 7 dias do ano|Sim||  
  
## <a name="tzoffset"></a>TZoffset  
O **TZoffset** (**tz**) é retornado como o número de minutos (assinado). A instrução a seguir retorna um deslocamento de fuso horário de 310 minutos.
  
```sql
SELECT DATEPART (TZoffset, '2007-05-10  00:00:01.1234567 +05:10');  
```  
O valor de TZoffset é processado da seguinte maneira:
- Para obter datetime2 e datetimeoffset, TZoffset retorna o deslocamento de tempo em minutos, em que o deslocamento para datetime2 é sempre 0 minutos.
- Para tipos de dados que podem ser convertidos implicitamente em datetimeoffset ou datetime2, com exceção dos outros tipos de dados de data/hora, ele retorna o deslocamento de tempo em minutos.
- Parâmetros de todos os outros tipos resultam em erro.
  
  
## <a name="smalldatetime-date-argument"></a>Argumento de data smalldatetime  
Quando *data* é [smalldatetime](../../t-sql/data-types/smalldatetime-transact-sql.md), segundos serão retornados como 00.
  
## <a name="default-returned-for-a-datepart-that-is-not-in-a-date-argument"></a>Padrão retornado para um datepart que não esteja em um argumento de data  
Se o tipo de dados de *data* argumento não tiver especificado *datepart*, o padrão para que *datepart* será retornado somente quando um literal é especificado para *data*.
  
Por exemplo, o padrão ano-mês-dia para qualquer **data** tipo de dados é 1900-01-01. A instrução a seguir tem argumentos de parte de data para *datepart*, um argumento de tempo para *data*e retorna `1900, 1, 1, 1, 2`.
  
```sql
SELECT DATEPART(year, '12:10:30.123')  
    ,DATEPART(month, '12:10:30.123')  
    ,DATEPART(day, '12:10:30.123')  
    ,DATEPART(dayofyear, '12:10:30.123')  
    ,DATEPART(weekday, '12:10:30.123');  
```  
  
Se *data* é especificado como uma variável ou coluna de tabela e os dados de tipo para que variável ou coluna não tiver especificado *datepart*, erro 9810 é retornado. O código a seguir exemplo falhará porque a parte de ano da data não é válida para o **tempo** tipo de dados que é declarado para a variável  *@t* .
  
```sql
DECLARE @t time = '12:10:30.123';   
SELECT DATEPART(year, @t);  
```  
  
## <a name="fractional-seconds"></a>Frações de segundo
Segundos fracionários são retornados como mostrado nas seguintes instruções:
  
```sql
SELECT DATEPART(millisecond, '00:00:01.1234567'); -- Returns 123  
SELECT DATEPART(microsecond, '00:00:01.1234567'); -- Returns 123456  
SELECT DATEPART(nanosecond,  '00:00:01.1234567'); -- Returns 123456700  
```  
  
## <a name="remarks"></a>Comentários  
DATEPART pode ser usado na lista de seleção, cláusulas WHERE, HAVING, GROUP BY e ORDER BY.
  
Em [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], DATEPART converte implicitamente literais de cadeia de caracteres como um **datetime2** tipo. Isso significa que DATEPART não oferece suporte ao formato YDM quando a data é transmitida como cadeia de caracteres. É necessário converter explicitamente a cadeia de caracteres para um **datetime** ou **smalldatetime** tipo para usar o formato YDM.
  
## <a name="examples"></a>Exemplos  
O exemplo a seguir retorna o ano base: O ano base é útil para cálculos de data. No exemplo, a data é especificada como um número. Observe que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] interpreta 0 como 1º de janeiro de 1900.
  
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
  
## <a name="see-also"></a>Consulte também
[CAST e CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)
  
  

