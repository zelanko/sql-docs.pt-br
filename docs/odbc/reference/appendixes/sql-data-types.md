---
description: Tipos de dados SQL
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8209463c3c316a5bd2e45a2d7b08eb65b3cb113d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88483149"
---
# <a name="sql-data-types"></a>Tipos de dados SQL
Cada DBMS define seus próprios tipos de SQL. Cada driver ODBC expõe apenas os tipos de dados SQL que o DBMS associado define. Informações sobre como um driver mapeia tipos SQL DBMS para os identificadores de tipo SQL definidos pelo ODBC e como um driver mapeia tipos SQL DBMS para seus próprios identificadores de tipo SQL específicos de driver são retornados por meio de uma chamada para **SQLGetTypeInfo**. Um driver também retorna os tipos de dados SQL ao descrever os tipos de dados de colunas e parâmetros por meio de chamadas para **SQLColAttribute**, **SQLColumns**, **SQLDescribeCol**, **SQLDescribeParam**, **SQLProcedureColumns**e **SQLSpecialColumns**.  
  
> [!NOTE]  
>  Os tipos de dados SQL estão contidos nos campos SQL_DESC_ CONCISE_TYPE, SQL_DESC_TYPE e SQL_DESC_DATETIME_INTERVAL_CODE dos descritores de implementação. As características dos tipos de dados SQL estão contidas nos campos SQL_DESC_PRECISION, SQL_DESC_SCALE, SQL_DESC_LENGTH e SQL_DESC_OCTET_LENGTH dos descritores de implementação. Para obter mais informações, consulte [identificadores e descritores de tipo de dados](../../../odbc/reference/appendixes/data-type-identifiers-and-descriptors.md) mais adiante neste apêndice.  
  
 Um determinado driver e fonte de dados não oferecem necessariamente suporte a todos os tipos de dados SQL definidos neste apêndice. O suporte de um driver para tipos de dados SQL depende do nível de SQL-92 ao qual o driver está em conformidade. Para determinar o nível de gramática do SQL-92 suportado pelo driver, um aplicativo chama **SQLGetInfo** com o tipo de informação SQL_SQL_CONFORMANCE. Além disso, um determinado driver e fonte de dados podem dar suporte a tipos de dados do SQL adicionais específicos do driver. Para determinar a quais tipos de dados um driver dá suporte, um aplicativo chama **SQLGetTypeInfo**. Para obter informações sobre tipos de dados do SQL específicos do driver, consulte a documentação do driver. Para obter informações sobre os tipos de dados em uma fonte de dados específica, consulte a documentação dessa fonte de dados.  
  
> [!IMPORTANT]  
>  As tabelas em todo este apêndice são apenas diretrizes e mostram nomes, intervalos e limites usados normalmente de tipos de dados SQL. Uma determinada fonte de dados pode dar suporte a apenas alguns dos tipos de dados listados, e as características dos tipos de dados com suporte podem ser diferentes das listadas.  
  
 A tabela a seguir lista os identificadores de tipo SQL válidos para todos os tipos de dados SQL. A tabela também lista o nome e a descrição do tipo de dados correspondente do SQL-92 (se houver).  
  
