---
title: SQLSetStmtAttr (Biblioteca do Cursor) | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1bdd9b3b559d5cc78a0d44f5280aae347bc8996a
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300486"
---
# <a name="sqlsetstmtattr-cursor-library"></a>SQLSetStmtAttr (Biblioteca de cursores)
> [!IMPORTANT]  
>  Esse recurso será removido em uma versão futura do Windows. Evite usar esse recurso em novos trabalhos de desenvolvimento e planeje modificar aplicativos que atualmente usam esse recurso. A Microsoft recomenda o uso da funcionalidade do cursor do driver.  
  
 Este tópico discute o uso da função **SQLSetStmtAttr** na biblioteca do cursor. Para obter informações gerais sobre **sqlsetstmtAttr**, consulte [SQLSetStmtAttr Function](../../../odbc/reference/syntax/sqlsetstmtattr-function.md).  
  
 A biblioteca do cursor suporta os atributos de declaração a seguir com **SQLSetStmtAttr**:  
  
|||  
|-|-|  
|SQL_ATTR_CONCURRENCY|SQL_ATTR_ROW_BIND_OFFSET_PTR|  
|SQL_ATTR_CURSOR_TYPE|SQL_ATTR_ROW_BIND_TYPE|  
|SQL_ATTR_FETCH_BOOKMARK_PTR|SQL_ATTR_ROWSET_ARRAY_SIZE|  
|SQL_ATTR_PARAM_BIND_OFFSET_PTR|SQL_ATTR_SIMULATE_CURSOR|  
|SQL_ATTR_PARAM_BIND_TYPE|SQL_ATTR_USE_BOOKMARKS|  
  
 A biblioteca do cursor suporta apenas os valores SQL_CURSOR_FORWARD_ONLY e SQL_CURSOR_STATIC do atributo de declaração SQL_ATTR_CURSOR_TYPE.  
  
 Para cursores somente para avanços, a biblioteca do cursor suporta o valor SQL_CONCUR_READ_ONLY do atributo de declaração SQL_ATTR_CONCURRENCY. Para cursores estáticos, a biblioteca do cursor suporta os valores SQL_CONCUR_READ_ONLY e SQL_CONCUR_VALUES do atributo de declaração SQL_ATTR_CONCURRENCY.  
  
 A biblioteca do cursor suporta apenas o valor SQL_SC_NON_UNIQUE do atributo de declaração SQL_ATTR_SIMULATE_CURSOR.  
  
 Embora a especificação ODBC suporte chamadas para **SQLSetStmtAttr** com os atributos SQL_ATTR_PARAM_BIND_TYPE ou SQL_ATTR_ROW_BIND_TYPE após **sQLFetch** **ou SQLFetchScroll** ter sido chamado, a biblioteca do cursor não. Antes de alterar o tipo de vinculação na biblioteca do cursor, o aplicativo deve fechar o cursor. A biblioteca do cursor suporta alterar os atributos de declaração SQL_ATTR_ROW_BIND_OFFSET_PTR, SQL_ATTR_PARAM_BIND_OFFSET_PTR, SQL_ATTR_ROWS_FETCHED_PTR e SQL_ATTR_PARAMS_PROCESSED_PTR quando um cursor está aberto.  
  
 Um aplicativo pode chamar **SQLSetStmtAttr** com um **atributo** de SQL_ATTR_ROW_ARRAY_SIZE alterar o tamanho do conjunto de linhas enquanto um cursor está aberto. O novo tamanho do conjunto de linhas entrará em vigor na próxima vez que **SQLFetchScroll** ou **SQLFetch** forem chamados.  
  
 A biblioteca do cursor suporta a definição do atributo de declaração SQL_ATTR_PARAM_BIND_OFFSET_PTR ou SQL_ATTR_ROW_BIND_OFFSET_PTR para habilitar deslocamentos de vinculação. O deslocamento de vinculação não será usado para chamadas para **SQLFetch** quando a biblioteca do cursor for usada com um ODBC 2. *x* driver.  
  
 A biblioteca do cursor suporta a definição do atributo de declaração SQL_ATTR_USE_BOOKMARKS para SQL_UB_VARIABLE.
