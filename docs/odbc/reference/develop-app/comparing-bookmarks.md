---
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 44da652ad1e52934fa48f32b1b2f88b30212ad3b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68083299"
---
# <a name="comparing-bookmarks"></a>Comparar indicadores
Como os indicadores são comparáveis por byte, eles podem ser comparados por igualdade ou desigualdade. Para fazer isso, um aplicativo trata cada indicador como uma matriz de bytes e compara dois indicadores de byte por byte. Como os indicadores têm a garantia de serem distintos apenas dentro de um conjunto de resultados, não faz sentido comparar os indicadores que foram obtidos de diferentes conjuntos de resultados.
