---
title: 'SQL to C: intervalos de tempo de dia | Microsoft Docs'
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: db39751059d84e4e3a7950acbbbcb7f1a2b0b00d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68056864"
---
# <a name="sql-to-c-day-time-intervals"></a>SQL para C: intervalos de tempo-dia

Os identificadores para os tipos de dados SQL ODBC do intervalo de tempo de dia são os seguintes:

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

A tabela a seguir mostra os tipos de dados ODBC C para os quais os dados SQL do intervalo de tempo de dia podem ser convertidos. Para obter uma explicação das colunas e dos termos na tabela, consulte [convertendo dados de SQL para tipos de dados C](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md).

|Identificador de tipo C|Teste|**TargetValuePtr*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|Todos os tipos de intervalo de C de dia-hora|Parte dos campos à direita não truncada<br /><br /> Parte dos campos à direita truncada<br /><br /> A precisão inicial do destino não é grande o suficiente para manter os dados da origem|data<br /><br /> Dados truncados<br /><br /> Indefinido|Comprimento dos dados<br /><br /> Comprimento dos dados<br /><br /> Indefinido|n/d<br /><br /> 01S07<br /><br /> 22015|  
|SQL_C_STINYINT [b] SQL_C_UTINYINT [b] SQL_C_USHORT [b] SQL_C_SHORT [b] SQL_C_SLONG [b] SQL_C_ULONG [b] SQL_C_NUMERIC [b] SQL_C_BIGINT [b]|A precisão do intervalo era um único campo e os dados foram convertidos sem truncamento<br /><br /> A precisão do intervalo era um único campo e uma fração truncada<br /><br /> A precisão do intervalo era um único campo e um todo truncado<br /><br /> A precisão do intervalo não era um campo único|data<br /><br /> Dados truncados<br /><br /> Dados truncados<br /><br /> Indefinido|Tamanho do tipo de dados C<br /><br /> Comprimento dos dados<br /><br /> Comprimento dos dados<br /><br /> Tamanho do tipo de dados C|n/d<br /><br /> 01S07<br /><br /> 22003<br /><br /> 07006|  
|SQL_C_BINARY|Comprimento de bytes de dados <= *BufferLength*<br /><br /> Comprimento de bytes de dados > *BufferLength*|data<br /><br /> Indefinido|Comprimento dos dados<br /><br /> Indefinido|n/d<br /><br /> 22003|  
|SQL_C_CHAR|Comprimento de bytes de caracteres < *BufferLength*<br /><br /> Número de dígitos inteiros (em oposição a fracionários) < *BufferLength*<br /><br /> Número de dígitos inteiros (em oposição a fracionários) >= *BufferLength*|data<br /><br /> Dados truncados<br /><br /> Indefinido|Tamanho do tipo de dados C<br /><br /> Tamanho do tipo de dados C<br /><br /> Indefinido|n/d<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_WCHAR|Comprimento do caractere < *BufferLength*<br /><br /> Número de dígitos inteiros (em oposição a fracionários) < *BufferLength*<br /><br /> Número de dígitos inteiros (em oposição a fracionários) >= *BufferLength*|data<br /><br /> Dados truncados<br /><br /> Indefinido|Tamanho do tipo de dados C<br /><br /> Tamanho do tipo de dados C<br /><br /> Indefinido|n/d<br /><br /> 01004<br /><br /> 22003|  
  
 [a] um tipo SQL de intervalo de tempo de dia pode ser convertido em qualquer tipo de intervalo de dia C.  
  
 [b] se a precisão do intervalo for um único campo (um dos dias, hora, minuto ou segundo), o tipo SQL do intervalo poderá ser convertido em qualquer numérico exato (SQL_C_STINYINT, SQL_C_UTINYINT, SQL_C_USHORT, SQL_C_SHORT, SQL_C_SLONG, SQL_C_ULONG ou SQL_C_NUMERIC).  
  
A conversão padrão de um tipo SQL de intervalo é para o tipo de dados de intervalo de C correspondente. Em seguida, o aplicativo associa a coluna ou o parâmetro (ou define o campo SQL_DESC_DATA_PTR no registro apropriado do ARD) para apontar para a estrutura de SQL_INTERVAL_STRUCT inicializada (ou passa um ponteiro para a estrutura de INTERVAL_STRUCT SQL_ como o argumento *TargetValuePtr* em uma chamada para **SQLGetData**).  
  
O exemplo a seguir demonstra como transferir dados de uma coluna do tipo SQL_INTERVAL_DAY_TO_MINUTE para a estrutura de SQL_INTERVAL_STRUCT de forma que ele volte como um intervalo de DAY_TO_HOUR.  

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
