---
title: SQLSetScrollOptions (biblioteca de Cursor) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- SQLSetScrollOptions function [ODBC], Cursor Library
ms.assetid: c5c0ac6d-a6c1-4077-8186-1644df1944f8
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e4b8d28541eda6afea8d72c442922f79b5160a62
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="sqlsetscrolloptions-cursor-library"></a>SQLSetScrollOptions (biblioteca de Cursor)
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. A Microsoft recomenda o uso da funcionalidade de cursor do driver.  
  
 Este tópico discute o uso do **SQLSetScrollOptions** função na biblioteca de cursor. Para obter informações gerais sobre **SQLSetScrollOptions**, consulte [SQLSetScrollOptions função](../../../odbc/reference/syntax/sqlsetscrolloptions-function.md).  
  
 A biblioteca de cursores dá suporte a **SQLSetScrollOptions** somente para compatibilidade com versões anteriores; aplicativos devem usar os atributos de instrução SQL_ATTR_CURSOR_TYPE, SQL_ATTR_CONCURRENCY e SQL_ATTR_ROW_ARRAY_SIZE em vez disso.
