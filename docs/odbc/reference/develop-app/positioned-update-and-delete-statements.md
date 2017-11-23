---
title: "Posicionado instruções Update e Delete | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- positioned deletes [ODBC]
- data updates [ODBC], positioned update or delete
- positioned updates [ODBC]
- updating data [ODBC], positioned update or delete
ms.assetid: 0eafba50-02c7-46ca-a439-ef3307b935dc
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a35d57aaa00f7f2406b779f987c4dd07e694f737
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/20/2017
---
# <a name="positioned-update-and-delete-statements"></a>Posicionada instruções Update e Delete
Aplicativos podem atualizar ou excluir a linha atual em um conjunto de resultados com uma atualização posicionada ou instrução delete. Posicionado update e delete instruções são suportadas por algumas fontes de dados, mas não todas. Para determinar se um suporte de fonte de dados posicionado instruções update e delete, um aplicativo chama **SQLGetInfo** com SQL_DYNAMIC_CURSOR_ATTRIBUTES1 SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1, SQL_KEYSET_CURSOR_ ATTRIBUTES1 ou SQL_STATIC_CURSOR_ATTRIBUTES1 *informação* (dependendo do tipo de cursor). Observe que a biblioteca de cursores ODBC simula posicionado instruções update e delete.  
  
 Para usar uma atualização posicionada ou instrução de exclusão, o aplicativo deve criar um conjunto de resultados com um **Selecione para atualizar** instrução. A sintaxe dessa instrução é:  
  
 **Selecione** [**todos os** &#124; **DISTINCT**] *lista de select*  
  
 **DE** *lista de referências de tabela*  
  
 [**Onde** *critério de pesquisa*]  
  
 **PARA atualização de** [*nome de coluna* [**,** *nome de coluna*]...]  
  
 O aplicativo, em seguida, posiciona o cursor na linha a ser atualizada ou excluída. Ele pode fazer isso chamando **SQLFetchScroll** para recuperar um conjunto de linhas que contém a linha necessária e chamando **SQLSetPos** para posicionar o cursor de conjunto de linhas em que a linha. O aplicativo executa a instrução delete ou atualização posicionada em uma instrução diferente que a instrução que está sendo usada pelo conjunto de resultados. A sintaxe das instruções a seguir é:  
  
 **ATUALIZAÇÃO** *nome de tabela*  
  
 **DEFINIR** *identificador de coluna*  **=**  {*expressão* &#124; **Nulo**}  
  
 [**,** *identificador de coluna*  **=**  {*expressão* &#124; **Nulo**}]...  
  
 **WHERE CURRENT OF** *nome de cursor*  
  
 **DELETE FROM** *nome de tabela* **WHERE CURRENT OF** *nome de cursor*  
  
 Observe que essas instruções exigem um nome de cursor. O aplicativo pode especificar um nome de cursor com **SQLSetCursorName** gerar um nome de cursor antes de executar a instrução que cria o resultado definido ou pode permitir que a fonte de dados automaticamente, quando o cursor é criado. No último caso, o aplicativo recupera esse nome de cursor para uso em instruções de exclusão e atualização posicionada chamando **SQLGetCursorName**.  
  
 Por exemplo, o código a seguir permite que um usuário rolar a tabela de clientes e excluir registros de cliente ou atualizar seus endereços e números de telefone. Ele chama **SQLSetCursorName** para especificar um nome de cursor antes que ele cria o conjunto de resultados de clientes e usa três identificadores de instrução: *hstmtCust* para o conjunto de resultados, *hstmtUpdate* para uma instrução de atualização posicionada, e *hstmtDelete* para um posicionadas instrução delete. Embora o código pode associar variáveis separadas para os parâmetros na instrução update posicionada, ele atualiza os buffers de linhas e associa os elementos desses buffers. Isso impede que os buffers de linhas sincronizados com os dados atualizados.  
  
```  
#define POSITIONED_UPDATE 100  
#define POSITIONED_DELETE 101  
  
SQLUINTEGER    CustIDArray[10];  
SQLCHAR        NameArray[10][51], AddressArray[10][51],   
               PhoneArray[10][11];  
SQLINTEGER     CustIDIndArray[10], NameLenOrIndArray[10],   
               AddressLenOrIndArray[10],  
               PhoneLenOrIndArray[10];  
SQLUSMALLINT   RowStatusArray[10], Action, RowNum;  
SQLHSTMT       hstmtCust, hstmtUpdate, hstmtDelete;  
  
// Set the SQL_ATTR_BIND_TYPE statement attribute to use column-wise   
// binding. Declare the rowset size with the SQL_ATTR_ROW_ARRAY_SIZE   
// statement attribute. Set the SQL_ATTR_ROW_STATUS_PTR statement   
// attribute to point to the row status array.  
SQLSetStmtAttr(hstmtCust, SQL_ATTR_ROW_BIND_TYPE, SQL_BIND_BY_COLUMN, 0);  
SQLSetStmtAttr(hstmtCust, SQL_ATTR_ROW_ARRAY_SIZE, 10, 0);  
SQLSetStmtAttr(hstmtCust, SQL_ATTR_ROW_STATUS_PTR, RowStatusArray, 0);  
  
// Bind arrays to the CustID, Name, Address, and Phone columns.  
SQLBindCol(hstmtCust, 1, SQL_C_ULONG, CustIDArray, 0, CustIDIndArray);  
SQLBindCol(hstmtCust, 2, SQL_C_CHAR, NameArray, sizeof(NameArray[0]),  
            NameLenOrIndArray);  
SQLBindCol(hstmtCust, 3, SQL_C_CHAR, AddressArray, sizeof(AddressArray[0]),  
         AddressLenOrIndArray);  
SQLBindCol(hstmtCust, 4, SQL_C_CHAR, PhoneArray, sizeof(PhoneArray[0]),  
            PhoneLenOrIndArray);  
  
// Set the cursor name to Cust.  
SQLSetCursorName(hstmtCust, "Cust", SQL_NTS);  
  
// Prepare positioned update and delete statements.  
SQLPrepare(hstmtUpdate,  
   "UPDATE Customers SET Address = ?, Phone = ? WHERE CURRENT OF Cust",  
   SQL_NTS);  
SQLPrepare(hstmtDelete, "DELETE FROM Customers WHERE CURRENT OF Cust", SQL_NTS);  
  
// Execute a statement to retrieve rows from the Customers table.  
SQLExecDirect(hstmtCust,  
   "SELECT CustID, Name, Address, Phone FROM Customers FOR UPDATE OF Address, Phone",  
   SQL_NTS);  
  
// Fetch and display the first 10 rows.  
SQLFetchScroll(hstmtCust, SQL_FETCH_NEXT, 0);  
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
         SQLFetchScroll(hstmtCust, Action, RowNum);  
         DisplayData(CustIDArray, CustIDIndArray, NameArray, NameLenOrIndArray,  
                     AddressArray, AddressLenOrIndArray, PhoneArray,  
                     PhoneLenOrIndArray, RowStatusArray);  
         break;  
  
      case POSITIONED_UPDATE:  
         // Get the new data and place it in the rowset buffers.  
         GetNewData(AddressArray[RowNum - 1], &AddressLenOrIndArray[RowNum - 1],  
                     PhoneArray[RowNum - 1], &PhoneLenOrIndArray[RowNum - 1]);  
  
         // Bind the elements of the arrays at position RowNum-1 to the   
         // parameters of the positioned update statement.  
         SQLBindParameter(hstmtUpdate, 1, SQL_PARAM_INPUT, SQL_C_CHAR, SQL_CHAR,  
                           50, 0, AddressArray[RowNum - 1], sizeof(AddressArray[0]),  
                           &AddressLenOrIndArray[RowNum - 1]);  
         SQLBindParameter(hstmtUpdate, 2, SQL_PARAM_INPUT, SQL_C_CHAR, SQL_CHAR,  
                           10, 0, PhoneArray[RowNum - 1], sizeof(PhoneArray[0]),  
                           &PhoneLenOrIndArray[RowNum - 1]);  
  
         // Position the rowset cursor. The rowset is 1-based.  
         SQLSetPos(hstmtCust, RowNum, SQL_POSITION, SQL_LOCK_NO_CHANGE);  
  
         // Execute the positioned update statement to update the row.  
         SQLExecute(hstmtUpdate);  
         break;  
  
      case POSITIONED_DELETE:  
         // Position the rowset cursor. The rowset is 1-based.  
         SQLSetPos(hstmtCust, RowNum, SQL_POSITION, SQL_LOCK_NO_CHANGE);  
  
         // Execute the positioned delete statement to delete the row.  
         SQLExecute(hstmtDelete);  
         break;  
   }  
}  
  
// Close the cursor.  
SQLCloseCursor(hstmtCust);  
```
