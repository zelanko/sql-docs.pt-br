---
title: SQLSetScrollOptions (biblioteca de cursores) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSetScrollOptions function [ODBC], Cursor Library
ms.assetid: c5c0ac6d-a6c1-4077-8186-1644df1944f8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e1fe6765c0ff8a057aac8e86ea5ad4aa1ac388b4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63297485"
---
# <a name="sqlsetscrolloptions-cursor-library"></a>SQLSetScrollOptions (Biblioteca de cursores)
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que usam esse recurso atualmente. A Microsoft recomenda usar a funcionalidade de cursor do driver.  
  
 Este tópico discute o uso do **SQLSetScrollOptions** função na biblioteca de cursor. Para obter informações gerais sobre **SQLSetScrollOptions**, consulte [função SQLSetScrollOptions](../../../odbc/reference/syntax/sqlsetscrolloptions-function.md).  
  
 Oferece suporte a biblioteca de cursores **SQLSetScrollOptions** somente para compatibilidade com versões anteriores; aplicativos devem usar os atributos de instrução SQL_ATTR_CURSOR_TYPE, SQL_ATTR_CONCURRENCY e SQL_ATTR_ROW_ARRAY_SIZE em vez disso.
