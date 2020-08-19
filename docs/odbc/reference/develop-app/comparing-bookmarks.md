---
description: Comparar indicadores
title: Comparando indicadores | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- result sets [ODBC], bookmarks
- comparing bookmarks [ODBC]
- bookmarks [ODBC]
ms.assetid: ea347635-fbe3-41c1-b537-4048b7c0f7da
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 939c3780fc9c6738a307e9a969a346951cfac5e7
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476778"
---
# <a name="comparing-bookmarks"></a>Comparar indicadores
Como os indicadores são comparáveis por byte, eles podem ser comparados por igualdade ou desigualdade. Para fazer isso, um aplicativo trata cada indicador como uma matriz de bytes e compara dois indicadores de byte por byte. Como os indicadores têm a garantia de serem distintos apenas dentro de um conjunto de resultados, não faz sentido comparar os indicadores que foram obtidos de diferentes conjuntos de resultados.
