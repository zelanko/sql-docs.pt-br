---
title: SQL Server, objeto LogPool FreePool | Microsoft Docs
description: Saiba mais sobre o objeto de desempenho SQLServer:LogPool FreePool, que fornece contadores de estatísticas do pool livre dentro do Pool de Logs.
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- SQLServer:LogPool FreePool
ms.assetid: 8ffd569b-045f-4c3f-a473-4a491d6a1d80
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: b3ffe8512adc1fd21bcf33741d0a10db058d5752
ms.sourcegitcommit: 9470c4d1fc8d2d9d08525c4f811282999d765e6e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/17/2020
ms.locfileid: "86457712"
---
# <a name="sql-server-logpool-freepool-object"></a>SQL Server, objeto LogPool FreePool
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
O objeto de desempenho **SQLServer:LogPool FreePool** fornece contadores de estatísticas para o pool livre dentro do Pool de Logs.

A tabela a seguir descreve os objetos de desempenho **LogPool FreePool** do SQL Server.

|**Contadores de LogPool FreePool do SQL Server**|Descrição|  
|-------------|-----------------|  
|**Reabastecimentos do Buffer Gratuito/seg**|Número de buffers alocados para reabastecimento por segundo.|
|**Comprimento de lista livre**|Comprimento da lista livre.|

Há uma instância do contador para cada categoria do pool de logs.

## <a name="see-also"></a>Consulte Também  
[Monitorar o uso de recursos (Monitor do Sistema)](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)

