---
title: SQLSetStmtAttr (biblioteca de cursores) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSetStmtAttr function [ODBC], Cursor Library
ms.assetid: 6018a733-c2c8-4047-92ec-92cf85031767
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7d4e5bd6ec27891e80933dfcc42beec9056d2d3a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62735204"
---
# <a name="sqlsetstmtattr-cursor-library"></a>SQLSetStmtAttr (Biblioteca de cursores)
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que usam esse recurso atualmente. A Microsoft recomenda usar a funcionalidade de cursor do driver.  
  
 Este tópico discute o uso do **SQLSetStmtAttr** função na biblioteca de cursor. Para obter informações gerais sobre **SQLSetStmtAttr**, consulte [função SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md).  
  
 A biblioteca de cursor suporta os seguintes atributos de instrução com **SQLSetStmtAttr**:  
  
|||  
|-|-|  
|SQL_ATTR_CONCURRENCY|SQL_ATTR_ROW_BIND_OFFSET_PTR|  
|SQL_ATTR_CURSOR_TYPE|SQL_ATTR_ROW_BIND_TYPE|  
|SQL_ATTR_FETCH_BOOKMARK_PTR|SQL_ATTR_ROWSET_ARRAY_SIZE|  
|SQL_ATTR_PARAM_BIND_OFFSET_PTR|SQL_ATTR_SIMULATE_CURSOR|  
|SQL_ATTR_PARAM_BIND_TYPE|SQL_ATTR_USE_BOOKMARKS|  
  
 A biblioteca de cursores dá suporte a apenas os valores SQL_CURSOR_FORWARD_ONLY e SQL_CURSOR_STATIC do atributo SQL_ATTR_CURSOR_TYPE instrução.  
  
 Cursores de somente avanço, a biblioteca de cursores dá suporte ao valor SQL_CONCUR_READ_ONLY do atributo de instrução SQL_ATTR_CONCURRENCY. Para Cursores estáticos, a biblioteca de cursores dá suporte aos valores de atributo de instrução SQL_ATTR_CONCURRENCY SQL_CONCUR_READ_ONLY e SQL_CONCUR_VALUES.  
  
 A biblioteca de cursores dá suporte a apenas o valor SQL_SC_NON_UNIQUE do atributo de instrução SQL_ATTR_SIMULATE_CURSOR.  
  
 Embora a especificação de ODBC dá suporte a chamadas para **SQLSetStmtAttr** com os atributos SQL_ATTR_PARAM_BIND_TYPE ou SQL_ATTR_ROW_BIND_TYPE após **SQLFetch** ou **SQLFetchScroll**  tiver sido chamado, o cursor não biblioteca. Antes que ele pode alterar o tipo de associação na biblioteca de cursor, o aplicativo deve fechar o cursor. A biblioteca de cursores dá suporte à alteração de SQL_ATTR_ROW_BIND_OFFSET_PTR, SQL_ATTR_PARAM_BIND_OFFSET_PTR, SQL_ATTR_ROWS_FETCHED_PTR e atributos de instrução SQL_ATTR_PARAMS_PROCESSED_PTR quando um cursor é aberto.  
  
 Um aplicativo pode chamar **SQLSetStmtAttr** com um **atributo** de SQL_ATTR_ROW_ARRAY_SIZE para alterar o tamanho do conjunto de linhas, enquanto um cursor é aberto. O novo tamanho do conjunto de linhas entrarão em vigor na próxima vez que **SQLFetchScroll** ou **SQLFetch** é chamado.  
  
 A biblioteca de cursores dá suporte à configuração do atributo de instrução SQL_ATTR_PARAM_BIND_OFFSET_PTR ou SQL_ATTR_ROW_BIND_OFFSET_PTR para habilitar os deslocamentos de associação. O deslocamento de associação não será usado para chamadas para **SQLFetch** quando a biblioteca de cursores é usada com um ODBC 2. *x* driver.  
  
 A biblioteca de cursores dá suporte à configuração do atributo de instrução de SQL_ATTR_USE_BOOKMARKS como SQL_UB_VARIABLE.
