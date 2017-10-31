---
title: DATENAME (Transact-SQL) | Microsoft Docs
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
- DATENAME_TSQL
- DATENAME
dev_langs:
- TSQL
helpviewer_keywords:
- dates [SQL Server], functions
- DATENAME function [SQL Server
- functions [SQL Server], time
- functions [SQL Server], date and time
- dateparts [SQL Server], datename
- date and time [SQL Server], DATENAME
- comparing dates times [SQL Server]
- dates [SQL Server], dateparts
ms.assetid: 11855b56-c554-495d-aad4-ba446990153b
caps.latest.revision: 59
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 2d41bbf5a83f0dee8518ece6f074181b8412bad8
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="datename-transact-sql"></a>DATENAME (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Retorna uma cadeia de caracteres que representa a *datepart* especificada *data*
  
Para obter uma visão geral de todos os [!INCLUDE[tsql](../../includes/tsql-md.md)] tipos de dados de data e hora e funções, consulte [data e hora tipos de dados e funções &#40; Transact-SQL &#41; ](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md).
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
  
```sql
DATENAME ( datepart , date )  
```  
  
## <a name="arguments"></a>Argumentos  
*datepart*  
É a parte do *data* para retornar. A seguinte tabela lista válida *datepart* argumentos. Equivalentes de variável definidos pelo usuário não são válidos.
  
|*datepart*|Abreviações|  
|---|---|
|**ano**|**AA, AAAA**|  
|**trimestre**|**tq, t**|  
|**mês**|**mm, m**|  
|**DAYOFYEAR**|**dy, y**|  
|**dia**|**dd, d**|  
|**semana**|**sem, ww**|  
|**dia da semana**|**data warehouse, w**|  
|**hora**|**hh**|  
|**minuto**|**min, n**|  
|**segundo**|**SS, s**|  
|**milissegundos**|**MS**|  
|**microssegundos**|**MCS**|  
|**nanossegundos**|**NS**|  
|**TZoffset**|**TZ**|  
|**ISO_WEEK**|**ISOWK, ISOWW**|  
  
*date*  
É uma expressão que pode ser resolvida para um **tempo**, **data**, **smalldatetime**, **datetime**, **datetime2**, ou **datetimeoffset** valor. *data* pode ser uma expressão, a expressão de coluna, a variável definida pelo usuário ou a cadeia de caracteres literal.  
Para evitar ambiguidade, use anos de quatro dígitos. Para obter informações sobre anos de dois dígitos, consulte [configurar o ano de dois dígitos corte opção de configuração de servidor](../../database-engine/configure-windows/configure-the-two-digit-year-cutoff-server-configuration-option.md).
  
## <a name="return-type"></a>Tipo de retorno  
**nvarchar**
  
## <a name="return-value"></a>Valor de retorno  
  
-   Cada *datepart* e suas abreviações retornam o mesmo valor.  
  
O valor de retorno depende do ambiente de idioma definido por meio de [SET LANGUAGE](../../t-sql/statements/set-language-transact-sql.md) e o [configurar o idioma padrão da opção de configuração de servidor](../../database-engine/configure-windows/configure-the-default-language-server-configuration-option.md) do logon. O valor de retorno é dependente no [SET DATEFORMAT](../../t-sql/statements/set-dateformat-transact-sql.md) se *data* é uma cadeia de caracteres literal de alguns formatos. SET DATEFORMAT não afeta o valor de retorno quando a data é uma expressão de coluna de um tipo de dados de data de hora.
  
Quando o *data* parâmetro tem um **data** argumento de tipo de dados, o valor de retorno depende da configuração especificada pelo usando [SET DATEFIRST](../../t-sql/statements/set-datefirst-transact-sql.md).
  
## <a name="tzoffset-datepart-argument"></a>Argumento datepart TZoffset  
Se *datepart* argumento é **TZoffset** (**tz**) e o *data* argumento não tiver nenhum deslocamento de fuso horário, será retornado 0.
  
## <a name="smalldatetime-date-argument"></a>Argumento de data smalldatetime  
Quando *data* é [smalldatetime](../../t-sql/data-types/smalldatetime-transact-sql.md), segundos serão retornados como 00.
  
## <a name="default-returned-for-a-datepart-that-is-not-in-the-date-argument"></a>Padrão retornado para um datepart que não está no argumento de data  
Se o tipo de dados de *data* argumento não tiver especificado *datepart*, o padrão para que *datepart* será retornado somente quando um literal é especificado para *data*.
  
Por exemplo, o padrão ano-mês-dia para qualquer **data** tipo de dados é 1900-01-01. A instrução a seguir tem argumentos de parte de data para *datepart*, um argumento de tempo para *data*e retorna `1900, January, 1, 1, Monday`.
  
```sql
SELECT DATENAME(year, '12:10:30.123')  
    ,DATENAME(month, '12:10:30.123')  
    ,DATENAME(day, '12:10:30.123')  
    ,DATENAME(dayofyear, '12:10:30.123')  
    ,DATENAME(weekday, '12:10:30.123');  
```  
  
Se *data* é especificado como uma variável ou coluna de tabela e os dados de tipo para que variável ou coluna não tiver especificado *datepart*, erro 9810 é retornado. O código a seguir exemplo falhará porque a parte de ano da data não é válida para o **tempo** tipo de dados que é declarado para a variável  *@t* .
  
```sql
DECLARE @t time = '12:10:30.123';   
SELECT DATENAME(year, @t);  
```  
  
## <a name="remarks"></a>Comentários  
DATENAME pode ser usado na lista de seleção, cláusulas WHERE, HAVING, GROUP BY e ORDER BY.
  
Em [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], DATENAME converte implicitamente literais de cadeia de caracteres como um **datetime2** tipo. Isso significa que DATENAME não oferece suporte ao formato YDM quando a data é transmitida como cadeia de caracteres. É necessário converter explicitamente a cadeia de caracteres para um **datetime** ou **smalldatetime** tipo para usar o formato YDM.
  
## <a name="examples"></a>Exemplos  
O exemplo a seguir retorna as partes de data da data especificada.
  
`SELECT DATENAME(datepart,'2007-10-30 12:15:32.1234567 +05:10');`
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
|*datepart*|Valor de retorno|  
|---|---|
|**ano, dd, AA**|2007|  
|**trimestre, tq, t**|4|  
|**mês, mm, m**|Outubro|  
|**DAYOFYEAR, dy, y**|303|  
|**dia, dd, d**|30|  
|**semana, wk, ww**|44|  
|**dia da semana, dw**|Terça-feira|  
|**hora, hh**|12|  
|**minuto, n**|15|  
|**segundo, ss, s**|32|  
|**milissegundo, ms**|123|  
|**microssegundos, mcs**|123456|  
|**nanossegundos, ns**|123456700|  
|**TZoffset, tz**|310|  
|**ISO_WEEK, ISOWK, ISOWW**|44|  
  
[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]e[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]

O exemplo a seguir retorna as partes de data da data especificada.
  
```sql
SELECT DATENAME(datepart,'2007-10-30 12:15:32.1234567 +05:10');  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
|*datepart*|Valor de retorno|  
|---|---|
|**ano, dd, AA**|2007|  
|**trimestre, tq, t**|4|  
|**mês, mm, m**|Outubro|  
|**DAYOFYEAR, dy, y**|303|  
|**dia, dd, d**|30|  
|**semana, wk, ww**|44|  
|**dia da semana, dw**|Terça-feira|  
|**hora, hh**|12|  
|**minuto, n**|15|  
|**segundo, ss, s**|32|  
|**milissegundo, ms**|123|  
|**microssegundos, mcs**|123456|  
|**nanossegundos, ns**|123456700|  
|**TZoffset, tz**|310|  
|**ISO_WEEK, ISOWK, ISOWW**|44|  
  
## <a name="see-also"></a>Consulte também
[CAST e CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)
  
  


