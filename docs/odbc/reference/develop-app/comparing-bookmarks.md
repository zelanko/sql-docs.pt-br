---
title: Comparando indicadores | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- result sets [ODBC], bookmarks
- comparing bookmarks [ODBC]
- bookmarks [ODBC]
ms.assetid: ea347635-fbe3-41c1-b537-4048b7c0f7da
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: c3d26095cf879859e6ea74784fcf87694ba5eb5d
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/20/2017
---
# <a name="comparing-bookmarks"></a>Comparando indicadores
Como os indicadores são bytes comparável, podem ser comparados para igualdade ou de desigualdade. Para fazer isso, um aplicativo trata cada indicador como uma matriz de bytes e compara os dois indicadores byte a byte. Como indicadores têm garantia distintos apenas dentro de um conjunto de resultados, ele faz sentido para comparar os marcadores que foram obtidos de diferentes conjuntos de resultados.
