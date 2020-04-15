---
title: SQLExtendedFetch (Biblioteca cursor) | Microsoft Docs
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
ms.openlocfilehash: fe39b2d2cbbaf72ce3844c35187040589d1dac58
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302057"
---
# <a name="sqlextendedfetch-cursor-library"></a>SQLExtendedFetch (Biblioteca de cursores)
> [!IMPORTANT]  
>  Esse recurso será removido em uma versão futura do Windows. Evite usar esse recurso em novos trabalhos de desenvolvimento e planeje modificar aplicativos que atualmente usam esse recurso. A Microsoft recomenda o uso da funcionalidade do cursor do driver.  
  
 Este tópico discute o uso da função **SQLExtendedFetch** na biblioteca do cursor. Para obter informações gerais sobre **o SQLExtendedFetch,** consulte [SQLExtendedFetch Function](../../../odbc/reference/syntax/sqlextendedfetch-function.md).  
  
 A biblioteca do cursor implementa **o SQLExtendedFetch** chamando repetidamente **sqlfetch** no driver.  
  
 A biblioteca do cursor suporta chamar **SQLExtendedFetch** com uma orientação de *SQL_FETCH_BOOKMARK.*  
  
 Quando a biblioteca do cursor é usada, as chamadas para **SQLExtendedFetch** não podem ser misturadas com chamadas para **SQLFetchScroll** ou **SQLFetch**.
