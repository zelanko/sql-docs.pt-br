---
description: SQLFreeStmt (Biblioteca de cursores)
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9bc9ba1bc747f2c4408c308b13924afc8b3ba875
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88448986"
---
# <a name="sqlfreestmt-cursor-library"></a>SQLFreeStmt (Biblioteca de cursores)
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em novos trabalhos de desenvolvimento e planeje modificar os aplicativos que atualmente usam esse recurso. A Microsoft recomenda usar a funcionalidade de cursor do driver.  
  
 Este tópico discute o uso da função **SQLFreeStmt** na biblioteca de cursores. Para obter informações gerais sobre **SQLFreeStmt**, consulte [SQLFreeStmt function](../../../odbc/reference/syntax/sqlfreestmt-function.md).  
  
 Se um aplicativo chamar **SQLFreeStmt** com a opção SQL_UNBIND depois de chamar **SQLExtendedFetch**, **SQLFetch**ou **SQLFetchScroll**, a biblioteca de cursores retornará um erro. Antes de poder desassociar as colunas do conjunto de resultados, um aplicativo deve chamar **SQLCloseCursor** ou **SQLFreeStmt** com a opção SQL_CLOSE.
