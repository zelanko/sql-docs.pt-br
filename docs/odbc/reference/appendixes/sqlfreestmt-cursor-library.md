---
title: SQLFreeStmt (Biblioteca Cursor) | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d78075593926c15dbaeb1904603b08e990f64983
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302017"
---
# <a name="sqlfreestmt-cursor-library"></a>SQLFreeStmt (Biblioteca de cursores)
> [!IMPORTANT]  
>  Esse recurso será removido em uma versão futura do Windows. Evite usar esse recurso em novos trabalhos de desenvolvimento e planeje modificar aplicativos que atualmente usam esse recurso. A Microsoft recomenda o uso da funcionalidade do cursor do driver.  
  
 Este tópico discute o uso da função **SQLFreeStmt** na biblioteca do cursor. Para obter informações gerais sobre **o SQLFreeStmt,** consulte [SQLFreeStmt Function](../../../odbc/reference/syntax/sqlfreestmt-function.md).  
  
 Se um aplicativo chamar **o SQLFreeStmt** com a opção SQL_UNBIND depois de chamar **SQLExtendedFetch,** **SQLFetch**ou **SQLFetchScroll,** a biblioteca do cursor retorna um erro. Antes de desvincular colunas de conjunto de resultados, um aplicativo deve chamar **SQLCloseCursor** ou **SQLFreeStmt** com a opção SQL_CLOSE.
