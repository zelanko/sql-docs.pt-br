---
title: SQLFreeStmt (biblioteca de Cursor) | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: SQLFreeStmt function [ODBC], Cursor Library
ms.assetid: 47bfbd4d-9453-4609-958d-1e05794cb223
caps.latest.revision: "8"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: bc56f0c16b373a3bf9e8f73d9321cb6b04751136
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="sqlfreestmt-cursor-library"></a>SQLFreeStmt (biblioteca de Cursor)
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. A Microsoft recomenda o uso da funcionalidade de cursor do driver.  
  
 Este tópico discute o uso do **SQLFreeStmt** função na biblioteca de cursor. Para obter informações gerais sobre **SQLFreeStmt**, consulte [função SQLFreeStmt](../../../odbc/reference/syntax/sqlfreestmt-function.md).  
  
 Se um aplicativo chamar **SQLFreeStmt** com a opção SQL_UNBIND depois de chamar **SQLExtendedFetch**, **SQLFetch**, ou **SQLFetchScroll**, a biblioteca de cursores retornará um erro. Antes de ele pode desassociar colunas do conjunto de resultados, um aplicativo deve chamar **SQLCloseCursor** ou **SQLFreeStmt** com a opção SQL_CLOSE.
