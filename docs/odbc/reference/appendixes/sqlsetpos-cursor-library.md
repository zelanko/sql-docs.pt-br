---
title: SQLSetPos (biblioteca de Cursor) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- SQLSetPos function [ODBC], Cursor Library
ms.assetid: 574399c3-2bb2-4d19-829c-7c77bd82858d
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 9a2d311c894f7e0b9e7fa59b387b995ab1205a27
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="sqlsetpos-cursor-library"></a>SQLSetPos (biblioteca de Cursor)
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. A Microsoft recomenda o uso da funcionalidade de cursor do driver.  
  
 Este tópico discute o uso do **SQLSetPos** função na biblioteca de cursor. Para obter informações gerais sobre **SQLSetPos**, consulte [função SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md).  
  
 A biblioteca de cursores oferece suporte a operação SQL_POSITION apenas para o *operação* argumento **SQLSetPos**. Ele dá suporte o valor SQL_LOCK_NO_CHANGE somente para o *LockType* argumento.  
  
 Se o driver não dá suporte a operações em massa, a biblioteca de cursores retornará SQLSTATE HYC00 (o Driver não funciona) quando **SQLSetPos** é chamado com *RowNumber* igual a 0. Esse comportamento de driver não é recomendado.  
  
 A biblioteca de cursores não oferece suporte as operações de SQL_UPDATE e SQL_DELETE em uma chamada para **SQLSetPos**. O implementa biblioteca de cursor posicionados de uma instrução update ou delete SQL criando um pesquisada instrução update ou delete com uma cláusula WHERE que enumera os valores armazenados no cache para cada coluna associada. Para obter mais informações, consulte [processamento posicionado instruções Update e excluir](../../../odbc/reference/appendixes/processing-positioned-update-and-delete-statements.md).  
  
 Se o driver não dá suporte a Cursores estáticos, um aplicativo que trabalhar com a biblioteca de cursores deve chamar **SQLSetPos** somente em um conjunto de linhas buscado por **SQLExtendedFetch** ou **SQLFetchScroll** , não pelo **SQLFetch**. A biblioteca de cursores implementa **SQLExtendedFetch** e **SQLFetchScroll** fazendo chamadas repetidas de **SQLFetch** (com um tamanho de conjunto de linhas de 1) no driver. A biblioteca de cursores passa chamadas para **SQLFetch**, no outro lado, por meio do driver. Se **SQLSetPos** é chamado em um conjunto de linhas de várias linhas buscado por **SQLFetch** quando o driver não dá suporte a Cursores estáticos, a chamada falhará porque **SQLSetPos** não funciona com cursores de somente avanço. Isso ocorrerá mesmo se um aplicativo tiver sido chamado com êxito **SQLSetStmtAttr** para definir SQL_ATTR_CURSOR_TYPE para SQL_CURSOR_STATIC, que oferece suporte a biblioteca de cursores mesmo se o driver não dá suporte a Cursores estáticos.
