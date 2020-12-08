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
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.openlocfilehash: 8c41d49b9fb5e25381879a803b3b10963b13b8ba
ms.sourcegitcommit: 0e0cd9347c029e0c7c9f3fe6d39985a6d3af967d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/02/2020
ms.locfileid: "96505650"
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

