---
title: DATEDIFF_BIG (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/29/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: "7"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 6c8228f0db3e37fe3bf6425d60fd4f9067e92220
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="datediffbig-transact-sql"></a>DATEDIFF_BIG (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

Retorna a contagem (inteiro assinado grande) de especificado *datepart* limites cruzados entre especificado *startdate* e *enddate*.
  
Para obter uma visão geral de todos os [!INCLUDE[tsql](../../includes/tsql-md.md)] tipos de dados de data e hora e funções, consulte [data e hora tipos de dados e funções &#40; Transact-SQL &#41; ](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md).
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
  
```sql
  
DATEDIFF_BIG ( datepart , startdate , enddate )  
```  
  
## <a name="arguments"></a>Argumentos  
*datepart*  
É a parte do *startdate* e *enddate* que especifica o tipo de limite ultrapassado. A seguinte tabela lista válida *datepart* argumentos. Equivalentes de variável definidos pelo usuário não são válidos.
  
|*datepart*|Abreviações|  
|---|---|
|**ano**|**AA, AAAA**|  
|**trimestre**|**tq, t**|  
|**mês**|**mm, m**|  
|**DAYOFYEAR**|**dy, y**|  
|**dia**|**dd, d**|  
|**semana**|**sem, ww**|  
|**hora**|**hh**|  
|**minuto**|**min, n**|  
|**segundo**|**SS, s**|  
|**milissegundos**|**MS**|  
|**microssegundos**|**MCS**|  
|**nanossegundos**|**NS**|  
  
*startdate*  
É uma expressão que pode ser resolvida para um **tempo**, **data**, **smalldatetime**, **datetime**, **datetime2**, ou **datetimeoffset** valor. *data* pode ser uma expressão, a expressão de coluna, a variável definida pelo usuário ou a cadeia de caracteres literal. *StartDate* é subtraído de *enddate*.  
Para evitar ambiguidade, use anos de quatro dígitos. Para obter informações sobre anos de dois dígitos, consulte [configurar o ano de dois dígitos corte opção de configuração de servidor](../../database-engine/configure-windows/configure-the-two-digit-year-cutoff-server-configuration-option.md).
  
*Data de término*  
Consulte *startdate*.
  
## <a name="return-type"></a>Tipo de retorno  
 Assinado   
        **bigint**  
  
## <a name="return-value"></a>Valor de retorno  
Contagem de retorna (bigint assinado) dos limites especificados de datepart cruzados entre a data de início especificada e a data de término.
-   Cada *datepart* e suas abreviações retornam o mesmo valor.  
  
Se o valor de retorno estiver fora do intervalo de **bigint** (-9.223.372.036.854.775.808 a 9.223.372.036.854.775.807), um erro será retornado. Para **milissegundo**, a diferença máxima entre *startdate* e *enddate* é de 24 dias, 20 horas, 31 minutos e 23.647 segundos. Para **segundo**, a diferença máxima é de 68 anos.
  
Se *startdate* e *enddate* forem atribuídos apenas um valor de hora e o *datepart* não é uma hora *datepart*, será retornado 0.
  
Componente do deslocamento de um fuso horário *startdate* ou *endate* não é usado no cálculo do valor de retorno.
  
Porque [smalldatetime](../../t-sql/data-types/smalldatetime-transact-sql.md) é preciso somente em minutos, quando um **smalldatetime** valor é usado para *startdate* ou *enddate*, em segundos e milissegundos são sempre definidos como 0 no valor de retorno.
  
Se apenas um valor de hora for atribuído a uma variável de tipo de dados “data”, o valor da parte “data” faltante será definido como o valor padrão: 1900-01-01. Se apenas um valor de data for atribuído a uma variável de tipo de dados “hora” ou “data”, o valor da parte “hora” faltante será definido como o valor padrão: 00:00:00. Se qualquer um dos *startdate* ou *enddate* ter apenas uma parte de hora e a outra somente uma parte de data, hora e partes de data são definidas para os valores padrão.
  
Se *startdate* e *enddate* forem de tipos de dados de data diferente e um tiver mais partes de tempo ou a precisão fracionária de segundos que o outro, as partes faltantes do outro são definidas como 0.
  
## <a name="datepart-boundaries"></a>limites de DatePart
As instruções a seguir têm o mesmo *startdate* e o mesmo *endate*. Essas datas são adjacentes e diferem, quanto à hora, em 0,0000001 segundo. A diferença entre o *startdate* e *endate* em cada instrução cruza um calendário ou limite de hora de seu *datepart*. Cada instrução retorna 1. Se anos diferentes forem usados neste exemplo e se *startdate* e *endate* estão na mesma semana de calendário, o valor de retorno **semana** será 0.

```sql
SELECT DATEDIFF_BIG(year, '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF_BIG(quarter, '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF_BIG(month, '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF_BIG(dayofyear, '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF_BIG(day, '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF_BIG(week, '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF_BIG(hour, '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF_BIG(minute, '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF_BIG(second, '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF_BIG(millisecond, '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
```
  
## <a name="remarks"></a>Comentários  
DATEDIFF_BIG pode ser usado na lista de seleção, cláusulas WHERE, HAVING, GROUP BY e ORDER BY.
  
DATEDIFF_BIG converte implicitamente literais de cadeia de caracteres como um **datetime2** tipo. Isso significa que o DATEDIFF_BIG não dá suporte ao formato YDM quando a data é transmitida como uma cadeia de caracteres. É necessário converter explicitamente a cadeia de caracteres para um **datetime** ou **smalldatetime** tipo para usar o formato YDM.
  
Especificação de SET DATEFIRST não tem nenhum efeito em DATEDIFF_BIG. DATEDIFF_BIG sempre usa domingo como o primeiro dia da semana para garantir que a função é determinística.
  
## <a name="examples"></a>Exemplos  
Os exemplos a seguir usam diferentes tipos de expressões como argumentos para o *startdate* e *enddate* parâmetros.
  
### <a name="specifying-columns-for-startdate-and-enddate"></a>Especificando colunas para startdate e enddate  
O exemplo a seguir calcula o número de limites de dia que são cruzados entre as datas de duas colunas de uma tabela.
  
```sql
CREATE TABLE dbo.Duration  
    (  
    startDate datetime2  
    ,endDate datetime2  
    );  
INSERT INTO dbo.Duration(startDate,endDate)  
    VALUES('2007-05-06 12:10:09','2007-05-07 12:10:09');  
SELECT DATEDIFF_BIG(day,startDate,endDate) AS 'Duration'  
FROM dbo.Duration;  
-- Returns: 1  
```  
  
Para muitos exemplos adicionais, consulte os exemplos relacionados [DATEDIFF &#40; Transact-SQL &#41; ](../../t-sql/functions/datediff-transact-sql.md).
  
## <a name="see-also"></a>Consulte também
[CAST e CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[DATEDIFF &#40; Transact-SQL &#41;](../../t-sql/functions/datediff-transact-sql.md)
  
  
