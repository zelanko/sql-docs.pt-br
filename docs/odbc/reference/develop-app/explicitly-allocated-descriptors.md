---
title: Explicitamente alocada descritores | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- descriptors [ODBC], allocating and freeing
- explicitly allocated descriptors [ODBC]
- allocating and freeing descriptors [ODBC]
ms.assetid: f590251d-56a6-4d58-a405-9e85e68fbc47
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 791d7620afc4f952ccb99c80cad980ebd2e2e9ea
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="explicitly-allocated-descriptors"></a>Descritores explicitamente alocados
Um aplicativo pode alocar explicitamente um descritor de aplicativo em uma conexão a qualquer momento em que ele está conectado ao banco de dados. Ao especificar esse identificador de descritor como tratar de um atributo de uma instrução usando **SQLSetStmtAttr**, o aplicativo instrui o driver para usar esse descritor no lugar correspondente alocado implicitamente o aplicativo descritores. O aplicativo não é possível especificar descritores de implementação alternativa.  
  
 Um aplicativo pode associar um descritor alocado explicitamente a mais de uma instrução. Somente quando um aplicativo, na verdade, está conectado ao banco de dados um descritor de pode ser um descritor alocado explicitamente. O aplicativo pode liberar tal um descritor explicitamente ou implicitamente, liberando sua conexão.
