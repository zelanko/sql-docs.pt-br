---
title: SQLNativeSql (biblioteca de Cursor) | Microsoft Docs
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
ms.topic: conceptual
helpviewer_keywords:
- SQLNativeSql function [ODBC], Cursor Library
ms.assetid: c4459092-1177-4b2a-b7f5-e0083d3bf2b2
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 90935f2a12ba3c39115570f0c56fe4517b8205be
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="sqlnativesql-cursor-library"></a>SQLNativeSql (biblioteca de Cursor)
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. A Microsoft recomenda o uso da funcionalidade de cursor do driver.  
  
 Este tópico discute o uso do **SQLNativeSql** função na biblioteca de cursor. Para obter informações gerais sobre **SQLNativeSql**, consulte [função SQLNativeSql](../../../odbc/reference/syntax/sqlnativesql-function.md).  
  
 Se o driver dá suporte a essa função, a biblioteca de cursores chama **SQLNativeSql** no driver e a transmite a instrução SQL. Para uma atualização posicionada, posicionada delete, e **Selecione para atualizar** instruções, a biblioteca de cursores modifica a instrução antes de passar para o driver.  
  
> [!NOTE]  
>  A biblioteca de cursores incorretamente retornará SQLSTATE 34000 (nome de cursor inválido) se o nome do cursor é inválido em uma atualização posicionada ou uma instrução delete que é passada a *InStatementText* argumento de **SQLNativeSql** . **SQLNativeSql** não se destina a retornar erros de sintaxe, que são retornados somente após a preparação da instrução ou a execução.
