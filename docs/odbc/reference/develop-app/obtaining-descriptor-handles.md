---
title: Como obter o descritor manipula | Microsoft Docs
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
- descriptors [ODBC], retrieving or setting field values
ms.assetid: 936f983f-c7e9-43f3-97ea-dd4b1bbf4654
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: eefe0ed5b32c2c6b3f815a239f52cc82a947735a
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="obtaining-descriptor-handles"></a>Como obter o descritor manipula
Um aplicativo obtém o identificador de qualquer descritor alocado explicitamente como um argumento de saída da chamada para **SQLAllocHandle**. O identificador de um descritor alocado implicitamente é obtido chamando **SQLGetStmtAttr**.
