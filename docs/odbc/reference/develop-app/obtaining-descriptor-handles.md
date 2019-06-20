---
title: Obtendo identificadores de descritor | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- descriptors [ODBC], retrieving or setting field values
ms.assetid: 936f983f-c7e9-43f3-97ea-dd4b1bbf4654
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 983097de95e41914bb4d577cb071d790a795f96d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63254682"
---
# <a name="obtaining-descriptor-handles"></a>Obter identificadores de descritor
Um aplicativo obtém o identificador de qualquer descritor alocado explicitamente como um argumento de saída da chamada para **SQLAllocHandle**. O identificador de um descritor de implicitamente alocado é obtido chamando **SQLGetStmtAttr**.
