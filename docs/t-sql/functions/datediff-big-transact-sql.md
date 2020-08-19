---
description: DATEDIFF_BIG (Transact-SQL)
title: DATEDIFF_BIG (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/18/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DATEDIFF_BIG
- DATEDIFF_BIG_TSQL
helpviewer_keywords:
- DATEDIFF_BIG function [SQL Server]
- dates [SQL Server]. functions
- date and time [SQL Server], DATEDIFF_BIG
- functions [SQL Server], time
- functions [SQL Server], date and time
- time [SQL Server], functions
ms.assetid: 19ac1693-3cfa-400d-bf83-20a9cb46599a
author: markingmyname
ms.author: maghan
ms.openlocfilehash: a50a1fe5872afad4df5f7e8811c3babd139ce354
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88445843"
---
# <a name="datediff_big-transact-sql"></a>DATEDIFF_BIG (Transact-SQL)
[!INCLUDE [sqlserver2016-asdb-asdbmi-asa](../../includes/applies-to-version/sqlserver2016-asdb-asdbmi-asa.md)]

Essa função retorna a contagem (como um grande valor inteiro com sinal) dos limites de *datepart* especificados cruzados entre os parâmetros especificados *startdate* e *enddate*.
  
Consulte [Tipos de dados e funções de data e hora &#40;Transact-SQL&#41;](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md) para obter uma visão geral de todos os tipos de dados e funções de data e hora do [!INCLUDE[tsql](../../includes/tsql-md.md)].
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
  
```
DATEDIFF_BIG ( datepart , startdate , enddate )  
```  

## <a name="arguments"></a>Argumentos
*datepart*  
A parte de *startdate* e de *enddate* que especifica o tipo de limite ultrapassado.

> [!NOTE]
> `DATEDIFF_BIG` não aceitará valores de *datepart* de variáveis definidas pelo usuário ou como cadeias de caracteres entre aspas.

Esta tabela lista todos os nomes e abreviações de argumentos *datepart* válidos.
  
|Nome do *datepart*| Abreviação do *datepart*|  
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

> [!NOTE]
> Cada nome e abreviação de *datepart* específico para esse nome de *datepart* retornará um mesmo valor.

*startdate*  
Uma expressão que pode resolver um dos seguintes valores:

+ **date**
+ **datetime**
+ **datetimeoffset**
+ **datetime2** 
+ **smalldatetime**
+ **time**

Para *date*, `DATEDIFF_BIG` aceitará uma variável de expressão de coluna, de expressão, de literal de cadeia de caracteres ou definida pelo usuário. Um valor literal de cadeia de caracteres deve resolver um **datetime**. Para evitar ambiguidade, use anos de quatro dígitos. `DATEDIFF_BIG` subtrai *startdate* de *enddate*. Para evitar ambiguidade, use anos de quatro dígitos. Consulte [Configurar a opção two digit year cutoff de configuração de servidor](../../database-engine/configure-windows/configure-the-two-digit-year-cutoff-server-configuration-option.md) para obter informações sobre anos de dois dígitos.
  
*enddate*  
Consulte *startdate*.
  
## <a name="return-type"></a>Tipo de retorno  
**bigint** com sinal  
  
## <a name="return-value"></a>Valor retornado  
Retorna a diferença **bigint** entre *startdate* e *enddate* expressa no coundary definido por *datepart*.
  
Para um valor retornado fora do intervalo para **bigint** (-9.223.372.036.854.775.808 a 9.223.372.036.854.775.807), `DATEDIFF_BIG` retorna um erro. Diferentemente de `DATEDIFF`, que retorna um **int** e, portanto, pode estourar com uma precisão de **minuto** ou superior, `DATEDIFF_BIG` só poderá estourar se estiver usando uma precisão de **nanossegundos**, em que a diferença entre *enddate* e *startdate* é superior a 292 anos, 3 meses, 10 dias, 23 horas, 47 minutos e 16,8547758 segundos.
  
Se *startdate* e *enddate* receberem apenas um valor temporal e *datepart* não for um *datepart* de hora, `DATEDIFF_BIG` retornará 0.
  
`DATEDIFF_BIG` não usa um componente de deslocamento de fuso horário de *startdate* ou *enddate* para calcular o valor retornado.
  
Para um valor **smalldatetime** usado para *startdate* ou para *enddate*, `DATEDIFF_BIG` sempre define segundos e milissegundos como 0 no valor retornado, porque [smalldatetime](../../t-sql/data-types/smalldatetime-transact-sql.md) tem apenas a precisão do minuto.
  
Se apenas um valor temporal for atribuído a uma variável de tipo de dados de data, `DATEDIFF_BIG` definirá o valor da parte de data ausente como o valor padrão: `1900-01-01`. Se apenas um valor de data for atribuído a uma variável de um tipo de dados de data ou hora, `DATEDIFF_BIG` definirá o valor da parte de hora ausente como o valor padrão: `00:00:00`. Se *startdate* ou *enddate* tiver apenas uma parte de hora e a outra apenas uma parte de data, `DATEDIFF_BIG` definirá as partes de hora e data ausentes como os valores padrão.
  
Se *startdate* e *enddate* tiverem diferentes tipos de dados de data e um tiver mais partes de hora ou precisão de segundos fracionários do que o outro, `DATEDIFF_BIG` definirá as partes ausentes do outro como 0.
  
## <a name="datepart-boundaries"></a>Limites de datepart
As instruções a seguir têm os mesmos valores de *startdate* e de *enddate*. Essas datas são adjacentes e diferem no tempo em um microssegundo (0,0000001 segundo). A diferença entre *startdate* e *enddate* em cada instrução cruza um calendário ou limite de hora de sua *datepart*. Cada instrução retorna 1. Se *startdate* e *enddate* tiverem diferentes valores de ano, mas os mesmos valores de semana do calendário, `DATEDIFF_BIG` retornará 0 para *datepart* **week**.

```sql
SELECT DATEDIFF_BIG(year,        '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF_BIG(quarter,     '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF_BIG(month,       '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF_BIG(dayofyear,   '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF_BIG(day,         '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF_BIG(week,        '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF_BIG(hour,        '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF_BIG(minute,      '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF_BIG(second,      '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF_BIG(millisecond, '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
```
  
## <a name="remarks"></a>Comentários  
Use `DATEDIFF_BIG` nas cláusulas `SELECT <list>`, `WHERE`, `HAVING`, `GROUP BY` e `ORDER BY`.
  
`DATEDIFF_BIG` converte implicitamente literais de cadeias de caracteres como um tipo **datetime2**. Isso significa que `DATEDIFF_BIG` não é compatível com o formato YDM quando a data é transmitida como cadeia de caracteres. É necessário converter explicitamente a cadeia de caracteres em um tipo de **datetime** ou **smalldatetime** para usar o formato YDM.
  
Especificar `SET DATEFIRST` não tem efeito sobre `DATEDIFF_BIG`. `DATEDIFF_BIG` sempre usa domingo como o primeiro dia da semana para garantir que a função opere de maneira determinística.

`DATEDIFF_BIG` poderá estourar com uma precisão de **nanossegundos** se a diferença entre *enddate* e *startdate* retornar um valor fora do intervalo para **bigint**.
  
## <a name="examples"></a>Exemplos 
  
### <a name="specifying-columns-for-startdate-and-enddate"></a>Especificando colunas para startdate e enddate  
Este exemplos usa diferentes tipos de expressões como argumentos para os parâmetros *startdate* e *enddate*. Ele calcula o número de limites de dia cruzados entre datas em duas colunas de uma tabela.
  
```sql
CREATE TABLE dbo.Duration  
    (startDate datetime2, endDate datetime2);  
    
INSERT INTO dbo.Duration(startDate,endDate)  
    VALUES('2007-05-06 12:10:09', '2007-05-07 12:10:09');  
    
SELECT DATEDIFF_BIG(day, startDate, endDate) AS 'Duration'  
    FROM dbo.Duration;  
-- Returns: 1  
```  

### <a name="finding-difference-between-startdate-and-enddate-as-date-parts-strings"></a>Localizando a diferença entre startdate e enddate como cadeias de caracteres de partes de data

```sql
DECLARE @date1 DATETIME2, @date2 DATETIME2, @result VARCHAR(100)
DECLARE @years BIGINT, @months BIGINT, @days BIGINT, @hours BIGINT, @minutes BIGINT, @seconds BIGINT, @milliseconds BIGINT

SET @date1 = '0001-01-01 00:00:00.00000000'
SET @date2 = '2018-12-12 07:08:01.12345678'

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
2017 years, 11 months, 11 days, 7 hours, 8 minutes and 1.123 seconds
```   

Veja de perto exemplos relacionados em [DATEDIFF &#40;Transact-SQL&#41;](../../t-sql/functions/datediff-transact-sql.md).
  
## <a name="see-also"></a>Confira também
[CAST e CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[DATEDIFF &#40;Transact-SQL&#41;](../../t-sql/functions/datediff-transact-sql.md)
  
  