|Identificador de tipo SQL [1]|Dados SQL típicos<br /><br /> tipo [2]|Descrição do tipo típico|  
|------------------------------|------------------------------------|------------------------------|  
|SQL_CHAR|CHAR (*n*)|Cadeia de caracteres do comprimento de cadeia de caracteres fixo *n*.|  
|SQL_VARCHAR|VARCHAR (*n*)|Cadeia de caracteres de comprimento variável com um comprimento máximo de cadeia de caracteres *n*.|  
|SQL_LONGVARCHAR|LONG VARCHAR|Dados de caractere de comprimento variável. O comprimento máximo é dependente da fonte de dados. 99|  
|SQL_WCHAR|WCHAR (*n*)|Cadeia de caracteres Unicode de comprimento de cadeia de caracteres fixa *n*|  
|SQL_WVARCHAR|VARWCHAR (*n*)|Cadeia de caracteres de comprimento variável Unicode com um comprimento máximo de cadeia de caracteres *n*|  
|SQL_WLONGVARCHAR|LONGWVARCHAR|Dados de caractere Unicode de comprimento variável. O comprimento máximo é dependente da fonte de dados|  
|SQL_DECIMAL|DECIMAL (*p*,*s*)|Valor numérico assinado, exato com uma precisão de pelo menos *p* e escala *s.* (A precisão máxima é definida pelo driver.) (1 <= *p* <= 15; *s*  <=  *p*). quatro|  
|SQL_NUMERIC|NUMERIC (*p*,*s*)|Valor numérico assinado, exato com uma precisão *p* e escala *s* (1 <= *p* <= 15; *s*  <=  *p*). quatro|  
|SQL_SMALLINT|SMALLINT|Valor numérico exato com precisão 5 e escala 0 (assinado:-32.768 <= *n* <= 32.767, não assinado: 0 <= *n* <= 65535) [3].|  
|SQL_INTEGER|INTEGER|Valor numérico exato com precisão 10 e escala 0 (assinado:-2 [31] <= *n* <= 2 [31]-1, não assinado: 0 <= *n* <= 2 [32]-1) [3].|  
|SQL_REAL|real|Um valor numérico assinado, aproximado com uma precisão binária 24 (zero ou valor absoluto 10 [-38] a 10 [38]).|  
|SQL_FLOAT|FLOAT (*p*)|Valor numérico assinado, aproximado com uma precisão binária de pelo menos *p*. (A precisão máxima é definida pelo driver.) 05|  
|SQL_DOUBLE|DOUBLE PRECISION|Um valor numérico assinado, aproximado com uma precisão binária 53 (zero ou valor absoluto 10 [-308] a 10 [308]).|  
|SQL_BIT|BIT|Dados binários de bit único. 8|  
|SQL_TINYINT|TINYINT|Valor numérico exato com precisão 3 e escala 0 (assinado:-128 <= *n* <= 127, não assinado: 0 <= *n* <= 255) [3].|  
|SQL_BIGINT|bigint|Valor numérico exato com precisão 19 (se assinada) ou 20 (se não assinado) e escala 0 (assinado:-2 [63] <= *n* <= 2 [63]-1, não assinado: 0 <= *n* <= 2 [64]-1) [3], [9].|  
|SQL_BINARY|BINÁRIO (*n*)|Dados binários de comprimento fixo *n*. 99|  
|SQL_VARBINARY|VARBINARY (*n*)|Dados binários de comprimento variável de comprimento máximo *n*. O máximo é definido pelo usuário. 99|  
|SQL_LONGVARBINARY|VARBINARY LONGO|Dados binários de comprimento variável. O comprimento máximo é dependente da fonte de dados. 99|  
|SQL_TYPE_DATE [6]|DATE|Campos de ano, mês e dia, em conformidade com as regras do calendário gregoriano. (Consulte [restrições do calendário gregoriano](../../../odbc/reference/appendixes/constraints-of-the-gregorian-calendar.md), mais adiante neste apêndice.)|  
|SQL_TYPE_TIME [6]|HORA (*p*)|Campos de hora, minuto e segundo, com valores válidos para horas de 00 a 23, valores válidos para minutos de 00 a 59 e valores válidos para segundos de 00 a 61. A precisão *p* indica a precisão de segundos.|  
|SQL_TYPE_TIMESTAMP [6]|TIMESTAMP (*p*)|Campos ano, mês, dia, hora, minuto e segundo, com valores válidos, conforme definido para os tipos de dados de data e hora.|  
|SQL_TYPE_UTCDATETIME|UTCDATEtime|Campos ano, mês, dia, hora, minuto, segundo, utchour e utcminute. Os campos utchour e utcminute têm precisão de 1/10 microssegundos.|  
|SQL_TYPE_UTCTIME|UTCTIME|Campos de hora, minuto, segundo, utchour e utcminute. Os campos utchour e utcminute têm precisão de 1/10 microssegundos.|  
|SQL_INTERVAL_MONTH [7]|MÊS do intervalo (*p*)|Número de meses entre duas datas; *p* é a precisão à esquerda do intervalo.|  
|SQL_INTERVAL_YEAR [7]|ANO de intervalo (*p*)|Número de anos entre duas datas; *p* é a precisão à esquerda do intervalo.|  
|SQL_INTERVAL_YEAR_TO_MONTH [7]|ANO de intervalo (*p*) para mês|Número de anos e meses entre duas datas; *p* é a precisão à esquerda do intervalo.|  
|SQL_INTERVAL_DAY [7]|DIA do intervalo (*p*)|Número de dias entre duas datas; *p* é a precisão à esquerda do intervalo.|  
|SQL_INTERVAL_HOUR [7]|INTERVALO de horas (*p*)|Número de horas entre duas datas/horas; *p* é a precisão à esquerda do intervalo.|  
|SQL_INTERVAL_MINUTE [7]|INTERVALO de minutos (*p*)|Número de minutos entre duas datas/horas; *p* é a precisão à esquerda do intervalo.|  
|SQL_INTERVAL_SECOND [7]|INTERVALO em segundo (*p*,*q*)|Número de segundos entre duas datas/horas; *p* é a precisão inicial do intervalo e *q* é a precisão do intervalo em segundos.|  
|SQL_INTERVAL_DAY_TO_HOUR [7]|DIA do intervalo (*p*) a hora|Número de dias/horas entre duas data/hora; *p* é a precisão à esquerda do intervalo.|  
|SQL_INTERVAL_DAY_TO_MINUTE [7]|DIA do intervalo (*p*) a minuto|Número de dias/horas/minutos entre duas datas/horários; *p* é a precisão à esquerda do intervalo.|  
|SQL_INTERVAL_DAY_TO_SECOND [7]|INTERVALO dia (*p*) a segundo (*p*)|Número de dias/horas/minutos/segundos entre duas datas/horas; *p* é a precisão inicial do intervalo e *q* é a precisão do intervalo em segundos.|  
|SQL_INTERVAL_HOUR_TO_MINUTE [7]|INTERVALO de horas (*p*) a minuto|Número de horas/minutos entre duas datas/horas; *p* é a precisão à esquerda do intervalo.|  
|SQL_INTERVAL_HOUR_TO_SECOND [7]|INTERVALO de horas (*p*) a segundo (*p*)|Número de horas/minutos/segundos entre duas datas/horas; *p* é a precisão inicial do intervalo e *q* é a precisão do intervalo em segundos.|  
|SQL_INTERVAL_MINUTE_TO_SECOND [7]|INTERVALO de minutos (*p*) a segundo (*p*)|Número de minutos/segundos entre duas datas/horas; *p* é a precisão inicial do intervalo e *q* é a precisão do intervalo em segundos.|  
|SQL_GUID|GUID|GUID de comprimento fixo.|  
  
 [1] esse é o valor retornado na coluna DATA_TYPE por uma chamada para **SQLGetTypeInfo**.  
  
 [2] esse é o valor retornado na coluna nome e criar parâmetros por uma chamada para **SQLGetTypeInfo**. A coluna NAME retorna a designação-por exemplo, CHAR-enquanto a coluna CREATE PARAMs retorna uma lista separada por vírgulas de parâmetros de criação, como precisão, escala e comprimento.  
  
 [3] um aplicativo usa **SQLGetTypeInfo** ou **SQLColAttribute** para determinar se um determinado tipo de dados ou uma determinada coluna em um conjunto de resultados não está assinado.  
  
 [4] os tipos de dados SQL_DECIMAL e SQL_NUMERIC diferem apenas em sua precisão. A precisão de um DECIMAL (*p*,*s*) é uma precisão decimal definida pela implementação que não é menor que *p*, enquanto a precisão de um numérico (*p*,*s*) é exatamente igual a *p*.  
  
 [5] dependendo da implementação, a precisão do SQL_FLOAT pode ser 24 ou 53: se for 24, o tipo de dados SQL_FLOAT será o mesmo que SQL_REAL; Se for 53, o tipo de dados SQL_FLOAT será o mesmo que SQL_DOUBLE.  
  
 [6] no ODBC *3. x*, os tipos de dados SQL Date, time e timestamp são SQL_TYPE_DATE, SQL_TYPE_TIME e SQL_TYPE_TIMESTAMP, respectivamente; no ODBC *2. x*, os tipos de dados são SQL_DATE, SQL_TIME e SQL_TIMESTAMP.  
  
 [7] para obter mais informações sobre os tipos de dados SQL de intervalo, consulte a seção [tipos de dados de intervalo](../../../odbc/reference/appendixes/interval-data-types.md) , mais adiante neste apêndice.  
  
 [8] o tipo de dados SQL_BIT tem características diferentes do tipo de BIT em SQL-92.  
  
 [9] este tipo de dados não tem nenhum tipo de dados correspondente em SQL-92.  
  
 Esta seção fornece o exemplo a seguir.  
  
-   [Conjunto de resultados SQLGetTypeInfo de exemplo](../../../odbc/reference/appendixes/example-sqlgettypeinfo-result-set.md)
