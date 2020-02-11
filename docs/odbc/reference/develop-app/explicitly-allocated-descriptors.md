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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5808265a9ab70b9947cea64fef790497c7229da8
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68069935"
---
# <a name="explicitly-allocated-descriptors"></a>Descritores explicitamente alocados
Um aplicativo pode alocar explicitamente um descritor de aplicativo em uma conexão a qualquer momento que estiver conectado ao banco de dados. Ao especificar esse identificador de descritor como um atributo de um identificador de instrução usando **SQLSetStmtAttr**, o aplicativo direciona o driver para usar esse descritor no lugar dos descripdores de aplicativos implicitamente alocados correspondentes. O aplicativo não pode especificar descritores de implementação alternativos.  
  
 Um aplicativo pode associar um descritor explicitamente alocado com mais de uma instrução. Somente quando um aplicativo está realmente conectado ao banco de dados, um descritor pode ser um descritor explicitamente alocado. O aplicativo pode liberar um descritor explicitamente, ou implicitamente, liberando sua conexão.
