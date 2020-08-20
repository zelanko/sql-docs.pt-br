---
description: SQLFetch (Biblioteca de cursores)
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ce9da3c0c5b95be4336c58896b17b6ba5daf6443
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88465998"
---
# <a name="sqlfetch-cursor-library"></a>SQLFetch (Biblioteca de cursores)
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em novos trabalhos de desenvolvimento e planeje modificar os aplicativos que atualmente usam esse recurso. A Microsoft recomenda usar a funcionalidade de cursor do driver.  
  
 Este tópico discute o uso da função **SQLFetch** na biblioteca de cursores. Para obter informações gerais sobre **SQLFetch**, consulte [função SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md).  
  
 Quando a biblioteca de cursores é usada, as chamadas para **SQLFetch** não podem ser misturadas com chamadas para **SQLFetchScroll** ou **SQLExtendedFetch**.  
  
 Se **SQLFetch** for chamado com SQL_ATTR_ROW_ARRAY_SIZE definido como um valor maior que 1, a biblioteca de cursores passará a chamada para o driver. Se o driver for um ODBC 2. *x* Driver, o tamanho do conjunto de linhas será ignorado e a chamada para **SQLFetch** retornará uma única linha de dados.  
  
 Se a biblioteca de cursores for usada com um ODBC 2. *x* Driver, um deslocamento de ligação (conforme definido pelo atributo de instrução SQL_ATTR_ROW_BIND_OFFSET_PTR) não é usado quando **SQLFetch** é chamado.  
  
 Quando a biblioteca de cursores é carregada, um aplicativo não pode chamar **SQLFetch** para buscar colunas de indicador. A biblioteca de cursores passa a chamada para **SQLFetch** até o driver, mas as chamadas de função para habilitar indicadores e associar a coluna de indicador são interceptadas pela biblioteca de cursores.
