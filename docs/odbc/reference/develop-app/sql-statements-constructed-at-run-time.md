---
title: "Instruções SQL construídas em tempo de execução | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- run time constructed SQL statements [ODBC]
- SQL statements [ODBC], constructing
- SQL statements [ODBC], building at run time
ms.assetid: f6554486-d49c-436a-82e3-4c158d26acd8
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 8ccd79048c250c73867752ebaf0b2b7060a6c19b
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="sql-statements-constructed-at-run-time"></a>Instruções SQL construídas em tempo de execução
Aplicativos que executam a análise ad hoc comumente construa instruções SQL em tempo de execução. Por exemplo, uma planilha pode permitir que um usuário selecionar colunas do qual recuperar dados:  
  
```  
// SQL_Statements_Constructed_at_Run_Time.cpp  
#include <windows.h>  
#include <stdio.h>  
#include <sqltypes.h>  
  
int main() {  
   SQLCHAR *Statement = 0, *TableName = 0;  
   SQLCHAR **TableNamesArray, **ColumnNamesArray = 0;  
   BOOL *ColumnSelectedArray = 0;  
   BOOL  CommaNeeded;  
   SQLSMALLINT i = 0, NumColumns = 0;  
  
   // Use SQLTables to build a list of tables (TableNamesArray[]). Let the  
   // user select a table and store the selected table in TableName.  
  
   // Use SQLColumns to build a list of the columns in the selected table  
   // (ColumnNamesArray). Set NumColumns to the number of columns in the  
   // table. Let the user select one or more columns and flag these columns  
   // in ColumnSelectedArray[].  
  
   // Build a SELECT statement from the selected columns.  
   CommaNeeded = FALSE;  
   Statement = (SQLCHAR*)malloc(8);  
   strcpy_s((char*)Statement, 8, "SELECT ");  
  
   for (i = 0 ; i = NumColumns ; i++) {  
      if (ColumnSelectedArray[i]) {  
         if (CommaNeeded)  
            strcat_s((char*)Statement, sizeof(Statement), ",");  
         else  
            CommaNeeded = TRUE;  
         strcat_s((char*)Statement, sizeof(Statement), (char*)ColumnNamesArray[i]);  
      }  
   }  
  
   strcat_s((char*)Statement, 15, " FROM ");  
   // strcat_s((char*)Statement, 100, (char*)TableName);  
  
   // Execute the statement . It will be executed once, do not prepare it.  
   // SQLExecDirect(hstmt, Statement, SQL_NTS);  
}  
```  
  
 Outra classe de aplicativos que normalmente construa instruções SQL em tempo de execução são ambientes de desenvolvimento de aplicativo. No entanto, as instruções que eles constroem são embutidos em código no aplicativo que são criados, onde podem normalmente ser otimizados e testados.  
  
 Aplicativos que construa instruções SQL em tempo de execução podem fornecer grande flexibilidade para o usuário. Como pode ser visto no exemplo anterior, que não oferecia suporte até mesmo operações comuns como **onde** cláusulas, **ORDER BY** cláusulas ou junções, construindo instruções SQL em tempo de execução é muito mais complexo que codificar instruções. Além disso, esses aplicativos de teste é problemático porque eles podem construir um número arbitrário de instruções SQL.  
  
 Uma desvantagem potencial de construindo instruções SQL em tempo de execução é que leva mais tempo para construir uma instrução de usar uma instrução codificada. Felizmente, raramente é uma preocupação. Esses aplicativos tendem a ser com uso intensivo de interface do usuário e a hora em que o aplicativo gasta construindo instruções SQL geralmente é pequena em comparação com o tempo que o usuário passa inserindo critérios.

