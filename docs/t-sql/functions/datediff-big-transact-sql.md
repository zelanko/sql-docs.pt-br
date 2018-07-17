---
title: DATEDIFF_BIG (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/29/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
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
caps.latest.revision: 7
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: b309bb7411d3c75aa1c98a219123efffc5dbca3e
ms.sourcegitcommit: 05e18a1e80e61d9ffe28b14fb070728b67b98c7d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/04/2018
ms.locfileid: "37782517"
---
# <a name="datediffbig-transact-sql"></a>DATEDIFF_BIG (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

Essa função retorna a contagem (como um grande valor inteiro com sinal) dos limites de *datepart* especificados cruzados entre os parâmetros especificados *startdate* e *enddate*.
  
Consulte [Tipos de dados e funções de data e hora &#40;Transact-SQL&#41;](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md) para obter uma visão geral de todos os tipos de dados e funções de data e hora do [!INCLUDE[tsql](../../includes/tsql-md.md)].
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
  
```sql
  
DATEDIFF_BIG ( datepart , startdate , enddate )  
```  
  
## <a name="arguments"></a>Argumentos  
*datepart*  
A parte de *startdate* e de *enddate* que especifica o tipo de limite ultrapassado. `DATEDIFF_BIG` não aceitarão equivalentes de variável definidos pelo usuário. Esta tabela lista todos os argumentos *datepart* válidos.

> [!NOTE]
> `DATEDIFF_BIG` não aceita os equivalentes de variável definidos pelo usuário para os argumentos *datepart*.
  
|*datepart*|Abreviações|  
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
  
*startdate*  
Uma expressão que pode resolver um dos seguintes valores:

+ **date**
+ **datetime**
+ **datetimeoffset**
+ **datetime2** 
+ **smalldatetime**
+ **time**

Para *date*, `DATEDIFF_BIG` aceitará uma variável de expressão de coluna, de expressão, de literal de cadeia de caracteres ou definida pelo usuário. Um valor literal de cadeia de caracteres deve resolver um **datetime**. Para evitar ambiguidade, use anos de quatro dígitos. `DATEDIFF_BIG` subtrai *enddate* de *startdate*. Para evitar ambiguidade, use anos de quatro dígitos. Consulte [Configurar a opção two digit year cutoff de configuração de servidor](../../database-engine/configure-windows/configure-the-two-digit-year-cutoff-server-configuration-option.md) para obter informações sobre anos de dois dígitos.
  
*enddate*  
Consulte *startdate*.
  
## <a name="return-type"></a>Tipo de retorno  

**bigint** com sinal  
  
## <a name="return-value"></a>Valor retornado  
Retorna a contagem (como um valor bigint com sinal) dos limites de datepart especificados cruzados entre a startdate e a enddate especificadas.
-   Cada *datepart* específico e as abreviações desse *datepart* retornarão o mesmo valor.  
  
Para um valor retornado fora do intervalo para **bigint** (-9.223.372.036.854.775.808 a 9.223.372.036.854.775.807), `DATEDIFF_BIG` retorna um erro. Para **millisecond**, a diferença máxima entre *startdate* e *enddate* é de 24 dias, 20 horas, 31 minutos e 23.647 segundos. Para **second**, a diferença máxima é de 68 anos.
  
Se *startdate* e *enddate* receberem apenas um valor temporal e *datepart* não for um *datepart* de hora, `DATEDIFF_BIG` retornará 0.
  
`DATEDIFF_BIG` não usa um componente de deslocamento de fuso horário de *startdate* ou *enddate* para calcular o valor retornado.
  
Para um valor **smalldatetime** usado para *startdate* ou para *enddate*, `DATEDIFF_BIG` sempre define segundos e milissegundos como 0 no valor retornado, porque [smalldatetime](../../t-sql/data-types/smalldatetime-transact-sql.md) tem apenas a precisão do minuto.
  
Se apenas um valor temporal for atribuído a uma variável de tipo de dados de data, `DATEDIFF_BIG` definirá o valor da parte de data ausente como o valor padrão: 1900-01-01. Se apenas um valor de data for atribuído a uma variável de um tipo de dados de data ou hora, `DATEDIFF_BIG` definirá o valor da parte de hora ausente como o valor padrão: 00:00:00. Se *startdate* ou *enddate* tiver apenas uma parte de hora e a outra apenas uma parte de data, `DATEDIFF_BIG` definirá as partes de hora e data ausentes como os valores padrão.
  
Se *startdate* e *enddate* tiverem diferentes tipos de dados de data e um tiver mais partes de hora ou precisão de segundos fracionários do que o outro, `DATEDIFF_BIG` definirá as partes ausentes do outro como 0.
  
## <a name="datepart-boundaries"></a>Limites de datepart
As instruções a seguir têm os mesmos valores de *startdate* e de *enddate*. Essas datas são adjacentes e diferem, quanto à hora, em 0,0000001 segundo. A diferença entre *startdate* e *enddate* em cada instrução cruza um calendário ou limite de hora de sua *datepart*. Cada instrução retorna 1. Se *startdate* e *enddate* tiverem diferentes valores de ano, mas os mesmos valores semanais de calendário, `DATEDIFF_BIG` retornará 0 para *datepart* **week**.

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
  
## <a name="remarks"></a>Remarks  
Use `DATEDIFF_BIG` nas cláusulas SELECT <list>, WHERE, HAVING, GROUP BY e ORDER BY.
  
`DATEDIFF_BIG` converte implicitamente literais de cadeias de caracteres como um tipo **datetime2**. Isso significa que `DATEDIFF_BIG` não é compatível com o formato YDM quando a data é transmitida como cadeia de caracteres. É necessário converter explicitamente a cadeia de caracteres em um tipo de **datetime** ou **smalldatetime** para usar o formato YDM.
  
A especificação SET DATEFIRST não tem efeito sobre `DATEDIFF_BIG`. `DATEDIFF_BIG` sempre usa domingo como o primeiro dia da semana para garantir que a função opere de maneira determinística.
  
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

Veja de perto exemplos relacionados em [DATEDIFF &#40;Transact-SQL&#41;](../../t-sql/functions/datediff-transact-sql.md).
  
## <a name="see-also"></a>Confira também
[CAST e CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[DATEDIFF &#40;Transact-SQL&#41;](../../t-sql/functions/datediff-transact-sql.md)
  
  
