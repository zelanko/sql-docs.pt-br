---
title: Data, hora e carimbo de data | Microsoft Docs
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81288292"
---
# <a name="date-time-and-timestamp-literals"></a>Data, hora e literais de carimbo de data/hora
A seqüência de fuga para data, hora e carimbo de tempo literals é  
  
 **{**  _- tipo_ **'** _valor_ **'}**  
  
 onde *o tipo literal* é um dos valores listados na tabela a seguir.  
  
|*tipo literal*|Significado|Formato de *valor*|  
|---------------------|-------------|-----------------------|  
|**D**|Data|*yyyy*-*mm*-*dd*|  
|**t**|Tempo*|*hh:**mm:**ss*[1]|  
|**Ts**|Timestamp|*yyyy*-*mm*-*dd* *hh:**mm*:*ss*[.* f...*] [1]|  
  
 [1] O número de dígitos à direita do ponto decimal em um intervalo de tempo ou carimbo de tempo que contém um componente de segundos depende da precisão dos segundos, conforme contido no campo descritor SQL_DESC_PRECISION. (Para obter mais informações, consulte [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md).)  
  
 Para obter mais informações sobre as seqüências de fuga de data, hora e carimbo de tempo, consulte [Sequências de fuga de data, hora e carimbo de tempo](../../../odbc/reference/appendixes/date-time-and-timestamp-escape-sequences.md) no apêndice C: Gramática SQL.  
  
 Por exemplo, ambas as seguintes declarações de SQL atualizam a data de abertura da ordem de venda 1023 na tabela Ordens. A primeira declaração usa a sintaxe da seqüência de fuga. A segunda declaração usa a sintaxe nativa Oracle Rdb para a coluna DATE e não é interoperável.  
  
```  
UPDATE Orders SET OpenDate={d '1995-01-15'} WHERE OrderID=1023  
UPDATE Orders SET OpenDate='15-Jan-1995' WHERE OrderID=1023  
```  
  
 A seqüência de escape para um literal de data, hora ou carimbo de tempo também pode ser colocada em uma variável de caractere vinculada a um parâmetro de data, hora ou carimbo de tempo. Por exemplo, o código a seguir usa um parâmetro de data vinculado a uma variável de caractere para atualizar a data de abertura da ordem de venda1023 na tabela Ordens:  
  
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
  
 No entanto, geralmente é mais eficiente vincular o parâmetro diretamente a uma estrutura de data:  
  
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
  
 Para determinar se um driver suporta as seqüências de fuga do ODBC para literais de data, hora ou carimbo de data, um aplicativo chama **SQLGetTypeInfo**. Se a fonte de dados suportar um tipo de data, hora ou carimbo de data, ele também deve suportar a seqüência de fuga correspondente.  
  
 As fontes de dados também podem suportar os literais de data-hora definidos na especificação ANSI SQL-92, que são diferentes das seqüências de escape do ODBC para literais de data, hora ou carimbo de data. Para determinar se uma fonte de dados suporta os literais ANSI, um aplicativo chama **sqlGetInfo** com a opção SQL_ANSI_SQL_DATETIME_LITERALS.  
  
 Para determinar se um driver suporta as seqüências de fuga do ODBC para literais de intervalo, um aplicativo chama **SQLGetTypeInfo**. Se a fonte de dados suportar um tipo de dados de intervalo de data, ele também deve suportar a seqüência de fuga correspondente.  
  
 As fontes de dados também podem suportar os literais de data-hora definidos na especificação ANSI SQL-92, que são diferentes das seqüências de escape do ODBC para literais de intervalo de data. Para determinar se uma fonte de dados suporta os literais ANSI, um aplicativo chama **sqlGetInfo** com a opção SQL_ANSI_SQL_DATETIME_LITERALS.
