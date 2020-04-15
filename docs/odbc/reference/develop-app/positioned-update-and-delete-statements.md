---
title: Instruções de atualização e exclusão posicionadas | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- positioned deletes [ODBC]
- data updates [ODBC], positioned update or delete
- positioned updates [ODBC]
- updating data [ODBC], positioned update or delete
ms.assetid: 0eafba50-02c7-46ca-a439-ef3307b935dc
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6e5316bee7057b30eace326b3ca82b30b75741fb
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81282357"
---
# <a name="positioned-update-and-delete-statements"></a>Instruções de atualização e exclusão posicionadas
Os aplicativos podem atualizar ou excluir a linha atual em um conjunto de resultados com uma atualização posicionada ou uma declaração de exclusão. As declarações de atualização e exclusão posicionadas são suportadas por algumas fontes de dados, mas não todas. Para determinar se uma fonte de dados suporta instruções posicionadas de atualização e exclusão, um aplicativo chama **sqlGetInfo** com o SQL_DYNAMIC_CURSOR_ATTRIBUTES1, SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1, SQL_KEYSET_CURSOR_ATTRIBUTES1 ou SQL_STATIC_CURSOR_ATTRIBUTES1 *InfoType* (dependendo do tipo do cursor). Observe que a biblioteca do cursor ODBC simula a atualização posicionada e exclui as declarações.  
  
 Para usar uma declaração de atualização ou exclusão posicionada, o aplicativo deve criar um conjunto de resultados com uma declaração **SELECT FOR UPDATE.** A sintaxe desta declaração é:  
  
 **Selecionar** [**TODAS as** &#124; **LISTA** *DISTINTA* ]  
  
 **DA** *lista de referência da tabela*  
  
 [**ONDE** *condição de pesquisa*]  
  
 **Para atualização de** [*nome da coluna* [**,** nome *da coluna*]...]  
  
 Em seguida, o aplicativo posiciona o cursor na linha para ser atualizado ou excluído. Ele pode fazer isso chamando **SQLFetchScroll** para recuperar um conjunto de linhas contendo a linha necessária e chamando **SQLSetPos** para posicionar o cursor de conjunto de linhas nessa linha. Em seguida, o aplicativo executa a declaração de atualização posicionada ou exclusão em uma declaração diferente da declaração que está sendo usada pelo conjunto de resultados. A sintaxe dessas declarações é:  
  
 **ATUALIZAR** *nome da tabela*  
  
 **Identificador** *column-identifier* **=** de coluna SET {*expressão* &#124; **NULL**}  
  
 [**,** *foto-identificador* **=** de coluna {*expressão* &#124; **NULL**}]...  
  
 **ONDE CORRENTE DO** *cursor-nome*  
  
 **EXCLUIR DO** *nome da tabela* ONDE CORRENTE **DO** *cursor-nome*  
  
 Observe que essas declarações requerem um nome de cursor. O aplicativo pode especificar um nome de cursor com **SQLSetCursorName** antes de executar a declaração que cria o conjunto de resultados ou pode permitir que a fonte de dados gere automaticamente um nome cursor quando o cursor for criado. Neste último caso, o aplicativo recupera este nome cursor para uso em instruções de atualização posicionadas e exclusão, chamando **SQLGetCursorName**.  
  
 Por exemplo, o código a seguir permite que um usuário role pela tabela Clientes e exclua registros de clientes ou atualize seus endereços e números de telefone. Ele chama **sqlSetCursorName** para especificar um nome de cursor antes de criar o conjunto de resultados de clientes e usa três alças de declaração: *hstmtCust* para o conjunto de resultados, *hstmtUpdate* para uma declaração de atualização posicionada e *hstmtDelete* para uma declaração de exclusão posicionada. Embora o código possa vincular variáveis separadas aos parâmetros da declaração de atualização posicionada, ele atualiza os buffers do conjunto de linhas e vincula os elementos desses buffers. Isso mantém os buffers de conjunto de linhas sincronizados com os dados atualizados.  
  
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
