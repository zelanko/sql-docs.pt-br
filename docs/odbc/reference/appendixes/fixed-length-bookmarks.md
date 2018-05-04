---
title: Indicadores de comprimento fixo | Microsoft Docs
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
- backward compatibility [ODBC], bookmarks
- bookmarks [ODBC]
- compatibility [ODBC], bookmarks
- fixed-length bookmarks [ODBC]
ms.assetid: cbd8185e-fb03-408f-b80b-1a2e164534fd
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c94d79500047fe1f918689426846a3faa98bb2d7
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="fixed-length-bookmarks"></a>Indicadores de comprimento fixo
Se um ODBC 3 *. x* driver deve funcionar com um ODBC 2. *x* aplicativo que usa indicadores de comprimento fixo, o driver devem oferecer suporte a seguir:  
  
-   SQL_UB_ON como um valor para a opção de instrução SQL_USE_BOOKMARKS. (SQL_UB_ON foi preterido no ODBC 3 *. x*.)  
  
-   A opção de instrução SQL_GET_BOOKMARK.
