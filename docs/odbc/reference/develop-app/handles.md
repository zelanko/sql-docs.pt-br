---
title: Identificadores | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81300206"
---
# <a name="handles"></a>Alças
Os identificadores são valores opacos de 32 bits que identificam um item específico; no ODBC, esse item pode ser um ambiente, uma conexão, uma instrução ou um descritor. Quando o aplicativo chama **SQLAllocHandle**, o Driver Manager ou driver cria um novo item do tipo especificado e retorna seu identificador para o aplicativo. Posteriormente, o aplicativo usa o identificador para identificar esse item ao chamar funções ODBC. O driver e o Gerenciador de driver usam o identificador para localizar informações sobre o item.  
  
 Por exemplo, o código a seguir usa dois identificadores de instrução (*hstmtOrder* e *hstmtLine*) para identificar as instruções nas quais criar conjuntos de resultados de ordens de venda e números de linha de ordem de venda. Posteriormente, ele usa esses identificadores para identificar o conjunto de resultados do qual buscar dados.  
  
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
  
 Os identificadores são significativos apenas para o componente ODBC que os criou; ou seja, somente o Gerenciador de driver pode interpretar identificadores do Gerenciador de driver e apenas um driver pode interpretar seus próprios identificadores.  
  
 Por exemplo, suponha que o driver no exemplo anterior aloque uma estrutura para armazenar informações sobre uma instrução e retorna o ponteiro para essa estrutura como o identificador da instrução. Quando o aplicativo chama **SQLPrepare**, ele passa uma instrução SQL e o identificador da instrução usada para números de linha de ordem de venda. O driver envia a instrução SQL para a fonte de dados, que a prepara e retorna um identificador de plano de acesso. O driver usa o identificador para localizar a estrutura na qual armazenar esse identificador.  
  
 Posteriormente, quando o aplicativo chama **SQLExecute** para gerar o conjunto de resultados de números de linha para uma ordem de venda específica, ele passa o mesmo identificador. O driver usa o identificador para recuperar o identificador de plano de acesso da estrutura. Ele envia o identificador para a fonte de dados para informar qual plano deve ser executado.  
  
 O ODBC tem dois níveis de identificadores: identificadores do Gerenciador de driver e identificadores de driver. O aplicativo usa identificadores do Gerenciador de driver ao chamar funções ODBC porque ele chama essas funções no Gerenciador de driver. O Gerenciador de driver usa esse identificador para localizar o identificador de driver correspondente e usa o identificador de driver ao chamar a função no driver. Para obter um exemplo de como os identificadores do driver e do Gerenciador de driver são usados, consulte [função do Gerenciador de driver no processo de conexão](../../../odbc/reference/develop-app/driver-manager-s-role-in-the-connection-process.md).  
  
 Que há dois níveis de identificadores é um artefato da arquitetura ODBC; na maioria dos casos, não é relevante para o aplicativo ou driver. Embora geralmente não haja motivo para isso, é possível que o aplicativo determine os identificadores de driver chamando **SQLGetInfo**.  
  
 Esta seção contém os seguintes tópicos.  
  
-   [Identificadores de ambiente](../../../odbc/reference/develop-app/environment-handles.md)  
  
-   [Identificadores de conexão](../../../odbc/reference/develop-app/connection-handles.md)  
  
-   [Identificadores de instrução](../../../odbc/reference/develop-app/statement-handles.md)  
  
-   [Identificadores de descritor](../../../odbc/reference/develop-app/descriptor-handles.md)  
  
-   [Transições de estado](../../../odbc/reference/develop-app/state-transitions.md)
