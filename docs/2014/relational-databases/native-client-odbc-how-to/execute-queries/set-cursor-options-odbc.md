---
title: Definir opções de Cursor (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- cursors [ODBC], options
ms.assetid: 0e72b48a-fc5a-4656-8cf5-39f57d8c1565
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a37b09f88f9156f6363ed99a9fea56b2f9a5932b
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37419765"
---
# <a name="set-cursor-options-odbc"></a>Definir opções de cursor (ODBC)
  Para definir opções de cursor, chame [SQLSetStmtAttr](../../native-client-odbc-api/sqlsetstmtattr.md) para definir ou [SQLGetStmtAttr](../../native-client-odbc-api/sqlgetstmtattr.md) para obter as opções de instrução que controlam o comportamento do cursor.  
  
|*Atributo*|Especifica|  
|-----------------|---------------|  
|SQL_ATTR_CURSOR_TYPE|Tipo de cursor: somente avanço, estático, dinâmico ou controlado por conjunto de chaves.|  
|SQL_ATTR_CONCURRENCY|Opção de controle de simultaneidade: somente leitura, bloqueio, otimista usando carimbos de data/hora ou otimista usando valores.|  
|SQL_ATTR_ROW_ARRAY_SIZE|Número de linhas recuperadas em cada busca.|  
|SQL_ATTR_CURSOR_SENSITIVITY|Cursor que mostra ou não atualizações nas linhas de cursor feitas por outras conexões.|  
|SQL_ATTR_CURSOR_SCROLLABLE|Cursor que pode avançar e recuar.|  
  
 Os valores padrão desses atributos (somente avanço, somente leitura, tamanho de conjunto de linhas de 1) não usam cursores de servidor. Para usar cursores de servidor, pelo menos um desses atributos deve ser definido como um valor diferente do padrão e a instrução executada deve ser uma instrução SELECT ou um procedimento armazenado que contém uma única instrução SELECT. Quando cursores de servidor forem usados, as instruções SELECT não poderão usar cláusulas às quais os cursores de servidor não ofereçam suporte: COMPUTE, COMPUTE BY, FOR BROWSE e INTO.  
  
 Você pode controlar o tipo de cursor usado ao definir SQL_ATTR_CURSOR_TYPE e SQL_ATTR_CONCURRENCY ou ao definir SQL_ATTR_CURSOR_SENSITIVITY e SQL_ATTR_CURSOR_SCROLLABLE. Você não deve misturar os dois métodos de especificação de comportamento de cursor.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir aloca um identificador de instrução, define um tipo de cursor dinâmico com simultaneidade otimista de controle de versão de linha e, então, executa uma instrução SELECT.  
  
```  
retcode = SQLAllocHandle(SQL_HANDLE_STMT, hdbc1, &hstmt1);  
retcode = SQLSetStmtAttr(hstmt1, SQL_ATTR_CURSOR_TYPE, (SQLPOINTER)SQL_CURSOR_DYNAMIC, SQL_IS_INTEGER);  
retcode = SQLSetStmtAttr(hstmt1, SQL_ATTR_CONCURRENCY, SQLPOINTER)SQL_CONCUR_ROWVER, SQL_IS_INTEGER);  
retcode = SQLExecDirect(hstmt1, SELECT au_lname FROM authors", SQL_NTS);  
```  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir aloca um identificador de instrução, define um cursor sensível rolável e, então, executa uma instrução SELECT.  
  
```  
retcode = SQLAllocHandle(SQL_HANDLE_STMT, hdbc1, &hstmt1);  
  
// Set the cursor options and execute the statement.  
retcode = SQLSetStmtAttr(hstmt1, SQL_ATTR_CURSOR_SCROLLABLE, SQLPOINTER)SQL_SCROLLABLE, SQL_IS_INTEGER);  
retcode = SQLSetStmtAttr(hstmt1, SQL_ATTR_CURSOR_SENSITIVITY, SQLPOINTER)SQL_INSENSITIVE, SQL_IS_INTEGER);  
retcode = SQLExecDirect(hstmt1, select au_lname from authors", SQL_NTS);  
```  
  
## <a name="see-also"></a>Consulte também  
 [Executar consultas de tópicos de instruções &#40;ODBC&#41;](executing-queries-how-to-topics-odbc.md)  
  
  
