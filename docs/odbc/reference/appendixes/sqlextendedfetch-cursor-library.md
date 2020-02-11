---
title: SQLExtendedFetch (biblioteca de cursores) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLExtendedFetch function [ODBC], Cursor Library
ms.assetid: 06fbf06f-127b-475c-b636-7b784918475d
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a3fd7d02d74b0e19d91871c5df7c9c5915d028f5
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68064447"
---
# <a name="sqlextendedfetch-cursor-library"></a>SQLExtendedFetch (Biblioteca de cursores)
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em novos trabalhos de desenvolvimento e planeje modificar os aplicativos que atualmente usam esse recurso. A Microsoft recomenda usar a funcionalidade de cursor do driver.  
  
 Este tópico discute o uso da função **SQLExtendedFetch** na biblioteca de cursores. Para obter informações gerais sobre **SQLExtendedFetch**, consulte [SQLExtendedFetch function](../../../odbc/reference/syntax/sqlextendedfetch-function.md).  
  
 A biblioteca de cursores implementa o **SQLExtendedFetch** chamando **SQLFetch** repetidamente no driver.  
  
 A biblioteca de cursores dá suporte à chamada de **SQLExtendedFetch** com um *FetchOrientation* de SQL_FETCH_BOOKMARK.  
  
 Quando a biblioteca de cursores é usada, as chamadas para **SQLExtendedFetch** não podem ser misturadas com chamadas para **SQLFetchScroll** ou **SQLFetch**.
