---
title: SQLNativeSql (Cursor Library) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLNativeSql function [ODBC], Cursor Library
ms.assetid: c4459092-1177-4b2a-b7f5-e0083d3bf2b2
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c5b87f64963e7b0ad45fbec33e410165cd0c9723
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63298488"
---
# <a name="sqlnativesql-cursor-library"></a>SQLNativeSql (Biblioteca de cursores)
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que usam esse recurso atualmente. A Microsoft recomenda usar a funcionalidade de cursor do driver.  
  
 Este tópico discute o uso do **SQLNativeSql** função na biblioteca de cursor. Para obter informações gerais sobre **SQLNativeSql**, consulte [função SQLNativeSql](../../../odbc/reference/syntax/sqlnativesql-function.md).  
  
 Se o driver dá suporte a essa função, a biblioteca de cursores chama **SQLNativeSql** no driver e o passa a instrução SQL. Para uma atualização posicionada, posicionada delete, e **Selecione para atualizar** instruções, a biblioteca de cursores modifica a instrução antes de passá-la para o driver.  
  
> [!NOTE]  
>  A biblioteca de cursores incorretamente retornará SQLSTATE 34000 (nome de cursor inválido) se o nome de cursor é inválido em uma atualização posicionada ou uma instrução delete que é passada a *InStatementText* argumento do **SQLNativeSql** . **SQLNativeSql** não se destina para retornar erros de sintaxe, que são retornados somente após a preparação da instrução ou a execução.
