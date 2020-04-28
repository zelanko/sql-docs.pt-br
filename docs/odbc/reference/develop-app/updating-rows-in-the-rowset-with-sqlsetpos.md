---
title: Atualizando linhas no conjunto de linhas com SQLSetPos | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- updating data [ODBC], SQLSetPos
- data updates [ODBC], SQLSetPos
- SQLSetPos function [ODBC], updating rows
ms.assetid: d83a8c2a-5aa8-4f19-947c-79a817167ee1
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4851d4ba741379fc188b2b88c895a378ef3bb80d
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81298966"
---
# <a name="updating-rows-in-the-rowset-with-sqlsetpos"></a>Atualizar linhas no conjunto de linhas com SQLSetPos
A operação de atualização de **SQLSetPos** faz com que a fonte de dados atualize uma ou mais linhas selecionadas de uma tabela, usando dados nos buffers de aplicativo para cada coluna associada (a menos que o valor no buffer de comprimento/indicador seja SQL_COLUMN_IGNORE). As colunas que não estão associadas não serão atualizadas.  
  
 Para atualizar linhas com **SQLSetPos**, o aplicativo faz o seguinte:  
  
1.  Coloca os novos valores de dados nos buffers de conjunto de linhas. Para obter informações sobre como enviar dados longos com o **SQLSetPos**, consulte [Long data e SQLSetPos e SQLBulkOperations](../../../odbc/reference/develop-app/long-data-and-sqlsetpos-and-sqlbulkoperations.md).  
  
2.  Define o valor no buffer de comprimento/indicador de cada coluna, conforme necessário. Esse é o comprimento de bytes dos dados ou SQL_NTS para colunas vinculadas a buffers de cadeia de caracteres, o comprimento de bytes dos dados para colunas vinculadas a buffers binários e SQL_NULL_DATA para qualquer coluna a ser definida como NULL.  
  
3.  Define o valor no buffer de comprimento/indicador das colunas que não devem ser atualizadas para SQL_COLUMN_IGNORE. Embora o aplicativo possa ignorar essa etapa e reenviar os dados existentes, isso é ineficiente e os riscos de envio de valores para a fonte de dados que foram truncados quando foram lidos.  
  
4.  Chama **SQLSetPos** com a *operação* definida como SQL_UPDATE e *RowNumber* definido como o número da linha a ser atualizada. Se *RowNumber* for 0, todas as linhas no conjunto de linhas serão atualizadas.  
  
 Após o retorno de **SQLSetPos** , a linha atual é definida como a linha atualizada.  
  
 Ao atualizar todas as linhas do conjunto de linhas (*RowNumber* é igual a 0), um aplicativo pode desabilitar a atualização de determinadas linhas definindo os elementos correspondentes da matriz de operação de linha (apontada pelo atributo de instrução SQL_ATTR_ROW_OPERATION_PTR) para SQL_ROW_IGNORE. A matriz de operação de linha corresponde ao tamanho e ao número de elementos para a matriz de status de linha (apontada pelo atributo de instrução SQL_ATTR_ROW_STATUS_PTR). Para atualizar somente as linhas no conjunto de resultados que foram buscadas com êxito e que não foram excluídas do conjunto de linhas, o aplicativo usa a matriz de status de linha da função que buscou o conjunto de linhas como a matriz de operações de linha para **SQLSetPos**.  
  
 Para cada linha enviada à fonte de dados como uma atualização, os buffers de aplicativo devem ter dados de linha válidos. Se os buffers de aplicativo foram preenchidos pela busca e se uma matriz de status de linha tiver sido mantida, seus valores em cada uma dessas posições de linha não devem ser SQL_ROW_DELETED, SQL_ROW_ERROR ou SQL_ROW_NOROW.  
  
 Por exemplo, o código a seguir permite que um usuário percorra a tabela Customers e atualize, exclua ou adicione novas linhas. Ele coloca os novos dados nos buffers de conjunto de linhas antes de chamar **SQLSetPos** para atualizar ou adicionar novas linhas. Uma linha extra é alocada no final dos buffers de conjunto de linhas para conter novas linhas; Isso impede que os dados existentes sejam substituídos quando os dados de uma nova linha são colocados nos buffers.  
  
