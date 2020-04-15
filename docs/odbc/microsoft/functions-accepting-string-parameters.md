---
title: Funções aceitando parâmetros de corda | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- desktop database drivers [ODBC], string parameters
- ODBC desktop database drivers [ODBC], string parameters
- Jet-based ODBC drivers [ODBC], string parameters
- functions [ODBC], string parameters
- string parameters [ODBC]
ms.assetid: 869b8421-f71e-4dfd-adce-691bd3012b16
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 01d0f143c72f57e946f7fe2bf52a50910d4e56aa
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81286296"
---
# <a name="functions-accepting-string-parameters"></a>Funções que aceitam parâmetros de cadeias de caracteres
Todas as funções que tomam parâmetros de string serão convertidas em Unicode. (A forma "W" da função será exportada.) A contagem de bytes é convertida em contagem de caracteres para as APIs ODBC aplicáveis. Isso se aplica às seguintes funções:  
  
-   **SQLConnect**  
  
-   **SQLDriverConnect**  
  
-   **SQLColAttributea**  
  
-   **SQLDescribeCol**  
  
-   **SQLError** (substituído por **SQLGetDiagField**)  
  
-   **SQLExecDirect**  
  
-   **SQLGetCursorName**  
  
-   **Sqlsetcursorname**  
  
-   **SQLGetStmtAttr**  
  
-   **SQLGetInfo**  
  
-   **SQLGetStmtOption** (torna-se **SQLGetStmtAttr**)  
  
-   **SQLSetStmtOption** (torna-se **SQLSetStmtAttr**)  
  
-   **Opção SQLGetConnect**  
  
-   **Sqlsetconnectoption**  
  
-   **SQLGetTypeInfo**  
  
-   **SQLStatistics**  
  
-   **SQLTables**  
  
-   **SQlnativesqL**  
  
-   **SQLSpecialColumns**  
  
-   **ConfigdSnex**  
  
-   **Configdsn**
