---
title: 'SQL para c: Intervalos de tempo do dia | Microsoft Docs'
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
manager: craigg
ms.openlocfilehash: ee08f42a4ccd7eb51f45e1654f20e264f80c49d2
ms.sourcegitcommit: 480961f14405dc0b096aa8009855dc5a2964f177
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/22/2019
ms.locfileid: "54420031"
---
# <a name="sql-to-c-day-time-intervals"></a>SQL para c: Intervalos de tempo do dia

Os identificadores para os tipos de dados SQL ODBC intervalo de tempo do dia são os seguintes:

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

A tabela a seguir mostra os tipos de dados ao qual o intervalo de tempo-dia de dados do SQL pode ser convertido de ODBC C. Para obter uma explicação das colunas e os termos na tabela, consulte [conversão de dados do SQL para tipos de dados C](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md).

|Identificador de tipo C|Teste|**TargetValuePtr*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|Todos os tipos de intervalo de C de tempo-dia|Parte de campos à direita não truncado<br /><br /> Parte de campos à direita truncado<br /><br /> A precisão do destino inicial não é grande o suficiente para manter os dados de origem|Dados<br /><br /> Dados truncados<br /><br /> Indefinido|Comprimento dos dados<br /><br /> Comprimento dos dados<br /><br /> Indefinido|n/d<br /><br /> 01S07<br /><br /> 22015|  
|SQL_C_STINYINT[b] SQL_C_UTINYINT[b] SQL_C_USHORT[b] SQL_C_SHORT[b] SQL_C_SLONG[b] SQL_C_ULONG[b] SQL_C_NUMERIC[b] SQL_C_BIGINT[b]|Precisão de intervalo foi um único campo e os dados foi convertidos sem truncamento<br /><br /> Precisão de intervalo era um único campo e truncado fracionário<br /><br /> Precisão de intervalo foi um único campo e truncado para inteiros<br /><br /> Precisão de intervalo não era um único campo|Dados<br /><br /> Dados truncados<br /><br /> Dados truncados<br /><br /> Indefinido|Tamanho do tipo de dados C<br /><br /> Comprimento dos dados<br /><br /> Comprimento dos dados<br /><br /> Tamanho do tipo de dados C|n/d<br /><br /> 01S07<br /><br /> 22003<br /><br /> 07006|  
|SQL_C_BINARY|Comprimento de bytes de dados < = *BufferLength*<br /><br /> Comprimento de bytes de dados > *BufferLength*|Dados<br /><br /> Indefinido|Comprimento dos dados<br /><br /> Indefinido|n/d<br /><br /> 22003|  
|SQL_C_CHAR|Bytes de comprimento de caracteres < *BufferLength*<br /><br /> Número de dígitos de inteiro (em vez de fracionários) < *BufferLength*<br /><br /> Número de dígitos de inteiro (em vez de fracionários) > = *BufferLength*|Dados<br /><br /> Dados truncados<br /><br /> Indefinido|Tamanho do tipo de dados C<br /><br /> Tamanho do tipo de dados C<br /><br /> Indefinido|n/d<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_WCHAR|Comprimento de caracteres < *BufferLength*<br /><br /> Número de dígitos de inteiro (em vez de fracionários) < *BufferLength*<br /><br /> Número de dígitos de inteiro (em vez de fracionários) > = *BufferLength*|Dados<br /><br /> Dados truncados<br /><br /> Indefinido|Tamanho do tipo de dados C<br /><br /> Tamanho do tipo de dados C<br /><br /> Indefinido|n/d<br /><br /> 01004<br /><br /> 22003|  
  
 [a] intervalo de tempo-dia de um tipo SQL pode ser convertido em qualquer tipo de intervalo de tempo-dia C.  
  
 [b] se a precisão de intervalo é um único campo (um do dia, hora, minuto ou segundo), o intervalo de tipo SQL pode ser convertido em qualquer numérico exato (SQL_C_STINYINT, SQL_C_UTINYINT, SQL_C_USHORT, SQL_C_SHORT, SQL_C_SLONG, SQL_C_ULONG ou SQL_C_NUMERIC).  
  
A conversão padrão de um intervalo de tipo de SQL é o tipo de dados de intervalo de C correspondente. O aplicativo, em seguida, associa a coluna ou parâmetro (ou define o campo SQL_DESC_DATA_PTR no registro apropriado da descartar) para apontar para a estrutura SQL_INTERVAL_STRUCT inicializada (ou passa um ponteiro para a estrutura de SQL _ INTERVAL_STRUCT como o *TargetValuePtr* argumento em uma chamada para **SQLGetData**).  
  
O exemplo a seguir demonstra como transferir dados de uma coluna de tipo SQL_INTERVAL_DAY_TO_MINUTE na estrutura SQL_INTERVAL_STRUCT, de modo que se trata de volta como um intervalo DAY_TO_HOUR.  

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
