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
ms.openlocfilehash: 8bfa0b36ecca3af655efde84c3ce3f22ab0c1f88
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68086316"
---
# <a name="obtaining-descriptor-handles"></a>Obter identificadores de descritor
Um aplicativo obtém o identificador de qualquer descritor explicitamente alocado como um argumento de saída da chamada para **SQLAllocHandle**. O identificador de um descritor implicitamente alocado é obtido chamando **SQLGetStmtAttr**.
