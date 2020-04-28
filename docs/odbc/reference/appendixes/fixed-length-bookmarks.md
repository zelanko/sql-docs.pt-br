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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f90c5888a68506c056b2a56fce516080148528e7
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81306977"
---
# <a name="fixed-length-bookmarks"></a>Indicadores de comprimento fixo
Se um driver ODBC *3. x* deve funcionar com um aplicativo ODBC *2. x* que usa indicadores de comprimento fixo, o driver deve dar suporte ao seguinte:  
  
-   SQL_UB_ON como um valor para a opção de instrução SQL_USE_BOOKMARKS. (O SQL_UB_ON é preterido no ODBC *3. x*.)  
  
-   A opção de instrução SQL_GET_BOOKMARK.
