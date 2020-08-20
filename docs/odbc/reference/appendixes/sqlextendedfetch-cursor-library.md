---
description: SQLExtendedFetch (Biblioteca de cursores)
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ab7d091dc6cee3630b5ed9b8bf3a3a479c0613e8
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88466008"
---
# <a name="sqlextendedfetch-cursor-library"></a>SQLExtendedFetch (Biblioteca de cursores)
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em novos trabalhos de desenvolvimento e planeje modificar os aplicativos que atualmente usam esse recurso. A Microsoft recomenda usar a funcionalidade de cursor do driver.  
  
 Este tópico discute o uso da função **SQLExtendedFetch** na biblioteca de cursores. Para obter informações gerais sobre **SQLExtendedFetch**, consulte [SQLExtendedFetch function](../../../odbc/reference/syntax/sqlextendedfetch-function.md).  
  
 A biblioteca de cursores implementa o **SQLExtendedFetch** chamando **SQLFetch** repetidamente no driver.  
  
 A biblioteca de cursores dá suporte à chamada de **SQLExtendedFetch** com um *FetchOrientation* de SQL_FETCH_BOOKMARK.  
  
 Quando a biblioteca de cursores é usada, as chamadas para **SQLExtendedFetch** não podem ser misturadas com chamadas para **SQLFetchScroll** ou **SQLFetch**.
