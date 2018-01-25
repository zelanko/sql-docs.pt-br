---
title: Coleta de lixo de SQL Server XTP | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: performance-monitor
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 64ae91e5-b420-44b4-af1a-f8bca83d7f41
caps.latest.revision: "8"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 7586018babe172065e701a8ade9be56593fd6af8
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/18/2018
---
# <a name="sql-server-xtp-garbage-collection"></a>Coleta de Lixo de XTP do SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  O objeto de desempenho Coleta de Lixo de XTP do SQL Server contém os contadores relacionados ao coletor de lixo do mecanismo OLTP in-memory.  
  
 Esta tabela descreve os contadores de **Coleta de Lixo de XTP do SQL Server** .  
  
|Contador|Description|  
|-------------|-----------------|  
|**Tentativas de verificação de canto sujo/s (emitido pelo GC)**|O número de tentativas de digitalização devido a conflitos de gravação durante as varreduras de canto sujo emitidas pelo coletor de lixo (em média), por segundo. Este é um contador de nível muito baixo, não planejado para uso do cliente.|  
|**Itens principais do trabalho do GC/s**|O número de itens de trabalho processados pelo thread principal do GC.|  
|**Item de trabalho do GC em paralelo/s**|O número de vezes que um thread paralelo executou um item de trabalho do GC.|  
|**Linhas processadas/s**|O número de linhas processadas pelo coletor de lixo (em média), por segundo|  
|**Linhas processadas/s (primeiro no bucket e removidas)**|O número de linhas processadas pelo coletor de lixo que estavam primeiro no bucket de hash correspondente e podiam ser removidas imediatamente (em média), por segundo.|  
|**Linhas processadas/s (primeiro no bucket)**|O número de linhas processadas pelo coletor de lixo que estavam primeiro no bucket de hash correspondente (em média), por segundo.|  
|**Linhas processadas/s (marcadas para desvinculação)**|O número de linhas processadas pelo coletor de lixo que já estavam marcadas para desvinculação (em média), por segundo.|  
|**Linhas processadas/s (sem varredura necessária)**|O número de linhas processadas pelo coletor de lixo que não exigirão uma varredura de canto sujo (em média), por segundo.|  
|**Linhas expiradas varridas removidas/s**|O número de linhas expiradas removidas durante varreduras de canto sujo (em média), por segundo.|  
|**Linhas expiradas varridas tocadas/s**|O número de linhas expiradas tocadas durante varreduras de canto sujo (em média), por segundo.|  
|**Linhas expirando varridas tocadas/s**|O número de linhas expirando tocadas durante varreduras de canto sujo (em média), por segundo.|  
|**Linhas varridas tocadas/s**|O número de linhas tocadas durante varreduras de canto sujo (em média), por segundo.|  
|**Verificações de varredura iniciadas/s**|O número de verificações de varredura de canto sujo iniciadas (em média), por segundo.|  
  
## <a name="see-also"></a>Consulte Também  
 [Contadores de desempenho XTP &#40;OLTP in-memory&#41; do SQL Server](../../relational-databases/performance-monitor/sql-server-xtp-in-memory-oltp-performance-counters.md)  
  
  
