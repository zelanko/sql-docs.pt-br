---
title: Tipos de dados SQL | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL data types [ODBC]
- SQL data types [ODBC], about SQL data types
- data types [ODBC], SQL data types
ms.assetid: 1b22f985-f5e4-4779-87eb-e43329a442b1
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 623ac38791eebc6db84380dfadd499651af938af
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63280918"
---
# <a name="sql-data-types"></a>Tipos de dados SQL
Cada DBMS define seus próprios tipos SQL. Cada driver ODBC expõe apenas esses tipos de dados SQL que define o DBMS associado. Informações sobre como um driver mapeia tipos de DBMS SQL para os identificadores de tipo definidas pelo ODBC SQL e como um driver mapeia os tipos de DBMS SQL para seus próprio identificadores de tipo SQL específica do driver é retornado por uma chamada para **SQLGetTypeInfo**. Um driver também retorna os tipos de dados SQL ao descrever os tipos de dados de colunas e parâmetros por meio de chamadas para **SQLColAttribute**, **SQLColumns**, **SQLDescribeCol**, **SQLDescribeParam**, **SQLProcedureColumns**, e **SQLSpecialColumns**.  
  
> [!NOTE]  
>  Os tipos de dados SQL estão contidos nos campos SQL_DESC_ CONCISE_TYPE, SQL_DESC_TYPE e SQL_DESC_DATETIME_INTERVAL_CODE dos descritores de implementação. Características dos tipos de dados SQL estão contidas nos campos SQL_DESC_PRECISION, SQL_DESC_SCALE, SQL_DESC_LENGTH e SQL_DESC_OCTET_LENGTH dos descritores de implementação. Para obter mais informações, consulte [Data Type Identifiers and Descriptors](../../../odbc/reference/appendixes/data-type-identifiers-and-descriptors.md) mais adiante neste apêndice.  
  
 Uma determinada fonte de dados e o driver não suportam necessariamente todos os tipos de dados SQL que são definidos neste apêndice. Suporte de um driver para tipos de dados SQL depende do nível de SQL-92 que o driver está em conformidade com. Para determinar o nível de gramática de SQL-92 com suporte pelo driver, um aplicativo chama **SQLGetInfo** com o tipo de informação SQL_SQL_CONFORMANCE. Além disso, uma determinada fonte de dados e driver pode dar suporte a tipos de dados SQL adicionais, específicos de driver. Para determinar quais tipos de dados um driver oferece suporte, um aplicativo chama **SQLGetTypeInfo**. Para obter informações sobre tipos de dados SQL específico do driver, consulte a documentação do driver. Para obter informações sobre os tipos de dados em uma fonte de dados específicos, consulte a documentação dessa fonte de dados.  
  
> [!IMPORTANT]  
>  As tabelas em todo este apêndice são apenas diretrizes e mostrar normalmente usado nomes, intervalos e limites de tipos de dados SQL. Apenas alguns dos tipos de dados listados pode dar suporte a uma determinada fonte de dados e as características dos tipos de dados com suporte podem diferir das que são listados.  
  
 A tabela a seguir lista os identificadores de tipo SQL válidos para todos os tipos de dados SQL. A tabela também lista o nome e a descrição do tipo de dados correspondente do SQL-92 (se houver).  
  
