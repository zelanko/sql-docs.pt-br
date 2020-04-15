---
title: Comparando marcadores | Microsoft Docs
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
ms.openlocfilehash: c28392c0d48984b4aaf8a8df442b6a4054a7eced
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307471"
---
# <a name="comparing-bookmarks"></a>Comparar indicadores
Como os marcadores são comparáveis, eles podem ser comparados por igualdade ou desigualdade. Para isso, um aplicativo trata cada marcador como uma matriz de bytes e compara dois marcadores byte-by-byte. Como os marcadores são garantidos para serem distintos apenas dentro de um conjunto de resultados, não faz sentido comparar marcadores que foram obtidos de diferentes conjuntos de resultados.
