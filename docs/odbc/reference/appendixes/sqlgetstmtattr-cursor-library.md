---
title: SQLGetStmtAttr (biblioteca de cursores) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLGetStmtAttr function [ODBC], Cursor Library
ms.assetid: 6c34e1ef-4273-4afb-a7d3-f9017ab69c5e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a9b29d21c166751f5a57b7951cb6c028861cb501
ms.sourcegitcommit: 99f61724de5edf6640efd99916d464172eb23f92
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/28/2020
ms.locfileid: "87362946"
---
# <a name="sqlgetstmtattr-cursor-library"></a>SQLGetStmtAttr (Biblioteca de cursores)
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em novos trabalhos de desenvolvimento e planeje modificar os aplicativos que atualmente usam esse recurso. A Microsoft recomenda usar a funcionalidade de cursor do driver.  
  
 Este tópico discute o uso da função **SQLGetStmtAttr** na biblioteca de cursores. Para obter informações gerais sobre **SQLGetStmtAttr**, consulte [SQLGetStmtAttr function](../../../odbc/reference/syntax/sqlgetstmtattr-function.md).  
  
 A biblioteca de cursores dá suporte aos seguintes atributos de instrução com **SQLGetStmtAttr**:  

:::row:::
    :::column:::
        SQL_ATTR_CONCURRENCY  
        SQL_ATTR_CURSOR_TYPE  
        SQL_ATTR_FETCH_BOOKMARK_PTR  
        SQL_ATTR_PARAM_BIND_OFFSET_PTR  
        SQL_ATTR_PARAM_BIND_TYPE  
    :::column-end:::
    :::column:::
        SQL_ATTR_ROW_ARRAY_SIZE  
        SQL_ATTR_ROW_BIND_OFFSET_PTR  
        SQL_ATTR_ROW_BIND_TYPE  
        SQL_ATTR_ROW_NUMBER  
        SQL_ATTR_SIMULATE_CURSOR  
    :::column-end:::
:::row-end:::
