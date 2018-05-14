---
title: Bancos de dados XTP do SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: performance-monitor
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQL Server 2016 XTP Databases
ms.assetid: 488ff55e-173f-43f6-9bdb-67b35e7cebfe
caps.latest.revision: 3
author: dagiro
ms.author: v-dagir
manager: craigg
ms.openlocfilehash: a5550c9a6df1ae646d4960a0d9eca8bd5a43bec4
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="sql-server-xtp-databases"></a>Bancos de dados XTP do SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

O objeto de desempenho **Bancos de dados XTP do SQL Server** fornece contadores específicos do banco de dados OLTP in-memory.

> [!NOTE]
>  No momento, os contadores Bancos de dados XTP do SQL Server não são visíveis em sys.dm_os_performance_counters.  Os contadores podem ser exibidos no [Monitor do Sistema](../../relational-databases/performance/start-system-monitor-windows.md).

Esta tabela descreve os contadores **Bancos de dados XTP do SQL Server** .

|Contador|Description| 
|-------------|-----------------|  
|**Tamanho Médio de Dados Grandes do Segmento de Transação**|Tamanho médio da carga de dados grandes do segmento de transação. Este é um contador de nível muito baixo, não planejado para uso do cliente.|
|**Tamanho Médio do Segmento de Transação**|Tamanho médio da carga do segmento de transação. Se esse valor chegar a zero, um número maior de páginas será alocado pelo alocador de back-end. Este é um contador de nível muito baixo, não planejado para uso do cliente.|
|**Profundidade da Fila de 256K do Thread de Liberação**|Profundidade da fila do Thread de Liberação para solicitações de E/S de 256K.|
|**Profundidade da Fila de 4K do Thread de Liberação**|Profundidade da fila do Thread de Liberação para solicitações de E/S de 4K.|
|**Profundidade da Fila de 64K do Thread de Liberação**|Profundidade da fila do Thread de Liberação para solicitações de E/S de 64K.|
|**E/Ss Congelados do Thread de Liberação/s (256K)**|O número de solicitações de E/S de 256K encontradas durante o processamento da página de liberação que estão acima do limite de congelamento e que, portanto, não podem ser emitidas.|
|**E/Ss Congelados do Thread de Liberação/s (4K)**|O número de solicitações de E/S de 4K encontradas durante o processamento da página de liberação que estão acima do limite de congelamento e que, portanto, não podem ser emitidas.|
|**E/Ss Congelados do Thread de Liberação/s (64K)**|O número de solicitações de E/S de 64K encontradas durante o processamento da página de liberação que estão acima do limite de congelamento e que, portanto, não podem ser emitidas.|
|**Contagem de Lista Livre de IoPagePool256K**|Número de páginas na lista livre de 256K no pool de páginas de E/S. Se esse valor chegar a zero, um número maior de páginas será alocado pelo alocador de back-end. Este é um contador de nível muito baixo, não planejado para uso do cliente.|
|**IoPagePool256K Total Alocado**|Número total de páginas alocadas e mantidas pelo pool de páginas de E/S de 256K do alocador de back-end. Este é um contador de nível muito baixo, não planejado para uso do cliente.|
|**Contagem de Lista Livre de IoPagePool4K**|Número de páginas na lista livre de 4K no pool de páginas de E/S. Se esse valor chegar a zero, um número maior de páginas será alocado pelo alocador de back-end. Este é um contador de nível muito baixo, não planejado para uso do cliente.|
|**IoPagePool4K Total Alocado**|Número total de páginas alocadas e mantidas pelo pool de páginas de E/S de 4K do alocador de back-end. Este é um contador de nível muito baixo, não planejado para uso do cliente.|
|**Contagem de Lista Livre de IoPagePool64K**|Número de páginas na lista livre de 64K no pool de páginas de E/S. Se esse valor chegar a zero, um número maior de páginas será alocado pelo alocador de back-end. Este é um contador de nível muito baixo, não planejado para uso do cliente.|
|**IoPagePool64K Total Alocado**|Número total de páginas alocadas e mantidas pelo pool de páginas de E/S de 64K do alocador de back-end. Este é um contador de nível muito baixo, não planejado para uso do cliente.|
|**Contagem de Expansão de 256K de MtLog**|Número de vezes que um MtLog de 256K foi expandido. Este é um contador de nível muito baixo, não planejado para uso do cliente.|
|**E/Ss de 256K de MtLog Pendentes**|O número de solicitações de E/S de 256K pendentes emitidas por MtLog.|
|**% de Preenchimento de Página de 256K de MtLog/Página Liberada**|Percentual de preenchimento médio de cada página de MtLog de 256K liberada. Este é um contador de nível muito baixo, não planejado para uso do cliente.|
|**Bytes de Gravação de 256K de MtLog/s**|Bytes de gravação por segundo em objetos de MtLog de 256K. Este é um contador de nível muito baixo, não planejado para uso do cliente.|
|**Contagem de Expansão de 4K de MtLog**|Número de vezes que um MtLog de 4K foi expandido. Este é um contador de nível muito baixo, não planejado para uso do cliente.|
|**E/Ss de 4K de MtLog Pendentes**|O número de solicitações de E/S de 4K pendentes emitidas por MtLog.|
|**% de Preenchimento de Página de 4K de MtLog/Página Liberada**|Percentual de preenchimento médio de cada página de MtLog de 4K liberada. Este é um contador de nível muito baixo, não planejado para uso do cliente.|
|**Bytes de Gravação de 4K de MtLog/s**|Bytes de gravação por segundo em objetos de MtLog de 4K. Este é um contador de nível muito baixo, não planejado para uso do cliente.|
|**Contagem de Expansão de 64K de MtLog**|Número de vezes que um MtLog de 64K foi expandido. Este é um contador de nível muito baixo, não planejado para uso do cliente.|
|**E/Ss de 64K de MtLog Pendentes**|O número de solicitações de E/S de 64K pendentes emitidas por MtLog.|
|**% de Preenchimento de Página de 64K de MtLog/Página Liberada**|Percentual de preenchimento médio de cada página de MtLog de 64K liberada. Este é um contador de nível muito baixo, não planejado para uso do cliente.|
|**Bytes de Gravação de 64K de MtLog/s**|Bytes de gravação por segundo em objetos de MtLog de 64K. Este é um contador de nível muito baixo, não planejado para uso do cliente.|
|**Número de mesclagens**|O número de mesclagens em trânsito.|
|**Mesclagens de Num./s**|O número de mesclagens criadas por segundo (em média).|
|**Serializações de Num.**|O número de serializações em trânsito.|
|**Serializações de Num./s**|O número de serializações criadas por segundo (em média).|
|**Contagem de Páginas da Parte Final do Cache**|Número de páginas alocadas na Parte Final do Cache. Este é um contador de nível muito baixo, não planejado para uso do cliente.|
|**Pico de Contagem de Páginas da Parte Final do Cache**|Maior número de páginas alocadas na Parte Final do Cache. Este é um contador de nível muito baixo, não planejado para uso do cliente.|


## <a name="see-also"></a>Consulte Também  
[Contadores de desempenho XTP &#40;OLTP in-memory&#41; do SQL Server](../../relational-databases/performance-monitor/sql-server-xtp-in-memory-oltp-performance-counters.md)
