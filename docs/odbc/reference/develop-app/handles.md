---
title: Manipula | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- handles [ODBC]
- driver handles [ODBC]
- driver manager [ODBC], handles
- handles [ODBC], about handles
ms.assetid: f663101e-a4cc-402b-b9d7-84d5e975be71
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 05788f48f4a3fdb695fc3064023e52c2a3750c2e
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="handles"></a>Alças
Identificadores são valores opacos, 32 bits que identifica um item específico; no ODBC, este item pode ser um ambiente, a conexão, a instrução ou o descritor. Quando o aplicativo chama **SQLAllocHandle**, o Gerenciador de Driver ou driver cria um novo item do tipo especificado e retorna o identificador para o aplicativo. Posteriormente, o aplicativo usa o identificador para identificar o item ao chamar funções ODBC. O Gerenciador de Driver e o driver usam o identificador para localizar informações sobre o item.  
  
 Por exemplo, o código a seguir usa dois identificadores de instrução (*hstmtOrder* e *hstmtLine*) para identificar as instruções no qual criar conjuntos de resultados de vendas de vendas e pedidos de ordem de números de linha. Posteriormente, ele usa essas alças para identificar qual resultado definido como para obter dados.  
  
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
  
 Os identificadores são significativos somente para o componente ODBC que foram criadas; ou seja, o Gerenciador de Driver pode interpretar os identificadores do Gerenciador de Driver e apenas um driver pode interpretar seus próprios identificadores.  
  
 Por exemplo, suponha que o driver no exemplo anterior, aloca uma estrutura para armazenar informações sobre uma instrução e retorna o ponteiro para essa estrutura como o identificador de instrução. Quando o aplicativo chama **SQLPrepare**, ele transmite uma instrução SQL e o identificador da instrução usada para números de linha do pedido de vendas. O driver envia a instrução SQL para a fonte de dados, o que prepara e retorna um identificador de plano de acesso. O driver usa o identificador para localizar a estrutura na qual deseja armazenar esse identificador.  
  
 Posteriormente, quando o aplicativo chama **SQLExecute** para gerar o conjunto de resultados de números de linha para uma determinada ordem de venda, transmite o mesmo identificador. O driver usa o identificador para recuperar o identificador do plano de acesso da estrutura. Envia o identificador para a fonte de dados para informá-lo que planeja executar.  
  
 ODBC tem dois níveis de identificadores: identificadores de Gerenciador de Driver e driver. O aplicativo usa identificadores de Gerenciador de Driver ao chamar funções ODBC porque chama as funções no Gerenciador de Driver. O Gerenciador de Driver usa esse identificador para localizar o identificador do driver correspondente e usa o identificador do driver ao chamar a função no driver. Para obter um exemplo de como o driver e o Gerenciador de Driver identificadores são usados, consulte [do Gerenciador de Driver de função no processo de Conexão](../../../odbc/reference/develop-app/driver-manager-s-role-in-the-connection-process.md).  
  
 Que há dois níveis de identificadores de é um artefato da arquitetura do ODBC; Na maioria dos casos, não é relevante para o aplicativo ou driver. Embora normalmente não há nenhum motivo para fazer isso, é possível que o aplicativo determinar os identificadores de driver chamando **SQLGetInfo**.  
  
 Esta seção contém os tópicos a seguir.  
  
-   [Identificadores de ambiente](../../../odbc/reference/develop-app/environment-handles.md)  
  
-   [Identificadores de conexão](../../../odbc/reference/develop-app/connection-handles.md)  
  
-   [Identificadores de instrução](../../../odbc/reference/develop-app/statement-handles.md)  
  
-   [Identificadores de descritor](../../../odbc/reference/develop-app/descriptor-handles.md)  
  
-   [Transições de estado](../../../odbc/reference/develop-app/state-transitions.md)

