---
title: Marcadores de comprimento fixo | Microsoft Docs
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306977"
---
# <a name="fixed-length-bookmarks"></a>Indicadores de comprimento fixo
Se um driver ODBC *3.x* trabalhar com um aplicativo ODBC *2.x* que use marcadores de comprimento fixo, o driver deve suportar o seguinte:  
  
-   SQL_UB_ON como um valor para a opção de declaração SQL_USE_BOOKMARKS. (SQL_UB_ON é preterido em ODBC *3.x*.)  
  
-   A opção de declaração SQL_GET_BOOKMARK.
