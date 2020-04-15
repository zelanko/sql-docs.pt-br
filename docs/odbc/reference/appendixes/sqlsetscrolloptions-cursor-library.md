---
title: SQLSetScrollOptions (Biblioteca cursor) | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0099ca5e9bcb3aefdd86e0132f52d110ab64e8a4
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304907"
---
# <a name="sqlsetscrolloptions-cursor-library"></a>SQLSetScrollOptions (Biblioteca de cursores)
> [!IMPORTANT]  
>  Esse recurso será removido em uma versão futura do Windows. Evite usar esse recurso em novos trabalhos de desenvolvimento e planeje modificar aplicativos que atualmente usam esse recurso. A Microsoft recomenda o uso da funcionalidade do cursor do driver.  
  
 Este tópico discute o uso da função **SQLSetScrollOptions** na biblioteca do cursor. Para obter informações gerais sobre **sqlsetscrolloptions,** consulte [SQLSetScrollOptions Function](../../../odbc/reference/syntax/sqlsetscrolloptions-function.md).  
  
 A biblioteca do cursor suporta **Opções de SQLSetScrollsomente** apenas para compatibilidade retrógrada; em vez disso, os aplicativos devem usar os atributos de declaração SQL_ATTR_CONCURRENCY, SQL_ATTR_CURSOR_TYPE e SQL_ATTR_ROW_ARRAY_SIZE.
