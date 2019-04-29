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
manager: craigg
ms.openlocfilehash: 690acf80bfabdc04d5f70b780e41943337c18cb9
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63026609"
---
# <a name="comparing-bookmarks"></a>Comparar indicadores
Como os indicadores são comparáveis de byte, eles podem ser comparados para igualdade ou desigualdade. Para fazer isso, um aplicativo trata cada indicador como uma matriz de bytes e compara os dois indicadores byte a byte. Como os indicadores são certamente distintas dentro de um conjunto de resultados, ele não faz sentido para comparar os indicadores que foram obtidos de diferentes conjuntos de resultados.
