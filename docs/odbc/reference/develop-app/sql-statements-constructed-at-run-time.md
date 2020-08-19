---
description: Instruções SQL construídas em tempo de execução
title: Instruções SQL construídas em tempo de execução | Microsoft Docs
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
ms.openlocfilehash: fff9f7a4e579ce4e1d1177b8f5fa67f7d13a4fdc
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424548"
---
# <a name="sql-statements-constructed-at-run-time"></a>Instruções SQL construídas em tempo de execução
Os aplicativos que executam a análise ad hoc normalmente criam instruções SQL em tempo de execução. Por exemplo, uma planilha pode permitir que um usuário Selecione colunas da qual recuperar dados:  
  
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
  
 Outra classe de aplicativos que normalmente constrói instruções SQL em tempo de execução são ambientes de desenvolvimento de aplicativos. No entanto, as instruções que eles constroem são embutidas em código no aplicativo que estão compilando, em que normalmente eles podem ser otimizados e testados.  
  
 Os aplicativos que constroem instruções SQL em tempo de execução podem fornecer uma enorme flexibilidade ao usuário. Como pode ser visto no exemplo anterior, que não dá suporte a tais operações comuns como cláusulas **Where** , cláusulas **order by** ou junções, a construção de instruções SQL em tempo de execução é muito mais complexa do que as instruções de codificação embutida. Além disso, o teste desses aplicativos é problemático porque eles podem construir um número arbitrário de instruções SQL.  
  
 Uma desvantagem potencial da construção de instruções SQL em tempo de execução é que demora muito mais tempo para construir uma instrução do que usar uma instrução embutida em código. Felizmente, isso raramente é uma preocupação. Esses aplicativos tendem a ser intensivas na interface do usuário e o tempo que o aplicativo gasta construindo instruções SQL é geralmente pequeno em comparação com o tempo que o usuário gasta ao inserir critérios.
