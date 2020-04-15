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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3cc91213533aa39f30be1bc838cc014c20e70884
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305000"
---
# <a name="sql-data-types"></a>Tipos de dados SQL
Cada DBMS define seus próprios tipos de SQL. Cada driver ODBC expõe apenas os tipos de dados SQL que o DBMS associado define. Informações sobre como um driver mapeia os tipos De SQL DBMS para os identificadores de tipo SQL definidos pelo ODBC e como um driver mapeia os tipos De SQL para seus próprios identificadores de tipo SQL específicos para o driver são retornados através de uma chamada para **SQLGetTypeInfo**. Um driver também retorna os tipos de dados SQL ao descrever os tipos de dados de colunas e parâmetros através de chamadas para **SQLColAttribute,** **SQLColumns,** **SQLDescribeCol,** **SQLDescribeParam,** **SQLProcedureColumns**e **SQLSpecialColumns**.  
  
> [!NOTE]  
>  Os tipos de dados SQL estão contidos nos campos de CONCISE_TYPE, SQL_DESC_TYPE e SQL_DESC_DATETIME_INTERVAL_CODE SQL_DESC_ dos descritores de implementação. As características dos tipos de dados SQL estão contidas nos campos SQL_DESC_PRECISION, SQL_DESC_SCALE, SQL_DESC_LENGTH e SQL_DESC_OCTET_LENGTH dos descritores de implementação. Para obter mais informações, consulte [Identificadores e Descritores de tipo de dados](../../../odbc/reference/appendixes/data-type-identifiers-and-descriptors.md) mais tarde neste apêndice.  
  
 Um determinado driver e uma fonte de dados não suportam necessariamente todos os tipos de dados SQL definidos neste apêndice. O suporte de um driver para tipos de dados SQL depende do nível de SQL-92 que o driver cumpre. Para determinar o nível de gramática SQL-92 suportada pelo driver, um aplicativo chama **SQLGetInfo** com o tipo de informação SQL_SQL_CONFORMANCE. Além disso, um determinado driver e uma fonte de dados podem suportar tipos adicionais de dados SQL específicos para o driver. Para determinar quais tipos de dados um driver suporta, um aplicativo chama **SQLGetTypeInfo**. Para obter informações sobre os tipos de dados SQL específicos do driver, consulte a documentação do motorista. Para obter informações sobre os tipos de dados em uma fonte de dados específica, consulte a documentação dessa fonte de dados.  
  
> [!IMPORTANT]  
>  As tabelas ao longo deste apêndice são apenas diretrizes e mostram nomes, intervalos e limites tipicamente usados dos tipos de dados SQL. Uma determinada fonte de dados pode suportar apenas alguns dos tipos de dados listados, e as características dos tipos de dados suportados podem diferir daqueles listados.  
  
 A tabela a seguir lista identificadores de tipo SQL válidos para todos os tipos de dados SQL. A tabela também lista o nome e a descrição do tipo de dados correspondentes do SQL-92 (se existir).  
  