```  
#define UPDATE_ROW   100  
#define DELETE_ROW   101  
#define ADD_ROW      102  
  
SQLUINTEGER    CustIDArray[11];  
SQLCHAR        NameArray[11][51], AddressArray[11][51],   
               PhoneArray[11][11];  
SQLINTEGER     CustIDIndArray[11], NameLenOrIndArray[11],   
               AddressLenOrIndArray[11],  
               PhoneLenOrIndArray[11];  
SQLUSMALLINT   RowStatusArray[10], Action, RowNum;  
SQLRETURN      rc;  
SQLHSTMT       hstmt;  
  
// Set the SQL_ATTR_ROW_BIND_TYPE statement attribute to use column-wise   
// binding. Declare the rowset size with the SQL_ATTR_ROW_ARRAY_SIZE   
// statement attribute. Set the SQL_ATTR_ROW_STATUS_PTR statement   
// attribute to point to the row status array.  
SQLSetStmtAttr(hstmt, SQL_ATTR_CURSOR_TYPE, SQL_CURSOR_KEYSET_DRIVEN, 0);  
SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_BIND_TYPE, SQL_BIND_BY_COLUMN, 0);  
SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_ARRAY_SIZE, 10, 0);  
SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_STATUS_PTR, RowStatusArray, 0);  
  
// Bind arrays to the CustID, Name, Address, and Phone columns.  
SQLBindCol(hstmt, 1, SQL_C_ULONG, CustIDArray, 0, CustIDIndArray);  
SQLBindCol(hstmt, 2, SQL_C_CHAR, NameArray, sizeof(NameArray[0]), NameLenOrIndArray);  
SQLBindCol(hstmt, 3, SQL_C_CHAR, AddressArray, sizeof(AddressArray[0]),  
            AddressLenOrIndArray);  
SQLBindCol(hstmt, 4, SQL_C_CHAR, PhoneArray, sizeof(PhoneArray[0]),  
            PhoneLenOrIndArray);  
  
// Execute a statement to retrieve rows from the Customers table.  
SQLExecDirect(hstmt, "SELECT CustID, Name, Address, Phone FROM Customers", SQL_NTS);  
  
// Fetch and display the first 10 rows.  
rc = SQLFetchScroll(hstmt, SQL_FETCH_NEXT, 0);  
DisplayData(CustIDArray, CustIDIndArray, NameArray, NameLenOrIndArray, AddressArray,  
            AddressLenOrIndArray, PhoneArray, PhoneLenOrIndArray, RowStatusArray);  
  
// Call GetAction to get an action and a row number from the user.  
while (GetAction(&Action, &RowNum)) {  
   switch (Action) {  
  
      case SQL_FETCH_NEXT:  
      case SQL_FETCH_PRIOR:  
      case SQL_FETCH_FIRST:  
      case SQL_FETCH_LAST:  
      case SQL_FETCH_ABSOLUTE:  
      case SQL_FETCH_RELATIVE:  
         // Fetch and display the requested data.  
         SQLFetchScroll(hstmt, Action, RowNum);  
         DisplayData(CustIDArray, CustIDIndArray,  
                     NameArray, NameLenOrIndArray,  
                     AddressArray, AddressLenOrIndArray,  
                     PhoneArray, PhoneLenOrIndArray, RowStatusArray);  
         break;  
  
      case UPDATE_ROW:  
         // Place the new data in the rowset buffers and update the   
         // specified row.  
         GetNewData(&CustIDArray[RowNum - 1], &CustIDIndArray[RowNum - 1],  
                  NameArray[RowNum - 1], &NameLenOrIndArray[RowNum - 1],  
                  AddressArray[RowNum - 1], &AddressLenOrIndArray[RowNum - 1],  
                  PhoneArray[RowNum - 1], &PhoneLenOrIndArray[RowNum - 1]);  
         SQLSetPos(hstmt, RowNum, SQL_UPDATE, SQL_LOCK_NO_CHANGE);  
         break;  
  
      case DELETE_ROW:  
         // Delete the specified row.  
         SQLSetPos(hstmt, RowNum, SQL_DELETE, SQL_LOCK_NO_CHANGE);  
         break;  
  
      case ADD_ROW:  
         // Place the new data in the rowset buffers at index 10.   
         // This is an extra element for new rows so rowset data is   
         // not overwritten. Insert the new row. Row 11 corresponds   
         // to index 10.  
         GetNewData(&CustIDArray[10], &CustIDIndArray[10],  
                     NameArray[10], &NameLenOrIndArray[10],  
                     AddressArray[10], &AddressLenOrIndArray[10],  
                     PhoneArray[10], &PhoneLenOrIndArray[10]);  
         SQLSetPos(hstmt, 11, SQL_ADD, SQL_LOCK_NO_CHANGE);  
         break;  
   }  
}  
  
// Close the cursor.  
SQLCloseCursor(hstmt);  
```
