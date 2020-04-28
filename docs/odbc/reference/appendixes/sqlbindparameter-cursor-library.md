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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 55708cc5192fb40149d6db7710f6ee638c4880d2
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81305424"
---
# <a name="sqlbindparameter-cursor-library"></a>SQLBindParameter (Biblioteca de cursores)
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em novos trabalhos de desenvolvimento e planeje modificar os aplicativos que atualmente usam esse recurso. A Microsoft recomenda usar a funcionalidade de cursor do driver.  
  
 Este tópico discute o uso da função **SQLBindParameter** na biblioteca de cursores. Para obter informações gerais sobre **SQLBindParameter**, consulte [SQLBindParameter function](../../../odbc/reference/syntax/sqlbindparameter-function.md).  
  
 Um aplicativo pode chamar **SQLBindParameter** para reassociar parâmetros, desde que o tipo de dados C, o tamanho da coluna e os dígitos decimais da coluna associada permaneçam os mesmos.  
  
 A biblioteca de cursores dá suporte à definição do atributo instrução SQL_ATTR_ROW_BIND_OFFSET_PTR para usar deslocamentos de ligação. (**SQLBindParameter** não precisa ser chamado para que essa reassociação ocorra.)  
  
 A biblioteca de cursores dá suporte à associação de parâmetros de dados em execução.
