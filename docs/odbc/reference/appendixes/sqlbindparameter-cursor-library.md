---
title: SQLBindParameter (biblioteca de cursores) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLBindParameter function [ODBC], Cursor Library
ms.assetid: 04c53e4c-cd1d-40b2-9997-684ebe43499f
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: eafab0f29cb4e1b7ecdfea378f9315ba29cf133f
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63199675"
---
# <a name="sqlbindparameter-cursor-library"></a>SQLBindParameter (Biblioteca de cursores)
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que usam esse recurso atualmente. A Microsoft recomenda usar a funcionalidade de cursor do driver.  
  
 Este tópico discute o uso do **SQLBindParameter** função na biblioteca de cursor. Para obter informações gerais sobre **SQLBindParameter**, consulte [função SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md).  
  
 Um aplicativo pode chamar **SQLBindParameter** para reassociar os parâmetros, desde que o tipo de dados C, tamanho da coluna e dígitos decimais da coluna acoplada permanecem os mesmos.  
  
 A biblioteca de cursores dá suporte à configuração do atributo de instrução SQL_ATTR_ROW_BIND_OFFSET_PTR para usar os deslocamentos de associação. (**SQLBindParameter** não precisa ser chamado para essa nova associação ocorra.)  
  
 A biblioteca de cursores dá suporte a parâmetros de dados em execução de associação.
