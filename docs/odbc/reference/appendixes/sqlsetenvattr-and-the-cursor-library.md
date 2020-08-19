---
description: SQLSetEnvAttr e a Biblioteca de cursores
title: SQLSetEnvAttr e a biblioteca de cursores | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSetEnvAttr function [ODBC], Cursor Library
ms.assetid: 59cc8eae-09ae-4796-869a-c5806488ae83
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 97751c4735ed7357b87a3b50df5f116f7bb38c7d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476928"
---
# <a name="sqlsetenvattr-and-the-cursor-library"></a>SQLSetEnvAttr e a Biblioteca de cursores
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em novos trabalhos de desenvolvimento e planeje modificar os aplicativos que atualmente usam esse recurso. A Microsoft recomenda usar a funcionalidade de cursor do driver.  
  
 Este tópico discute o uso da função **SQLSetEnvAttr** com a biblioteca de cursores. Para obter informações gerais sobre **SQLSetEnvAttr**, consulte [SQLSetEnvAttr function](../../../odbc/reference/syntax/sqlsetenvattr-function.md).  
  
 A biblioteca de cursores não é afetada pela configuração do atributo de ambiente SQL_ATTR_ODBC_VERSION, independentemente da versão do aplicativo ou da versão do driver.
