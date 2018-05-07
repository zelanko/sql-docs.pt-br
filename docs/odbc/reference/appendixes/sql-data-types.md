---
title: Tipos de dados SQL | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQL data types [ODBC]
- SQL data types [ODBC], about SQL data types
- data types [ODBC], SQL data types
ms.assetid: 1b22f985-f5e4-4779-87eb-e43329a442b1
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3c2022f1a0e034741a7259cef2613ce69361285a
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="sql-data-types"></a>Tipos de dados SQL
Cada DBMS define seus próprios tipos SQL. Cada driver ODBC expõe apenas os tipos de dados SQL que define o DBMS associado. Obter informações sobre como um driver mapeia tipos de DBMS SQL para os identificadores de tipo definidas pelo ODBC SQL e como um driver mapeia os tipos de DBMS SQL para seus próprio identificadores de tipo SQL específica do driver é retornado por uma chamada a **SQLGetTypeInfo**. Um driver também retorna os tipos de dados SQL ao descrever os tipos de dados das colunas e parâmetros por meio de chamadas **SQLColAttribute**, **SQLColumns**, **SQLDescribeCol**, **SQLDescribeParam**, **SQLProcedureColumns**, e **SQLSpecialColumns**.  
  
> [!NOTE]  
>  Os tipos de dados SQL estão contidos nos campos SQL_DESC_ CONCISE_TYPE, SQL_DESC_TYPE e SQL_DESC_DATETIME_INTERVAL_CODE dos descritores de implementação. Características dos tipos de dados SQL estão contidas nos campos SQL_DESC_PRECISION, SQL_DESC_SCALE, SQL_DESC_LENGTH e SQL_DESC_OCTET_LENGTH dos descritores de implementação. Para obter mais informações, consulte [identificadores de tipo de dados e os descritores de](../../../odbc/reference/appendixes/data-type-identifiers-and-descriptors.md) mais adiante neste apêndice.  
  
 Uma determinada fonte de dados e o driver não suportam necessariamente todos os tipos de dados SQL que são definidos neste apêndice. Suporte do driver para tipos de dados SQL depende do nível de SQL-92 que o driver está em conformidade com. Para determinar o nível de suporte do driver de gramática de SQL-92, um aplicativo chama **SQLGetInfo** com o tipo de informação SQL_SQL_CONFORMANCE. Além disso, uma determinada fonte de dados e o driver pode dar suporte a tipos de dados SQL adicionais e específicas do driver. Para determinar quais dados tipos um driver oferece suporte, um aplicativo chama **SQLGetTypeInfo**. Para obter informações sobre tipos de dados SQL específico do driver, consulte a documentação do driver. Para obter informações sobre os tipos de dados em uma fonte de dados específicos, consulte a documentação para essa fonte de dados.  
  
> [!IMPORTANT]  
>  As tabelas em todo este apêndice são apenas diretrizes e nomes de Mostrar geralmente usada, intervalos e limites de tipos de dados SQL. Uma determinada fonte de dados pode dar suporte a apenas alguns dos tipos de dados listados, e as características dos tipos de dados com suporte podem ser diferentes daqueles listados.  
  
 A tabela a seguir lista os identificadores de tipo SQL válidos para todos os tipos de dados SQL. A tabela também lista o nome e a descrição do tipo de dados correspondente do SQL-92 (se houver).  
  
