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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d899938be4689daab50a773f189219a797794006
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81288292"
---
# <a name="date-time-and-timestamp-literals"></a>Data, hora e literais de carimbo de data/hora
A sequência de escape para literais de data, hora e timestamp é  
  
 **{**  _-Type_ **'** _valor_ **'}**  
  
 em que *tipo literal* é um dos valores listados na tabela a seguir.  
  
|*tipo literal*|Significado|Formato do *valor*|  
|---------------------|-------------|-----------------------|  
|**d**|Data|*aaaa*-*mm*mm-*DD*|  
|**t**|Momento|*hh*:*mm*:*SS*[1]|  
|**ts**|Timestamp|*aaaa*-*mm*mm-*DD* *hh*:*mm*:*SS*[.* f...*] uma|  
  
 [1] o número de dígitos à direita do ponto decimal em um literal de tempo ou carimbo de data/hora que contém um componente de segundos depende da precisão de segundos, conforme contido no campo descritor de SQL_DESC_PRECISION. (Para obter mais informações, consulte [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md).)  
  
 Para obter mais informações sobre as sequências de escape de data, hora e carimbo de hora, consulte [data, hora e sequências de escape de carimbo](../../../odbc/reference/appendixes/date-time-and-timestamp-escape-sequences.md) de hora no Apêndice C: gramática SQL.  
  
 Por exemplo, ambas as instruções SQL a seguir atualizam a data de abertura da ordem de venda 1023 na tabela Orders. A primeira instrução usa a sintaxe da sequência de escape. A segunda instrução usa a sintaxe nativa de RDB do Oracle para a coluna de data e não é interoperável.  
  
```  
UPDATE Orders SET OpenDate={d '1995-01-15'} WHERE OrderID=1023  
UPDATE Orders SET OpenDate='15-Jan-1995' WHERE OrderID=1023  
```  
  
 A sequência de escape para um literal de data, hora ou timestamp também pode ser colocada em uma variável de caractere associada a um parâmetro date, time ou timestamp. Por exemplo, o código a seguir usa um parâmetro de data associado a uma variável de caractere para atualizar a data de abertura da ordem de venda 1023 na tabela Orders:  
  
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
  
 No entanto, geralmente é mais eficiente associar o parâmetro diretamente a uma estrutura de data:  
  
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
  
 Para determinar se um driver dá suporte a sequências de escape ODBC para literais de data, hora ou timestamp, um aplicativo chama **SQLGetTypeInfo**. Se a fonte de dados der suporte a um tipo de dados Date, time ou timestamp, ela também deverá oferecer suporte à sequência de escape correspondente.  
  
 As fontes de dados também podem dar suporte aos literais DateTime definidos na especificação ANSI SQL-92, que são diferentes das sequências de escape ODBC para literais de data, hora ou carimbo. Para determinar se uma fonte de dados dá suporte a literais ANSI, um aplicativo chama **SQLGetInfo** com a opção SQL_ANSI_SQL_DATETIME_LITERALS.  
  
 Para determinar se um driver dá suporte a sequências de escape ODBC para literais de intervalo, um aplicativo chama **SQLGetTypeInfo**. Se a fonte de dados der suporte a um tipo de dados de intervalo de DateTime, ela também deverá oferecer suporte à sequência de escape correspondente.  
  
 As fontes de dados também podem dar suporte aos literais DateTime definidos na especificação ANSI SQL-92, que são diferentes das sequências de escape ODBC para literais de intervalo DateTime. Para determinar se uma fonte de dados dá suporte a literais ANSI, um aplicativo chama **SQLGetInfo** com a opção SQL_ANSI_SQL_DATETIME_LITERALS.
