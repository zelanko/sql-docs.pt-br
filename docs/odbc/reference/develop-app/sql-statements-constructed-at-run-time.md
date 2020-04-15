---
title: Declarações SQL construídas em tempo de execução | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- run time constructed SQL statements [ODBC]
- SQL statements [ODBC], constructing
- SQL statements [ODBC], building at run time
ms.assetid: f6554486-d49c-436a-82e3-4c158d26acd8
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 795335be2a2a3aab1be6dac26bf6d213161fe42e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301967"
---
# <a name="sql-statements-constructed-at-run-time"></a>Instruções SQL construídas em tempo de execução
Aplicativos que executam análise ad hoc geralmente constroem instruções SQL em tempo de execução. Por exemplo, uma planilha pode permitir que um usuário selecione colunas das quais recuperar dados:  
  
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
  
 Outra classe de aplicativos que comumente constrói instruções SQL em tempo de execução são os ambientes de desenvolvimento de aplicativos. No entanto, as declarações que eles constroem são codificadas na aplicação que estão construindo, onde geralmente podem ser otimizadas e testadas.  
  
 Aplicativos que constroem instruções SQL em tempo de execução podem fornecer uma tremenda flexibilidade ao usuário. Como pode ser visto no exemplo anterior, que nem sequer suportava operações comuns como **ONDE** cláusulas, **cláusulas de ORDEM POR** OU junções, a construção de declarações SQL em tempo de execução é muito mais complexa do que as declarações de codificação dura. Além disso, testar tais aplicativos é problemático porque eles podem construir um número arbitrário de declarações SQL.  
  
 Uma desvantagem potencial de construir declarações SQL em tempo de execução é que leva muito mais tempo para construir uma declaração do que usar uma instrução codificada. Felizmente, isso raramente é uma preocupação. Esses aplicativos tendem a ser intensivos em interface de usuário, e o tempo que o aplicativo gasta construindo instruções SQL é geralmente pequeno em comparação com o tempo que o usuário gasta inserindo critérios.
