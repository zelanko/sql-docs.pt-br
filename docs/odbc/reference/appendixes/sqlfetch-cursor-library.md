---
title: SQLFetch (Biblioteca do Cursor) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLFetch function [ODBC], Cursor Library
ms.assetid: 35a0d493-778b-4fb1-84ee-a13540e2fe0e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: bee83ccb5497888b57a45673599af6b92931a704
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298716"
---
# <a name="sqlfetch-cursor-library"></a>SQLFetch (Biblioteca de cursores)
> [!IMPORTANT]  
>  Esse recurso será removido em uma versão futura do Windows. Evite usar esse recurso em novos trabalhos de desenvolvimento e planeje modificar aplicativos que atualmente usam esse recurso. A Microsoft recomenda o uso da funcionalidade do cursor do driver.  
  
 Este tópico discute o uso da função **SQLFetch** na biblioteca do cursor. Para obter informações gerais sobre **o SQLFetch,** consulte [SQLFetch Function](../../../odbc/reference/syntax/sqlfetch-function.md).  
  
 Quando a biblioteca do cursor é usada, as chamadas para **SQLFetch** não podem ser misturadas com chamadas para **SQLFetchScroll** ou **SQLExtendedFetch**.  
  
 Se **o SQLFetch** for chamado com SQL_ATTR_ROW_ARRAY_SIZE definido para um valor maior que 1, a biblioteca do cursor passará a chamada para o driver. Se o driver for um ODBC 2. *x* driver, o tamanho do conjunto de linhas será ignorado e a chamada para **SQLFetch** retornará uma única linha de dados.  
  
 Se a biblioteca do cursor for usada com um ODBC 2. *x* driver, uma compensação de vinculação (como definido pelo atributo de declaração SQL_ATTR_ROW_BIND_OFFSET_PTR) não é usada quando **o SQLFetch** é chamado.  
  
 Quando a biblioteca do cursor é carregada, um aplicativo não pode chamar **o SQLFetch** para buscar colunas de marcadores. A biblioteca do cursor passa a chamada para **SQLFetch** através do driver, mas as chamadas de função para ativar marcadores e vincular a coluna de marcadores são interceptadas pela biblioteca do cursor.
