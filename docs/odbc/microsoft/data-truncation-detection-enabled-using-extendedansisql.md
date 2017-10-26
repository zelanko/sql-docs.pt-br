---
title: "Detecção de truncamento de dados habilitada usando ExtendedAnsiSQL | Microsoft Docs"
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
- truncating data [ODBC]
- extendedANSISQL [ODBC], data truncation detection
ms.assetid: cec2359b-917d-4e1d-9625-5cd678b62f10
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 87affbd567a817ea119c405b64f96effe2358052
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="data-truncation-detection-enabled-using-extendedansisql"></a>Detecção de truncamento de dados habilitada usando ExtendedAnsiSQL
Quando o sinalizador ExtendedAnsiSQL está ativado e o aplicativo estiver inserindo dados em uma coluna binária ou de char e os dados são truncados, o truncamento será detectado. Quando o sinalizador ExtendedAnsiSQL estiver desativado, os dados são truncados sem aviso, como ele era em versões anteriores dos Drivers de banco de dados de área de trabalho do ODBC.

