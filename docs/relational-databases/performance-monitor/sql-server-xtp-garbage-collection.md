---
title: Coleta de lixo de SQL Server XTP | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 64ae91e5-b420-44b4-af1a-f8bca83d7f41
caps.latest.revision: 8
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 84e7b0df9fdd52f6f67113b9dc019fc905a9aaff
ms.contentlocale: pt-br
ms.lasthandoff: 06/22/2017

---
# <a name="sql-server-xtp-garbage-collection"></a>Coleta de Lixo de XTP do SQL Server
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  O objeto de desempenho Coleta de Lixo de XTP do SQL Server contém os contadores relacionados ao coletor de lixo do mecanismo OLTP in-memory.  
  
 Esta tabela descreve os contadores de **Coleta de Lixo de XTP do SQL Server** .  
  
|Contador|Descrição|  
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
  
## <a name="see-also"></a>Consulte também  
 [Contadores de desempenho XTP &#40;OLTP in-memory&#41; do SQL Server](../../relational-databases/performance-monitor/sql-server-xtp-in-memory-oltp-performance-counters.md)  
  
  

