---
title: SQLSetStmtAttr (biblioteca de Cursor) | Microsoft Docs
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
helpviewer_keywords: SQLSetStmtAttr function [ODBC], Cursor Library
ms.assetid: 6018a733-c2c8-4047-92ec-92cf85031767
caps.latest.revision: "8"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 2d707170f7e321ce41d096da6651c0e825621713
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="sqlsetstmtattr-cursor-library"></a>SQLSetStmtAttr (biblioteca de Cursor)
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. A Microsoft recomenda o uso da funcionalidade de cursor do driver.  
  
 Este tópico discute o uso do **SQLSetStmtAttr** função na biblioteca de cursor. Para obter informações gerais sobre **SQLSetStmtAttr**, consulte [função SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md).  
  
 A biblioteca de cursores suporta os seguintes atributos de instrução com **SQLSetStmtAttr**:  
  
|||  
|-|-|  
|SQL_ATTR_CONCURRENCY|SQL_ATTR_ROW_BIND_OFFSET_PTR|  
|SQL_ATTR_CURSOR_TYPE|SQL_ATTR_ROW_BIND_TYPE|  
|SQL_ATTR_FETCH_BOOKMARK_PTR|SQL_ATTR_ROWSET_ARRAY_SIZE|  
|SQL_ATTR_PARAM_BIND_OFFSET_PTR|SQL_ATTR_SIMULATE_CURSOR|  
|SQL_ATTR_PARAM_BIND_TYPE|SQL_ATTR_USE_BOOKMARKS|  
  
 A biblioteca de cursores dá suporte a apenas os valores SQL_CURSOR_FORWARD_ONLY e SQL_CURSOR_STATIC do atributo de instrução SQL_ATTR_CURSOR_TYPE.  
  
 Para cursores de somente avanço, a biblioteca de cursores suporta o valor SQL_CONCUR_READ_ONLY do atributo de instrução SQL_ATTR_CONCURRENCY. Cursores estáticos, a biblioteca de cursores dá suporte aos valores de atributo de instrução SQL_ATTR_CONCURRENCY SQL_CONCUR_READ_ONLY e SQL_CONCUR_VALUES.  
  
 A biblioteca de cursores dá suporte a apenas o valor SQL_SC_NON_UNIQUE do atributo de instrução SQL_ATTR_SIMULATE_CURSOR.  
  
 Embora a especificação de ODBC dá suporte a chamadas para **SQLSetStmtAttr** com os atributos SQL_ATTR_PARAM_BIND_TYPE ou SQL_ATTR_ROW_BIND_TYPE após **SQLFetch** ou **SQLFetchScroll**  foi chamado, o cursor biblioteca não. Antes que ele pode alterar o tipo de associação na biblioteca de cursor, o aplicativo deve fechar o cursor. A biblioteca de cursores oferece suporte à alteração SQL_ATTR_ROW_BIND_OFFSET_PTR SQL_ATTR_PARAM_BIND_OFFSET_PTR, SQL_ATTR_ROWS_FETCHED_PTR e atributos de instrução SQL_ATTR_PARAMS_PROCESSED_PTR quando um cursor é aberto.  
  
 Um aplicativo pode chamar **SQLSetStmtAttr** com um **atributo** de SQL_ATTR_ROW_ARRAY_SIZE para alterar o tamanho do conjunto de linhas, enquanto um cursor é aberto. O novo tamanho do conjunto de linhas entrará em vigor na próxima vez que **SQLFetchScroll** ou **SQLFetch** é chamado.  
  
 A biblioteca de cursores dá suporte à configuração do atributo de instrução SQL_ATTR_PARAM_BIND_OFFSET_PTR ou SQL_ATTR_ROW_BIND_OFFSET_PTR para habilitar os deslocamentos de associação. O deslocamento de associação não será usado para chamadas para **SQLFetch** quando a biblioteca de cursores é usada com um ODBC 2. *x* driver.  
  
 A biblioteca de cursores dá suporte à configuração do atributo de instrução de SQL_ATTR_USE_BOOKMARKS para SQL_UB_VARIABLE.
