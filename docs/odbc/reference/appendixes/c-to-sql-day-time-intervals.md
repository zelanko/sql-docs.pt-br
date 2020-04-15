---
title: 'C a SQL: Intervalos diurnos | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- day-time intervals [ODBC]
- data conversions from C to SQL types [ODBC], day-time intervals
- converting data from c to SQL types [ODBC], day-time intervals
- intervals [ODBC], converting
ms.assetid: f9ee1ddb-dec7-4f78-b6e2-5ba34e7d6f59
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1c3f7efb443b442d44a94cfd43629cdaedd6195b
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81291916"
---
# <a name="c-to-sql-day-time-intervals"></a>C para SQL: intervalos de tempo-dia
Os identificadores para os tipos de dados ODBC C do intervalo diurno são:  
  
 SQL_C_INTERVAL_DAY  
  
 SQL_C_INTERVAL_HOUR  
  
 SQL_C_INTERVAL_MINUTE  
  
 SQL_C_INTERVAL_SECOND  
  
 SQL_C_INTERVAL_DAY_TO_HOUR  
  
 SQL_C_INTERVAL_DAY_TO_MINUTE  
  
 SQL_C_INTERVAL_DAY_TO_SECOND  
  
 SQL_C_INTERVAL_HOUR_TO_MINUTE  
  
 SQL_C_INTERVAL_HOUR_TO_SECOND  
  
 SQL_C_INTERVAL_MINUTE_TO_SECOND  
  
 A tabela a seguir mostra os tipos de dados ODBC SQL para os quais os dados do intervalo C podem ser convertidos. Para obter uma explicação das colunas e termos da tabela, consulte [Convertendo Dados de C para Tipos de Dados SQL](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md).  
  
|Identificador tipo SQL|Teste|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHAR[a]<br /><br /> SQL_VARCHAR[a]<br /><br /> SQL_LONGVARCHAR[a]|Comprimento do byte da coluna >= Comprimento do byte do caractere<br /><br /> Comprimento do byte da coluna < comprimento do byte do personagem[a]<br /><br /> O valor dos dados não é um intervalo válido literal|n/d<br /><br /> 22001<br /><br /> 22015|  
|SQL_WCHAR[a]<br /><br /> SQL_WVARCHAR[a]<br /><br /> SQL_WLONGVARCHAR[a]|Comprimento do caractere da coluna >= Comprimento do caractere dos dados<br /><br /> Comprimento do caractere da coluna < comprimento do caractere dos dados[a]<br /><br /> O valor dos dados não é um intervalo válido literal|n/d<br /><br /> 22001<br /><br /> 22015|  
|SQL_TINYINT[b]<br /><br /> SQL_SMALLINT[b] SQL_INTEGER[b]<br /><br /> SQL_BIGINT[b] SQL_NUMERIC[b]<br /><br /> SQL_DECIMAL[b]|A conversão de um intervalo de campo único não resultou em truncação de dígitos inteiros<br /><br /> A conversão resultou em truncação de dígitos inteiros|n/d<br /><br /> 22003|  
|SQL_INTERVAL_DAY<br /><br /> SQL_INTERVAL_HOUR<br /><br /> SQL_INTERVAL_MINUTE<br /><br /> SQL_INTERVAL_SECOND<br /><br /> SQL_INTERVAL_DAY_TO_HOUR<br /><br /> SQL_INTERVAL_DAY_TO_MINUTE<br /><br /> SQL_INTERVAL_DAY_TO_SECOND<br /><br /> SQL_INTERVAL_HOUR_TO_MINUTE<br /><br /> SQL_INTERVAL_HOUR_TO_SECOND<br /><br /> SQL_INTERVAL_MINUTE_TO_SECOND|O valor dos dados foi convertido sem truncação de quaisquer campos<br /><br /> Um ou mais campos de valor de dados foram truncados durante a conversão|n/d<br /><br /> 22015|  
  
 [a] Todos os tipos de dados de intervalo C podem ser convertidos em um tipo de dados de caracteres.  
  
 [b] Se o tipo de campo na estrutura do intervalo for tal que o intervalo seja um único campo (SQL_DAY, SQL_HOUR, SQL_MINUTE ou SQL_SECOND), o tipo C do intervalo pode ser convertido para qualquer numérico exato (SQL_TINYINT, SQL_SMALLINT, SQL_INTEGER, SQL_BIGINT, SQL_DECIMAL ou SQL_NUMERIC).  
  
 A conversão padrão de um tipo de intervalo C é para o tipo SQL de intervalo diurno correspondente.  
  
 O driver ignora o valor de comprimento/indicador ao converter dados do tipo de dados do intervalo C e assume que o tamanho do buffer de dados é o tamanho do tipo de dados do intervalo C. O valor de comprimento/indicador é passado no argumento *StrLen_or_Ind* no **SQLPutData** e no buffer especificado com o *argumento StrLen_or_IndPtr* no **SQLBindParameter**. O buffer de dados é especificado com o argumento *DataPtr* no **SQLPutData** e o argumento *ParameterValuePtr* no **SQLBindParameter**.  
  
 O exemplo a seguir demonstra como enviar dados do intervalo C armazenados na estrutura SQL_INTERVAL_STRUCT em uma coluna de banco de dados. A estrutura do intervalo contém um intervalo de DAY_TO_SECOND; ele será armazenado em uma coluna de banco de dados de tipo SQL_INTERVAL_DAY_TO_MINUTE.  
  
```  
SQL_INTERVAL_STRUCT is;  
SQLINTEGER cbValue;  
  
// Initialize the interval struct to contain the DAY_TO_SECOND  
// interval "154 days, 22 hours, 44 minutes, and 10 seconds"  
is.intval.day_second.day      = 154;  
is.intval.day_second.hour     = 22;  
is.intval.day_second.minute   = 44;  
is.intval.day_second.second   = 10;  
is.interval_sign              = SQL_FALSE;  
  
// Bind the dynamic parameter  
SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_INTERVAL_DAY_TO_SECOND,  
                  SQL_INTERVAL_DAY_TO_MINUTE, 0, 0, &is,  
                  sizeof(SQL_INTERVAL_STRUCT), &cbValue);  
  
// Execute an insert statement; "interval_column" is a column  
// whose data type is SQL_INTERVAL_DAY_TO_MINUTE.  
SQLExecDirect(hstmt,"INSERT INTO table(interval_column) VALUES (?)",SQL_NTS);  
```
