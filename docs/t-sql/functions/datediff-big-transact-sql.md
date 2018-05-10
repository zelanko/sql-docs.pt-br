---
title: DATEDIFF_BIG (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/29/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: t-sql|functions
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
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 6c0cfefde5609455f53d2afcb33659cd5c1d99bb
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="datediffbig-transact-sql"></a>DATEDIFF_BIG (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

Retorna a contagem (inteiro grande com sinal) dos limites de *datepart* especificados cruzados entre a *startdate* e a *enddate* especificadas.
  
Para obter uma visão geral das funções e dos tipos de dados de data e hora de [!INCLUDE[tsql](../../includes/tsql-md.md)], confira [Funções e tipos de dados de data e hora &#40;Transact-SQL&#41;](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md).
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
  
```sql
  
DATEDIFF_BIG ( datepart , startdate , enddate )  
```  
  
## <a name="arguments"></a>Argumentos  
*datepart*  
É a parte da *startdate* e *enddate* que especifica o tipo de limite ultrapassado. A tabela a seguir lista todos os argumentos válidos de *datepart*. Equivalentes de variável definidos pelo usuário não são válidos.
  
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
É uma expressão que pode ser resolvida em um valor de **time**, **date**, **smalldatetime**, **datetime**, **datetime2** ou **datetimeoffset**. *date* pode ser uma expressão, uma expressão de coluna, uma variável definida pelo usuário ou um literal de cadeia de caracteres. *startdate* é subtraído de *enddate*.  
Para evitar ambiguidade, use anos de quatro dígitos. Para obter mais informações sobre anos de dois dígitos, confira [Configurar a opção Corte de Ano de Dois Dígitos do servidor](../../database-engine/configure-windows/configure-the-two-digit-year-cutoff-server-configuration-option.md).
  
*enddate*  
Consulte *startdate*.
  
## <a name="return-type"></a>Tipo de retorno  
 Com sinal   
        **bigint**  
  
## <a name="return-value"></a>Valor retornado  
Retorna a contagem (inteiro grande com sinal) dos limites de datepart especificados cruzados entre a startdate e a enddate especificadas.
-   Cada *datepart* e suas abreviações retornam o mesmo valor.  
  
Se o valor retornado estiver fora do intervalo de **bigint** (-9,223,372,036,854,775,808 a 9,223,372,036,854,775,807), um erro será retornado. Para **millisecond**, a diferença máxima entre *startdate* e *enddate* é de 24 dias, 20 horas, 31 minutos e 23.647 segundos. Para **second**, a diferença máxima é de 68 anos.
  
Se *startdate* e *enddate* recebem apenas um valor temporal e a *datepart* não é uma *datepart* de hora, será retornado 0.
  
Um componente de deslocamento de fuso horário de *startdate* ou *enddate* não é usado no cálculo do valor retornado.
  
Como [smalldatetime](../../t-sql/data-types/smalldatetime-transact-sql.md) tem precisão apenas quanto ao minuto, quando um valor **smalldatetime** é usado para *startdate* ou *enddate*, os segundos e milissegundos são sempre definidos como 0 no valor retornado.
  
Se apenas um valor de hora for atribuído a uma variável de tipo de dados “data”, o valor da parte “data” faltante será definido como o valor padrão: 1900-01-01. Se apenas um valor de data for atribuído a uma variável de tipo de dados “hora” ou “data”, o valor da parte “hora” faltante será definido como o valor padrão: 00:00:00. Se *startdate* ou *enddate* tem apenas uma parte de hora e a outra apenas uma parte de data, as partes de hora e data ausentes são definidas com os valores padrão.
  
Se *startdate* e *enddate* forem de tipos de dados de data diferentes e um tiver mais partes de hora ou precisão de segundos fracionários do que o outro, as partes ausentes do outro serão definidas como 0.
  
## <a name="datepart-boundaries"></a>Limites de datepart
As instruções a seguir têm as mesmas *startdate* e *endate*. Essas datas são adjacentes e diferem, quanto à hora, em 0,0000001 segundo. A diferença entre *startdate* e *endate* em cada instrução cruza um calendário ou limite de hora de seu *datepart*. Cada instrução retorna 1. Se anos diferentes forem usados neste exemplo e se *startdate* e *endate* estiverem na mesma semana de calendário, o valor retornado para **week** será 0.

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
  
## <a name="remarks"></a>Remarks  
DATEDIFF_BIG pode ser usado na lista de seleção e nas cláusulas WHERE, HAVING, GROUP BY e ORDER BY.
  
DATEDIFF_BIG converte implicitamente literais de cadeia de caracteres em um tipo **datetime2**. Isso significa que DATEDIFF_BIG não dá suporte ao formato YDM quando a data é passada como uma cadeia de caracteres. É necessário converter explicitamente a cadeia de caracteres em um tipo **datetime** ou **smalldatetime** para usar o formato YDM.
  
A especificação de SET DATEFIRST não tem nenhum efeito em DATEDIFF_BIG. DATEDIFF_BIG sempre usa Domingo como o primeiro dia da semana para garantir que a função seja determinística.
  
## <a name="examples"></a>Exemplos  
Os exemplos a seguir usam diferentes tipos de expressões como argumentos para os parâmetros *startdate* e *enddate*.
  
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
  
Para obter muitos outros exemplos, consulte os exemplos relacionados em [DATEDIFF &#40;Transact-SQL&#41;](../../t-sql/functions/datediff-transact-sql.md).
  
## <a name="see-also"></a>Confira também
[CAST e CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[DATEDIFF &#40;Transact-SQL&#41;](../../t-sql/functions/datediff-transact-sql.md)
  
  
