---
title: Data, hora e literais de carimbo de hora | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- escape sequences [ODBC], literals
ms.assetid: 2b42a52a-6353-494c-a179-3a7533cd729f
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: aa7fb107e67d529c656a49b271744757a1a73746
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47651314"
---
# <a name="date-time-and-timestamp-literals"></a>Data, hora e literais de carimbo de data/hora
É a sequência de escape para literais de data, hora e carimbo de hora  
  
 **{***-tipo* **'** *valor* **'}**   
  
 em que *tipo literal* é um dos valores listado na tabela a seguir.  
  
|*tipo de literal*|Significado|Formato de *valor*|  
|---------------------|-------------|-----------------------|  
|**d**|data|*yyyy*-*mm*-*dd*|  
|**t**|Hora *|*hh*:*mm*:*ss*[1]|  
|**TS**|Timestamp|*aaaa*-*mm*-*dd* *hh*:*mm*:*ss*[.*f...*] [1]|  
  
 [1] o número de dígitos à direita da vírgula decimal em um intervalo de tempo ou carimbo de hora literal que contém um componente de segundos é dependente de precisão de segundos, conforme contido no campo de descritor SQL_DESC_PRECISION. (Para obter mais informações, consulte [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md).)  
  
 Para obter mais informações sobre a data, hora e sequências de escape de carimbo de hora, consulte [data, hora e sequências de Escape de carimbo de hora](../../../odbc/reference/appendixes/date-time-and-timestamp-escape-sequences.md) na gramática do apêndice c: SQL.  
  
 Por exemplo, ambas as seguintes instruções SQL atualizar a data de abertura da ordem de venda 1023 na tabela Orders. A primeira instrução usa a sintaxe da sequência de escape. A segunda instrução usa a sintaxe de Oracle Rdb nativa para a coluna de data e não é interoperável.  
  
```  
UPDATE Orders SET OpenDate={d '1995-01-15'} WHERE OrderID=1023  
UPDATE Orders SET OpenDate='15-Jan-1995' WHERE OrderID=1023  
```  
  
 A sequência de escape para uma data, hora ou literal de carimbo de hora também pode ser colocada em uma variável de caracteres associada a uma data, hora ou parâmetro de carimbo de hora. Por exemplo, o código a seguir usa um parâmetro de data associado a uma variável de caractere para atualizar a data de abertura da ordem de venda 1023 na tabela Orders:  
  
```  
SQLCHAR      OpenDate[56]; // The size of a date literal is 55.  
SQLINTEGER   OpenDateLenOrInd = SQL_NTS;  
  
// Bind the parameter.  
SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_CHAR, SQL_TYPE_DATE, 0, 0,  
                  OpenDate, sizeof(OpenDate), &OpenDateLenOrInd);  
  
// Place the date in the OpenDate variable. In addition to the escape  
// sequence shown, it would also be possible to use either of the  
// strings "{d '1995-01-15'}" and "15-Jan-1995", although the latter  
// is data source-specific.  
strcpy_s( (char*) OpenDate, _countof(OpenDate), "{d '1995-01-15'}");  
  
// Execute the statement.  
SQLExecDirect(hstmt, "UPDATE Orders SET OpenDate=? WHERE OrderID = 1023", SQL_NTS);  
```  
  
 No entanto, é geralmente mais eficiente para associar o parâmetro diretamente a uma estrutura de data:  
  
```  
SQL_DATE_STRUCT   OpenDate;  
SQLINTEGER        OpenDateInd = 0;  
  
// Bind the parameter.  
SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_TYPE_DATE, SQL_TYPE_DATE, 0, 0,  
                  &OpenDate, 0, &OpenDateLen);  
  
// Place the date in the dsOpenDate structure.  
OpenDate.year = 1995;  
OpenDate.month = 1;  
OpenDate.day = 15;  
  
// Execute the statement.  
SQLExecDirect(hstmt, "UPDATE Employee SET OpenDate=? WHERE OrderID = 1023", SQL_NTS);  
```  
  
 Para determinar se um driver suporta as sequências de escape ODBC para data, hora ou literais de carimbo de hora, um aplicativo chama **SQLGetTypeInfo**. Se a fonte de dados oferece suporte a um tipo de dados de data, hora ou carimbo de hora, ele também deverá dar suporte a sequência de escape correspondente.  
  
 Fontes de dados também podem dar suporte a literais de data e hora definidas na especificação ANSI SQL-92, que são diferentes das sequências de escape ODBC para data, hora ou literais de carimbo de hora. Para determinar se uma fonte de dados dá suporte a literais de ANSI, um aplicativo chama **SQLGetInfo** com a opção SQL_ANSI_SQL_DATETIME_LITERALS.  
  
 Para determinar se um driver suporta as sequências de escape ODBC para literais de intervalo, um aplicativo chama **SQLGetTypeInfo**. Se a fonte de dados oferece suporte a um tipo de dados de intervalo de data e hora, ele também deverá dar suporte a sequência de escape correspondente.  
  
 Fontes de dados também podem dar suporte a literais de data e hora definidas na especificação ANSI SQL-92, que são diferentes das sequências de escape ODBC para literais de intervalo de data e hora. Para determinar se uma fonte de dados dá suporte a literais de ANSI, um aplicativo chama **SQLGetInfo** com a opção SQL_ANSI_SQL_DATETIME_LITERALS.
