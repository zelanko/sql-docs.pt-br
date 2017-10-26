---
title: Explicitamente alocada descritores | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- descriptors [ODBC], allocating and freeing
- explicitly allocated descriptors [ODBC]
- allocating and freeing descriptors [ODBC]
ms.assetid: f590251d-56a6-4d58-a405-9e85e68fbc47
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 7a4679fa6c6d2185f6e474407882080fea6b7c8a
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="explicitly-allocated-descriptors"></a>Descritores explicitamente alocados
Um aplicativo pode alocar explicitamente um descritor de aplicativo em uma conexão a qualquer momento em que ele está conectado ao banco de dados. Ao especificar esse identificador de descritor como tratar de um atributo de uma instrução usando **SQLSetStmtAttr**, o aplicativo instrui o driver para usar esse descritor no lugar correspondente alocado implicitamente o aplicativo descritores. O aplicativo não é possível especificar descritores de implementação alternativa.  
  
 Um aplicativo pode associar um descritor alocado explicitamente a mais de uma instrução. Somente quando um aplicativo, na verdade, está conectado ao banco de dados um descritor de pode ser um descritor alocado explicitamente. O aplicativo pode liberar tal um descritor explicitamente ou implicitamente, liberando sua conexão.

