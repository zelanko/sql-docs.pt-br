---
title: Executando lotes | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- batches [ODBC], executing
- SQL statements [ODBC], batches
ms.assetid: f082c717-4f82-4820-a2fa-ba607d8fd872
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 22c034d4be28ca8c3212fad4ee1493cb0a22d915
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32909891"
---
# <a name="executing-batches"></a>Lotes em execução
Antes de um aplicativo executa um lote de instruções, deve primeiro verificar se eles têm suporte. Para fazer isso, o aplicativo chama **SQLGetInfo** com as opções SQL_BATCH_SUPPORT, SQL_PARAM_ARRAY_ROW_COUNTS e SQL_PARAM_ARRAY_SELECTS. A primeira opção retorna se geração de contagem de linha e o resultado da geração de conjunto de instruções têm suporte em lotes explícitas e procedimentos, enquanto as duas últimas opções define retornam informações sobre a disponibilidade de contagens de linhas e o resultado em parametrizados execução.  
  
 Lotes de instruções são executadas por meio de **SQLExecute** ou **SQLExecDirect**. Por exemplo, a chamada a seguir executa um lote explícito de instruções para abrir uma nova ordem de venda.  
  
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
  
 Quando um lote de geração de resultado instruções é executado, ele retorna um ou mais contagens de linhas ou resultado define. Para obter informações sobre como recuperar essas, consulte [vários resultados](../../../odbc/reference/develop-app/multiple-results.md).  
  
 Se um lote de instruções inclui marcadores de parâmetro, eles são numerados de aumentar a ordem do parâmetro, como em qualquer outra instrução. Por exemplo, o lote de instruções a seguir tem parâmetros numerados de 1 a 21; aqueles na primeira **inserir** instrução são numerados 1 a 5 e aqueles na última **inserir** instrução são numerados 18 a 21.  
  
```  
INSERT INTO Orders (OrderID, CustID, OpenDate, SalesPerson, Status)  
   VALUES (?, ?, ?, ?, ?);  
INSERT INTO Lines (OrderID, Line, PartID, Quantity) VALUES (?, ?, ?, ?);  
INSERT INTO Lines (OrderID, Line, PartID, Quantity) VALUES (?, ?, ?, ?);  
INSERT INTO Lines (OrderID, Line, PartID, Quantity) VALUES (?, ?, ?, ?);  
INSERT INTO Lines (OrderID, Line, PartID, Quantity) VALUES (?, ?, ?, ?);  
```  
  
 Para obter mais informações sobre parâmetros, consulte [parâmetros de instrução](../../../odbc/reference/develop-app/statement-parameters.md), mais adiante nesta seção.
