---
description: Obter identificadores de descritor
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c46ce0bff7240c121c6c56a5c3cd1b19769afb04
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429198"
---
# <a name="obtaining-descriptor-handles"></a>Obter identificadores de descritor
Um aplicativo obtém o identificador de qualquer descritor explicitamente alocado como um argumento de saída da chamada para **SQLAllocHandle**. O identificador de um descritor implicitamente alocado é obtido chamando **SQLGetStmtAttr**.