|Identificador do tipo SQL[1]|Dados típicos de SQL<br /><br /> tipo[2]|Descrição típica do tipo|  
|------------------------------|------------------------------------|------------------------------|  
|SQL_CHAR|CHAR(*n*)|Seqüência de caracteres de comprimento de corda fixa *n*.|  
|SQL_VARCHAR|VARCHAR*n*|Seqüência de caracteres de comprimento variável com um comprimento máximo de seqüência *n*.|  
|SQL_LONGVARCHAR|LONG VARCHAR|Dados de caractere de comprimento variável. O comprimento máximo é dependente da fonte de dados. [9]|  
|SQL_WCHAR|WCHAR(*n*)|Seqüência de caracteres Unicode de comprimento de seqüência de string fixa *n*|  
|SQL_WVARCHAR|VARWCHAR*n*|Seqüência de caracteres de comprimento variável unicode com um comprimento máximo de seqüência *n*|  
|SQL_WLONGVARCHAR|LONGWVARCHAR|Dados de caractere Unicode de comprimento variável. O comprimento máximo é dependente da fonte de dados|  
|SQL_DECIMAL|DECIMAL(*p,**s*)|Valor assinado, exato, numérico com uma precisão de pelo menos *p* e escala *s.* (A precisão máxima é definida pelo driver.) (1 <= *<p* = 15; *s* <= *p*). [4]|  
|SQL_NUMERIC|NUMERIC(*p,**s*)|Valor numérico assinado, exato e numérico com precisão *p* e escala *s* (1 <= *p* <= 15; *s* <= *p*). [4]|  
|SQL_SMALLINT|SMALLINT|Valor numérico exato com precisão 5 e escala 0 (assinado: -32.768 <= *n* <= 32.767, não assinado: 0 <= *n* <= 65.535)[3].|  
|SQL_INTEGER|INTEGER|Valor numérico exato com precisão 10 e escala 0 (assinado: -2[31] <= *n* <= 2[31] - 1, não assinado: 0 <= *n* <= 2[32] - 1)[3].|  
|SQL_REAL|real|Valor numérico assinado, aproximado, com precisão binária 24 (valor zero ou absoluto 10[-38] a 10[38]).|  
|SQL_FLOAT|FLOAT *(p)*|Valor numérico assinado, aproximado, com precisão binária de pelo menos *p*. (A precisão máxima é definida pelo driver.) [5]|  
|SQL_DOUBLE|DOUBLE PRECISION|Valor numérico assinado, aproximado, com precisão binária 53 (valor zero ou absoluto 10[-308] a 10[308]).|  
|SQL_BIT|BIT|Dados binários de um único bit. [8]|  
|SQL_TINYINT|TINYINT|Valor numérico exato com precisão 3 e escala 0 (assinado: -128 <= *n* <= 127, não assinado: 0 <= *n* <= 255)[3].|  
|SQL_BIGINT|bigint|Valor numérico exato com precisão 19 (se assinado) ou 20 (se não assinado) e escala 0 (assinado: -2[63] <= *n* <= 2[63] - 1, não assinado: 0 <= *n* <= 2[64] - 1][3],[9].|  
|SQL_BINARY|BINÁRIO(*n*)|Dados binários de comprimento fixo *n*. [9]|  
|SQL_VARBINARY|VARBINARY(*n)*|Dados binários de comprimento variável de comprimento máximo *n*. O máximo é definido pelo usuário. [9]|  
|SQL_LONGVARBINARY|VARBINARY LONGO|Dados binários de comprimento variável. O comprimento máximo é dependente da fonte de dados. [9]|  
|SQL_TYPE_DATE[6]|DATE|Ano, mês e campos diurnos, de acordo com as regras do calendário gregoriano. (Veja [as restrições do calendário gregoriano](../../../odbc/reference/appendixes/constraints-of-the-gregorian-calendar.md), mais tarde neste apêndice.)|  
|SQL_TYPE_TIME[6]|TIME(*p)*|Dias, minuto e segundo campos, com valores válidos para horas de 00 a 23, valores válidos para minutos de 00 a 59, e valores válidos para segundos de 00 a 61. Precisão *p* indica a precisão dos segundos.|  
|SQL_TYPE_TIMESTAMP[6]|CARIMBO DE TEMPO *(p)*|Ano, mês, dia, hora, minuto e segundo campos, com valores válidos definidos para os tipos de dados DATA e HORA.|  
|SQL_TYPE_UTCDATETIME|Utcdatetime|Ano, mês, dia, hora, minuto, segundo, utchour, e campos de utcminute. Os campos utchour e utcminute têm precisão de 1/10 microssegundos.|  
|SQL_TYPE_UTCTIME|UTCTIME|Hora, minuto, segundo, utchour, e campos de utcminute. Os campos utchour e utcminute têm precisão de 1/10 microssegundos.|  
|SQL_INTERVAL_MONTH[7]|MÊS DE INTERVALO(*p)*|Número de meses entre duas datas; *p* é o intervalo de precisão de liderança.|  
|SQL_INTERVAL_YEAR[7]|ANO-INTERVALO(*p)*|Número de anos entre duas datas; *p* é o intervalo de precisão de liderança.|  
|SQL_INTERVAL_YEAR_TO_MONTH[7]|ANO-INTERVALO(*p*) A MÊS|Número de anos e meses entre duas datas; *p* é o intervalo de precisão de liderança.|  
|SQL_INTERVAL_DAY[7]|DIA DO INTERVALO(*p)*|Número de dias entre duas datas; *p* é o intervalo de precisão de liderança.|  
|SQL_INTERVAL_HOUR[7]|HORA DO INTERVALO(*p)*|Número de horas entre duas datas/horários; *p* é o intervalo de precisão de liderança.|  
|SQL_INTERVAL_MINUTE[7]|MINUTO DO INTERVALO *(p)*|Número de minutos entre duas datas/horários; *p* é o intervalo de precisão de liderança.|  
|SQL_INTERVAL_SECOND[7]|INTERVALO SEGUNDO (*p,**q*)|Número de segundos entre duas datas/horários; *p* é o intervalo de precisão líder e *q* é a precisão de segundos de intervalo.|  
|SQL_INTERVAL_DAY_TO_HOUR[7]|DIA DO INTERVALO(*p)* A HORA|Número de dias/horas entre duas datas/horários; *p* é o intervalo de precisão de liderança.|  
|SQL_INTERVAL_DAY_TO_MINUTE[7]|DIA DO INTERVALO(*p*) PARA MINUTO|Número de dias/horas/minutos entre duas datas/horários; *p* é o intervalo de precisão de liderança.|  
|SQL_INTERVAL_DAY_TO_SECOND[7]|DIA DO INTERVALO(*p*) PARA Segundo *(q*)|Número de dias/horas/minutos/segundos entre duas datas/horários; *p* é o intervalo de precisão líder e *q* é a precisão de segundos de intervalo.|  
|SQL_INTERVAL_HOUR_TO_MINUTE[7]|HORA DO*INTERVALO(p)* PARA MINUTO|Número de horas/minutos entre duas datas/horários; *p* é o intervalo de precisão de liderança.|  
|SQL_INTERVAL_HOUR_TO_SECOND[7]|HORA DO INTERVALO(*p*) Para Segundo *(q*)|Número de horas/minutos/segundos entre duas datas/horários; *p* é o intervalo de precisão líder e *q* é a precisão de segundos de intervalo.|  
|SQL_INTERVAL_MINUTE_TO_SECOND[7]|MINUTO DO*INTERVALO(p)* PARA Segundo *(q*)|Número de minutos/segundos entre duas datas/horários; *p* é o intervalo de precisão líder e *q* é a precisão de segundos de intervalo.|  
|SQL_GUID|GUID|GUID de comprimento fixo.|  
  
 [1] Este é o valor devolvido na coluna DATA_TYPE por uma chamada para **SQLGetTypeInfo**.  
  
 [2] Este é o valor retornado na coluna NAME e CREATE PARAMS por uma chamada para **SQLGetTypeInfo**. A coluna NAME retorna a designação - por exemplo, CHAR-enquanto a coluna CREATE PARAMS retorna uma lista separada por comuma de parâmetros de criação, como precisão, escala e comprimento.  
  
 [3] Um aplicativo usa **SQLGetTypeInfo** ou **SQLColAttribute** para determinar se um determinado tipo de dados ou uma determinada coluna em um conjunto de resultados não está assinado.  
  
 [4] SQL_DECIMAL e SQL_NUMERIC tipos de dados diferem apenas em sua precisão. A precisão de um DECIMAL*é*uma precisão decimal definida pela implementação que não é inferior a *p,* enquanto a precisão de um NUMERIC *(p,**s)* é exatamente igual a *p.**s*  
  
 [5] Dependendo da implementação, a precisão do SQL_FLOAT pode ser de 24 ou 53: se for 24, o SQL_FLOAT tipo de dados é o mesmo que SQL_REAL; se for 53, o SQL_FLOAT tipo de dados é o mesmo que SQL_DOUBLE.  
  
 [6] No ODBC *3.x*, os tipos de dados de data, hora e carimbo de data sql são SQL_TYPE_DATE, SQL_TYPE_TIME e SQL_TYPE_TIMESTAMP, respectivamente; em ODBC *2.x*, os tipos de dados são SQL_DATE, SQL_TIME e SQL_TIMESTAMP.  
  
 [7] Para obter mais informações sobre os tipos de dados SQL de intervalo, consulte a seção [Tipos de dados de intervalo,](../../../odbc/reference/appendixes/interval-data-types.md) mais tarde neste apêndice.  
  
 [8] O SQL_BIT tipo de dados tem características diferentes do tipo BIT no SQL-92.  
  
 [9] Este tipo de dados não tem nenhum tipo de dados correspondente no SQL-92.  
  
 Esta seção fornece o seguinte exemplo.  
  
-   [Conjunto de resultados SQLGetTypeInfo de exemplo](../../../odbc/reference/appendixes/example-sqlgettypeinfo-result-set.md)
