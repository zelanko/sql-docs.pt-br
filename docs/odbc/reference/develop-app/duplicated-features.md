---
title: Duplicado recursos | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- duplicated functions [ODBC]
- compatibility [ODBC], duplicated functions
- ODBC drivers [ODBC], backward compatibility
- functions [ODBC], duplicated functions
- backward compatibility [ODBC], duplicated functions
ms.assetid: 641b16bc-f791-46d8-b093-31736473fe3d
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: b12ba1b5b8c70e6ab0f7efe6f0811984411a6022
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="duplicated-features"></a>Recursos duplicados
A seguir ODBC 2. *x* funções foram duplicadas pelo ODBC 3. *x* funções. Como resultado, o ODBC 2. *x* funções são substituídas no ODBC 3. *x*. O ODBC 3. *x* funções são referidas como funções de substituição.  
  
 Quando um aplicativo usa um preterido ODBC 2. *x* função e o driver subjacente é um ODBC 3. *x* driver, o Gerenciador de Driver mapeia a chamada de função para a função de substituição correspondente. A única exceção a essa regra é **SQLExtendedFetch**. (Consulte a nota de rodapé no final da tabela a seguir). Para obter mais informações sobre esses mapeamentos, consulte [mapeamento preterido funções](../../../odbc/reference/appendixes/mapping-deprecated-functions.md) no Apêndice g: Driver diretrizes para compatibilidade com versões anteriores.  
  
 Quando um aplicativo usa uma função de substituição e o driver subjacente é um ODBC 2. *x* driver, o Gerenciador de Driver mapeia a chamada de função para a função preterida correspondente.  
  
|ODBC 2. *x* função|ODBC 3. *x* função|  
|-------------------------|-------------------------|  
|**SQLAllocConnect**|**SQLAllocHandle**|  
|**SQLAllocEnv**|**SQLAllocHandle**|  
|**SQLAllocStmt**|**SQLAllocHandle**|  
|**SQLColAttributes**|**SQLColAttribute**|  
|**SQLError**|**SQLGetDiagRec**|  
|**SQLExtendedFetch**[1]|**SQLFetchScroll**|  
|**SQLFreeConnect**|**SQLFreeHandle**|  
|**SQLFreeEnv**|**SQLFreeHandle**|  
|**SQLGetConnectOption**|**SQLGetConnectAttr**|  
|**SQLGetStmtOption**|**SQLGetStmtAttr**|  
|**Para SQLParamOptions**|**SQLSetStmtAttr**, **SQLGetStmtAttr**|  
|**SQLSetConnectOption**|**SQLSetConnectAttr**|  
|**SQLSetParam**|**SQLBindParameter**|  
|**SQLSetStmtOption**|**SQLSetStmtAttr**|  
|**SQLTransact**|**SQLEndTran**|  
  
 [1] a função **SQLExtendedFetch** funcionalidade duplicados; **SQLFetchScroll** fornece a mesma funcionalidade em ODBC 3. *x*. No entanto, o Gerenciador de Driver não mapear **SQLExtendedFetch** para **SQLFetchScroll** partindo contra um ODBC 3. *x* driver. Para obter mais informações, consulte [que o Gerenciador de Driver faz](../../../odbc/reference/appendixes/what-the-driver-manager-does.md) no Apêndice g: Driver diretrizes para compatibilidade com versões anteriores. O Gerenciador de Driver mapeia **SQLFetchScroll** para **SQLExtendedFetch** partindo contra um ODBC 2. *x* driver.  
  
> [!NOTE]  
>  A função **SQLBindParam** é um caso especial. **SQLBindParam** funcionalidade duplicados. Isso não é um ODBC 2*. x* função, mas uma função que está presente nos padrões ISO e Open Group. A funcionalidade fornecida por essa função é completamente incluída do **SQLBindParameter**. Como resultado, o Gerenciador de Driver mapeia uma chamada para **SQLBindParam** para **SQLBindParameter** quando o driver subjacente é um ODBC 3. *x* driver. No entanto, quando o driver subjacente é um ODBC 2*. x* driver, o Gerenciador de Driver não executa esse mapeamento.

