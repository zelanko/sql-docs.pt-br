---
title: Executando lotes | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- batches [ODBC], executing
- SQL statements [ODBC], batches
ms.assetid: f082c717-4f82-4820-a2fa-ba607d8fd872
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 84d3cf65284d767d437987c8ff2b21793466106e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67901267"
---
# <a name="executing-batches"></a>Lotes em execução
Antes que um aplicativo execute um lote de instruções, ele deve primeiro verificar se há suporte. Para fazer isso, o aplicativo chama **SQLGetInfo** com as opções SQL_BATCH_SUPPORT, SQL_PARAM_ARRAY_ROW_COUNTS e SQL_PARAM_ARRAY_SELECTS. A primeira opção retorna se as instruções de geração de contagem de linhas e de conjunto de resultados são suportadas em lotes e procedimentos explícitos, enquanto as duas últimas opções retornam informações sobre a disponibilidade de contagens de linhas e conjuntos de resultados em parâmetros chão.  
  
 Lotes de instruções são executados por meio de **SQLExecute** ou **SQLExecDirect**. Por exemplo, a chamada a seguir executa um lote explícito de instruções para abrir uma nova ordem de venda.  
  
```  
SQLCHAR *BatchStmt =  
   "INSERT INTO Orders (OrderID, CustID, OpenDate, SalesPerson, Status)"  
      "VALUES (2002, 1001, {fn CURDATE()}, 'Garcia', 'OPEN');"  
   "INSERT INTO Lines (OrderID, Line, PartID, Quantity) VALUES (2002, 1, 1234, 10);"  
   "INSERT INTO Lines (OrderID, Line, PartID, Quantity) VALUES (2002, 2, 987, 8);"  
   "INSERT INTO Lines (OrderID, Line, PartID, Quantity) VALUES (2002, 3, 566, 17);"  
   "INSERT INTO Lines (OrderID, Line, PartID, Quantity) VALUES (2002, 4, 412, 500)";  
  
SQLExecDirect(hstmt, BatchStmt, SQL_NTS);  
```  
  
 Quando um lote de instruções de geração de resultados é executado, ele retorna uma ou mais contagens de linhas ou conjuntos de resultados. Para obter informações sobre como recuperá-los, consulte [vários resultados](../../../odbc/reference/develop-app/multiple-results.md).  
  
 Se um lote de instruções incluir marcadores de parâmetro, eles serão numerados no aumento da ordem dos parâmetros como estão em qualquer outra instrução. Por exemplo, o seguinte lote de instruções tem parâmetros numerados de 1 a 21; aqueles na primeira instrução **Insert** são numerados de 1 a 5 e aqueles na última instrução **Insert** são numerados de 18 a 21.  
  
```  
INSERT INTO Orders (OrderID, CustID, OpenDate, SalesPerson, Status)  
   VALUES (?, ?, ?, ?, ?);  
INSERT INTO Lines (OrderID, Line, PartID, Quantity) VALUES (?, ?, ?, ?);  
INSERT INTO Lines (OrderID, Line, PartID, Quantity) VALUES (?, ?, ?, ?);  
INSERT INTO Lines (OrderID, Line, PartID, Quantity) VALUES (?, ?, ?, ?);  
INSERT INTO Lines (OrderID, Line, PartID, Quantity) VALUES (?, ?, ?, ?);  
```  
  
 Para obter mais informações sobre parâmetros, consulte [parâmetros de instrução](../../../odbc/reference/develop-app/statement-parameters.md), mais adiante nesta seção.
