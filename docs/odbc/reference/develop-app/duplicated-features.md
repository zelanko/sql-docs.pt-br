---
title: Recursos duplicados | Microsoft Docs
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
ms.openlocfilehash: ca73b5b9b41c99bd6db8e6181fa3582cae47c1d1
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68046897"
---
# <a name="duplicated-features"></a>Recursos duplicados
As funções ODBC *2. x* a seguir foram duplicadas pelas funções ODBC *3. x* . Como resultado, as funções ODBC *2. x* são preteridas no ODBC *3. x*. As funções ODBC *3. x* são chamadas de funções de substituição.  
  
 Quando um aplicativo usa uma função ODBC *2. x* substituída e o driver subjacente é um driver ODBC *3. x* , o Gerenciador de driver mapeia a chamada de função para a função de substituição correspondente. A única exceção a essa regra é **SQLExtendedFetch**. (Consulte a nota de rodapé no final da tabela a seguir.) Para obter mais informações sobre esses mapeamentos, consulte [mapeando funções preteridas](../../../odbc/reference/appendixes/mapping-deprecated-functions.md) no apêndice G: diretrizes de driver para compatibilidade com versões anteriores.  
  
 Quando um aplicativo usa uma função de substituição e o driver subjacente é um driver ODBC *2. x* , o Gerenciador de driver mapeia a chamada de função para a função preterida correspondente.  
  
|Função ODBC *2. x*|Função ODBC *3. x*|  
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
|**SQLParamOptions**|**SQLSetStmtAttr**, **SQLGetStmtAttr**|  
|**SQLSetConnectOption**|**SQLSetConnectAttr**|  
|**SQLSetParam**|**SQLBindParameter**|  
|**SQLSetStmtOption**|**SQLSetStmtAttr**|  
|**SQLTransact**|**SQLEndTran**|  
  
 [1] a função **SQLExtendedFetch** é uma funcionalidade duplicada; O **SQLFetchScroll** fornece a mesma funcionalidade no ODBC *3. x*. No entanto, o Gerenciador de driver não mapeia **SQLExtendedFetch** para **SQLFetchScroll** ao ir para um driver ODBC *3. x* . Para obter mais informações, consulte o [que o Gerenciador de driver faz](../../../odbc/reference/appendixes/what-the-driver-manager-does.md) no apêndice G: diretrizes de driver para compatibilidade com versões anteriores. O Gerenciador de driver mapeia **SQLFetchScroll** para **SQLExtendedFetch** ao ir para um driver ODBC *2. x* .  
  
> [!NOTE]
>  A função **SQLBindParam** é um caso especial. **SQLBindParam** é uma funcionalidade duplicada. Essa não é uma função ODBC *2. x* , mas uma função que está presente no grupo aberto e nos padrões ISO. A funcionalidade fornecida por essa função é completamente incorporadasda pelo **SQLBindParameter**. Como resultado, o Gerenciador de driver mapeia uma chamada para **SQLBindParam** para **SQLBindParameter** quando o driver subjacente é um driver ODBC *3. x* . No entanto, quando o driver subjacente é um driver ODBC *2. x* , o Gerenciador de driver não executa esse mapeamento.
