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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c28392c0d48984b4aaf8a8df442b6a4054a7eced
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81307471"
---
# <a name="comparing-bookmarks"></a>Comparar indicadores
Como os indicadores são comparáveis por byte, eles podem ser comparados por igualdade ou desigualdade. Para fazer isso, um aplicativo trata cada indicador como uma matriz de bytes e compara dois indicadores de byte por byte. Como os indicadores têm a garantia de serem distintos apenas dentro de um conjunto de resultados, não faz sentido comparar os indicadores que foram obtidos de diferentes conjuntos de resultados.
