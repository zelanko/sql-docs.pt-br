---
title: Comparando indicadores | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- result sets [ODBC], bookmarks
- comparing bookmarks [ODBC]
- bookmarks [ODBC]
ms.assetid: ea347635-fbe3-41c1-b537-4048b7c0f7da
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 7ebcf375311af498dbb4c777707b7febcddb05a3
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="comparing-bookmarks"></a>Comparando indicadores
Como os indicadores são bytes comparável, podem ser comparados para igualdade ou de desigualdade. Para fazer isso, um aplicativo trata cada indicador como uma matriz de bytes e compara os dois indicadores byte a byte. Como indicadores têm garantia distintos apenas dentro de um conjunto de resultados, ele faz sentido para comparar os marcadores que foram obtidos de diferentes conjuntos de resultados.
