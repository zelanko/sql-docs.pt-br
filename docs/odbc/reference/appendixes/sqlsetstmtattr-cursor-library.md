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
ms.openlocfilehash: bc222c1c8669769060de4fc0a1390a9bf02e3f31
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68091690"
---
# <a name="sqlsetstmtattr-cursor-library"></a>SQLSetStmtAttr (Biblioteca de cursores)
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em novos trabalhos de desenvolvimento e planeje modificar os aplicativos que atualmente usam esse recurso. A Microsoft recomenda usar a funcionalidade de cursor do driver.  
  
 Este tópico discute o uso da função **SQLSetStmtAttr** na biblioteca de cursores. Para obter informações gerais sobre **SQLSetStmtAttr**, consulte [SQLSetStmtAttr function](../../../odbc/reference/syntax/sqlsetstmtattr-function.md).  
  
 A biblioteca de cursores dá suporte aos seguintes atributos de instrução com **SQLSetStmtAttr**:  
  
|||  
|-|-|  
|SQL_ATTR_CONCURRENCY|SQL_ATTR_ROW_BIND_OFFSET_PTR|  
|SQL_ATTR_CURSOR_TYPE|SQL_ATTR_ROW_BIND_TYPE|  
|SQL_ATTR_FETCH_BOOKMARK_PTR|SQL_ATTR_ROWSET_ARRAY_SIZE|  
|SQL_ATTR_PARAM_BIND_OFFSET_PTR|SQL_ATTR_SIMULATE_CURSOR|  
|SQL_ATTR_PARAM_BIND_TYPE|SQL_ATTR_USE_BOOKMARKS|  
  
 A biblioteca de cursores dá suporte apenas aos valores SQL_CURSOR_FORWARD_ONLY e SQL_CURSOR_STATIC do atributo de instrução SQL_ATTR_CURSOR_TYPE.  
  
 Para cursores somente de avanço, a biblioteca de cursores dá suporte ao valor SQL_CONCUR_READ_ONLY do atributo SQL_ATTR_CONCURRENCY Statement. Para cursores estáticos, a biblioteca de cursores dá suporte aos valores de SQL_CONCUR_READ_ONLY e SQL_CONCUR_VALUES do atributo de instrução SQL_ATTR_CONCURRENCY.  
  
 A biblioteca de cursores dá suporte apenas ao valor SQL_SC_NON_UNIQUE do atributo SQL_ATTR_SIMULATE_CURSOR Statement.  
  
 Embora a especificação ODBC dê suporte a chamadas para **SQLSetStmtAttr** com os atributos SQL_ATTR_PARAM_BIND_TYPE ou SQL_ATTR_ROW_BIND_TYPE após **SQLFetch** ou **SQLFetchScroll** ser chamado, a biblioteca de cursores não. Antes de poder alterar o tipo de associação na biblioteca de cursores, o aplicativo deve fechar o cursor. A biblioteca de cursores dá suporte à alteração dos atributos de instrução SQL_ATTR_ROW_BIND_OFFSET_PTR, SQL_ATTR_PARAM_BIND_OFFSET_PTR, SQL_ATTR_ROWS_FETCHED_PTR e SQL_ATTR_PARAMS_PROCESSED_PTR quando um cursor é aberto.  
  
 Um aplicativo pode chamar **SQLSetStmtAttr** com um **atributo** de SQL_ATTR_ROW_ARRAY_SIZE para alterar o tamanho do conjunto de linhas enquanto um cursor está aberto. O novo tamanho do conjunto de linhas entrará em vigor na próxima vez que **SQLFetchScroll** ou **SQLFetch** for chamado.  
  
 A biblioteca de cursores dá suporte à definição do atributo de instrução SQL_ATTR_PARAM_BIND_OFFSET_PTR ou SQL_ATTR_ROW_BIND_OFFSET_PTR para habilitar deslocamentos de associação. O deslocamento de associação não será usado para chamadas para **SQLFetch** quando a biblioteca de cursores for usada com um ODBC 2. Driver *x* .  
  
 A biblioteca de cursores dá suporte à definição do atributo SQL_ATTR_USE_BOOKMARKS Statement como SQL_UB_VARIABLE.