|Identificador de tipo SQL [1]|Típica de dados do SQL<br /><br /> tipo [2]|Descrição do tipo típico|  
|------------------------------|------------------------------------|------------------------------|  
|SQL_CHAR|CHAR (*n*)|Cadeia de caracteres de comprimento de cadeia de caracteres fixa *n*.|  
|SQL_VARCHAR|VARCHAR (*n*)|Cadeia de caracteres de comprimento variável com um comprimento máximo da cadeia de caracteres *n*.|  
|SQL_LONGVARCHAR|LONG VARCHAR|Dados de caracteres de comprimento variável. Comprimento máximo é – dependente da fonte de dados. [9]|  
|SQL_WCHAR|WCHAR (*n*)|Cadeia de caracteres Unicode de comprimento de cadeia de caracteres fixa *n*|  
|SQL_WVARCHAR|VARWCHAR (*n*)|Cadeia de caracteres de comprimento variável Unicode com um comprimento máximo da cadeia de caracteres *n*|  
|SQL_WLONGVARCHAR|LONGWVARCHAR|Dados de caractere de comprimento variável Unicode. Comprimento máximo é de – dependente da fonte de dados|  
|SQL_DECIMAL|DECIMAL (*p*,*s*)|Assinado, valor numérico exato com precisão de pelo menos *p* e escala *s.* (A precisão máxima é definido pelo driver.) (1 < = *p* < = 15; *s* <= *p*). [ 4]|  
|SQL_NUMERIC|NUMÉRICO (*p*,*s*)|Conectado, o valor numérico exato com precisão *p* e escala *s* (1 < = *p* < = 15; *s* <= *p*). [ 4]|  
|SQL_SMALLINT|SMALLINT|Valor numérico com precisão 5 exato e escala de 0 (assinado: – 32.768 < = *n* < = 32.767, não assinado: 0 < = *n* < = 65.535) [3].|  
_INTEGER|INTEGER|Valor numérico com precisão 10 exato e escala de 0 (assinado: – 2 [31] < = *n* < = 2 [31] – 1, não assinado: 0 < = *n* < = 2 [32] – 1) [3].|  
|SQL_REAL|REAL|Conectado, o valor numérico aproximado com uma precisão de binária 24 (zero ou valor absoluto 10 [–38] para 10[38]).|  
|SQL_FLOAT|FLOAT (*p*)|Assinado, valor numérico aproximado com uma precisão de binária de pelo menos *p*. (A precisão máxima é definido pelo driver.) [5]|  
|SQL_DOUBLE|DOUBLE PRECISION|Conectado, o valor numérico aproximado com uma precisão de binária 53 (zero ou valor absoluto 10 [–308] para 10[308]).|  
|SQL_BIT|BIT|Dados binários de bit único. [8]|  
|SQL_TINYINT|TINYINT|Valor numérico com precisão 3 exato e escala de 0 (assinado: –128 < = *n* < = 127, não assinado: 0 < = *n* < = 255) [3].|  
_BIGINT|bigint|Exato de valor numérico com precisão 19 (se conectado) ou 20 (se não assinado) e a escala de 0 (assinado: – 2 [63] < = *n* < = 2 63 – 1, não assinado: 0 < = *n* < = 2 [64] – 1) [3], [9].|  
|SQL_BINARY|BINÁRIO (*n*)|Dados binários de comprimento fixo *n*. [ 9]|  
|SQL_VARBINARY|VARBINARY (*n*)|Dados binários de comprimento máximo de comprimento variável *n*. O máximo é definido pelo usuário. [9]|  
|SQL_LONGVARBINARY|VARBINARY LONGO|Dados binários de comprimento variável. Comprimento máximo é – dependente da fonte de dados. [9]|  
|SQL_TYPE_DATE [6]|DATE|Ano, mês e dia campos, em conformidade com as regras do calendário gregoriano. (Consulte [restrições do calendário gregoriano](../../../odbc/reference/appendixes/constraints-of-the-gregorian-calendar.md), mais adiante neste apêndice.)|  
|SQL_TYPE_TIME [6]|TEMPO (*p*)|Hora, minuto e segundo campos, com os valores válidos para horas de 00 a 23, os valores válidos para minutos de 00 a 59 e os valores válidos para segundos de 00 a 61. Precisão *p* indica a precisão de segundos.|  
|SQL_TYPE_TIMESTAMP [6]|TIMESTAMP (*p*)|Ano, mês, dia, hora, minuto e segundo campos, com os valores válidos conforme definido para os tipos de dados de data e hora.|  
_TYPE_UTCDATETIME|UTCDATETIME|Campos de ano, mês, dia, hora, minuto, segundo, utchour e utcminute. Os campos utchour e utcminute têm precisão de 1 a 10 microssegundos.|  
|SQL_TYPE_UTCTIME|UTCTIME|Campos de hora, minuto, segundo, utchour e utcminute. Os campos utchour e utcminute têm precisão de 1 a 10 microssegundos.|  
|SQL_INTERVAL_MONTH [7]|INTERVALO de mês (*p*)|Número de meses entre duas datas; *p* é o intervalo de precisão principal.|  
|SQL_INTERVAL_YEAR [7]|ANO de intervalo (*p*)|Número de anos entre duas datas; *p* é o intervalo de precisão principal.|  
|SQL_INTERVAL_YEAR_TO_MONTH [7]|ANO de intervalo (*p*) para o mês|Número de anos e meses entre duas datas; *p* é o intervalo de precisão principal.|  
|SQL_INTERVAL_DAY [7]|DIA de intervalo (*p*)|Número de dias entre duas datas; *p* é o intervalo de precisão principal.|  
|SQL_INTERVAL_HOUR [7]|HORA de intervalo (*p*)|Número de horas entre dois data/horas; *p* é o intervalo de precisão principal.|  
|SQL_INTERVAL_MINUTE [7]|MINUTOS de intervalo (*p*)|Número de minutos entre dois data/horas; *p* é o intervalo de precisão principal.|  
|SQL_INTERVAL_SECOND [7]|INTERVALO de segundo (*p*,*p*)|Número de segundos entre dois data/horas; *p* é o intervalo de precisão principal e *p* é a precisão de segundos de intervalo.|  
_INTERVAL_DAY_TO_HOUR [7]|DIA de intervalo (*p*) hora|Número de dias/horas entre dois data/horas; *p* é o intervalo de precisão principal.|  
|SQL_INTERVAL_DAY_TO_MINUTE [7]|DIA de intervalo (*p*) para o minuto|Número de dias/horas/minutos entre dois data/horas; *p* é o intervalo de precisão principal.|  
|SQL_INTERVAL_DAY_TO_SECOND [7]|DIA de intervalo (*p*) para o segundo (*p*)|Número de dias/horas/minutos/segundos entre dois data/horas; *p* é o intervalo de precisão principal e *p* é a precisão de segundos de intervalo.|  
|SQL_INTERVAL_HOUR_TO_MINUTE [7]|HORA de intervalo (*p*) para o minuto|Número de horas/minutos entre dois data/horas; *p* é o intervalo de precisão principal.|  
|SQL_INTERVAL_HOUR_TO_SECOND [7]|HORA de intervalo (*p*) para o segundo (*p*)|Número de horas/minutos/segundos entre dois data/horas; *p* é o intervalo de precisão principal e *p* é a precisão de segundos de intervalo.|  
_INTERVAL_MINUTE_TO_SECOND [7]|MINUTOS de intervalo (*p*) para o segundo (*p*)|Número de minutos/segundos entre dois data/horas; *p* é o intervalo de precisão principal e *p* é a precisão de segundos de intervalo.|  
|SQL_GUID|GUID|GUID de comprimento fixo.|  
  
 [1] este é o valor retornado na coluna DATA_TYPE por uma chamada para **SQLGetTypeInfo**.  
  
 [2]] este é o valor retornado na coluna Nome e criar parâmetros por uma chamada para **SQLGetTypeInfo**. A coluna de nome retorna a designação — por exemplo, CHAR, enquanto a coluna criar PARAMS retorna uma lista separada por vírgulas dos parâmetros de criação, como a precisão, escala e comprimento.  
  
 [3] um aplicativo usa **SQLGetTypeInfo** ou **SQLColAttribute** para determinar se um determinado tipo de dados ou uma coluna específica em um conjunto de resultados é não assinada.  
  
 [4] tipos de dados SQL_DECIMAL e SQL_NUMERIC diferem apenas em sua precisão. A precisão de um DECIMAL (*p*,*s*) é uma implementação definida precisão decimal é menor do que *p*, enquanto que a precisão de um NUMÉRICO (*p* ,*s*) é exatamente igual ao *p*.  
  
 [5] dependendo da implementação, a precisão de SQL_FLOAT pode ser 24 ou 53: se for 24, o tipo de dados SQL_FLOAT é o mesmo que SQL_REAL; Se for 53, o tipo de dados SQL_FLOAT é o mesmo que SQL_DOUBLE.  
  
 [6] em ODBC 3 *. x*, os tipos de dados de data, hora e carimbo de hora do SQL são SQL_TYPE_DATE, SQL_TYPE_TIME e SQL_TYPE_TIMESTAMP, respectivamente; no ODBC 2. *x*, os tipos de dados são SQL_DATE, SQL_TIME e SQL_TIMESTAMP.  
  
 [7] para obter mais informações sobre os tipos de dados SQL do intervalo, consulte o [tipos de dados de intervalo](../../../odbc/reference/appendixes/interval-data-types.md) seção mais adiante neste apêndice.  
  
 [8] o tipo de dados SQL_BIT tem características diferentes de tipo de BIT em SQL-92.  
  
 [9] este tipo de dados não tem nenhum tipo de dados correspondente no SQL-92.  
  
 Esta seção fornece o exemplo a seguir.  
  
-   [Conjunto de resultados SQLGetTypeInfo de exemplo](../../../odbc/reference/appendixes/example-sqlgettypeinfo-result-set.md)
