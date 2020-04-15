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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0ce0c043fcfad41a624ad129a757a047d2c87fb6
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305727"
---
# <a name="executing-batches"></a>Lotes em execução
Antes que um aplicativo execute um lote de declarações, ele deve primeiro verificar se eles são suportados. Para isso, o aplicativo chama **o SQLGetInfo** com as opções SQL_BATCH_SUPPORT, SQL_PARAM_ARRAY_ROW_COUNTS e SQL_PARAM_ARRAY_SELECTS. A primeira opção retorna se as instruções de geração de contagem de linhas e de geração de resultados são suportadas em lotes e procedimentos explícitos, enquanto as duas últimas opções retornam informações sobre a disponibilidade de contagem de linhas e conjuntos de resultados em execução parametrizada.  
  
 Os lotes de instruções são executados através **do SQLExecute** ou **do SQLExecDirect**. Por exemplo, a chamada a seguir executa um lote explícito de declarações para abrir uma nova ordem de venda.  
  
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
  
 Quando um lote de instruções geradoras de resultados é executado, ele retorna uma ou mais contagens de linha ou conjuntos de resultados. Para obter informações sobre como recuperá-los, consulte [Múltiplos Resultados](../../../odbc/reference/develop-app/multiple-results.md).  
  
 Se um lote de declarações incluir marcadores de parâmetros, estes serão numerados na ordem de parâmetros crescente como estão em qualquer outra instrução. Por exemplo, o lote a seguir de declarações tem parâmetros numerados de 1 a 21; aqueles na primeira instrução **INSERT** são numerados de 1 a 5 e aqueles na última instrução **INSERT** são numerados de 18 a 21.  
  
```  
INSERT INTO Orders (OrderID, CustID, OpenDate, SalesPerson, Status)  
   VALUES (?, ?, ?, ?, ?);  
INSERT INTO Lines (OrderID, Line, PartID, Quantity) VALUES (?, ?, ?, ?);  
INSERT INTO Lines (OrderID, Line, PartID, Quantity) VALUES (?, ?, ?, ?);  
INSERT INTO Lines (OrderID, Line, PartID, Quantity) VALUES (?, ?, ?, ?);  
INSERT INTO Lines (OrderID, Line, PartID, Quantity) VALUES (?, ?, ?, ?);  
```  
  
 Para obter mais informações sobre parâmetros, consulte [Parâmetros de declaração,](../../../odbc/reference/develop-app/statement-parameters.md)mais tarde nesta seção.
