---
title: Duplicado recursos | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- duplicated functions [ODBC]
- compatibility [ODBC], duplicated functions
- ODBC drivers [ODBC], backward compatibility
- functions [ODBC], duplicated functions
- backward compatibility [ODBC], duplicated functions
ms.assetid: 641b16bc-f791-46d8-b093-31736473fe3d
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c88175f314290c06c4239a9ca855ce41512be2b9
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47707224"
---
# <a name="duplicated-features"></a>Recursos duplicados
A seguir ODBC 2. *x* funções foram duplicadas em ODBC 3. *x* funções. Como resultado, o ODBC 2. *x* funções foram preteridas em ODBC 3. *x*. O ODBC 3. *x* funções são referidas como funções de substituição.  
  
 Quando um aplicativo usa um preterido ODBC 2. *x* função e o driver subjacente é um ODBC 3. *x* driver, o Gerenciador de Driver mapeia a chamada de função para a função de substituição correspondentes. A única exceção a essa regra é **SQLExtendedFetch**. (Consulte a nota de rodapé no final da tabela a seguir). Para obter mais informações sobre esses mapeamentos, consulte [mapeamento funções preteridas](../../../odbc/reference/appendixes/mapping-deprecated-functions.md) no Apêndice g: Driver diretrizes para compatibilidade com versões anteriores.  
  
 Quando um aplicativo usa uma função de substituição e o driver subjacente é um ODBC 2. *x* driver, o Gerenciador de Driver mapeia a chamada de função para a função preterida correspondente.  
  
|ODBC 2. *x* função|ODBC 3. *x* função|  
|-------------------------|-------------------------|  
|**SQLAllocConnect**|**Falha de SQLAllocHandle**|  
|**SQLAllocEnv**|**Falha de SQLAllocHandle**|  
|**SQLAllocStmt**|**Falha de SQLAllocHandle**|  
|**SQLColAttributes**|**SQLColAttribute**|  
|**SQLError**|**SQLGetDiagRec**|  
|**SQLExtendedFetch**[1]|**SQLFetchScroll**|  
|**SQLFreeConnect**|**SQLFreeHandle**|  
|**SQLFreeEnv**|**SQLFreeHandle**|  
|**SQLGetConnectOption**|**SQLGetConnectAttr**|  
|**SQLGetStmtOption**|**SQLGetStmtAttr**|  
|**SQLParamOptions**|**SQLSetStmtAttr**, **SQLGetStmtAttr**|  
|**SQLSetConnectOption**|**SQLSetConnectAttr**|  
|**SQLSetParam**|**SQLBindParameter**|  
|**SQLSetStmtOption**|**SQLSetStmtAttr**|  
|**SQLTransact**|**SQLEndTran**|  
  
 [1] a função **SQLExtendedFetch** é uma funcionalidade duplicada; **SQLFetchScroll** fornece a mesma funcionalidade em ODBC 3. *x*. No entanto, o Gerenciador de Driver não mapeia **SQLExtendedFetch** à **SQLFetchScroll** quando vai contra um ODBC 3. *x* driver. Para obter mais informações, consulte [o que o Gerenciador de Driver faz](../../../odbc/reference/appendixes/what-the-driver-manager-does.md) no Apêndice g: Driver diretrizes para compatibilidade com versões anteriores. O Gerenciador de Driver mapeia **SQLFetchScroll** à **SQLExtendedFetch** quando vai contra um ODBC 2. *x* driver.  
  
> [!NOTE]  
>  A função **SQLBindParam** é um caso especial. **SQLBindParam** é a função duplicada. Isso não é um ODBC 2 *. x* função, mas uma função que está presente nos padrões ISO e Open Group. A funcionalidade fornecida por essa função é completamente incluída da **SQLBindParameter**. Como resultado, o Gerenciador de Driver mapeia uma chamada para **SQLBindParam** à **SQLBindParameter** quando o driver subjacente é um ODBC 3. *x* driver. No entanto, quando o driver subjacente é um ODBC 2 *. x* driver, o Gerenciador de Driver não realiza esse mapeamento.
