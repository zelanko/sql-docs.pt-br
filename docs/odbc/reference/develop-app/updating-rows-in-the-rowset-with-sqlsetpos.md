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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: dfb57a6512245c9adb36a511ce48721dd901995c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63313095"
---
# <a name="updating-rows-in-the-rowset-with-sqlsetpos"></a>Atualizar linhas no conjunto de linhas com SQLSetPos
A operação de atualização do **SQLSetPos** faz com que a fonte de dados atualizar um ou mais linhas selecionadas de uma tabela, usando dados nos buffers de aplicativo para cada coluna associada (a menos que o valor no buffer de comprimento/indicador é SQL_COLUMN_IGNORE). Colunas que não são associadas não serão atualizadas.  
  
 Para atualizar linhas com **SQLSetPos**, o aplicativo faz o seguinte:  
  
1.  Coloca os novos valores de dados nos buffers de conjunto de linhas. Para obter informações sobre como enviar dados longos com **SQLSetPos**, consulte [dados Long e SQLSetPos e SQLBulkOperations](../../../odbc/reference/develop-app/long-data-and-sqlsetpos-and-sqlbulkoperations.md).  
  
2.  Define o valor no buffer de comprimento/indicador de cada coluna, conforme necessário. Esse é o comprimento de bytes dos dados ou SQL_NTS para colunas associadas a buffers de cadeia de caracteres, o tamanho de bytes dos dados para colunas associadas a buffers binários e SQL_NULL_DATA para todas as colunas a ser definido como NULL.  
  
3.  Define o valor no buffer de comprimento/indicador dessas colunas que não devem ser atualizados para SQL_COLUMN_IGNORE. Embora o aplicativo pode ignorar esta etapa e reenviar os dados existentes, isso é ineficiente e o risco de enviar valores para a fonte de dados foram truncados quando foram lidas.  
  
4.  Chamadas **SQLSetPos** com *operação* definido como SQL_UPDATE e *RowNumber* definido como o número da linha para atualizar. Se *RowNumber* for 0, todas as linhas no conjunto de linhas são atualizadas.  
  
 Após **SQLSetPos** retorna, a linha atual é definida como a linha atualizada.  
  
 Ao atualizar todas as linhas do conjunto de linhas (*RowNumber* é igual a 0), um aplicativo pode desativar a atualização de determinadas linhas, definindo os elementos correspondentes da matriz de operação de linha (apontada para o SQL_ATTR_ROW_OPERATION_PTR atributo de instrução) para SQL_ROW_IGNORE. A matriz de operação de linha corresponde no tamanho e número de elementos na matriz de status de linha (apontada para o atributo da instrução SQL_ATTR_ROW_STATUS_PTR). Para atualizar somente as linhas no conjunto de resultados que foram obtidas com êxito e não foram excluídas do conjunto de linhas, o aplicativo usa a matriz de status de linha da função que buscadas o conjunto de linhas como a matriz para a operação linha **SQLSetPos**.  
  
 Para cada linha é enviada à fonte de dados como uma atualização, os buffers do aplicativo devem ter dados de linha válido. Se os buffers do aplicativo foram preenchidos pela busca e se uma matriz de status de linha foi mantida, seus valores em cada uma das posições não devem ser SQL_ROW_DELETED, SQL_ROW_ERROR ou SQL_ROW_NOROW.  
  
 Por exemplo, o código a seguir permite que um usuário rolar a tabela de clientes e atualizar, excluir ou adicionar novas linhas. Ele coloca os novos dados nos buffers de conjunto de linhas antes de chamar **SQLSetPos** para atualizar ou adicionar novas linhas. Uma linha extra é alocada no final dos buffers de linhas para conter novas linhas; Isso impede que os dados existentes sendo substituído quando os dados para uma nova linha são colocados nos buffers.  
  
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
