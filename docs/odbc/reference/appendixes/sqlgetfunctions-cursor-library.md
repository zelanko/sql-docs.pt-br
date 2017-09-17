---
title: SQLGetFunctions (biblioteca de Cursor) | Microsoft Docs
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
- SQLGetFunctions function [ODBC], Cursor Library
ms.assetid: 931acd12-4eb6-4a78-9a77-157a18a9a2d0
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 6d8ca656e63183df424de2ec45c823ac275ef69f
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="sqlgetfunctions-cursor-library"></a>SQLGetFunctions (biblioteca de Cursor)
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. A Microsoft recomenda o uso da funcionalidade de cursor do driver.  
  
 Este tópico discute o uso do **SQLGetFunctions** função na biblioteca de cursor. Para obter informações gerais sobre **SQLGetFunctions**, consulte [função SQLGetFunctions](../../../odbc/reference/syntax/sqlgetfunctions-function.md).  
  
 Quando você chama **SQLGetFunctions**, a biblioteca de cursores retorna que ele oferece suporte **SQLExtendedFetch**, **SQLFetchScroll**, **SQLSetPos**, e **SQLSetScrollOptions**, além das funções com suporte pelo driver.
