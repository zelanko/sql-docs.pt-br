---
title: SQLFreeStmt (biblioteca de cursores) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLFreeStmt function [ODBC], Cursor Library
ms.assetid: 47bfbd4d-9453-4609-958d-1e05794cb223
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 4bfe5c91a90f874b514abb661ea06631be87e69c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68086407"
---
# <a name="sqlfreestmt-cursor-library"></a>SQLFreeStmt (Biblioteca de cursores)
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que usam esse recurso atualmente. A Microsoft recomenda usar a funcionalidade de cursor do driver.  
  
 Este tópico discute o uso do **SQLFreeStmt** função na biblioteca de cursor. Para obter informações gerais sobre **SQLFreeStmt**, consulte [função SQLFreeStmt](../../../odbc/reference/syntax/sqlfreestmt-function.md).  
  
 Se um aplicativo chamar **SQLFreeStmt** com a opção SQL_UNBIND depois que ele chama **SQLExtendedFetch**, **SQLFetch**, ou **SQLFetchScroll**, a biblioteca de cursores retornará um erro. Antes que ele pode desvincular colunas do conjunto de resultados, um aplicativo deve chamar **SQLCloseCursor** ou **SQLFreeStmt** com a opção SQL_CLOSE.
