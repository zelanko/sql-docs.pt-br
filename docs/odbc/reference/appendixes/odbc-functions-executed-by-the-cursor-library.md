---
title: Funções ODBC executadas pela Biblioteca Cursor | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- cursor library [ODBC], functions
- functions [ODBC], cursor library
- ODBC functions [ODBC], cursor library
- ODBC cursor library [ODBC], functions
ms.assetid: 2f1d3386-7e59-4d55-a5b4-3440b61343a3
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 70fb48a8764a913ea4c2376c1a44bcd8712e7d29
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298226"
---
# <a name="odbc-functions-executed-by-the-cursor-library"></a>Funções ODBC executadas pela biblioteca de cursores
> [!IMPORTANT]  
>  Esse recurso será removido em uma versão futura do Windows. Evite usar esse recurso em novos trabalhos de desenvolvimento e planeje modificar aplicativos que atualmente usam esse recurso. A Microsoft recomenda o uso da funcionalidade do cursor do driver.  
  
 A biblioteca do cursor executa as seguintes funções. Quando um aplicativo chama uma função nesta lista, o Gerenciador de driver invoca a biblioteca do cursor, não o driver. Observe que a biblioteca do cursor pode chamar o driver ao executar a função.  
  
|||  
|-|-|  
|**SQLBindCol**|**Opção SQLGetStmt**|  
|**SQLBindParam**|**SQLNativeSql**|  
|**SQLBindParameter**|**SQLNumParams**|  
|**SQLCloseCursor**|**Opções de SQLParam**|  
|**SQLEndTran**|**SQLRowCount**|  
|**Sqlextendedfetch**|**SQLSetConnectAttr**|  
|**SQLFetchScroll**|**Sqlsetconnectoption**|  
|**SQLFreeHandle**|**SQLSetDescField**|  
|**SQLFreeStmt**|**SQLSetDescRec**|  
|**SQLGetData**|**SQLSetPos**|  
|**SQLGetDescField**|**Opções de SQLSetScroll**|  
|**SQLGetDescRec**|**SQLSetStmtAttr**|  
|**SQLGetFunctions**|**SQLSetStmtOpção**|  
|**SQLGetInfo**|**SQLTransact**|  
|**SQLGetStmtAttr**||
