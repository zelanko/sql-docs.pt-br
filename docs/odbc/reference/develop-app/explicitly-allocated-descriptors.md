---
description: Descritores explicitamente alocados
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
ms.openlocfilehash: 7215d17a7156419f08bbd73528c468d7b6355b94
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461478"
---
# <a name="explicitly-allocated-descriptors"></a>Descritores explicitamente alocados
Um aplicativo pode alocar explicitamente um descritor de aplicativo em uma conexão a qualquer momento que estiver conectado ao banco de dados. Ao especificar esse identificador de descritor como um atributo de um identificador de instrução usando **SQLSetStmtAttr**, o aplicativo direciona o driver para usar esse descritor no lugar dos descripdores de aplicativos implicitamente alocados correspondentes. O aplicativo não pode especificar descritores de implementação alternativos.  
  
 Um aplicativo pode associar um descritor explicitamente alocado com mais de uma instrução. Somente quando um aplicativo está realmente conectado ao banco de dados, um descritor pode ser um descritor explicitamente alocado. O aplicativo pode liberar um descritor explicitamente, ou implicitamente, liberando sua conexão.
