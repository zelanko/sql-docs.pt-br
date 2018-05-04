---
title: Explicitamente alocada descritores | Microsoft Docs
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
- descriptors [ODBC], allocating and freeing
- explicitly allocated descriptors [ODBC]
- allocating and freeing descriptors [ODBC]
ms.assetid: f590251d-56a6-4d58-a405-9e85e68fbc47
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1f09c3d7817fdb3d7f992255a7c2242c515e9748
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="explicitly-allocated-descriptors"></a>Descritores explicitamente alocados
Um aplicativo pode alocar explicitamente um descritor de aplicativo em uma conexão a qualquer momento em que ele está conectado ao banco de dados. Ao especificar esse identificador de descritor como tratar de um atributo de uma instrução usando **SQLSetStmtAttr**, o aplicativo instrui o driver para usar esse descritor no lugar correspondente alocado implicitamente o aplicativo descritores. O aplicativo não é possível especificar descritores de implementação alternativa.  
  
 Um aplicativo pode associar um descritor alocado explicitamente a mais de uma instrução. Somente quando um aplicativo, na verdade, está conectado ao banco de dados um descritor de pode ser um descritor alocado explicitamente. O aplicativo pode liberar tal um descritor explicitamente ou implicitamente, liberando sua conexão.
