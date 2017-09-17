---
title: SQLFetch (biblioteca de Cursor) | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQLFetch function [ODBC], Cursor Library
ms.assetid: 35a0d493-778b-4fb1-84ee-a13540e2fe0e
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 1e5cabca53c503e2cd0c12147248b11da84ed157
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="sqlfetch-cursor-library"></a>SQLFetch (biblioteca de Cursor)
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. A Microsoft recomenda o uso da funcionalidade de cursor do driver.  
  
 Este tópico discute o uso do **SQLFetch** função na biblioteca de cursor. Para obter informações gerais sobre **SQLFetch**, consulte [função SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md).  
  
 Quando a biblioteca de cursores é usada, chamadas para **SQLFetch** não podem ser misturadas a chamadas para o **SQLFetchScroll** ou **SQLExtendedFetch**.  
  
 Se **SQLFetch** é chamado com SQL_ATTR_ROW_ARRAY_SIZE definido como um valor maior que 1, a biblioteca de cursores passará a chamada para o driver. Se o driver é um ODBC 2. *x* driver, o tamanho do conjunto de linhas será ignorado e a chamada para **SQLFetch** retornará uma única linha de dados.  
  
 Se a biblioteca de cursores é usada com um ODBC 2. *x* driver, uma ligação de deslocamento (conforme definido pelo atributo de instrução SQL_ATTR_ROW_BIND_OFFSET_PTR) não é usado quando **SQLFetch** é chamado.  
  
 Quando a biblioteca de cursores é carregada, um aplicativo não é possível chamar **SQLFetch** para buscar colunas de indicador. A biblioteca de cursores passará a chamada para **SQLFetch** por meio do driver, mas a função chamadas para habilitar os indicadores e associar a coluna de indicador são interceptadas pela biblioteca de cursores.
