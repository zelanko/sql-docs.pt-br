---
description: Detecção de truncamento de dados habilitada usando ExtendedAnsiSQL
title: Detecção de truncamento de dados habilitada usando ExtendedAnsiSQL | Microsoft Docs
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
ms.openlocfilehash: 26965093caecbc11e94ef738ba6b8ff757b43258
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88412880"
---
# <a name="data-truncation-detection-enabled-using-extendedansisql"></a>Detecção de truncamento de dados habilitada usando ExtendedAnsiSQL
Quando o sinalizador ExtendedAnsiSQL é ativado e o aplicativo está inserindo dados em uma coluna char ou Binary e os dados são truncados, o truncamento será detectado. Quando o sinalizador ExtendedAnsiSQL está desativado, os dados são truncados sem aviso, pois estavam em versões anteriores dos drivers de banco de dados da área de trabalho do ODBC.
