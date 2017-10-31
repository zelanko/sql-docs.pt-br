---
title: smalldatetime (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 7/22/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- smalldatetime_TSQL
- smalldatetime
dev_langs:
- TSQL
helpviewer_keywords:
- time [SQL Server], data types
- smalldatetime data type [SQL Server]
- dates [SQL Server], data types
- date and time [SQL Server], smalldatetime
- data types [SQL Server], date and time
ms.assetid: 68b74610-d54c-4c8e-b4b2-7e3747546ee0
caps.latest.revision: 50
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 07012d85a54292fa763a7b291d1b7318b6969ca4
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="smalldatetime-transact-sql"></a>smalldatetime (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Define uma data que é combinada com uma hora do dia. A hora se baseia em um dia de 24 horas, com segundos sempre zero (:00) e sem frações de segundo.
  
> [!NOTE]  
>  Use o **tempo**, **data**, **datetime2** e **datetimeoffset** tipos de dados para o novo trabalho. Esses tipos estão de acordo com o SQL padrão. Eles são mais portáteis. **tempo**, **datetime2** e **datetimeoffset** fornecem mais precisão em segundos. **DateTimeOffset** fornece suporte de fuso horário para aplicativos implantados globalmente.  
  
## <a name="smalldatetime-description"></a>smalldatetime descrição
  
|||  
|-|-|  
|Sintaxe|**smalldatetime**|  
|Uso|DECLARAR @MySmalldatetime **smalldatetime**<br /><br /> Criar tabela Table1 (Column1 **smalldatetime** )|  
|Formatos de literais de cadeia de caracteres padrão<br /><br /> (usado para cliente de nível inferior)|Não aplicável|  
|Intervalo de datas|01.01.00 a 06.06.79<br /><br /> 1º de janeiro de 1900 a 6 de junho de 2079|  
|Intervalo de horas|00:00:00 a 23:59:59<br /><br /> 2007-05-09 23:59:59 será arredondado para<br /><br /> 2007-05-10 00:00:00|  
|Intervalos de elementos|AAAA são quatro dígitos, variando de 1900 a 2079 e representando o ano.<br /><br /> MM são dois dígitos, variando de 01 a 12, que representam um mês do ano especificado.<br /><br /> DD são dois dígitos, variando de 01 a 31, dependendo do mês, que representam um dia do mês especificado.<br /><br /> hh são dois dígitos, variando de 00 a 23, que representam a hora.<br /><br /> mm são dois dígitos, variando de 00 a 59, que representam o minuto.<br /><br /> ss são dois dígitos, variando de 00 a 59, que representam o segundo. Valores iguais ou menores que 29,998 segundos têm o minuto arredondado para baixo; valores iguais ou maiores que 29,999 têm o minuto arredondado para cima.|  
|Comprimento de caracteres|máximo de 19 posições|  
|Tamanho de armazenamento|4 bytes, fixo.|  
|Precisão|Um minuto|  
|Valor padrão|1900-01-01 00:00:00|  
|Calendário|Gregoriano<br /><br /> (Não inclui o intervalo completo de anos.)|  
|Precisão de segundo fracionário definida pelo usuário|Não|  
|Preservação e reconhecimento de deslocamento de fuso horário|Não|  
|Reconhecimento de horário de verão|Não|  
  
## <a name="ansi-and-iso-8601-compliance"></a>Conformidade com ANSI e ISO 8601  
**smalldatetime** não for ANSI ou ISO 8601 compatível.
  
## <a name="converting-date-and-time-data"></a>Conversão de dados de data e hora
Ao fazer a conversão em tipos de dados de data e hora, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] rejeita todos os valores que não pode reconhecer como datas ou horas. Para obter informações sobre como usar as funções CAST e CONVERT com dados de data e hora, consulte [CAST e CONVERT & #40; Transact-SQL & #41; ](../../t-sql/functions/cast-and-convert-transact-sql.md).
  
### <a name="converting-smalldatetime-to-other-date-and-time-types"></a>Convertendo smalldatetime em outros tipos de data e hora
Esta seção descreve o que ocorre quando um **smalldatetime** tipo de dados é convertido em outros tipos de dados de data e hora.
  
No caso de conversão para **data**, o ano, mês e dia são copiados. O código a seguir mostra os resultados da conversão de um valor `smalldatetime` em um valor `date`.
  
```sql
DECLARE @smalldatetime smalldatetime = '1955-12-13 12:43:10';  
DECLARE @date date = @smalldatetime  
  
SELECT @smalldatetime AS '@smalldatetime', @date AS 'date';  
  
--Result  
--@smalldatetime          date  
------------------------- ----------  
--1955-12-13 12:43:00     1955-12-13  
--  
--(1 row(s) affected)  
```  
  
Quando a conversão é em **time (n)**, horas, minutos e segundos são copiados. As frações de segundo são definidas como 0. O código a seguir mostra os resultados da conversão de um valor `smalldatetime` em um valor `time(4)`.
  
```sql
DECLARE @smalldatetime smalldatetime = '1955-12-13 12:43:10';  
DECLARE @time time(4) = @smalldatetime;  
  
SELECT @smalldatetime AS '@smalldatetime', @time AS 'time';  
  
--Result  
--@smalldatetime          time  
------------------------- -------------  
--1955-12-13 12:43:00     12:43:00.0000  
--  
--(1 row(s) affected)  
```  
  
Quando a conversão é em **datetime**, o **smalldatetime** valor é copiado para o **datetime** valor. As frações de segundo são definidas como 0. O código a seguir mostra os resultados da conversão de um valor `smalldatetime` em um valor `datetime`.
  
```sql
DECLARE @smalldatetime smalldatetime = '1955-12-13 12:43:10';  
DECLARE @datetime datetime = @smalldatetime;  
  
SELECT @smalldatetime AS '@smalldatetime', @datetime AS 'datetime';  
  
--Result  
--@smalldatetime          datetime  
------------------------- -----------------------  
--1955-12-13 12:43:00     1955-12-13 12:43:00.000  
--  
--(1 row(s) affected)  
```  
  
No caso de conversão para **DateTimeOffset (n)**, o **smalldatetime** valor é copiado para o **DateTimeOffset (n)** valor. Os segundos fracionários são definidos como 0 e o deslocamento de fuso horário é definido como +00:0. O código a seguir mostra os resultados da conversão de um valor `smalldatetime` em um valor `datetimeoffset(4)`.
  
```sql
DECLARE @smalldatetime smalldatetime = '1955-12-13 12:43:10';  
DECLARE @datetimeoffset datetimeoffset(4) = @smalldatetime;  
  
SELECT @smalldatetime AS '@smalldatetime', @datetimeoffset AS 'datetimeoffset(4)';  
  
--Result  
--@smalldatetime          datetimeoffset(4)  
------------------------- ------------------------------  
--1955-12-13 12:43:00     1955-12-13 12:43:00.0000 +00:0  
--  
--(1 row(s) affected)  
```  
  
Para a conversão em **datetime2**, o **smalldatetime** valor é copiado para o **datetime2** valor. As frações de segundo são definidas como 0. O código a seguir mostra os resultados da conversão de um valor `smalldatetime` em um valor `datetime2(4)`.
  
```sql
DECLARE @smalldatetime smalldatetime = '1955-12-13 12:43:10';  
DECLARE @datetime2 datetime2(4) = @smalldatetime;  
  
SELECT @smalldatetime AS '@smalldatetime', @datetime2 AS ' datetime2(4)';  
  
--Result  
--@smalldatetime           datetime2(4)  
------------------------- ------------------------  
--1955-12-13 12:43:00     1955-12-13 12:43:00.0000  
--  
--(1 row(s) affected)  
```  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-casting-string-literals-with-seconds-to-smalldatetime"></a>A. Convertendo literais de cadeia de caracteres com segundos para smalldatetime  
O exemplo a seguir compara a conversão de segundos em literais de cadeia de caracteres para `smalldatetime`.
  
```sql
SELECT   
     CAST('2007-05-08 12:35:29'     AS smalldatetime)  
    ,CAST('2007-05-08 12:35:30'     AS smalldatetime)  
    ,CAST('2007-05-08 12:59:59.998' AS smalldatetime);  
```  
  
|Entrada|Saída|  
|---|---|
|2007-05-08 12:35:29|2007-05-08 12:35:00|  
|2007-05-08 12:35:30|2007-05-08 12:36:00|  
|2007-05-08 12:59:59.998|2007-05-08 13:00:00|  
  
### <a name="b-comparing-date-and-time-data-types"></a>B. Comparando tipos de dados de data e hora  
O exemplo a seguir compara os resultados da conversão de uma cadeia de caracteres para cada tipo de dados de data e hora.
  
```sql
SELECT   
     CAST('2007-05-08 12:35:29. 1234567 +12:15' AS time(7)) AS 'time'   
    ,CAST('2007-05-08 12:35:29. 1234567 +12:15' AS date) AS 'date'   
    ,CAST('2007-05-08 12:35:29.123' AS smalldatetime) AS   
        'smalldatetime'   
    ,CAST('2007-05-08 12:35:29.123' AS datetime) AS 'datetime'   
    ,CAST('2007-05-08 12:35:29. 1234567 +12:15' AS datetime2(7)) AS   
        'datetime2'  
    ,CAST('2007-05-08 12:35:29.1234567 +12:15' AS datetimeoffset(7)) AS   
        'datetimeoffset';  
```  
  
|Tipo de dados|Saída|  
|---|---|
|**time**|12:35:29. 1234567|  
|**date**|2007-05-08|  
|**smalldatetime**|2007-05-08 12:35:00|  
|**datetime**|2007-05-08 12:35:29.123|  
|**datetime2**|2007-05-08 12:35:29. 1234567|  
|**datetimeoffset**|2007-05-08 12:35:29.1234567 +12:15|  
  
## <a name="see-also"></a>Consulte também
[CAST e CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)
  
  

