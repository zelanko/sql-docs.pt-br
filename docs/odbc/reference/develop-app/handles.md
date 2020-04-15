---
title: Alças | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- handles [ODBC]
- driver handles [ODBC]
- driver manager [ODBC], handles
- handles [ODBC], about handles
ms.assetid: f663101e-a4cc-402b-b9d7-84d5e975be71
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 713c2a71ec195b75d682b97239413e98d07b5861
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300206"
---
# <a name="handles"></a>Alças
As alças são opacas, valores de 32 bits que identificam um determinado item; no ODBC, este item pode ser um ambiente, conexão, declaração ou descritor. Quando o aplicativo chama **SQLAllocHandle,** o Driver Manager ou driver cria um novo item do tipo especificado e retorna sua alça para o aplicativo. O aplicativo posteriormente usa a alça para identificar esse item ao chamar funções ODBC. O Driver Manager e o motorista usam a alça para localizar informações sobre o item.  
  
 Por exemplo, o código a seguir usa duas alças de instrução (*hstmtOrder* e *hstmtLine*) para identificar as instruções sobre as quais criar conjuntos de resultados de ordens de venda e números de linha de pedidos de venda. Mais tarde, ele usa essas alças para identificar qual resultado definido para buscar dados.  
  
```  
SQLHSTMT      hstmtOrder, hstmtLine; // Statement handles.  
SQLUINTEGER   OrderID;  
SQLINTEGER    OrderIDInd = 0;  
SQLRETURN     rc;  
  
// Prepare the statement that retrieves line number information.  
SQLPrepare(hstmtLine, "SELECT * FROM Lines WHERE OrderID = ?", SQL_NTS);  
  
// Bind OrderID to the parameter in the preceding statement.  
SQLBindParameter(hstmtLine, 1, SQL_PARAM_INPUT, SQL_C_ULONG, SQL_INTEGER, 5, 0,  
               &OrderID, 0, &OrderIDInd);  
  
// Bind the result sets for the Order table and the Lines table. Bind  
// OrderID to the OrderID column in the Orders table. When each row is  
// fetched, OrderID will contain the current order ID, which will then be  
// passed as a parameter to the statement tofetch line number  
// information. Code not shown.  
  
// Create a result set of sales orders.  
SQLExecDirect(hstmtOrder, "SELECT * FROM Orders", SQL_NTS);  
  
// Fetch and display the sales order data. Code to check if rc equals  
// SQL_ERROR or SQL_SUCCESS_WITH_INFO not shown.  
while ((rc = SQLFetch(hstmtOrder)) != SQL_NO_DATA) {  
   // Display the sales order data. Code not shown.  
  
   // Create a result set of line numbers for the current sales order.  
   SQLExecute(hstmtLine);  
  
   // Fetch and display the sales order line number data. Code to check  
   // if rc equals SQL_ERROR or SQL_SUCCESS_WITH_INFO not shown.  
   while ((rc = SQLFetch(hstmtLine)) != SQL_NO_DATA) {  
      // Display the sales order line number data. Code not shown.  
   }  
  
   // Close the sales order line number result set.  
   SQLCloseCursor(hstmtLine);  
}  
  
// Close the sales order result set.  
SQLCloseCursor(hstmtOrder);  
```  
  
 As alças são significativas apenas para o componente ODBC que as criou; ou seja, apenas o Driver Manager pode interpretar as alças do Driver Manager e apenas um motorista pode interpretar suas próprias alças.  
  
 Por exemplo, suponha que o driver no exemplo anterior aloque uma estrutura para armazenar informações sobre uma declaração e devolva o ponteiro para esta estrutura como a alça da declaração. Quando o aplicativo chama **SQLPrepare,** ele passa uma declaração SQL e a alça da declaração usada para números de linha de pedidos de vendas. O driver envia a declaração SQL para a fonte de dados, que a prepara e retorna um identificador de plano de acesso. O motorista usa a alça para encontrar a estrutura em que armazenar este identificador.  
  
 Mais tarde, quando o aplicativo chama **SQLExecute** para gerar o conjunto de resultados de números de linha para uma determinada ordem de venda, ele passa a mesma alça. O motorista usa a alça para recuperar o identificador do plano de acesso da estrutura. Ele envia o identificador para a fonte de dados para dizer qual plano executar.  
  
 A ODBC tem dois níveis de alças: alças do driver Manager e alças do driver. O aplicativo usa alças do Driver Manager ao ligar para funções ODBC porque ele chama essas funções no Gerenciador de driver. O Driver Manager usa esta alça para encontrar a alça do motorista correspondente e usa a alça do motorista ao chamar a função no motorista. Para obter um exemplo de como as alças driver e driver manager são usadas, consulte [a função do driver manager no processo de conexão](../../../odbc/reference/develop-app/driver-manager-s-role-in-the-connection-process.md).  
  
 Que existem dois níveis de alças é um artefato da arquitetura ODBC; na maioria dos casos, não é relevante nem para o aplicativo nem para o motorista. Embora geralmente não haja razão para fazê-lo, é possível que o aplicativo determine as alças do driver ligando para **sqlGetInfo**.  
  
 Esta seção contém os seguintes tópicos.  
  
-   [Identificadores de ambiente](../../../odbc/reference/develop-app/environment-handles.md)  
  
-   [Identificadores de conexão](../../../odbc/reference/develop-app/connection-handles.md)  
  
-   [Identificadores de instrução](../../../odbc/reference/develop-app/statement-handles.md)  
  
-   [Identificadores de descritor](../../../odbc/reference/develop-app/descriptor-handles.md)  
  
-   [Transições de estado](../../../odbc/reference/develop-app/state-transitions.md)
