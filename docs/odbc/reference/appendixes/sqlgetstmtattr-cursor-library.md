---
title: SQLGetStmtAttr (biblioteca de Cursor) | Microsoft Docs
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
ms.topic: article
helpviewer_keywords:
- SQLGetStmtAttr function [ODBC], Cursor Library
ms.assetid: 6c34e1ef-4273-4afb-a7d3-f9017ab69c5e
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 83092581e071e59ac1d4f4f7d16640d7ec4a79e4
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="sqlgetstmtattr-cursor-library"></a>SQLGetStmtAttr (biblioteca de Cursor)
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. A Microsoft recomenda o uso da funcionalidade de cursor do driver.  
  
 Este tópico discute o uso do **SQLGetStmtAttr** função na biblioteca de cursor. Para obter informações gerais sobre **SQLGetStmtAttr**, consulte [função SQLGetStmtAttr](../../../odbc/reference/syntax/sqlgetstmtattr-function.md).  
  
 A biblioteca de cursores suporta os seguintes atributos de instrução com **SQLGetStmtAttr**:  
  
|||  
|-|-|  
|SQL_ATTR_CONCURRENCY|SQL_ATTR_ROW_BIND_OFFSET_PTR|  
|SQL_ATTR_CURSOR_TYPE|SQL_ATTR_ROW_BIND_TYPE|  
|SQL_ATTR_FETCH_BOOKMARK_PTR|SQL_ATTR_ROW_NUMBER|  
|SQL_ATTR_PARAM_BIND_OFFSET_PTR|SQL_ATTR_ROW_ARRAY_SIZE|  
|SQL_ATTR_PARAM_BIND_TYPE|SQL_ATTR_SIMULATE_CURSOR|
