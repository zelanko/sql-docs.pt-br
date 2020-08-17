---
description: SQLSetPos (Biblioteca de cursores)
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d35f1461f6a5da3ee894d9275c6ca112bfabab44
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88339232"
---
# <a name="sqlsetpos-cursor-library"></a>SQLSetPos (Biblioteca de cursores)
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em novos trabalhos de desenvolvimento e planeje modificar os aplicativos que atualmente usam esse recurso. A Microsoft recomenda usar a funcionalidade de cursor do driver.  
  
 Este tópico discute o uso da função **SQLSetPos** na biblioteca de cursores. Para obter informações gerais sobre **SQLSetPos**, consulte [SQLSetPos function](../../../odbc/reference/syntax/sqlsetpos-function.md).  
  
 A biblioteca de cursores dá suporte à operação SQL_POSITION somente para o argumento de *operação* em **SQLSetPos**. Ele dá suporte ao valor de SQL_LOCK_NO_CHANGE apenas para o argumento *LockType* .  
  
 Se o driver não oferecer suporte a operações em massa, a biblioteca de cursores retornará SQLSTATE HYC00 (driver não compatível) quando **SQLSetPos** for chamado com *RowNumber* igual a 0. Esse comportamento de driver não é recomendado.  
  
 A biblioteca de cursores não oferece suporte às operações SQL_UPDATE e SQL_DELETE em uma chamada para **SQLSetPos**. A biblioteca de cursores implementa uma instrução SQL de atualização ou exclusão posicionada criando uma instrução UPDATE ou DELETE pesquisada com uma cláusula WHERE que enumera os valores armazenados em seu cache para cada coluna associada. Para obter mais informações, consulte [processando instruções UPDATE e DELETE posicionadas](../../../odbc/reference/appendixes/processing-positioned-update-and-delete-statements.md).  
  
 Se o driver não oferecer suporte a cursores estáticos, um aplicativo que trabalha com a biblioteca de cursores deve chamar **SQLSetPos** somente em um conjunto de linhas buscado por **SQLExtendedFetch** ou **SQLFetchScroll**, não por **SQLFetch**. A biblioteca de cursores implementa **SQLExtendedFetch** e **SQLFetchScroll** fazendo chamadas repetidas de **SQLFetch** (com um tamanho de conjunto de linhas de 1) no driver. A biblioteca de cursores passa chamadas para **SQLFetch**, por outro lado, até o driver. Se **SQLSetPos** for chamado em um conjunto de linhas de LinhaMúltipla buscado por **SQLFetch** quando o driver não oferecer suporte a cursores estáticos, a chamada falhará porque o **SQLSetPos** não funciona com cursores de somente avanço. Isso ocorrerá mesmo se um aplicativo tiver chamado **SQLSetStmtAttr** com êxito para definir SQL_ATTR_CURSOR_TYPE para SQL_CURSOR_STATIC, que a biblioteca de cursores dá suporte mesmo se o driver não oferecer suporte a cursores estáticos.
