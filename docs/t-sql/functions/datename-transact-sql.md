---
title: DATENAME (Transact-SQL) | Microsoft Docs
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
manager: craigg
ms.workload: Active
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: a8803278c567f01888b7b530885e82e4543c966a
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="datename-transact-sql"></a>DATENAME (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Retorna uma cadeia de caracteres que representa a *datepart* especificada da *date* especificada
  
Para obter uma visão geral das funções e dos tipos de dados de data e hora de [!INCLUDE[tsql](../../includes/tsql-md.md)], confira [Funções e tipos de dados de data e hora &#40;Transact-SQL&#41;](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md).
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
  
```sql
DATENAME ( datepart , date )  
```  
  
## <a name="arguments"></a>Argumentos  
*datepart*  
É a parte da *date* a ser retornada. A tabela a seguir lista todos os argumentos válidos de *datepart*. Equivalentes de variável definidos pelo usuário não são válidos.
  
|*datepart*|Abreviações|  
|---|---|
|**year**|**yy, yyyy**|  
|**quarter**|**qq, q**|  
|**month**|**mm, m**|  
|**dayofyear**|**dy, y**|  
|**day**|**dd, d**|  
|**week**|**wk, ww**|  
|**weekday**|**dw, w**|  
|**hour**|**hh**|  
|**minute**|**mi, n**|  
|**second**|**ss, s**|  
|**millisecond**|**ms**|  
|**microsecond**|**mcs**|  
|**nanosecond**|**ns**|  
|**TZoffset**|**tz**|  
|**ISO_WEEK**|**ISOWK, ISOWW**|  
  
*date*  
É uma expressão que pode ser resolvida em um valor de **time**, **date**, **smalldatetime**, **datetime**, **datetime2** ou **datetimeoffset**. *date* pode ser uma expressão, uma expressão de coluna, uma variável definida pelo usuário ou uma cadeia de caracteres literal.  
Para evitar ambiguidade, use anos de quatro dígitos. Para obter mais informações sobre anos de dois dígitos, consulte [Configurar a opção two digit year cutoff de configuração do servidor](../../database-engine/configure-windows/configure-the-two-digit-year-cutoff-server-configuration-option.md).
  
## <a name="return-type"></a>Tipo de retorno  
**nvarchar**
  
## <a name="return-value"></a>Valor retornado  
  
-   Cada *datepart* retorna o mesmo valor das abreviações dela.  
  
O valor retornado depende do ambiente de idioma definido usando [SET LANGUAGE](../../t-sql/statements/set-language-transact-sql.md) e de [Configurar opção default language de configuração de servidor](../../database-engine/configure-windows/configure-the-default-language-server-configuration-option.md) do logon. O valor retornado depende de [SET DATEFORMAT](../../t-sql/statements/set-dateformat-transact-sql.md) se *date* é uma literal de cadeia de caracteres de alguns formatos. SET DATEFORMAT não afeta o valor retornado quando a data é uma expressão de coluna de um tipo de dados de data de hora.
  
Quando o parâmetro *date* tem um argumento de tipo de dados **date**, o valor retornado depende da configuração especificada com o uso de [SET DATEFIRST](../../t-sql/statements/set-datefirst-transact-sql.md).
  
## <a name="tzoffset-datepart-argument"></a>Argumento datepart TZoffset  
Se o argumento *datepart* é **TZoffset** (**tz**) e o argumento *data* não tem nenhum deslocamento de fuso horário, é retornado 0.
  
## <a name="smalldatetime-date-argument"></a>Argumento smalldatetime de date  
Quando *date* é [smalldatetime](../../t-sql/data-types/smalldatetime-transact-sql.md), os segundos são retornados como 00.
  
## <a name="default-returned-for-a-datepart-that-is-not-in-the-date-argument"></a>Padrão retornado para um datepart que não está no argumento de data  
Se o tipo de dados do argumento de *date* não tiver a *datepart* especificada, o padrão dessa *datepart* será retornado apenas quando uma cadeia de caracteres literal for informada para *date*.
  
Por exemplo, o ano-mês-dia padrão para qualquer tipo de dados de **date** é 1900-01-01. A instrução a seguir tem argumentos de parte de data para *datepart*, um argumento de hora para *date* e retorna `1900, January, 1, 1, Monday`.
  
```sql
SELECT DATENAME(year, '12:10:30.123')  
    ,DATENAME(month, '12:10:30.123')  
    ,DATENAME(day, '12:10:30.123')  
    ,DATENAME(dayofyear, '12:10:30.123')  
    ,DATENAME(weekday, '12:10:30.123');  
```  
  
Se *date* é especificada como uma variável ou coluna de tabela e o tipo de dados dessa variável ou coluna não tem uma *datepart*, é retornado o erro 9810. O exemplo de código a seguir apresenta falha porque a parte de data year não é válida para o tipo de dados de **time** declarado para a variável *@t*.
  
```sql
DECLARE @t time = '12:10:30.123';   
SELECT DATENAME(year, @t);  
```  
  
## <a name="remarks"></a>Remarks  
DATENAME pode ser usado na lista de seleção, cláusulas WHERE, HAVING, GROUP BY e ORDER BY.
  
No [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], DATENAME converte implicitamente literais de cadeia de caracteres como um tipo **datetime2**. Isso significa que DATENAME não oferece suporte ao formato YDM quando a data é transmitida como cadeia de caracteres. É necessário converter explicitamente a cadeia de caracteres em um tipo de **datetime** ou **smalldatetime** para usar o formato YDM.
  
## <a name="examples"></a>Exemplos  
O exemplo a seguir retorna as partes de data da data especificada.
  
`SELECT DATENAME(datepart,'2007-10-30 12:15:32.1234567 +05:10');`
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
|*datepart*|Valor retornado|  
|---|---|
|**year, yyyy, yy**|2007|  
|**quarter, qq, q**|4|  
|**month, mm, m**|Outubro|  
|**dayofyear, dy, y**|303|  
|**day, dd, d**|30|  
|**week, wk, ww**|44|  
|**weekday, dw**|Terça-feira|  
|**hour, hh**|12|  
|**minute, n**|15|  
|**second, ss, s**|32|  
|**millisecond, ms**|123|  
|**microsecond, mcs**|123456|  
|**nanosecond, ns**|123456700|  
|**TZoffset, tz**|310|  
|**ISO_WEEK, ISOWK, ISOWW**|44|  
  
[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]

O exemplo a seguir retorna as partes de data da data especificada.
  
```sql
SELECT DATENAME(datepart,'2007-10-30 12:15:32.1234567 +05:10');  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
|*datepart*|Valor retornado|  
|---|---|
|**year, yyyy, yy**|2007|  
|**quarter, qq, q**|4|  
|**month, mm, m**|Outubro|  
|**dayofyear, dy, y**|303|  
|**day, dd, d**|30|  
|**week, wk, ww**|44|  
|**weekday, dw**|Terça-feira|  
|**hour, hh**|12|  
|**minute, n**|15|  
|**second, ss, s**|32|  
|**millisecond, ms**|123|  
|**microsecond, mcs**|123456|  
|**nanosecond, ns**|123456700|  
|**TZoffset, tz**|310|  
|**ISO_WEEK, ISOWK, ISOWW**|44|  
  
## <a name="see-also"></a>Confira também
[CAST e CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)
  
  

