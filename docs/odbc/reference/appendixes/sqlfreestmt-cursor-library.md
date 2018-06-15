---
title: SQLFreeStmt (biblioteca de Cursor) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQLFreeStmt function [ODBC], Cursor Library
ms.assetid: 47bfbd4d-9453-4609-958d-1e05794cb223
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8b7eea7d0a956543ba765dc7c15cf48102efa9e4
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32906261"
---
# <a name="sqlfreestmt-cursor-library"></a>SQLFreeStmt (biblioteca de Cursor)
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. A Microsoft recomenda o uso da funcionalidade de cursor do driver.  
  
 Este tópico discute o uso do **SQLFreeStmt** função na biblioteca de cursor. Para obter informações gerais sobre **SQLFreeStmt**, consulte [função SQLFreeStmt](../../../odbc/reference/syntax/sqlfreestmt-function.md).  
  
 Se um aplicativo chamar **SQLFreeStmt** com a opção SQL_UNBIND depois de chamar **SQLExtendedFetch**, **SQLFetch**, ou **SQLFetchScroll**, a biblioteca de cursores retornará um erro. Antes de ele pode desassociar colunas do conjunto de resultados, um aplicativo deve chamar **SQLCloseCursor** ou **SQLFreeStmt** com a opção SQL_CLOSE.
