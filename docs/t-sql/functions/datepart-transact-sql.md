---
title: DATEPART (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/29/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
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
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 5bec4347301ed95671b6d5df5b91a5b958bff584
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65945720"
---
# <a name="datepart-transact-sql"></a>DATEPART (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]


Essa função retorna um inteiro que representa o *datepart* especificado do argumento *date* especificado.
  
Consulte [Tipos de dados e funções de data e hora &#40;Transact-SQL&#41;](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md) para obter uma visão geral de todos os tipos de dados e funções de data e hora do [!INCLUDE[tsql](../../includes/tsql-md.md)].
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
  
```sql
DATEPART ( datepart , date )  
```  
  
## <a name="arguments"></a>Argumentos  
*datepart*  
A parte específica do argumento *date* para o qual `DATEPART` retornará um **inteiro**. Esta tabela lista todos os argumentos *datepart* válidos.

> [!NOTE]
> `DATEPART` não aceita os equivalentes de variável definidos pelo usuário para os argumentos *datepart*.
  
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
Uma expressão que é resolvida para um dos seguintes tipos de dados: 

+ **date**
+ **datetime**
+ **datetimeoffset**
+ **datetime2** 
+ **smalldatetime**
+ **time**

Para *date*, `DATEPART` aceitará uma variável de expressão de coluna, de expressão, de literal de cadeia de caracteres ou definida pelo usuário. Para evitar ambiguidade, use anos de quatro dígitos. Consulte [Configurar a opção two digit year cutoff de configuração de servidor](../../database-engine/configure-windows/configure-the-two-digit-year-cutoff-server-configuration-option.md) para obter informações sobre anos de dois dígitos.
  
## <a name="return-type"></a>Tipo de retorno  
 **int**  
  
## <a name="return-value"></a>Valor retornado  
Cada *datepart* retorna o mesmo valor das abreviações dela.
  
O valor retornado depende do ambiente de idioma definido por meio da instrução [SET LANGUAGE](../../t-sql/statements/set-language-transact-sql.md) e por [Configurar a opção de configuração do servidor de idioma padrão](../../database-engine/configure-windows/configure-the-default-language-server-configuration-option.md) do logon. O valor retornado depende de [SET DATEFORMAT](../../t-sql/statements/set-dateformat-transact-sql.md) se *date* é uma literal de cadeia de caracteres de alguns formatos. SET DATEFORMAT não altera o valor retornado quando a data é uma expressão de coluna de um tipo de dados de data ou de hora.
  
Esta tabela lista todos os argumentos *datepart* com valores retornados correspondentes para a instrução `SELECT DATEPART(datepart,'2007-10-30 12:15:32.1234567 +05:10')`. O argumento *date* tem um tipo de dados **datetimeoffset(7)** . As duas últimas posições do valor retornado **nanosecond** *datepart* são sempre `00` e esse valor tem uma escala de 9:

**.123456700**
  
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
Quando *datepart* é **week** (**wk**, **ww**) ou **weekday** (**dw**), o valor retornado `DATEPART` depende do valor definido usando [SET DATEFIRST](../../t-sql/statements/set-datefirst-transact-sql.md).
  
1º de janeiro de qualquer ano define o número inicial para o **week**_datepart_. Por exemplo:

DATEPART (**wk**, 'Jan 1, *xxx*x') = 1

em que *xxxx* é qualquer ano.
  
Esta tabela mostra o valor retornado para **week** e **weekday** *datepart* para

'2007-04-21 '

para cada argumento SET DATEFIRST. 1º de janeiro de 2007 cai em uma segunda-feira. 21 de abril de 2007 cai em um sábado. Para o Inglês (Estados Unidos),

SET DATEFIRST 7 -- ( Sunday )

funciona como o padrão. Depois de definir DATEFIRST, use essa instrução SQL sugerida para os valores da tabela datepart:

`SELECT DATEPART(week, '2007-04-21 '), DATEPART(weekday, '2007-04-21 ')`
  
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
O ISO 8601 inclui o sistema de data de semana ISO, um sistema de numeração para semanas. Cada semana está associada ao ano em que ocorre a quinta-feira. Por exemplo, a semana 1 de 2004 (2004W01) vai da segunda-feira 29 de dezembro de 2003 ao sábado 4 de janeiro de 2004. Países/regiões da Europa normalmente usam esse estilo de numeração. Países/regiões não europeus normalmente não o usam.

Observação: o maior número de semana em um ano pode ser 52 ou 53.
  
Os sistemas de numeração em países/regiões diferentes podem não estar em conformidade com o padrão ISO. Esta tabela mostra seis possibilidades:
  
|Primeiro dia da semana|Primeira semana do ano contém|Semanas atribuídas duas vezes|Usado por/em|  
|---|---|---|---|
|Domingo|1º de janeiro,<br /><br /> Primeiro sábado,<br /><br /> 1 a 7 dias do ano|Sim|Estados Unidos|  
|Segunda-feira|1º de janeiro,<br /><br /> Primeiro domingo,<br /><br /> 1 a 7 dias do ano|Sim|A maior parte da Europa e do Reino Unido|  
|Segunda-feira|4 de janeiro,<br /><br /> Primeira quinta-feira,<br /><br /> 4 a 7 dias do ano|Não|ISO 8601, Noruega e Suécia|  
|Segunda-feira|7 de janeiro,<br /><br /> Primeira segunda-feira,<br /><br /> 7 dias do ano|Não||  
|Quarta-feira|1º de janeiro,<br /><br /> Primeira terça-feira,<br /><br /> 1 a 7 dias do ano|Sim||  
|Sábado|1º de janeiro,<br /><br /> Primeira sexta-feira,<br /><br /> 1 a 7 dias do ano|Sim||  
  
## <a name="tzoffset"></a>TZoffset  
`DATEPART` retorna o valor **TZoffset** (**tz**) como o número de minutos (com sinal). Esta instrução retorna uma diferença de fuso horário de 310 minutos:
  
```sql
SELECT DATEPART (TZoffset, '2007-05-10  00:00:01.1234567 +05:10');  
```  
`DATEPART` renderiza o valor de TZoffset da seguinte maneira:
- Para datetimeoffset e datetime2 e, TZoffset retorna a diferença de tempo em minutos, que é sempre 0 para esse último tipo de dados.
- Para tipos de dados que podem ser convertidos implicitamente em **datetimeoffset** ou **datetime2**, `DATEPART` retorna a diferença de tempo em minutos. Exceção: outros tipos de dados de data/hora.
- Parâmetros de todos os outros tipos resultam em erro.
  
  
## <a name="smalldatetime-date-argument"></a>Argumento smalldatetime de date  
Para um valor [smalldatetime](../../t-sql/data-types/smalldatetime-transact-sql.md) *date*, `DATEPART` retorna os segundos como 00.
  
## <a name="default-returned-for-a-datepart-that-is-not-in-a-date-argument"></a>Padrão retornado para um datepart que não está em um argumento de date  
Se o tipo de dados do argumento *date* não tiver a *datepart* especificada, `DATEPART` retornará o padrão para essa *datepart* apenas quando um literal for especificado para *date*.
  
Por exemplo, o ano-mês-dia padrão para qualquer tipo de dados de **date** é 1900-01-01. Esta instrução tem argumentos de parte de data para *datepart*, um argumento de hora para *date* e ela retorna `1900, 1, 1, 1, 2`.
  
```sql
SELECT DATEPART(year, '12:10:30.123')  
    ,DATEPART(month, '12:10:30.123')  
    ,DATEPART(day, '12:10:30.123')  
    ,DATEPART(dayofyear, '12:10:30.123')  
    ,DATEPART(weekday, '12:10:30.123');  
```  
  
Se *date* é especificada como uma variável ou coluna de tabela e o tipo de dados dessa variável ou coluna não tem a *datepart* especificada, `DATEPART` retorna o erro 9810. Neste exemplo, a variável *@t* tem um tipo de dados **time**. O exemplo falha porque o ano da parte de data é inválido para o tipo de dados **time**:
  
```sql
DECLARE @t time = '12:10:30.123';   
SELECT DATEPART(year, @t);  
```  
  
## <a name="fractional-seconds"></a>Frações de segundo
Estas instruções mostram que `DATEPART` retorna frações de segundos:
  
```sql
SELECT DATEPART(millisecond, '00:00:01.1234567'); -- Returns 123  
SELECT DATEPART(microsecond, '00:00:01.1234567'); -- Returns 123456  
SELECT DATEPART(nanosecond,  '00:00:01.1234567'); -- Returns 123456700  
```  
  
## <a name="remarks"></a>Remarks  
`DATEPART` pode ser usado na lista de seleção e nas cláusulas WHERE, HAVING, GROUP BY e ORDER BY.
  
DATEPART converte implicitamente literais de cadeia de caracteres como um tipo **datetime2** em [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Isso significa que DATENAME não oferece suporte ao formato YDM quando a data é transmitida como cadeia de caracteres. É necessário converter explicitamente a cadeia de caracteres em um tipo de **datetime** ou **smalldatetime** para usar o formato YDM.
  
## <a name="examples"></a>Exemplos  
Este exemplo retorna o ano base. O ano base ajuda com cálculos de data. No exemplo, um número especifica a data. Note que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] interpreta 0 como 1º de janeiro de 1900.
  
```sql
SELECT DATEPART(year, 0), DATEPART(month, 0), DATEPART(day, 0);  
-- Returns: 1900    1    1 */  
```  
  
Este exemplo retorna a parte do dia da data `12/20/1974`.
  
```sql
-- Uses AdventureWorks  
  
SELECT TOP(1) DATEPART (day,'12/20/1974') FROM dbo.DimCustomer;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
--------
20
```  
  
Este exemplo retorna a parte do ano da data `12/20/1974`.
  
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
  
  
