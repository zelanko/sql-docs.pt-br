---
title: SQLGetFunctions (biblioteca de Cursor) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQLGetFunctions function [ODBC], Cursor Library
ms.assetid: 931acd12-4eb6-4a78-9a77-157a18a9a2d0
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 45778aeb876b50e44323f91a0aaf00d480130456
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="sqlgetfunctions-cursor-library"></a>SQLGetFunctions (biblioteca de Cursor)
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. A Microsoft recomenda o uso da funcionalidade de cursor do driver.  
  
 Este tópico discute o uso do **SQLGetFunctions** função na biblioteca de cursor. Para obter informações gerais sobre **SQLGetFunctions**, consulte [função SQLGetFunctions](../../../odbc/reference/syntax/sqlgetfunctions-function.md).  
  
 Quando você chama **SQLGetFunctions**, a biblioteca de cursores retorna que ele oferece suporte **SQLExtendedFetch**, **SQLFetchScroll**, **SQLSetPos**, e **SQLSetScrollOptions**, além das funções com suporte pelo driver.
