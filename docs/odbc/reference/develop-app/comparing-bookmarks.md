---
title: Comparando indicadores | Microsoft Docs
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
- result sets [ODBC], bookmarks
- comparing bookmarks [ODBC]
- bookmarks [ODBC]
ms.assetid: ea347635-fbe3-41c1-b537-4048b7c0f7da
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1cb844592d47e46a38f431f0127845583b82498a
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="comparing-bookmarks"></a>Comparando indicadores
Como os indicadores são bytes comparável, podem ser comparados para igualdade ou de desigualdade. Para fazer isso, um aplicativo trata cada indicador como uma matriz de bytes e compara os dois indicadores byte a byte. Como indicadores têm garantia distintos apenas dentro de um conjunto de resultados, ele faz sentido para comparar os marcadores que foram obtidos de diferentes conjuntos de resultados.
