---
title: DATENAME (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/29/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
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
author: MashaMSFT
ms.author: mathoma
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: e430a8b3555fe42377950d5176e63e7d487ff277
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47609164"
---
# <a name="datename-transact-sql"></a>DATENAME (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Esta função retorna uma cadeia de caracteres que representa o *datepart* especificado do argumento *date* especificado.

Consulte [Tipos de dados e funções de data e hora &#40;Transact-SQL&#41;](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md) para obter uma visão geral de todos os tipos de dados e funções de data e hora do [!INCLUDE[tsql](../../includes/tsql-md.md)].
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
  
```sql
DATENAME ( datepart , date )  
```  
  
## <a name="arguments"></a>Argumentos  
*datepart*  
A parte específica do argumento *date* que `DATENAME` retornará. Esta tabela lista todos os argumentos *datepart* válidos.

> [!NOTE]
> `DATENAME` não aceita os equivalentes de variável definidos pelo usuário para os argumentos *datepart*.
  
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

Uma expressão que pode ser resolvida para um dos seguintes tipos de dados: 

+ **date**
+ **datetime**
+ **datetimeoffset**
+ **datetime2** 
+ **smalldatetime**
+ **time**

Para *date*, `DATENAME` aceitará uma variável de expressão de coluna, de expressão, de literal de cadeia de caracteres ou definida pelo usuário. Para evitar ambiguidade, use anos de quatro dígitos. Consulte [Configurar a opção two digit year cutoff de configuração de servidor](../../database-engine/configure-windows/configure-the-two-digit-year-cutoff-server-configuration-option.md) para obter informações sobre anos de dois dígitos.
  
## <a name="return-type"></a>Tipo de retorno  
**nvarchar**
  
## <a name="return-value"></a>Valor retornado  
  
-   Cada *datepart* retorna o mesmo valor das abreviações dela.  
  
O valor retornado depende do ambiente de idioma definido por meio da instrução [SET LANGUAGE](../../t-sql/statements/set-language-transact-sql.md) e por [Configurar a opção de configuração do servidor de idioma padrão](../../database-engine/configure-windows/configure-the-default-language-server-configuration-option.md) do logon. O valor retornado depende de [SET DATEFORMAT](../../t-sql/statements/set-dateformat-transact-sql.md) se *date* é uma literal de cadeia de caracteres de alguns formatos. SET DATEFORMAT não altera o valor retornado quando a data é uma expressão de coluna de um tipo de dados de data ou de hora.
  
Quando o parâmetro *date* tem um argumento de tipo de dados **date**, o valor retornado depende da configuração especificada por [SET DATEFIRST](../../t-sql/statements/set-datefirst-transact-sql.md).
  
## <a name="tzoffset-datepart-argument"></a>Argumento datepart TZoffset  
Se o argumento *datepart* é **TZoffset** (**tz**) e o argumento *data* não tem nenhum deslocamento de fuso horário, `DATEADD` retorna 0.
  
## <a name="smalldatetime-date-argument"></a>Argumento smalldatetime de date  
Quando *date* é [smalldatetime](../../t-sql/data-types/smalldatetime-transact-sql.md), `DATENAME` retorna os segundos como 00.
  
## <a name="default-returned-for-a-datepart-that-is-not-in-the-date-argument"></a>Padrão retornado para um datepart que não está no argumento de data  
Se o tipo de dados do argumento *date* não tiver a *datepart* especificada, `DATENAME` retornará o padrão para essa *datepart* apenas quando o argumento *date* tiver um literal.
  
Por exemplo, o ano-mês-dia padrão para qualquer tipo de dados de **date** é 1900-01-01. Esta instrução tem argumentos de parte de data para *datepart*, um argumento de hora para *date* e `DATENAME` retorna `1900, January, 1, 1, Monday`.
  
```sql
SELECT DATENAME(year, '12:10:30.123')  
    ,DATENAME(month, '12:10:30.123')  
    ,DATENAME(day, '12:10:30.123')  
    ,DATENAME(dayofyear, '12:10:30.123')  
    ,DATENAME(weekday, '12:10:30.123');  
```  
  
Se *date* é especificada como uma variável ou coluna de tabela e o tipo de dados dessa variável ou coluna não tem a *datepart* especificada, `DATENAME` retorna o erro 9810. Neste exemplo, a variável *@t* tem um tipo de dados **time**. O exemplo falha porque o ano da parte de data é inválido para o tipo de dados **time**:
  
```sql
DECLARE @t time = '12:10:30.123';   
SELECT DATENAME(year, @t);  
```  
  
## <a name="remarks"></a>Remarks  

Use `DATENAME` nas seguintes cláusulas:

+ GROUP BY
+ HAVING
+ ORDER BY
+ SELECT \<list>
+ WHERE
  
No [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], DATENAME converte implicitamente literais de cadeia de caracteres como um tipo **datetime2**. Em outras palavras, `DATENAME` não é compatível com o formato YDM quando a data é transmitida como uma cadeia de caracteres. É necessário converter explicitamente a cadeia de caracteres em um tipo de **datetime** ou **smalldatetime** para usar o formato YDM.
  
## <a name="examples"></a>Exemplos  
Este exemplo retorna as partes da data especificada. Substitua um valor *datepart* da tabela para o argumento `datepart` na instrução SELECT:
  
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

Este exemplo retorna as partes da data especificada. Substitua um valor *datepart* da tabela para o argumento `datepart` na instrução SELECT:
  
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
  
  

