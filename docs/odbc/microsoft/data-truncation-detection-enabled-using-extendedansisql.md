---
title: Detecção de truncação de dados habilitada usando AnsiSQL estendido | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- truncating data [ODBC]
- extendedANSISQL [ODBC], data truncation detection
ms.assetid: cec2359b-917d-4e1d-9625-5cd678b62f10
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ae1aa7a8a8b9ea2c3f3054717546506e660d5270
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81280688"
---
# <a name="data-truncation-detection-enabled-using-extendedansisql"></a>Detecção de truncamento de dados habilitada usando ExtendedAnsiSQL
Quando o sinalizador ExtendedAnsiSQL é ligado e o aplicativo está inserindo dados em uma coluna char ou binária e os dados são truncados, a truncação será detectada. Quando o sinalizador ExtendedAnsiSQL é desligado, os dados são truncados sem aviso, como era nas versões anteriores do ODBC Desktop Database Drivers.
