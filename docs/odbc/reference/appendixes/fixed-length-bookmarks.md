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
ms.openlocfilehash: 5877a6cb7a99803f854338321e333c87037c2e90
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67913579"
---
# <a name="fixed-length-bookmarks"></a>Indicadores de comprimento fixo
Se um driver ODBC *3. x* deve funcionar com um aplicativo ODBC *2. x* que usa indicadores de comprimento fixo, o driver deve dar suporte ao seguinte:  
  
-   SQL_UB_ON como um valor para a opção de instrução SQL_USE_BOOKMARKS. (O SQL_UB_ON é preterido no ODBC *3. x*.)  
  
-   A opção de instrução SQL_GET_BOOKMARK.
