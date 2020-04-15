---
title: SQLSetPos (Biblioteca Cursor) | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4c46ef88075a5adbd96138d7d1f03c26712f7ea1
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300506"
---
# <a name="sqlsetpos-cursor-library"></a>SQLSetPos (Biblioteca de cursores)
> [!IMPORTANT]  
>  Esse recurso será removido em uma versão futura do Windows. Evite usar esse recurso em novos trabalhos de desenvolvimento e planeje modificar aplicativos que atualmente usam esse recurso. A Microsoft recomenda o uso da funcionalidade do cursor do driver.  
  
 Este tópico discute o uso da função **SQLSetPos** na biblioteca do cursor. Para obter informações gerais sobre **SQLSetPos,** consulte [SQLSetPos Function](../../../odbc/reference/syntax/sqlsetpos-function.md).  
  
 A biblioteca do cursor suporta a operação SQL_POSITION apenas para o argumento *Operação* em **SQLSetPos**. Ele suporta o valor SQL_LOCK_NO_CHANGE apenas para o argumento *LockType.*  
  
 Se o driver não suportar operações em massa, a biblioteca do cursor retorna SQLSTATE HYC00 (Driver não é capaz) quando **SQLSetPos** é chamado com *RowNumber* igual a 0. Este comportamento do motorista não é recomendado.  
  
 A biblioteca do cursor não suporta as operações de SQL_UPDATE e SQL_DELETE em uma chamada para **SQLSetPos**. A biblioteca do cursor implementa uma atualização posicionada ou exclui a declaração SQL criando uma atualização pesquisada ou exclui a declaração com uma cláusula WHERE que enumera os valores armazenados em seu cache para cada coluna vinculada. Para obter mais informações, consulte [Processamento de Instruções posicionadas e exclusão](../../../odbc/reference/appendixes/processing-positioned-update-and-delete-statements.md).  
  
 Se o driver não suportar cursores estáticos, um aplicativo que trabalha com a biblioteca do cursor deve chamar **SQLSetPos** apenas em um conjunto de linhas buscado por **SQLExtendedFetchou** ou **SQLFetchScroll,** não pelo **SQLFetch**. A biblioteca do cursor implementa **SQLExtendedFetch** e **SQLFetchScroll** fazendo chamadas repetidas de **SQLFetch** (com um tamanho de linha de 1) no driver. A biblioteca do cursor passa chamadas para **o SQLFetch,** por outro lado, até o driver. Se **o SQLSetPos** for chamado em um conjunto de linhas multi-row buscado pelo **SQLFetch** quando o driver não suportar cursores estáticos, a chamada falhará porque **o SQLSetPos** não funciona com cursores somente para frente. Isso ocorrerá mesmo se um aplicativo tiver chamado com sucesso **sqlsetstmtAttr** para definir SQL_ATTR_CURSOR_TYPE para SQL_CURSOR_STATIC, que a biblioteca do cursor suporta mesmo se o driver não suportar cursores estáticos.
