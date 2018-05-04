---
title: SQLRowCount (biblioteca de Cursor) | Microsoft Docs
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
- SQLRowCount function [ODBC], Cursor Library
ms.assetid: 781cf5a5-325e-4523-8633-d96d9e98277c
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 548387e46b4ce1d840c6bf0bb48112d45b643583
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="sqlrowcount-cursor-library"></a>SQLRowCount (biblioteca de Cursor)
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. A Microsoft recomenda o uso da funcionalidade de cursor do driver.  
  
 Este tópico discute o uso do **SQLRowCount** função na biblioteca de cursor. Para obter informações gerais sobre **SQLRowCount**, consulte [função SQLRowCount](../../../odbc/reference/syntax/sqlrowcount-function.md).  
  
 Quando um aplicativo chama **SQLRowCount** com a instrução associada com o cursor, a biblioteca de cursores retorna o número de linhas de dados que ele foi recuperada do driver.  
  
 Quando um aplicativo chama **SQLRowCount** com a instrução associada a uma atualização posicionada ou uma instrução delete, a biblioteca de cursores retorna o número de linhas afetadas pela instrução.  
  
 Quando um aplicativo chama **SQLRowCount** após um **selecione** instrução, a biblioteca de cursores retorna -1.
