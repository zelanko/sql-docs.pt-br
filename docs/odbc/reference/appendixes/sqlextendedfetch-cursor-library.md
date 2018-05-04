---
title: SQLExtendedFetch (biblioteca de Cursor) | Microsoft Docs
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
- SQLExtendedFetch function [ODBC], Cursor Library
ms.assetid: 06fbf06f-127b-475c-b636-7b784918475d
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 08fa807fcbfd3c55df7edcc221131479edee3e0b
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="sqlextendedfetch-cursor-library"></a>SQLExtendedFetch (biblioteca de Cursor)
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. A Microsoft recomenda o uso da funcionalidade de cursor do driver.  
  
 Este tópico discute o uso do **SQLExtendedFetch** função na biblioteca de cursor. Para obter informações gerais sobre **SQLExtendedFetch**, consulte [SQLExtendedFetch função](../../../odbc/reference/syntax/sqlextendedfetch-function.md).  
  
 A biblioteca de cursores implementa **SQLExtendedFetch** chamando repetidamente **SQLFetch** no driver.  
  
 A biblioteca de cursores dá suporte à chamada **SQLExtendedFetch** com um *FetchOrientation* de SQL_FETCH_BOOKMARK.  
  
 Quando a biblioteca de cursores é usada, chamadas para **SQLExtendedFetch** não podem ser misturadas a chamadas para o **SQLFetchScroll** ou **SQLFetch**.
