---
title: Detecção de truncamento de dados habilitada usando ExtendedAnsiSQL | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- truncating data [ODBC]
- extendedANSISQL [ODBC], data truncation detection
ms.assetid: cec2359b-917d-4e1d-9625-5cd678b62f10
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 070537a00c0d179888260bc5cdcdfac0540f12dc
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="data-truncation-detection-enabled-using-extendedansisql"></a>Detecção de truncamento de dados habilitada usando ExtendedAnsiSQL
Quando o sinalizador ExtendedAnsiSQL está ativado e o aplicativo estiver inserindo dados em uma coluna binária ou de char e os dados são truncados, o truncamento será detectado. Quando o sinalizador ExtendedAnsiSQL estiver desativado, os dados são truncados sem aviso, como ele era em versões anteriores dos Drivers de banco de dados de área de trabalho do ODBC.