|Identificador de tipo SQL [1]|Típica de dados do SQL<br /><br /> type[2]|Descrição de tipo comum|  
|------------------------------|------------------------------------|------------------------------|  
|SQL_CHAR|CHAR(*n*)|Cadeia de caracteres de comprimento de cadeia de caracteres fixa *n*.|  
|SQL_VARCHAR|VARCHAR(*n*)|Cadeia de caracteres de comprimento variável com um comprimento máximo da cadeia *n*.|  
|SQL_LONGVARCHAR|LONG VARCHAR|Dados de caracteres de comprimento variável. Comprimento máximo é dependente da fonte de dados. [9]|  
|SQL_WCHAR|WCHAR(*n*)|A cadeia de caracteres Unicode de comprimento de cadeia de caracteres fixa *n*|  
|SQL_WVARCHAR|VARWCHAR(*n*)|Cadeia de caracteres de comprimento variável de Unicode com um comprimento máximo da cadeia de caracteres *n*|  
|SQL_WLONGVARCHAR|LONGWVARCHAR|Dados de caractere de comprimento variável Unicode. Comprimento máximo é dependente da fonte de dados|  
|SQL_DECIMAL|DECIMAL(*p*,*s*)|Assinado, um valor numérico exato, com uma precisão de pelo menos *p* e a escala *s.* (A precisão máxima é definido pelo driver). (1 < = *p* < = 15; *s* <= *p*). [ 4]|  
|SQL_NUMERIC|NUMÉRICO (*p*,*s*)|Valor numérico exato, com uma precisão sinal *p* e a escala *s* (1 < = *p* < = 15; *s* <= *p*). [ 4]|  
|SQL_SMALLINT|SMALLINT|Valor numérico exato com precisão 5 e escala 0 (assinado: -32.768 < = *n* < = 32,767, sem sinal:  0 <= *n* <= 65,535)[3].|  
|SQL_INTEGER|INTEGER|Valor numérico exato com precisão 10 e escala 0 (assinado: -2 [31] < = *n* < = 2 [31] – 1, sem sinal:  0 <= *n* <= 2[32] - 1)[3].|  
|SQL_REAL|real|Assinado, o valor numérico aproximado com uma precisão binária de 24 (zero ou valor absoluto 10 [-38] para 10[38]).|  
|SQL_FLOAT|FLOAT (*p*)|Assinado, valor numérico aproximado com uma precisão binária de pelo menos *p*. (A precisão máxima é definido pelo driver). [5]|  
|SQL_DOUBLE|DOUBLE PRECISION|Assinado, o valor numérico aproximado com uma precisão binária de 53 (zero ou valor absoluto 10 [-308] para 10[308]).|  
|SQL_BIT|BIT|Dados binários de bit único. [8]|  
|SQL_TINYINT|TINYINT|Valor numérico exato com precisão 3 e escala 0 (assinado: -128 < = *n* < = 127, sem sinal:  0 <= *n* <= 255)[3].|  
|SQL_BIGINT|bigint|Valor numérico exato com precisão 19 (se tiver sinal) ou 20 (se não tiver sinal) e escala 0 (assinado: -2 [63] < = *n* < = 2 [63] – 1, sem sinal: 0 < = *n* < = 2 [64] – 1) [3], [9].|  
|SQL_BINARY|BINARY(*n*)|Dados binários de comprimento fixo *n*. [ 9]|  
|SQL_VARBINARY|VARBINARY(*n*)|Dados binários de comprimento máximo de comprimento variável *n*. O máximo é definido pelo usuário. [9]|  
|SQL_LONGVARBINARY|VARBINARY LONGO|Dados binários de comprimento variável. Comprimento máximo é dependente da fonte de dados. [9]|  
|SQL_TYPE_DATE[6]|DATE|Ano, mês e campos do dia, em conformidade com as regras do calendário gregoriano. (Consulte [restrições do calendário gregoriano](../../../odbc/reference/appendixes/constraints-of-the-gregorian-calendar.md), mais adiante neste apêndice.)|  
|SQL_TYPE_TIME[6]|TEMPO (*p*)|Hora, minuto e segundo campos, com os valores válidos para horas de 00 a 23, os valores válidos para de 00 a 59 minutos e valores válidos para segundos de 00 a 61. Precisão *p* indica a precisão de segundos.|  
|SQL_TYPE_TIMESTAMP[6]|Carimbo de hora (*p*)|Ano, mês, dia, hora, minuto e segundo campos, com os valores válidos conforme definido para os tipos de dados de data e hora.|  
|SQL_TYPE_UTCDATETIME|UTCDATETIME|Campos de ano, mês, dia, hora, minuto, segundo, utchour e utcminute. Os campos utchour e utcminute tem precisão de 1/10 microssegundos.|  
|SQL_TYPE_UTCTIME|UTCTIME|Campos de hora, minuto, segundo, utchour e utcminute. Os campos utchour e utcminute têm precisão de 1/10 microssegundo...|  
|SQL_INTERVAL_MONTH[7]|INTERVALO de mês (*p*)|Número de meses entre duas datas; *p* é o intervalo de precisão inicial.|  
|SQL_INTERVAL_YEAR[7]|INTERVALO de ano (*p*)|Número de anos entre duas datas; *p* é o intervalo de precisão inicial.|  
|SQL_INTERVAL_YEAR_TO_MONTH[7]|INTERVALO de ano (*p*) para o mês|Número de anos e meses entre duas datas; *p* é o intervalo de precisão inicial.|  
|SQL_INTERVAL_DAY[7]|INTERVALO-dia (*p*)|Número de dias entre duas datas; *p* é o intervalo de precisão inicial.|  
|SQL_INTERVAL_HOUR[7]|INTERVALO-hora (*p*)|Número de horas entre duas datas/horas; *p* é o intervalo de precisão inicial.|  
|SQL_INTERVAL_MINUTE[7]|MINUTOS de intervalo (*p*)|Número de minutos entre duas datas/horas; *p* é o intervalo de precisão inicial.|  
|SQL_INTERVAL_SECOND[7]|INTERVALO de segundo (*p*,*q*)|Número de segundos entre duas datas/horas; *p* é o intervalo de precisão inicial e *q* é a precisão de segundos de intervalo.|  
|SQL_INTERVAL_DAY_TO_HOUR[7]|INTERVALO-dia (*p*) para hora|Número de dias/horas entre duas datas/horas; *p* é o intervalo de precisão inicial.|  
|SQL_INTERVAL_DAY_TO_MINUTE[7]|INTERVALO-dia (*p*) para minuto|Número de dias/horas/minutos entre duas datas/horas; *p* é o intervalo de precisão inicial.|  
|SQL_INTERVAL_DAY_TO_SECOND[7]|INTERVALO-dia (*p*) para o segundo (*q*)|Número de dias/horas/minutos/segundos entre duas datas/horas; *p* é o intervalo de precisão inicial e *q* é a precisão de segundos de intervalo.|  
|SQL_INTERVAL_HOUR_TO_MINUTE[7]|INTERVALO-hora (*p*) para minuto|Número de horas/minutos entre duas datas/horas; *p* é o intervalo de precisão inicial.|  
|SQL_INTERVAL_HOUR_TO_SECOND[7]|INTERVALO-hora (*p*) para o segundo (*q*)|Número de horas/minutos/segundos entre duas datas/horas; *p* é o intervalo de precisão inicial e *q* é a precisão de segundos de intervalo.|  
|SQL_INTERVAL_MINUTE_TO_SECOND[7]|MINUTOS de intervalo (*p*) para o segundo (*q*)|Número de minutos/segundos entre duas datas/horas; *p* é o intervalo de precisão inicial e *q* é a precisão de segundos de intervalo.|  
|SQL_GUID|GUID|GUID de comprimento fixo.|  
  
 [1] esse é o valor retornado na coluna DATA_TYPE por uma chamada para **SQLGetTypeInfo**.  
  
 [2] esse é o valor retornado na coluna Nome e criar PARAMS por uma chamada para **SQLGetTypeInfo**. A coluna de nome retorna a designação-por exemplo, CHAR-enquanto a coluna criar PARAMS retorna uma lista separada por vírgulas dos parâmetros de criação, como precisão, escala e comprimento.  
  
 [3] um aplicativo usa **SQLGetTypeInfo** ou **SQLColAttribute** para determinar se um determinado tipo de dados ou uma coluna específica em um conjunto de resultados é sem sinal.  
  
 [4] tipos de dados SQL_DECIMAL e SQL_NUMERIC diferem apenas em sua precisão. A precisão de um DECIMAL (*p*,*s*) é uma precisão decimal definido pela implementação que é não inferior a *p*, enquanto que a precisão de um NUMÉRICO (*p* ,*s*) são exatamente iguais à *p*.  
  
 [5] dependendo da implementação, a precisão de SQL_FLOAT pode ser 24 ou 53: se ele for 24, o tipo de dados SQL_FLOAT é o mesmo que SQL_REAL; Se for 53, o tipo de dados SQL_FLOAT é o mesmo que SQL_DOUBLE.  
  
 [6] em ODBC 3 *. x*, os tipos de dados de data, hora e carimbo de hora do SQL são SQL_TYPE_DATE, SQL_TYPE_TIME e SQL_TYPE_TIMESTAMP, respectivamente; no ODBC 2. *x*, os tipos de dados são SQL_DATE, SQL_TIME e SQL_TIMESTAMP.  
  
 [7] para obter mais informações sobre os tipos de dados SQL de intervalo, consulte o [tipos de dados Interval](../../../odbc/reference/appendixes/interval-data-types.md) seção mais adiante neste apêndice.  
  
 [8] o tipo de dados SQL_BIT tem características diferentes de tipo de BIT em SQL-92.  
  
 [9] esse tipo de dados não tem nenhum tipo de dados correspondente no SQL-92.  
  
 Esta seção fornece o exemplo a seguir.  
  
-   [Conjunto de resultados SQLGetTypeInfo de exemplo](../../../odbc/reference/appendixes/example-sqlgettypeinfo-result-set.md)
