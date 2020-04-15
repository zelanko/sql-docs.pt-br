---
title: Descritores explicitamente alocados | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- descriptors [ODBC], allocating and freeing
- explicitly allocated descriptors [ODBC]
- allocating and freeing descriptors [ODBC]
ms.assetid: f590251d-56a6-4d58-a405-9e85e68fbc47
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a9950bc23a1e75606316039e6c2d66f3dba59940
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305687"
---
# <a name="explicitly-allocated-descriptors"></a>Descritores explicitamente alocados
Um aplicativo pode alocar explicitamente um descritor de aplicativo em uma conexão a qualquer momento que esteja conectado ao banco de dados. Ao especificar essa alça do descritor como um atributo de uma alça de instrução usando **SQLSetStmtAttr,** o aplicativo orienta o driver a usar esse descritor no lugar dos descritores de aplicativos implícitos correspondentes. O aplicativo não pode especificar descritores de implementação alternativos.  
  
 Um aplicativo pode associar um descritor explicitamente alocado com mais de uma instrução. Somente quando um aplicativo está realmente conectado ao banco de dados pode um descritor ser um descritor explicitamente alocado. O aplicativo pode liberar esse descritor explicitamente, ou implicitamente, liberando sua conexão.
