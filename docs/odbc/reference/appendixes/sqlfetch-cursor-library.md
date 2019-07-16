---
title: SQLFetch (biblioteca de cursores) | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2cb829f065421a13d3c7df06c670808bc3d9d77c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68064428"
---
# <a name="sqlfetch-cursor-library"></a>SQLFetch (Biblioteca de cursores)
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que usam esse recurso atualmente. A Microsoft recomenda usar a funcionalidade de cursor do driver.  
  
 Este tópico discute o uso do **SQLFetch** função na biblioteca de cursor. Para obter informações gerais sobre **SQLFetch**, consulte [função SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md).  
  
 Quando a biblioteca de cursores é usada, chamadas para **SQLFetch** não podem ser misturadas a chamadas para um **SQLFetchScroll** ou **SQLExtendedFetch**.  
  
 Se **SQLFetch** é chamado com SQL_ATTR_ROW_ARRAY_SIZE definido como um valor maior que 1, a biblioteca de cursores passará a chamada para o driver. Se o driver é um ODBC 2. *x* driver, o tamanho do conjunto de linhas será ignorado e a chamada para **SQLFetch** retornará uma única linha de dados.  
  
 Se a biblioteca de cursores é usada com um ODBC 2. *x* driver, uma ligação de deslocamento (conforme definido pelo atributo de instrução SQL_ATTR_ROW_BIND_OFFSET_PTR) não é usado quando **SQLFetch** é chamado.  
  
 Quando a biblioteca de cursores é carregada, um aplicativo não é possível chamar **SQLFetch** para buscar colunas de indicador. A biblioteca de cursores passará a chamada para **SQLFetch** por meio do driver, mas a função chamadas para habilitar indicadores e associar a coluna de indicador são interceptadas pela biblioteca de cursores.
