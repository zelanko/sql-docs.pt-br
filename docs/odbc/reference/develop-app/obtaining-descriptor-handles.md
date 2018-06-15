---
title: Como obter o descritor manipula | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- descriptors [ODBC], retrieving or setting field values
ms.assetid: 936f983f-c7e9-43f3-97ea-dd4b1bbf4654
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9848bf1fefed159865861ba609ec977e317094fd
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32911951"
---
# <a name="obtaining-descriptor-handles"></a>Como obter o descritor manipula
Um aplicativo obtém o identificador de qualquer descritor alocado explicitamente como um argumento de saída da chamada para **SQLAllocHandle**. O identificador de um descritor alocado implicitamente é obtido chamando **SQLGetStmtAttr**.
