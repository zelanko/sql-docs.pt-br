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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 00f5529cfbfacebcad78a0a4433e84f34034694a
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300476"
---
# <a name="duplicated-features"></a>Recursos duplicados
As seguintes funções ODBC *2.x* foram duplicadas pelas funções ODBC *3.x.* Como resultado, as funções ODBC *2.x* são depreciadas em ODBC *3.x*. As funções ODBC *3.x* são referidas como funções de substituição.  
  
 Quando um aplicativo usa uma função ODBC *2.x* depreciada e o driver subjacente é um driver ODBC *3.x,* o Driver Manager mapeia a chamada de função para a função de substituição correspondente. A única exceção a esta regra é **SQLExtendedFetch**. (Veja a nota de rodapé no final da tabela a seguir.) Para obter mais informações sobre esses mapeamentos, consulte [Mapeamento de Funções Depreciadas](../../../odbc/reference/appendixes/mapping-deprecated-functions.md) no Apêndice G: Diretrizes do driver para compatibilidade retrógrada.  
  
 Quando um aplicativo usa uma função de substituição e o driver subjacente é um driver ODBC *2.x,* o Driver Manager mapeia a chamada de função para a função depreciada correspondente.  
  
|Função ODBC *2.x*|Função ODBC *3.x*|  
|-------------------------|-------------------------|  
|**SQLAllocConnect**|**SQLAllocHandle**|  
|**SQLAllocEnv**|**SQLAllocHandle**|  
|**SQLAllocStmt**|**SQLAllocHandle**|  
|**SQLColAttributea**|**SQLColAttribute**|  
|**Sqlerror**|**SQLGetDiagRec**|  
|**SQLExtendedFetch**[1]|**SQLFetchScroll**|  
|**SQLFreeConnect**|**SQLFreeHandle**|  
|**SQLFreeEnv**|**SQLFreeHandle**|  
|**Opção SQLGetConnect**|**SQLGetConnectAttr**|  
|**Opção SQLGetStmt**|**SQLGetStmtAttr**|  
|**Opções de SQLParam**|**SQLSetStmtAttr**, **SQLGetStmtAttr**|  
|**Sqlsetconnectoption**|**SQLSetConnectAttr**|  
|**SQLSetParam**|**SQLBindParameter**|  
|**SQLSetStmtOpção**|**SQLSetStmtAttr**|  
|**SQLTransact**|**SQLEndTran**|  
  
 [1] A função **SQLExtendedFetch** é a funcionalidade duplicada; **SQLFetchScroll** fornece a mesma funcionalidade no ODBC *3.x*. No entanto, o Driver Manager não mapeia **SQLExtendedFetch** para **SQLFetchScroll** ao ir contra um driver ODBC *3.x.* Para obter mais informações, consulte [o que o driver manager faz](../../../odbc/reference/appendixes/what-the-driver-manager-does.md) no apêndice G: Diretrizes do driver para compatibilidade retrógrada. O Driver Manager mapeia **SQLFetchScroll** para **SQLExtendedFetch** ao ir contra um driver ODBC *2.x.*  
  
> [!NOTE]
>  A função **SQLBindParam** é um caso especial. **SQLBindParam** é uma funcionalidade duplicada. Esta não é uma função ODBC *2.x,* mas uma função que está presente nos padrões Open Group e ISO. A funcionalidade fornecida por esta função é completamente subsumida pela de **SQLBindParameter**. Como resultado, o Driver Manager mapeia uma chamada para **SQLBindParam** para **SQLBindParameter** quando o driver subjacente é um driver ODBC *3.x.* No entanto, quando o driver subjacente é um driver ODBC *2.x,* o Driver Manager não realiza esse mapeamento.
