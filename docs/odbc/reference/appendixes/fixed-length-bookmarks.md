---
title: Indicadores de comprimento fixo | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- backward compatibility [ODBC], bookmarks
- bookmarks [ODBC]
- compatibility [ODBC], bookmarks
- fixed-length bookmarks [ODBC]
ms.assetid: cbd8185e-fb03-408f-b80b-1a2e164534fd
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 279b6a3c1f8eb2f1eea5bba35ee10f0a6643fb49
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="fixed-length-bookmarks"></a>Indicadores de comprimento fixo
Se um ODBC 3*. x* driver deve funcionar com um ODBC 2. *x* aplicativo que usa indicadores de comprimento fixo, o driver devem oferecer suporte a seguir:  
  
-   SQL_UB_ON como um valor para a opção de instrução SQL_USE_BOOKMARKS. (SQL_UB_ON foi preterido no ODBC 3*. x*.)  
  
-   A opção de instrução SQL_GET_BOOKMARK.

