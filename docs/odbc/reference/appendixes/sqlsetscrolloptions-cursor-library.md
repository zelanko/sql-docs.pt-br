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
ms.openlocfilehash: 18a0bc111f6b4e8d82d0ed353837b499f920479e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68023363"
---
# <a name="sqlsetscrolloptions-cursor-library"></a>SQLSetScrollOptions (Biblioteca de cursores)
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em novos trabalhos de desenvolvimento e planeje modificar os aplicativos que atualmente usam esse recurso. A Microsoft recomenda usar a funcionalidade de cursor do driver.  
  
 Este tópico discute o uso da função **SQLSetScrollOptions** na biblioteca de cursores. Para obter informações gerais sobre **SQLSetScrollOptions**, consulte [SQLSetScrollOptions function](../../../odbc/reference/syntax/sqlsetscrolloptions-function.md).  
  
 A biblioteca de cursores dá suporte a **SQLSetScrollOptions** somente para compatibilidade com versões anteriores; os aplicativos devem usar os atributos de instrução SQL_ATTR_CONCURRENCY, SQL_ATTR_CURSOR_TYPE e SQL_ATTR_ROW_ARRAY_SIZE em vez disso.
