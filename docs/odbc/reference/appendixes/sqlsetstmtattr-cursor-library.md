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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 366af9f48f709ec7414c1efc43000f1b565ff6d6
ms.sourcegitcommit: 99f61724de5edf6640efd99916d464172eb23f92
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/28/2020
ms.locfileid: "87363438"
---
# <a name="sqlsetstmtattr-cursor-library"></a>SQLSetStmtAttr (Biblioteca de cursores)
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em novos trabalhos de desenvolvimento e planeje modificar os aplicativos que atualmente usam esse recurso. A Microsoft recomenda usar a funcionalidade de cursor do driver.  
  
 Este tópico discute o uso da função **SQLSetStmtAttr** na biblioteca de cursores. Para obter informações gerais sobre **SQLSetStmtAttr**, consulte [SQLSetStmtAttr function](../../../odbc/reference/syntax/sqlsetstmtattr-function.md).  
  
 A biblioteca de cursores dá suporte aos seguintes atributos de instrução com **SQLSetStmtAttr**:  

:::row:::
    :::column:::
        SQL_ATTR_CONCURRENCY  
        SQL_ATTR_CURSOR_TYPE  
        SQL_ATTR_FETCH_BOOKMARK_PTR  
        SQL_ATTR_PARAM_BIND_OFFSET_PTR  
        SQL_ATTR_PARAM_BIND_TYPE  
    :::column-end:::
    :::column:::
        SQL_ATTR_ROW_BIND_OFFSET_PTR  
        SQL_ATTR_ROW_BIND_TYPE  
        SQL_ATTR_ROWSET_ARRAY_SIZE  
        SQL_ATTR_SIMULATE_CURSOR  
        SQL_ATTR_USE_BOOKMARKS  
    :::column-end:::
:::row-end:::

 A biblioteca de cursores dá suporte apenas aos valores SQL_CURSOR_FORWARD_ONLY e SQL_CURSOR_STATIC do atributo de instrução SQL_ATTR_CURSOR_TYPE.  
  
 Para cursores somente de avanço, a biblioteca de cursores dá suporte ao valor SQL_CONCUR_READ_ONLY do atributo SQL_ATTR_CONCURRENCY Statement. Para cursores estáticos, a biblioteca de cursores dá suporte aos valores de SQL_CONCUR_READ_ONLY e SQL_CONCUR_VALUES do atributo de instrução SQL_ATTR_CONCURRENCY.  
  
 A biblioteca de cursores dá suporte apenas ao valor SQL_SC_NON_UNIQUE do atributo SQL_ATTR_SIMULATE_CURSOR Statement.  
  
 Embora a especificação ODBC dê suporte a chamadas para **SQLSetStmtAttr** com os atributos SQL_ATTR_PARAM_BIND_TYPE ou SQL_ATTR_ROW_BIND_TYPE após **SQLFetch** ou **SQLFetchScroll** ser chamado, a biblioteca de cursores não. Antes de poder alterar o tipo de associação na biblioteca de cursores, o aplicativo deve fechar o cursor. A biblioteca de cursores dá suporte à alteração dos atributos de instrução SQL_ATTR_ROW_BIND_OFFSET_PTR, SQL_ATTR_PARAM_BIND_OFFSET_PTR, SQL_ATTR_ROWS_FETCHED_PTR e SQL_ATTR_PARAMS_PROCESSED_PTR quando um cursor é aberto.  
  
 Um aplicativo pode chamar **SQLSetStmtAttr** com um **atributo** de SQL_ATTR_ROW_ARRAY_SIZE para alterar o tamanho do conjunto de linhas enquanto um cursor está aberto. O novo tamanho do conjunto de linhas entrará em vigor na próxima vez que **SQLFetchScroll** ou **SQLFetch** for chamado.  
  
 A biblioteca de cursores dá suporte à definição do atributo de instrução SQL_ATTR_PARAM_BIND_OFFSET_PTR ou SQL_ATTR_ROW_BIND_OFFSET_PTR para habilitar deslocamentos de associação. O deslocamento de associação não será usado para chamadas para **SQLFetch** quando a biblioteca de cursores for usada com um ODBC 2. Driver *x* .  
  
 A biblioteca de cursores dá suporte à definição do atributo SQL_ATTR_USE_BOOKMARKS Statement como SQL_UB_VARIABLE.
