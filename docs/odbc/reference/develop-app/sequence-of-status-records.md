---
title: "Sequência de registros de Status | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- diagnostic information [ODBC], diagnostic records
- status records [ODBC]
- diagnostic records [ODBC]
ms.assetid: 0e0436cc-230f-44b0-b373-04a57e83ee76
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a101cf26b66f3556330354c0fa9ded4c6d9ad583
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="sequence-of-status-records"></a>Sequência de registros de Status
Se dois ou mais registros de status são retornados, o Gerenciador de Driver e o driver classificação-las de acordo com as regras a seguir. O registro com a classificação mais alta é o primeiro registro. A fonte de um registro (Gerenciador de Driver, driver, gateway e assim por diante) não é considerada quando registros de classificação.  
  
-   **Erros** registros de Status que descrevem erros têm a classificação mais alta. Entre os registros de erro, os registros que indicam uma falha de transação ou a falha na transação possíveis outrank todos os outros registros. Se dois ou mais registros descrevem a mesma condição de erro, SQLSTATEs definidas pela especificação de CLI do grupo aberto (classes 03 por meio de HZ) outrank SQLSTATEs definidas pelo ODBC e definidos pelo driver.  
  
-   **Os valores de dados não definido pela implementação** registros de Status que descrevem os valores de dados não definidos pelo driver (classe 02) têm a segunda classificação mais alta.  
  
-   **Avisos** registros de Status que descreve os avisos (classe 01) têm a classificação mais baixa. Se dois ou mais registros descrevem a mesma condição de aviso, aviso SQLSTATEs definidas pela especificação de CLI do grupo aberto outrank SQLSTATEs definidas pelo ODBC e definidos pelo driver.  
  
 Se houver dois ou mais registros com classificação mais alta, não está definido qual for o primeiro registro. A ordem de todos os outros registros é indefinida. Em particular, porque podem aparecer antes de erros, aplicativos devem verificar todos os registros de status quando uma função retorna um valor diferente de SQL_SUCCESS.
