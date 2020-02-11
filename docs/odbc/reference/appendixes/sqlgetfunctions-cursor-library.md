---
title: SQLGetFunctions (biblioteca de cursores) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLGetFunctions function [ODBC], Cursor Library
ms.assetid: 931acd12-4eb6-4a78-9a77-157a18a9a2d0
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1497a7d2ec5951feedb36831ab541413e57152f4
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68073928"
---
# <a name="sqlgetfunctions-cursor-library"></a>SQLGetFunctions (Biblioteca de cursores)
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em novos trabalhos de desenvolvimento e planeje modificar os aplicativos que atualmente usam esse recurso. A Microsoft recomenda usar a funcionalidade de cursor do driver.  
  
 Este tópico discute o uso da função **SQLGetFunctions** na biblioteca de cursores. Para obter informações gerais sobre **SQLGetFunctions**, consulte [SQLGetFunctions function](../../../odbc/reference/syntax/sqlgetfunctions-function.md).  
  
 Quando você chama **SQLGetFunctions**, a biblioteca de cursores retorna que dá suporte a **SQLExtendedFetch**, **SQLFetchScroll**, **SQLSetPos**e **SQLSetScrollOptions**, além das funções com suporte pelo driver.
