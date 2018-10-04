---
title: Alocado explicitamente descritores | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: fbec69e0d984d843abc2b8754e111a1199c79a5a
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47644534"
---
# <a name="explicitly-allocated-descriptors"></a>Descritores explicitamente alocados
Um aplicativo pode alocar explicitamente um descritor de aplicativo em uma conexão a qualquer momento em que ele está conectado ao banco de dados. Especificando esse identificador do descritor de como tratar de um atributo de uma instrução usando **SQLSetStmtAttr**, o aplicativo direciona o driver para usar esse descritor no lugar de correspondente implicitamente alocados aplicativo descritores. O aplicativo não é possível especificar os descritores de implementação alternativa.  
  
 Um aplicativo pode associar um descritor explicitamente alocado com mais de uma instrução. Somente quando um aplicativo está realmente conectado ao banco de dados um descritor de pode ser um descritor alocado explicitamente. O aplicativo pode liberar tal um descritor explícita ou implicitamente ao liberar sua conexão.
