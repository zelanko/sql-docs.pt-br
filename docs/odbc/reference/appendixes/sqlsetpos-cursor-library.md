---
title: SQLSetPos (biblioteca de cursores) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSetPos function [ODBC], Cursor Library
ms.assetid: 574399c3-2bb2-4d19-829c-7c77bd82858d
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b41fad0f609b16640bfa28ab36f29f364e067b73
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63297414"
---
# <a name="sqlsetpos-cursor-library"></a>SQLSetPos (Biblioteca de cursores)
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que usam esse recurso atualmente. A Microsoft recomenda usar a funcionalidade de cursor do driver.  
  
 Este tópico discute o uso do **SQLSetPos** função na biblioteca de cursor. Para obter informações gerais sobre **SQLSetPos**, consulte [função SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md).  
  
 A biblioteca de cursores dá suporte a operação SQL_POSITION somente para o *operação* argumento **SQLSetPos**. Ele dá suporte o valor SQL_LOCK_NO_CHANGE somente para o *LockType* argumento.  
  
 Se o driver não oferece suporte a operações em massa, a biblioteca de cursores retornará SQLSTATE HYC00 (o Driver não funciona) quando **SQLSetPos** for chamado com *RowNumber* igual a 0. Esse comportamento de driver não é recomendado.  
  
 A biblioteca de cursores não oferece suporte as operações de SQL_UPDATE e SQL_DELETE em uma chamada para **SQLSetPos**. O implementa de biblioteca de cursor um posicionadas instrução update ou delete SQL, criando um pesquisada instrução update ou delete com uma cláusula WHERE que enumera os valores armazenados em seu cache para cada coluna associada. Para obter mais informações, consulte [processamento posicionado instruções Update e excluir](../../../odbc/reference/appendixes/processing-positioned-update-and-delete-statements.md).  
  
 Se o driver não oferece suporte a Cursores estáticos, um aplicativo trabalhar com a biblioteca de cursores deve chamar **SQLSetPos** somente em um conjunto de linhas buscado por **SQLExtendedFetch** ou **SQLFetchScroll** , não pelo **SQLFetch**. A biblioteca de cursores implementa **SQLExtendedFetch** e **SQLFetchScroll** fazendo repetidas chamadas de **SQLFetch** (com um tamanho de conjunto de linhas de 1) no driver. A biblioteca de cursores passa chamadas para **SQLFetch**, no outro lado, por meio do driver. Se **SQLSetPos** é chamado em um conjunto de linhas de várias linhas buscado por **SQLFetch** quando o driver não dá suporte a Cursores estáticos, a chamada falhará porque **SQLSetPos** não funciona com cursores de somente avanço. Isso ocorrerá mesmo se um aplicativo tiver sido chamado com êxito **SQLSetStmtAttr** definir SQL_ATTR_CURSOR_TYPE como SQL_CURSOR_STATIC, que a biblioteca de cursores dá suporte ao mesmo se o driver não oferece suporte a Cursores estáticos.
