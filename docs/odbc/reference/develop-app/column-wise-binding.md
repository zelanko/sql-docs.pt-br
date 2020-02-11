---
title: Associação de coluna | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- column-wise binding [ODBC]
- result sets [ODBC], binding columns
- binding columns [ODBC]
ms.assetid: 86d37637-3a25-455d-9c82-a0d7bff8d70d
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6f91dca1ac20173f9c10b4a52adf292e7abc45d0
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68083378"
---
# <a name="column-wise-binding"></a>Associação de coluna
Ao usar a associação de coluna, um aplicativo associa um ou dois casos de matrizes a cada coluna para a qual os dados serão retornados. A primeira matriz contém os valores de dados, e a segunda matriz contém buffers de comprimento/indicador. Os indicadores e os valores de comprimento podem ser armazenados em buffers separados definindo os campos de descritor SQL_DESC_INDICATOR_PTR e SQL_DESC_OCTET_LENGTH_PTR com valores diferentes; Se isso for feito, uma terceira matriz será associada. Cada matriz contém tantos elementos quantos houver linhas no conjunto de linhas.  
  
 O aplicativo declara que está usando Associação de coluna com o atributo de instrução SQL_ATTR_ROW_BIND_TYPE, que determina o tipo de associação para buffers de conjunto de linhas, em oposição aos buffers de conjunto de parâmetros. O driver retorna os dados para cada linha em elementos sucessivos de cada matriz. A ilustração a seguir mostra como a associação por coluna funciona.  
  
 ![Associação de coluna&#45;inteligente de três colunas](../../../odbc/reference/develop-app/media/pr21.gif "pr21")  
  
 Por exemplo, o código a seguir associa matrizes de 10 elementos às colunas OrderID, SalesPerson e status:  
  
```  
#define ROW_ARRAY_SIZE 10  
  
SQLUINTEGER    OrderIDArray[ROW_ARRAY_SIZE], NumRowsFetched;  
SQLCHAR        SalesPersonArray[ROW_ARRAY_SIZE][11],  
               StatusArray[ROW_ARRAY_SIZE][7];  
SQLINTEGER     OrderIDIndArray[ROW_ARRAY_SIZE],  
               SalesPersonLenOrIndArray[ROW_ARRAY_SIZE],  
               StatusLenOrIndArray[ROW_ARRAY_SIZE];  
SQLUSMALLINT   RowStatusArray[ROW_ARRAY_SIZE], i;  
SQLRETURN      rc;  
SQLHSTMT       hstmt;  
  
// Set the SQL_ATTR_ROW_BIND_TYPE statement attribute to use  
// column-wise binding. Declare the rowset size with the  
// SQL_ATTR_ROW_ARRAY_SIZE statement attribute. Set the  
// SQL_ATTR_ROW_STATUS_PTR statement attribute to point to the  
// row status array. Set the SQL_ATTR_ROWS_FETCHED_PTR statement  
// attribute to point to cRowsFetched.  
SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_BIND_TYPE, SQL_BIND_BY_COLUMN, 0);  
SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_ARRAY_SIZE, ROW_ARRAY_SIZE, 0);  
SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_STATUS_PTR, RowStatusArray, 0);  
SQLSetStmtAttr(hstmt, SQL_ATTR_ROWS_FETCHED_PTR, &NumRowsFetched, 0);  
  
// Bind arrays to the OrderID, SalesPerson, and Status columns.  
SQLBindCol(hstmt, 1, SQL_C_ULONG, OrderIDArray, 0, OrderIDIndArray);  
SQLBindCol(hstmt, 2, SQL_C_CHAR, SalesPersonArray, sizeof(SalesPersonArray[0]),  
            SalesPersonLenOrIndArray);  
SQLBindCol(hstmt, 3, SQL_C_CHAR, StatusArray, sizeof(StatusArray[0]),  
            StatusLenOrIndArray);  
  
// Execute a statement to retrieve rows from the Orders table.  
SQLExecDirect(hstmt, "SELECT OrderID, SalesPerson, Status FROM Orders", SQL_NTS);  
  
// Fetch up to the rowset size number of rows at a time. Print the actual  
// number of rows fetched; this number is returned in NumRowsFetched.  
// Check the row status array to print only those rows successfully  
// fetched. Code to check if rc equals SQL_SUCCESS_WITH_INFO or  
// SQL_ERROR not shown.  
while ((rc = SQLFetchScroll(hstmt,SQL_FETCH_NEXT,0)) != SQL_NO_DATA) {  
   for (i = 0; i < NumRowsFetched; i++) {  
      if ((RowStatusArray[i] == SQL_ROW_SUCCESS) ||  
            (RowStatusArray[i] == SQL_ROW_SUCCESS_WITH_INFO)) {  
         if (OrderIDIndArray[i] == SQL_NULL_DATA)  
            printf(" NULL      ");  
         else  
            printf("%d\t", OrderIDArray[i]);  
         if (SalesPersonLenOrIndArray[i] == SQL_NULL_DATA)  
            printf(" NULL      ");  
         else  
            printf("%s\t", SalesPersonArray[i]);  
         if (StatusLenOrIndArray[i] == SQL_NULL_DATA)  
            printf(" NULL\n");  
         else  
            printf("%s\n", StatusArray[i]);  
      }  
   }  
}  
  
// Close the cursor.  
SQLCloseCursor(hstmt);  
```
