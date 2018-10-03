---
title: A associação | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- row-wise binding [ODBC]
- result sets [ODBC], binding columns
- binding columns [ODBC]
ms.assetid: 4f622cf4-0603-47a1-a48b-944c4ef46364
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c596f4924e9859b3ac61d38f68bacbc3ecd54a2e
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47855854"
---
# <a name="row-wise-binding"></a>Associação de linha
Ao usar a associação, um aplicativo define uma estrutura que contém um ou dois, ou em alguns casos, três elementos para cada coluna para a qual data será retornado. O primeiro elemento contém o valor de dados, e o segundo elemento contém o buffer de comprimento/indicador. Indicadores e os valores de comprimento podem ser armazenados em buffers separadas ao definir os campos de descritor SQL_DESC_INDICATOR_PTR e SQL_DESC_OCTET_LENGTH_PTR como valores diferentes; Se isso for feito, a estrutura contém um terceiro elemento. O aplicativo, em seguida, aloca uma matriz dessas estruturas, que contém elementos tantas quantas forem as linhas no conjunto de linhas.  
  
 O aplicativo declara o tamanho da estrutura para o driver com o atributo da instrução SQL_ATTR_ROW_BIND_TYPE e associa o endereço de cada membro no primeiro elemento da matriz. Portanto, o driver pode calcular o endereço dos dados para uma determinada linha e coluna como  
  
```  
Address = Bound Address + ((Row Number - 1) * Structure Size)  
```  
  
 em que as linhas são numeradas de 1 para o tamanho do conjunto de linhas. (Um é subtraído do número de linha porque a matriz de indexação em C é baseado em zero.) A ilustração a seguir mostra como a associação funciona. Em geral, apenas as colunas que serão associadas são incluídas na estrutura. A estrutura pode conter campos que não são relacionados para colunas do conjunto de resultados. As colunas podem ser colocadas na estrutura em qualquer ordem, mas são mostradas em ordem sequencial para maior clareza.  
  
 ![Linha mostra&#45;associação wise](../../../odbc/reference/develop-app/media/pr22.gif "pr22")  
  
 Por exemplo, o código a seguir cria uma estrutura com elementos no qual retornar dados para as colunas OrderID, o vendedor e o Status e comprimento/indicadores para as colunas de vendedor e Status. Ele aloca 10 dessas estruturas e associa-os para as colunas OrderID, o vendedor e o Status.  
  
```  
#define ROW_ARRAY_SIZE 10  
  
// Define the ORDERINFO struct and allocate an array of 10 structs.  
typedef struct {  
   SQLUINTEGER   OrderID;  
   SQLINTEGER    OrderIDInd;  
   SQLCHAR       SalesPerson[11];  
   SQLINTEGER    SalesPersonLenOrInd;  
   SQLCHAR       Status[7];  
   SQLINTEGER    StatusLenOrInd;  
} ORDERINFO;  
ORDERINFO OrderInfoArray[ROW_ARRAY_SIZE];  
  
SQLULEN    NumRowsFetched;  
SQLUSMALLINT   RowStatusArray[ROW_ARRAY_SIZE], i;  
SQLRETURN      rc;  
SQLHSTMT       hstmt;  
  
// Specify the size of the structure with the SQL_ATTR_ROW_BIND_TYPE  
// statement attribute. This also declares that row-wise binding will  
// be used. Declare the rowset size with the SQL_ATTR_ROW_ARRAY_SIZE  
// statement attribute. Set the SQL_ATTR_ROW_STATUS_PTR statement  
// attribute to point to the row status array. Set the  
// SQL_ATTR_ROWS_FETCHED_PTR statement attribute to point to  
// NumRowsFetched.  
SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_BIND_TYPE, sizeof(ORDERINFO), 0);  
SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_ARRAY_SIZE, ROW_ARRAY_SIZE, 0);  
SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_STATUS_PTR, RowStatusArray, 0);  
SQLSetStmtAttr(hstmt, SQL_ATTR_ROWS_FETCHED_PTR, &NumRowsFetched, 0);  
  
// Bind elements of the first structure in the array to the OrderID,  
// SalesPerson, and Status columns.  
SQLBindCol(hstmt, 1, SQL_C_ULONG, &OrderInfoArray[0].OrderID, 0, &OrderInfoArray[0].OrderIDInd);  
SQLBindCol(hstmt, 2, SQL_C_CHAR, OrderInfoArray[0].SalesPerson,  
            sizeof(OrderInfoArray[0].SalesPerson),  
            &OrderInfoArray[0].SalesPersonLenOrInd);  
SQLBindCol(hstmt, 3, SQL_C_CHAR, OrderInfoArray[0].Status,  
            sizeof(OrderInfoArray[0].Status), &OrderInfoArray[0].StatusLenOrInd);  
  
// Execute a statement to retrieve rows from the Orders table.  
SQLExecDirect(hstmt, "SELECT OrderID, SalesPerson, Status FROM Orders", SQL_NTS);  
  
// Fetch up to the rowset size number of rows at a time. Print the actual  
// number of rows fetched; this number is returned in NumRowsFetched.  
// Check the row status array to print only those rows successfully  
// fetched. Code to check if rc equals SQL_SUCCESS_WITH_INFO or  
// SQL_ERRORnot shown.  
while ((rc = SQLFetchScroll(hstmt,SQL_FETCH_NEXT,0)) != SQL_NO_DATA) {  
   for (i = 0; i < NumRowsFetched; i++) {  
      if (RowStatusArray[i] == SQL_ROW_SUCCESS|| RowStatusArray[i] ==   
         SQL_ROW_SUCCESS_WITH_INFO) {  
         if (OrderInfoArray[i].OrderIDInd == SQL_NULL_DATA)  
            printf(" NULL      ");  
         else  
            printf("%d\t", OrderInfoArray[i].OrderID);  
         if (OrderInfoArray[i].SalesPersonLenOrInd == SQL_NULL_DATA)  
            printf(" NULL      ");  
         else  
            printf("%s\t", OrderInfoArray[i].SalesPerson);  
         if (OrderInfoArray[i].StatusLenOrInd == SQL_NULL_DATA)  
            printf(" NULL\n");  
         else  
            printf("%s\n", OrderInfoArray[i].Status);  
      }  
   }  
}  
  
// Close the cursor.  
SQLCloseCursor(hstmt);  
```
