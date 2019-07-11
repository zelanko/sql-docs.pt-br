---
title: Indicadores de comprimento fixo | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- backward compatibility [ODBC], bookmarks
- bookmarks [ODBC]
- compatibility [ODBC], bookmarks
- fixed-length bookmarks [ODBC]
ms.assetid: cbd8185e-fb03-408f-b80b-1a2e164534fd
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 21af6ef1be21e000d25582151650f274fe3561a4
ms.sourcegitcommit: 56b963446965f3a4bb0fa1446f49578dbff382e0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2019
ms.locfileid: "67793367"
---
# <a name="fixed-length-bookmarks"></a>Indicadores de comprimento fixo
Se um ODBC *3.x* driver deve funcionar com um ODBC *2.x* aplicativo que usa indicadores de comprimento fixo, o driver devem oferecer suporte a seguir:  
  
-   SQL_UB_ON como um valor para a opção de instrução SQL_USE_BOOKMARKS. (SQL_UB_ON foi preterido no ODBC *3.x*.)  
  
-   A opção de instrução SQL_GET_BOOKMARK.
