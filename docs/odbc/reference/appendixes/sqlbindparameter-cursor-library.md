---
description: SQLBindParameter (Biblioteca de cursores)
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
ms.openlocfilehash: 96fb4f3390b062a4b86f7a7b7f457c43c476c26c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88466068"
---
# <a name="sqlbindparameter-cursor-library"></a>SQLBindParameter (Biblioteca de cursores)
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em novos trabalhos de desenvolvimento e planeje modificar os aplicativos que atualmente usam esse recurso. A Microsoft recomenda usar a funcionalidade de cursor do driver.  
  
 Este tópico discute o uso da função **SQLBindParameter** na biblioteca de cursores. Para obter informações gerais sobre **SQLBindParameter**, consulte [SQLBindParameter function](../../../odbc/reference/syntax/sqlbindparameter-function.md).  
  
 Um aplicativo pode chamar **SQLBindParameter** para reassociar parâmetros, desde que o tipo de dados C, o tamanho da coluna e os dígitos decimais da coluna associada permaneçam os mesmos.  
  
 A biblioteca de cursores dá suporte à definição do atributo instrução SQL_ATTR_ROW_BIND_OFFSET_PTR para usar deslocamentos de ligação. (**SQLBindParameter** não precisa ser chamado para que essa reassociação ocorra.)  
  
 A biblioteca de cursores dá suporte à associação de parâmetros de dados em execução.
