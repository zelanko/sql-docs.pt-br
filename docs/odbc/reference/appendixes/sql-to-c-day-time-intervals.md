---
title: 'SQL a C: Intervalos diurnos | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- converting data from SQL to C types [ODBC], day-time intervals
- day-time intervals [ODBC]
- data conversions from SQL to C types [ODBC], day-time intervals
- intervals [ODBC], converting
ms.assetid: 8ea84d69-2292-4128-89a0-f184f68abb98
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1318da5285ba2384dd23e4c235e698aa72c7658e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81296466"
---
# <a name="sql-to-c-day-time-intervals"></a>SQL para C: intervalos de tempo-dia

Os identificadores para os tipos de dados ODBC SQL de intervalo diurno são os seguintes:

- SQL_INTERVAL_DAY
- SQL_INTERVAL_DAY_TO_MINUTE
- SQL_INTERVAL_HOUR
- SQL_INTERVAL_DAY_TO_SECOND
- SQL_INTERVAL_MINUTE
- SQL_INTERVAL_HOUR_TO_MINUTE
- SQL_INTERVAL_SECOND
- SQL_INTERVAL_HOUR_TO_SECOND
- SQL_INTERVAL_DAY_TO_HOUR
- SQL_INTERVAL_MINUTE_TO_SECOND

A tabela a seguir mostra os tipos de dados ODBC C para os quais os dados SQL de intervalo diurno podem ser convertidos. Para obter uma explicação das colunas e termos da tabela, consulte [Convertendo Dados de SQL para C Tipos de Dados](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md).

|Identificador de tipo C|Teste|**TargetValuePtr*|**Strlen_or_indptr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|Todos os tipos de intervalo C diurno|Porção de campos de arrasto não truncados<br /><br /> Porção de campos de arrasto truncados<br /><br /> A precisão líder do alvo não é grande o suficiente para conter dados da fonte|Dados<br /><br /> Dados truncados<br /><br /> Indefinido|Duração dos dados<br /><br /> Duração dos dados<br /><br /> Indefinido|n/d<br /><br /> 01S07<br /><br /> 22015|  
|SQL_C_STINYINT[b] SQL_C_UTINYINT[b] SQL_C_USHORT[b] SQL_C_SHORT[b] SQL_C_SLONG[b] SQL_C_ULONG[b] SQL_C_NUMERIC[b] SQL_C_BIGINT[b]|A precisão do intervalo era um único campo e os dados foram convertidos sem truncação<br /><br /> Precisão de intervalo foi um único campo e truncado fracionado<br /><br /> Precisão de intervalo era um único campo e truncado inteiro<br /><br /> A precisão do intervalo não era um único campo|Dados<br /><br /> Dados truncados<br /><br /> Dados truncados<br /><br /> Indefinido|Tamanho do tipo de dados C<br /><br /> Duração dos dados<br /><br /> Duração dos dados<br /><br /> Tamanho do tipo de dados C|n/d<br /><br /> 01S07<br /><br /> 22003<br /><br /> 07006|  
|SQL_C_BINARY|Comprimento de byte de dados <= *BufferLength*<br /><br /> Comprimento de byte de dados > *BufferLength*|Dados<br /><br /> Indefinido|Duração dos dados<br /><br /> Indefinido|n/d<br /><br /> 22003|  
|SQL_C_CHAR|Comprimento do byte do caractere < *BufferLength*<br /><br /> Número de dígitos inteiros (em oposição ao fracionado) < *BufferLength*<br /><br /> Número de dígitos inteiros (em oposição ao fracionado) >= *BufferLength*|Dados<br /><br /> Dados truncados<br /><br /> Indefinido|Tamanho do tipo de dados C<br /><br /> Tamanho do tipo de dados C<br /><br /> Indefinido|n/d<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_WCHAR|Comprimento do caractere < *BufferLength*<br /><br /> Número de dígitos inteiros (em oposição ao fracionado) < *BufferLength*<br /><br /> Número de dígitos inteiros (em oposição ao fracionado) >= *BufferLength*|Dados<br /><br /> Dados truncados<br /><br /> Indefinido|Tamanho do tipo de dados C<br /><br /> Tamanho do tipo de dados C<br /><br /> Indefinido|n/d<br /><br /> 01004<br /><br /> 22003|  
  
 [a] Um tipo SQL de intervalo diurno pode ser convertido para qualquer tipo de intervalo diurno C.  
  
 [b] Se a precisão do intervalo for um único campo (um de DIA, HORA, MINUTO ou SEGUNDO), o tipo SQL de intervalo pode ser convertido para qualquer numérico exato (SQL_C_STINYINT, SQL_C_UTINYINT, SQL_C_USHORT, SQL_C_SHORT, SQL_C_SLONG, SQL_C_ULONG ou SQL_C_NUMERIC).  
  
A conversão padrão de um tipo SQL de intervalo é para o tipo de dados de intervalo C correspondente. Em seguida, o aplicativo vincula a coluna ou parâmetro (ou define o campo SQL_DESC_DATA_PTR no registro apropriado do ARD) para apontar para a estrutura de SQL_INTERVAL_STRUCT inicializada (ou passa um ponteiro para a estrutura SQL_ INTERVAL_STRUCT como o argumento *TargetValuePtr* em uma chamada para **SQLGetData**).  
  
O exemplo a seguir demonstra como transferir dados de uma coluna de tipo SQL_INTERVAL_DAY_TO_MINUTE para a estrutura SQL_INTERVAL_STRUCT de tal forma que ele volte como um intervalo DAY_TO_HOUR.  

```cpp
SQL_INTERVAL_STRUCT is;  
SQLINTEGER    cbValue;  
SQLUINTEGER   days, hours;  
  
// Execute a select statement; "interval_column" is a column  
// whose data type is SQL_INTERVAL_DAY_TO_MINUTE.  
SQLExecDirect(hstmt, "SELECT interval_column FROM table", SQL_NTS);  
  
// Bind  
SQLBindCol(hstmt, 1, SQL_C_INTERVAL_DAY_TO_MINUTE, &is, sizeof(SQL_INTERVAL_STRUCT), &cbValue);  
  
// Fetch  
SQLFetch(hstmt);  
  
// Process data  
days = is.intval.day_second.day;  
hours = is.intval.day_second.hour;  
```
