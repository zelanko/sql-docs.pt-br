---
title: 'C para SQL: Intervalos de tempo do dia | Microsoft Docs'
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a3a4df236273b5afcaba78052ac236669bb133f0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68019367"
---
# <a name="c-to-sql-day-time-intervals"></a>C para SQL: Intervalos de dia-horário
Os identificadores para os tipos de dados do ODBC C de intervalo de tempo do dia são:  
  
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
  
 A tabela a seguir mostra o ODBC do SQL para o qual o intervalo de dados C pode ser convertido de tipos de dados. Para obter uma explicação das colunas e os termos na tabela, consulte [conversão de dados do C para tipos de dados SQL](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md).  
  
|Identificador de tipo SQL|Teste|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHAR[a]<br /><br /> SQL_VARCHAR[a]<br /><br /> SQL_LONGVARCHAR[a]|Comprimento de bytes da coluna > = comprimento de byte do caractere<br /><br /> Comprimento de bytes da coluna < caracteres de comprimento de bytes [a]<br /><br /> Valor de dados não é um literal de intervalo válido|n/d<br /><br /> 22001<br /><br /> 22015|  
|SQL_WCHAR[a]<br /><br /> SQL_WVARCHAR[a]<br /><br /> SQL_WLONGVARCHAR[a]|Comprimento de caracteres da coluna > = comprimento de caracteres de dados<br /><br /> Comprimento de caracteres da coluna < caracteres de comprimento de dados [a]<br /><br /> Valor de dados não é um literal de intervalo válido|n/d<br /><br /> 22001<br /><br /> 22015|  
|SQL_TINYINT[b]<br /><br /> SQL_SMALLINT[b] SQL_INTEGER[b]<br /><br /> SQL_BIGINT[b] SQL_NUMERIC[b]<br /><br /> SQL_DECIMAL[b]|Conversão de um único campo de intervalo não resultou em truncamento de dígitos inteiros<br /><br /> Conversão resultou em truncamento de dígitos inteiros|n/d<br /><br /> 22003|  
|SQL_INTERVAL_DAY<br /><br /> SQL_INTERVAL_HOUR<br /><br /> SQL_INTERVAL_MINUTE<br /><br /> SQL_INTERVAL_SECOND<br /><br /> SQL_INTERVAL_DAY_TO_HOUR<br /><br /> SQL_INTERVAL_DAY_TO_MINUTE<br /><br /> SQL_INTERVAL_DAY_TO_SECOND<br /><br /> SQL_INTERVAL_HOUR_TO_MINUTE<br /><br /> SQL_INTERVAL_HOUR_TO_SECOND<br /><br /> SQL_INTERVAL_MINUTE_TO_SECOND|Valor de dados foi convertido sem truncamento de todos os campos<br /><br /> Um ou mais campos de valor de dados foram truncados durante conversão|n/d<br /><br /> 22015|  
  
 [a] tipos de dados de intervalo de todos os C podem ser convertido em um tipo de dados de caractere.  
  
 [b] se o campo de tipo na estrutura de intervalo é, de modo que o intervalo é de um único campo (SQL_DAY, SQL_HOUR, SQL_MINUTE ou SQL_SECOND), o intervalo de tipo C pode ser convertido em qualquer numérico exato (SQL_TINYINT, SQL_SMALLINT, SQL_INTEGER, SQL_BIGINT SQL_DECIMAL ou SQL_NUMERIC).  
  
 A conversão de padrão de um tipo de intervalo de C é o intervalo de tempo-dia tipo SQL correspondente.  
  
 O driver ignora o valor de comprimento/indicador ao converter dados do tipo de dados de intervalo de C e pressupõe que o tamanho do buffer de dados é o tamanho do tipo de dados C de intervalo. O valor de comprimento/indicador é passado a *StrLen_or_Ind* argumento na **SQLPutData** e no buffer especificado com o *StrLen_or_IndPtr* argumento **SQLBindParameter**. O buffer de dados é especificado com o *DataPtr* argumento **SQLPutData** e o *ParameterValuePtr* argumento em **SQLBindParameter**.  
  
 O exemplo a seguir demonstra como enviar dados de intervalo C armazenados na estrutura de SQL_INTERVAL_STRUCT em uma coluna de banco de dados. A estrutura de intervalo contém um intervalo de DAY_TO_SECOND. ele será armazenado em uma coluna de banco de dados do tipo SQL_INTERVAL_DAY_TO_MINUTE.  
  
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
