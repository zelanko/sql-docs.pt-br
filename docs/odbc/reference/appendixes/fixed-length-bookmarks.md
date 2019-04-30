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
ms.openlocfilehash: e40947dc4dbad0830444870ea7e2d0c663490b25
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63188973"
---
# <a name="fixed-length-bookmarks"></a>Indicadores de comprimento fixo
Se um ODBC 3 *. x* driver deve funcionar com um ODBC 2. *x* aplicativo que usa indicadores de comprimento fixo, o driver devem oferecer suporte a seguir:  
  
-   SQL_UB_ON como um valor para a opção de instrução SQL_USE_BOOKMARKS. (SQL_UB_ON foi preterido no ODBC 3 *. x*.)  
  
-   A opção de instrução SQL_GET_BOOKMARK.
